## [​](#introduction)Introduction

Users in Filament can sign in with their email address and password by default. However, you can enable multi-factor authentication (MFA) to add an extra layer of security to your users’ accounts. When MFA is enabled, users must perform an extra step before they are authenticated and have access to the application. Filament includes two methods of MFA which you can enable out of the box:

- [App authentication](#app-authentication) uses a Google Authenticator-compatible app (such as the Google Authenticator, Authy, or Microsoft Authenticator apps) to generate a time-based one-time password (TOTP) that is used to verify the user.
- [Email authentication](#email-authentication) sends a one-time code to the user’s email address, which they must enter to verify their identity.In Filament, users set up multi-factor authentication from their [profile page](./overview#authentication-features). If you use Filament’s profile page feature, setting up multi-factor authentication will automatically add the correct UI elements to the profile page:

Copy

```
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->profile();
}

```

## [​](#app-authentication)App authentication

To enable app authentication in a panel, you must first add a new column to your `users` table (or whichever table is being used for your “authenticatable” Eloquent model in this panel). The column needs to store the secret key used to generate and verify the time-based one-time passwords. It can be a normal `text()` column in a migration:

Copy

```
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

Schema::table('users', function (Blueprint $table) {
    $table->text('app_authentication_secret')->nullable();
});

```

In the `User` model, you should implement the `HasAppAuthentication` interface and use the `InteractsWithAppAuthentication` trait which provides the necessary methods to interact with the secret code and other information about the integration:

Copy

```
use Filament\Auth\MultiFactor\App\Contracts\HasAppAuthentication;
use Filament\Auth\MultiFactor\App\Concerns\InteractsWithAppAuthentication;
use Filament\Models\Contracts\FilamentUser;
use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser, HasAppAuthentication, MustVerifyEmail
{
    use InteractsWithAppAuthentication;
  
    // ...
}

```

Filament provides a default implementation for speed and simplicity, but you could implement the required methods yourself and customize the column name or store the secret in a completely separate table.

Finally, you should activate the app authentication feature in your panel. To do this, use the `multiFactorAuthentication()` method in the [configuration](../panel-configuration), and pass a `AppAuthentication` instance to it:

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make(),
        ]);
}

```

### [​](#setting-up-app-recovery-codes)Setting up app recovery codes

If your users lose access to their two-factor authentication app, they will be unable to sign in to your application. To prevent this, you can generate a set of recovery codes that users can use to sign in if they lose access to their two-factor authentication app. In a similar way to the `app_authentication_secret` column, you should add a new column to your `users` table (or whichever table is being used for your “authenticatable” Eloquent model in this panel). The column needs to store the recovery codes. It can be a normal `text()` column in a migration:

Copy

```
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

Schema::table('users', function (Blueprint $table) {
    $table->text('app_authentication_recovery_codes')->nullable();
});

```

Next, you should implement the `HasAppAuthenticationRecovery` interface on the `User` model and use the `InteractsWithAppAuthenticationRecovery` trait which provides Filament with the necessary methods to interact with the recovery codes:

Copy

```
use Filament\Auth\MultiFactor\App\Contracts\HasAppAuthentication;
use Filament\Auth\MultiFactor\App\Concerns\InteractsWithAppAuthentication;
use Filament\Auth\MultiFactor\App\Contracts\HasAppAuthenticationRecovery;
use Filament\Auth\MultiFactor\App\Concerns\InteractsWithAppAuthenticationRecovery;
use Filament\Models\Contracts\FilamentUser;
use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser, HasAppAuthentication, HasAppAuthenticationRecovery, MustVerifyEmail
{
    use InteractsWithAppAuthentication;
    use InteractsWithAppAuthenticationRecovery;
  
    // ...
}

```

Filament provides a default implementation for speed and simplicity, but you could implement the required methods yourself and customize the column name or store the recovery codes in a completely separate table.

Finally, you should activate the app authentication recovery codes feature in your panel. To do this, pass the `recoverable()` method to the `AppAuthentication` instance in the `multiFactorAuthentication()` method in the [configuration](../panel-configuration):

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make()
                ->recoverable(),
        ]);
}

```

#### [​](#changing-the-number-of-recovery-codes-that-are-generated)Changing the number of recovery codes that are generated

By default, Filament generates 8 recovery codes for each user. If you want to change this, you can use the `recoveryCodeCount()` method on the `AppAuthentication` instance in the `multiFactorAuthentication()` method in the [configuration](../panel-configuration):

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make()
                ->recoverable()
                ->recoveryCodeCount(10),
        ]);
}

