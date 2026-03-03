## [​](#introduction)Introduction

Filament comes with a “stats overview” widget template, which you can use to display a number of different stats in a single widget, without needing to write a custom view. Start by creating a widget with the command:

Copy

```
php artisan make:filament-widget StatsOverview --stats-overview

```

This command will create a new `StatsOverview.php` file. Open it, and return `Stat` instances from the `getStats()` method:

Copy

```
<?php

namespace App\Filament\Widgets;

use Filament\Widgets\StatsOverviewWidget as BaseWidget;
use Filament\Widgets\StatsOverviewWidget\Stat;

class StatsOverview extends BaseWidget
{
    protected function getStats(): array
    {
        return [
            Stat::make('Unique views', '192.1k'),
            Stat::make('Bounce rate', '21%'),
            Stat::make('Average time on page', '3:12'),
        ];
    }
}

```

Now, check out your widget in the dashboard.

## [​](#adding-a-description-and-icon-to-a-stat)Adding a description and icon to a stat

You may add a `description()` to provide additional information, along with a `descriptionIcon()`:

Copy

```
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Unique views', '192.1k')
            ->description('32k increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up'),
        Stat::make('Bounce rate', '21%')
            ->description('7% decrease')
            ->descriptionIcon('heroicon-m-arrow-trending-down'),
        Stat::make('Average time on page', '3:12')
            ->description('3% increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up'),
    ];
}

```

The `descriptionIcon()` method also accepts a second parameter to put the icon before the description instead of after it:

Copy

```
use Filament\Support\Enums\IconPosition;
use Filament\Widgets\StatsOverviewWidget\Stat;

Stat::make('Unique views', '192.1k')
    ->description('32k increase')
    ->descriptionIcon('heroicon-m-arrow-trending-up', IconPosition::Before)

```

## [​](#changing-the-color-of-the-stat)Changing the color of the stat

You may also give stats a [color](../styling/colors):

Copy

```
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Unique views', '192.1k')
            ->description('32k increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up')
            ->color('success'),
        Stat::make('Bounce rate', '21%')
            ->description('7% increase')
            ->descriptionIcon('heroicon-m-arrow-trending-down')
            ->color('danger'),
        Stat::make('Average time on page', '3:12')
            ->description('3% increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up')
            ->color('success'),
    ];
}

```

## [​](#adding-extra-html-attributes-to-a-stat)Adding extra HTML attributes to a stat

You may also pass extra HTML attributes to stats using `extraAttributes()`:

Copy

```
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Processed', '192.1k')
            ->color('success')
            ->extraAttributes([
                'class' => 'cursor-pointer',
                'wire:click' => "\$dispatch('setStatusFilter', { filter: 'processed' })",
            ]),
        // ...
    ];
}

```

In this example, we are deliberately escaping the `$` in `$dispatch()` since this needs to be passed directly to the HTML, it is not a PHP variable.

## [​](#adding-a-chart-to-a-stat)Adding a chart to a stat

You may also add or chain a `chart()` to each stat to provide historical data. The `chart()` method accepts an array of data points to plot:

Copy

```
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Unique views', '192.1k')
            ->description('32k increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up')
            ->chart([7, 2, 10, 3, 15, 4, 17])
            ->color('success'),
        // ...
    ];
}

```

## [​](#live-updating-stats-polling)Live updating stats (polling)

By default, stats overview widgets refresh their data every 5 seconds. To customize this, you may override the `$pollingInterval` property on the class to a new interval:

Copy

```
protected ?string $pollingInterval = '10s';

```

Alternatively, you may disable polling altogether:

Copy

```
protected ?string $pollingInterval = null;

```

## [​](#disabling-lazy-loading)Disabling lazy loading

By default, widgets are lazy-loaded. This means that they will only be loaded when they are visible on the page. To disable this behavior, you may override the `$isLazy` property on the widget class:

Copy

```
protected static bool $isLazy = false;

```

## [​](#adding-a-heading-and-description)Adding a heading and description

You may also add heading and description text above the widget by overriding the `$heading` and `$description` properties:

Copy

```
protected ?string $heading = 'Analytics';

protected ?string $description = 'An overview of some analytics.';

```

If you need to dynamically generate the heading or description text, you can instead override the `getHeading()` and `getDescription()` methods:

Copy

```
protected function getHeading(): ?string
{
    return 'Analytics';
}

protected function getDescription(): ?string
{
    return 'An overview of some analytics.';
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/widgets/docs/02-stats-overview.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[Your logo here](https://github.com/sponsors/danharrin)

[Overview](/docs/5.x/widgets/overview)[Chart widgets](/docs/5.x/widgets/charts)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
