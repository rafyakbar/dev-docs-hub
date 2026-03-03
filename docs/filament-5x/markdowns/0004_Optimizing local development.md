This section includes optional tips to optimize performance when running your Filament app locally. If you’re looking for production-specific optimizations, check out [Deploying to production](../deployment).

## [​](#enabling-opcache)Enabling OPcache

[OPcache](https://www.php.net/manual/en/book.opcache.php) improves PHP performance by storing precompiled script bytecode in shared memory, thereby removing the need for PHP to load and parse scripts on each request. This can significantly speed up your local development environment, especially for larger applications.

### [​](#checking-opcache-status)Checking OPcache status

To check if [OPcache](https://www.php.net/manual/en/book.opcache.php) is enabled, run:

Copy

```
php -r "echo 'opcache.enable => ' . ini_get('opcache.enable') . PHP_EOL;"

```

You should see `opcache.enable => 1`. If not, enable it by adding the following line to your `php.ini`:

Copy

```
opcache.enable=1 # Enable OPcache

```

To locate your `php.ini` file, run: `php --ini`

### [​](#configuring-opcache-settings)Configuring OPcache settings

If you’re experiencing slow response times or suspect that OPcache is running out of space, you can adjust these parameters in your `php.ini` file:

Copy

```
opcache.memory_consumption=128
opcache.max_accelerated_files=10000

```

To locate your `php.ini` file, run: `php --ini`

- `opcache.memory_consumption`: defines how much memory (in megabytes) OPcache can use to store precompiled PHP code. You can try setting this to `128` and adjust based on your project’s needs.
- `opcache.max_accelerated_files`: sets the maximum number of PHP files that OPcache can cache. You can try `10000` as a starting point and increase if your application includes a large number of files.These settings are optional but useful if you’re troubleshooting performance or working on a large Laravel app.

## [​](#exclude-your-project-folder-from-antivirus-scanning)Exclude your project folder from antivirus scanning

Issues with the performance of Filament, particularly on Windows, often involve [Microsoft Defender](https://www.microsoft.com/en-us/microsoft-365/microsoft-defender-for-individuals). Security software, such as realtime file scanners or antivirus tools, can slow down your development environment by scanning files every time they’re accessed. This can affect PHP execution, view rendering, and performance in general. If you’re noticing slowness, consider excluding your local project folder from realtime scanning. Tools like [Microsoft Defender](https://www.microsoft.com/en-us/microsoft-365/microsoft-defender-for-individuals), or similar antivirus solutions, can be configured to skip specific directories. Check your antivirus or security software documentation for instructions on how to exclude specific folders from realtime scanning.

Only exclude folders from scanning if you fully trust the project and understand the risks.

## [​](#disabling-debugging-tools)Disabling debugging tools

Debugging tools can be very useful for local development, but they can significantly slow down your application when you aren’t actively using them. Temporarily disabling these tools when you need maximum performance can make a noticeable difference in your development experience.

### [​](#disabling-view-debugging-in-laravel-herd)Disabling view debugging in Laravel Herd

[Laravel Herd](https://herd.laravel.com/) includes a view debugging tool for [macOS](https://herd.laravel.com/docs/macos/debugging/dumps#views) and [Windows](https://herd.laravel.com/docs/windows/debugging/dumps#views). It shows which views were rendered and what data was passed to them during a request. While helpful for debugging, this feature can significantly slow down your app. If you’re not actively using it, it’s best to turn it off. To disable view debugging in Herd:

- Open Herd > Dumps.
- Click Settings.
- Uncheck the “Views” option.


### [​](#disabling-debugbar)Disabling Debugbar

While useful for debugging, [Laravel Debugbar](https://github.com/barryvdh/laravel-debugbar) can slow down your application, especially on complex pages, because it collects and renders a large amount of data on each request. If you’re noticing slowness, try disabling it by adding the following line to your `.env` file:

Copy

```
DEBUGBAR_ENABLED=false

```

If you still need Debugbar for development, consider disabling specific collectors you’re not using.
Refer to the [Debugbar documentation](https://github.com/barryvdh/laravel-debugbar?tab=readme-ov-file#debugbar-for-laravel) for details.

### [​](#disabling-xdebug)Disabling Xdebug

[Xdebug](https://xdebug.org) is a powerful tool for debugging, but it can significantly slow down performance. If you notice performance issues, check if `Xdebug` is installed and consider disabling it. If `Xdebug` is installed but not disabled, it will still be enabled by default. If you have it installed, make sure it is explicitly disabled in your `php.ini` file:

Copy

```
xdebug.mode=off # Disable Xdebug

```

To locate your `php.ini` file, run: `php --ini`

## [​](#caching-blade-icons)Caching Blade icons

Caching [Blade icons](https://blade-ui-kit.com/blade-icons) can help improve performance during local development, especially in views that render many icons. To enable caching, run:

Copy

```
php artisan icons:cache

```

Make sure that when you install new Blade icon packages, you run the command again to discover the new icons.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/01-introduction/04-optimizing-local-development.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[AI-assisted development](/docs/5.x/introduction/ai)[Help](/docs/5.x/introduction/help)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