```

#### [​](#preventing-users-from-regenerating-their-recovery-codes)Preventing users from regenerating their recovery codes

By default, users can visit their profile to regenerate their recovery codes. If you want to prevent this, you can use the `regenerableRecoveryCodes(false)` method on the `AppAuthentication` instance in the `multiFactorAuthentication()` method in the [configuration](../panel-configuration):

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make()
                ->recoverable()
                ->regenerableRecoveryCodes(false),
        ]);
}

```

### [​](#changing-the-app-code-expiration-time)Changing the app code expiration time

App codes are issued using a time-based one-time password (TOTP) algorithm, which means that they are only valid for a short period of time before and after the time they are generated. The time is defined in a “window” of time. By default, Filament uses an expiration window of `8`, which creates a 4-minute validity period on either side of the generation time (8 minutes in total). To change the window, for example to only be valid for 2 minutes after it is generated, you can use the `codeWindow()` method on the `AppAuthentication` instance, set to `4`:

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make()
                ->codeWindow(4),
        ]);
}

```

### [​](#customizing-the-app-authentication-brand-name)Customizing the app authentication brand name

Each app authentication integration has a “brand name” that is displayed in the authentication app. By default, this is the name of your app. If you want to change this, you can use the `brandName()` method on the `AppAuthentication` instance in the `multiFactorAuthentication()` method in the [configuration](../panel-configuration):

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make()
                ->brandName('Filament Demo'),
        ]);
}

```

## [​](#email-authentication)Email authentication

Email authentication sends the user one-time codes to their email address, which they must enter to verify their identity. To enable email authentication in a panel, you must first add a new column to your `users` table (or whichever table is being used for your “authenticatable” Eloquent model in this panel). The column needs to store a boolean indicating whether or not email authentication is enabled:

Copy

```
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

Schema::table('users', function (Blueprint $table) {
    $table->boolean('has_email_authentication')->default(false);
});

```

Next, you should implement the `HasEmailAuthentication` interface on the `User` model and use the `InteractsWithEmailAuthentication` trait which provides Filament with the necessary methods to interact with the column that indicates whether or not email authentication is enabled:

Copy

```
use Filament\Auth\MultiFactor\Email\Contracts\HasEmailAuthentication;
use Filament\Auth\MultiFactor\Email\Concerns\InteractsWithEmailAuthentication;
use Filament\Models\Contracts\FilamentUser;
use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser, HasEmailAuthentication, MustVerifyEmail
{
    use InteractsWithEmailAuthentication;
  
    // ...
}

```

Filament provides a default implementation for speed and simplicity, but you could implement the required methods yourself and customize the column name or store the value in a completely separate table.

Finally, you should activate the email authentication feature in your panel. To do this, use the `multiFactorAuthentication()` method in the [configuration](../panel-configuration), and pass an `EmailAuthentication` instance to it:

Copy

```
use Filament\Auth\MultiFactor\Email\EmailAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            EmailAuthentication::make(),
        ]);
}

```

### [​](#changing-the-email-code-expiration-time)Changing the email code expiration time

Email codes are issued with a lifetime of 4 minutes, after which they expire. To change the expiration period, for example to only be valid for 2 minutes after codes are generated, you can use the `codeExpiryMinutes()` method on the `EmailAuthentication` instance, set to `2`:

Copy

```
use Filament\Auth\MultiFactor\Email\EmailAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            EmailAuthentication::make()
                ->codeExpiryMinutes(2),
        ]);
}

```

## [​](#requiring-multi-factor-authentication)Requiring multi-factor authentication

By default, users are not required to set up multi-factor authentication. You can require users to configure it by passing `isRequired: true` as a parameter to the `multiFactorAuthentication()` method in the [configuration](../panel-configuration):

Copy

```
use Filament\Auth\MultiFactor\App\AppAuthentication;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->multiFactorAuthentication([
            AppAuthentication::make(),
        ], isRequired: true);
}

```

When this is enabled, users will be prompted to set up multi-factor authentication after they sign in, if they have not already done so.

## [​](#security-notes-about-multi-factor-authentication)Security notes about multi-factor authentication

In Filament, the multi-factor authentication process occurs before the user is actually authenticated into the app. This allows you to be sure that no users can authenticate and access the app without passing the multi-factor authentication step. You do not need to remember to add middleware to any of your authenticated routes to ensure that users completed the multi-factor authentication step. However, if you have other parts of your Laravel app that authenticate users, please bear in mind that they will not be challenged for multi-factor authentication if they are already authenticated elsewhere and then visit the panel, unless [multi-factor authentication is required](#requiring-multi-factor-authentication) and they have not set it up yet.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/07-users/02-multi-factor-authentication.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Overview](/docs/5.x/users/overview)[Multi-tenancy](/docs/5.x/users/tenancy)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
