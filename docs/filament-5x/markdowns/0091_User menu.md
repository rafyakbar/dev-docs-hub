## [​](#introduction)Introduction

The user menu is featured in the top right corner of the admin layout. It’s fully customizable. Each menu item is represented by an [action](../actions), and can be customized in the same way. To register new items, you can pass the actions to the `userMenuItems()` method of the [configuration](../panel-configuration):

Copy

```
use App\Filament\Pages\Settings;
use Filament\Actions\Action;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->userMenuItems([
            Action::make('settings')
                ->url(fn (): string => Settings::getUrl())
                ->icon('heroicon-o-cog-6-tooth'),
            // ...
        ]);
}

```

## [​](#moving-the-user-menu-to-the-sidebar)Moving the user menu to the sidebar

By default, the user menu is positioned in the topbar. If the topbar is disabled, it is added to the sidebar. You can choose to always move it to the sidebar by passing a `position` argument to the `userMenu()` method in the [configuration](../panel-configuration):

Copy

```
use Filament\Enums\UserMenuPosition;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->userMenu(position: UserMenuPosition::Sidebar);
}

```

## [​](#customizing-the-profile-link)Customizing the profile link

To customize the user profile link at the start of the user menu, register a new item with the `profile` array key, and pass a function that [customizes the action](../actions) object:

Copy

```
use Filament\Actions\Action;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->userMenuItems([
            'profile' => fn (Action $action) => $action->label('Edit profile'),
            // ...
        ]);
}

```

For more information on creating a profile page, check out the [authentication features documentation](../users#authentication-features).

## [​](#customizing-the-logout-link)Customizing the logout link

To customize the user logout link at the end of the user menu, register a new item with the `logout` array key, and pass a function that [customizes the action](../actions) object:

Copy

```
use Filament\Actions\Action;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->userMenuItems([
            'logout' => fn (Action $action) => $action->label('Log out'),
            // ...
        ]);
}

```

## [​](#conditionally-hiding-user-menu-items)Conditionally hiding user menu items

You can also conditionally hide a user menu item by using the `visible()` or `hidden()` methods, passing in a condition to check. Passing a function will defer condition evaluation until the menu is actually being rendered:

Copy

```
use App\Models\Payment;
use Filament\Actions\Action;

Action::make('payments')
    ->visible(fn (): bool => auth()->user()->can('viewAny', Payment::class))
    // or
    ->hidden(fn (): bool => ! auth()->user()->can('viewAny', Payment::class))

```

## [​](#sending-a-post-http-request-from-a-user-menu-item)Sending a `POST` HTTP request from a user menu item

You can send a `POST` HTTP request from a user menu item by passing a URL to the `url()` method, and also using `postToUrl()`:

Copy

```
use Filament\Actions\Action;

Action::make('lockSession')
    ->url(fn (): string => route('lock-session'))
    ->postToUrl()

```

## [​](#disabling-the-user-menu)Disabling the user menu

You may disable the user menu entirely by passing `false` to the `userMenu()` method:

Copy

```
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->userMenu(false);
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/06-navigation/03-user-menu.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[Your logo here](https://github.com/sponsors/danharrin)

[Custom pages](/docs/5.x/navigation/custom-pages)[Clusters](/docs/5.x/navigation/clusters)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
