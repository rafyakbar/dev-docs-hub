## [​](#introduction)Introduction

When building large-scale applications with Filament, you may want to organize your code using Domain-Driven Design (DDD) principles, splitting your application into self-contained modules. This guide explains how to integrate Filament with modular architecture packages like [InterNACHI/Modular](https://github.com/InterNACHI/modular).

## [​](#the-modular-approach)The modular approach

In a modular architecture, each domain of your application is structured as a separate Composer package, typically located in an `app-modules/` directory. Each module contains its own:

- Models and business logic
- Filament resources, pages, and widgets
- Service provider
- Routes, views, and configurations
- TestsThis approach offers several benefits:

- Clear separation of concerns between domains
- Easier team collaboration (different teams can own different modules)
- Better testability and maintainability
- Ability to reuse modules across projects


## [​](#setting-up-internachi/modular)Setting up InterNACHI/Modular

First, install the modular package:

Copy

```
composer require internachi/modular

```

Create a new module:

Copy

```
php artisan make:module alerts

```

This scaffolds a module structure:

Copy

```
.
+-- app-modules
|   +-- alerts
|   |   +-- composer.json
|   |   +-- src
|   |   |   +-- Providers
|   |   |   |   +-- AlertsServiceProvider.php
|   |   +-- routes
|   |   +-- resources
|   |   +-- database
|   |   +-- tests

```

### [​](#configuring-the-module’s-composer-json)Configuring the module’s composer.json

Each module should require `filament/filament` and define its service provider:

Copy

```
{
    "name": "my-app/alerts",
    "type": "library",
    "require": {
        "filament/filament": "^5.0"
    },
    "autoload": {
        "psr-4": {
            "Modules\\Alerts\\": "src/"
        }
    },
    "extra": {
        "laravel": {
            "providers": [
                "Modules\\Alerts\\Providers\\AlertsServiceProvider"
            ]
        }
    }
}

```

## [​](#creating-a-filament-plugin-for-your-module)Creating a Filament plugin for your module

Each module should define its own Filament plugin that registers its resources, pages, and widgets:

Copy

```
namespace Modules\Alerts;

use Filament\Contracts\Plugin;
use Filament\Panel;

class AlertsPlugin implements Plugin
{
    public function getId(): string
    {
        return 'alerts';
    }

    public static function make(): static
    {
        return app(static::class);
    }

    public function register(Panel $panel): void
    {
        $panel
            ->discoverResources(
                in: __DIR__ . '/Filament/Resources',
                for: 'Modules\\Alerts\\Filament\\Resources',
            )
            ->discoverPages(
                in: __DIR__ . '/Filament/Pages',
                for: 'Modules\\Alerts\\Filament\\Pages',
            )
            ->discoverWidgets(
                in: __DIR__ . '/Filament/Widgets',
                for: 'Modules\\Alerts\\Filament\\Widgets',
            );
    }

    public function boot(Panel $panel): void
    {
        //
    }
}

```

## [​](#registering-plugins-conditionally-for-specific-panels)Registering plugins conditionally for specific panels

When you have multiple panels (e.g., `admin`, `app`, `portal`), you’ll often want certain modules to only register their plugins for specific panels. Use `Panel::configureUsing()` in your module’s service provider to conditionally register plugins.

### [​](#basic-conditional-registration)Basic conditional registration

To register a plugin for all panels except one:

Copy

```
namespace Modules\Alerts\Providers;

use Filament\Panel;
use Illuminate\Support\ServiceProvider;
use Modules\Alerts\AlertsPlugin;

class AlertsServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        Panel::configureUsing(function (Panel $panel): void {
            if ($panel->getId() !== 'admin') {
                return;
            }

            $panel->plugin(AlertsPlugin::make());
        });
    }
}

```

### [​](#using-a-match-statement-for-multiple-panels)Using a match statement for multiple panels

When you need to register a plugin for specific panels or configure it differently per panel, use a `match` statement that calls `$panel->plugin()` directly:

Copy

```
namespace Modules\Alerts\Providers;

use Filament\Panel;
use Illuminate\Support\ServiceProvider;
use Modules\Alerts\AlertsPlugin;

class AlertsServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        Panel::configureUsing(function (Panel $panel): void {
            match ($panel->getId()) {
                'admin' => $panel->plugin(
                    AlertsPlugin::make()->enableAdminFeatures(),
                ),
                'staff' => $panel->plugin(
                    AlertsPlugin::make(),
                ),
                default => null,
            };
        });
    }
}

```

This approach lets you configure each plugin instance differently based on the panel, while panels not matched in the statement simply don’t receive the plugin.

## [​](#module-directory-structure)Module directory structure

A well-organized module with Filament integration might look like this:

Copy

```
.
+-- app-modules
|   +-- alerts
|   |   +-- composer.json
|   |   +-- config
|   |   |   +-- alerts.php
|   |   +-- database
|   |   |   +-- factories
|   |   |   +-- migrations
|   |   |   +-- seeders
|   |   +-- resources
|   |   |   +-- views
|   |   |   |   +-- filament
|   |   |   |   |   +-- pages
|   |   +-- routes
|   |   |   +-- web.php
|   |   +-- src
|   |   |   +-- AlertsPlugin.php
|   |   |   +-- Filament
|   |   |   |   +-- Pages
|   |   |   |   +-- Resources
|   |   |   |   |   +-- Alerts
|   |   |   |   |   |   +-- AlertResource.php
|   |   |   |   |   |   +-- Pages
|   |   |   |   |   |   |   +-- CreateAlert.php
|   |   |   |   |   |   |   +-- EditAlert.php
|   |   |   |   |   |   |   +-- ListAlerts.php
|   |   |   |   +-- Widgets
|   |   |   +-- Models
|   |   |   |   +-- Alert.php
|   |   |   +-- Providers
|   |   |   |   +-- AlertsServiceProvider.php
|   |   +-- tests

```

## [​](#sharing-resources-between-panels)Sharing resources between panels

Sometimes you may want a resource to appear in multiple panels with different configurations. You can achieve this by using resource discovery with panel-specific customizations:

Copy

```
namespace Modules\Users;

use Filament\Contracts\Plugin;
use Filament\Panel;
use Modules\Users\Filament\Resources\UserResource;

class UsersPlugin implements Plugin
{
    protected bool $canManageRoles = false;

    public function getId(): string
    {
        return 'users';
    }

    public static function make(): static
    {
        return app(static::class);
    }

    public function canManageRoles(bool $condition = true): static
    {
        $this->canManageRoles = $condition;

        return $this;
    }

    public function hasRoleManagement(): bool
    {
        return $this->canManageRoles;
    }

    public function register(Panel $panel): void
    {
        $panel->resources([
            UserResource::class,
        ]);
    }

    public function boot(Panel $panel): void
    {
        //
    }
}

```

Then register with different capabilities:

Copy

```
Panel::configureUsing(function (Panel $panel): void {
    match ($panel->getId()) {
        'admin' => $panel->plugin(
            UsersPlugin::make()->canManageRoles(),
        ),
        'staff' => $panel->plugin(
            UsersPlugin::make(),
        ),
        default => null,
    };
});

```

The `Panel::configureUsing()` approach is powerful because it allows modules to configure themselves without requiring changes to your panel provider files. When you add or remove a module, its Filament integration is automatically handled.

## [​](#registering-livewire-components-from-modules)Registering Livewire components from modules

If your module contains custom Livewire components used by Filament (such as custom pages or widgets), you can register them in the plugin’s `boot()` method:

Copy

```
use Livewire\Livewire;
use Modules\Alerts\Filament\Pages\AlertsDashboard;

public function boot(Panel $panel): void
{
    Livewire::component('alerts-dashboard', AlertsDashboard::class);
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/09-advanced/05-modular-architecture.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[File generation](/docs/5.x/advanced/file-generation)[Overview](/docs/5.x/testing/overview)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
