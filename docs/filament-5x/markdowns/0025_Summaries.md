## [​](#introduction)Introduction

You may render a “summary” section below your table content. This is great for displaying the results of calculations such as averages, sums, counts, and ranges of the data in your table. By default, there will be a single summary line for the current page of data, and an additional summary line for the totals for all data if multiple pages are available. You may also add summaries for [groups](./grouping) of records, see [“Summarising groups of rows”](#summarising-groups-of-rows). “Summarizer” objects can be added to any [table column](./columns) using the `summarize()` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('rating')
    ->summarize(Average::make())

```

Multiple “summarizers” may be added to the same column:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\Summarizers\Range;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('rating')
    ->numeric()
    ->summarize([
        Average::make(),
        Range::make(),
    ])

```
> The first column in a table may not use summarizers. That column is used to render the heading and subheading/s of the summary section.

## [​](#available-summarizers)Available summarizers

Filament ships with four types of summarizer:

- [Average](#average)
- [Count](#count)
- [Range](#range)
- [Sum](#sum)You may also [create your own custom summarizers](#custom-summaries) to display data in whatever way you wish.

## [​](#average)Average

Average can be used to calculate the average of all values in the dataset:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('rating')
    ->summarize(Average::make())

```

In this example, all ratings in the table will be added together and divided by the number of ratings.

## [​](#count)Count

Count can be used to find the total number of values in the dataset. Unless you just want to calculate the number of rows, you will probably want to [scope the dataset](#scoping-the-dataset) as well:

Copy

```
use Filament\Tables\Columns\IconColumn;
use Filament\Tables\Columns\Summarizers\Count;
use Illuminate\Database\Query\Builder;

IconColumn::make('is_published')
    ->boolean()
    ->summarize(
        Count::make()->query(fn (Builder $query) => $query->where('is_published', true)),
    ),

```

In this example, the table will calculate how many posts are published.

### [​](#counting-the-occurrence-of-icons)Counting the occurrence of icons

Using a count on an [icon column](./columns/icon) allows you to use the `icons()` method, which gives the user a visual representation of how many of each icon are in the table:

Copy

```
use Filament\Tables\Columns\IconColumn;
use Filament\Tables\Columns\Summarizers\Count;
use Illuminate\Database\Query\Builder;

IconColumn::make('is_published')
    ->boolean()
    ->summarize(Count::make()->icons()),

```

## [​](#range)Range

Range can be used to calculate the minimum and maximum value in the dataset:

Copy

```
use Filament\Tables\Columns\Summarizers\Range;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Range::make())

```

In this example, the minimum and maximum price in the table will be found.

### [​](#date-range)Date range

You may format the range as dates using the `minimalDateTimeDifference()` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Range;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('created_at')
    ->dateTime()
    ->summarize(Range::make()->minimalDateTimeDifference())

```

This method will present the minimal difference between the minimum and maximum date. For example:

- If the minimum and maximum dates are different days, only the dates will be displayed.
- If the minimum and maximum dates are on the same day at different times, both the date and time will be displayed.
- If the minimum and maximum dates and times are identical, they will only appear once.


### [​](#text-range)Text range

You may format the range as text using the `minimalTextualDifference()` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Range;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('sku')
    ->summarize(Range::make()->minimalTextualDifference())

```

This method will present the minimal difference between the minimum and maximum. For example:

- If the minimum and maximum start with different letters, only the first letters will be displayed.
- If the minimum and maximum start with the same letter, more of the text will be rendered until a difference is found.
- If the minimum and maximum are identical, they will only appear once.


### [​](#including-null-values-in-the-range)Including null values in the range

By default, we will exclude null values from the range. If you would like to include them, you may use the `excludeNull(false)` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Range;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('sku')
    ->summarize(Range::make()->excludeNull(false))

```

## [​](#sum)Sum

Sum can be used to calculate the total of all values in the dataset:

Copy

```
use Filament\Tables\Columns\Summarizers\Sum;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Sum::make())

```

In this example, all prices in the table will be added together.

## [​](#setting-a-label)Setting a label

You may set a summarizer’s label using the `label()` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Sum;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Sum::make()->label('Total'))

```

## [​](#scoping-the-dataset)Scoping the dataset

You may apply a database query scope to a summarizer’s dataset using the `query()` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;
use Illuminate\Database\Query\Builder;

TextColumn::make('rating')
    ->summarize(
        Average::make()->query(fn (Builder $query) => $query->where('is_published', true)),
    ),

```

In this example, now only rows where `is_published` is set to `true` will be used to calculate the average. This feature is especially useful with the [count](#count) summarizer, as it can count how many records in the dataset pass a test:

Copy

```
use Filament\Tables\Columns\IconColumn;
use Filament\Tables\Columns\Summarizers\Count;
use Illuminate\Database\Query\Builder;

IconColumn::make('is_published')
    ->boolean()
    ->summarize(
        Count::make()->query(fn (Builder $query) => $query->where('is_published', true)),
    ),

```

In this example, the table will calculate how many posts are published.

## [​](#formatting)Formatting

### [​](#number-formatting)Number formatting

The `numeric()` method allows you to format an entry as a number:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('rating')
    ->summarize(Average::make()->numeric())

```

If you would like to customize the number of decimal places used to format the number with, you can use the `decimalPlaces` argument:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('rating')
    ->summarize(Average::make()->numeric(
        decimalPlaces: 0,
    ))

```

By default, your app’s locale will be used to format the number suitably. If you would like to customize the locale used, you can pass it to the `locale` argument:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('rating')
    ->summarize(Average::make()->numeric(
        locale: 'nl',
    ))

```

### [​](#currency-formatting)Currency formatting

The `money()` method allows you to easily format monetary values, in any currency:

Copy

```
use Filament\Tables\Columns\Summarizers\Sum;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Sum::make()->money('EUR'))

```

There is also a `divideBy` argument for `money()` that allows you to divide the original value by a number before formatting it. This could be useful if your database stores the price in cents, for example:

Copy

```
use Filament\Tables\Columns\Summarizers\Sum;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Sum::make()->money('EUR', divideBy: 100))

```

By default, your app’s locale will be used to format the money suitably. If you would like to customize the locale used, you can pass it to the `locale` argument:

Copy

```
use Filament\Tables\Columns\Summarizers\Average;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Sum::make()->money('EUR', locale: 'nl'))

```

If you would like to customize the number of decimal places used to format the number with, you can use the `decimalPlaces` argument:

Copy

```
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->summarize(Sum::make()->money('EUR', decimalPlaces: 3))

```

### [​](#limiting-text-length)Limiting text length

You may `limit()` the length of the summary’s value:

Copy

```
use Filament\Tables\Columns\Summarizers\Range;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('sku')
    ->summarize(Range::make()->limit(5))

```

### [​](#adding-a-prefix-or-suffix)Adding a prefix or suffix

You may add a prefix or suffix to the summary’s value:

Copy

```
use Filament\Tables\Columns\Summarizers\Sum;
use Filament\Tables\Columns\TextColumn;
use Illuminate\Support\HtmlString;

TextColumn::make('volume')
    ->summarize(Sum::make()
        ->prefix('Total volume: ')
        ->suffix(new HtmlString(' m&sup3;'))
    )

```

## [​](#custom-summaries)Custom summaries

You may create a custom summary by returning the value from the `using()` method:

Copy

```
use Filament\Tables\Columns\Summarizers\Summarizer;
use Filament\Tables\Columns\TextColumn;
use Illuminate\Database\Query\Builder;

TextColumn::make('name')
    ->summarize(Summarizer::make()
        ->label('First last name')
        ->using(fn (Builder $query): string => $query->min('last_name')))

```

The callback has access to the database `$query` builder instance to perform calculations with. It should return the value to display in the table.

## [​](#conditionally-hiding-the-summary)Conditionally hiding the summary

To hide a summary, you may pass a boolean, or a function that returns a boolean, to the `hidden()` method. If you need it, you can access the Eloquent query builder instance for that summarizer via the `$query` argument of the function:

Copy

```
use Filament\Tables\Columns\Summarizers\Summarizer;
use Filament\Tables\Columns\TextColumn;
use Illuminate\Database\Eloquent\Builder;

TextColumn::make('sku')
    ->summarize(Summarizer::make()
        ->hidden(fn (Builder $query): bool => ! $query->exists()))

```

Alternatively, you can use the `visible()` method to achieve the opposite effect:

Copy

```
use Filament\Tables\Columns\Summarizers\Summarizer;
use Filament\Tables\Columns\TextColumn;
use Illuminate\Database\Eloquent\Builder;

TextColumn::make('sku')
    ->summarize(Summarizer::make()
        ->visible(fn (Builder $query): bool => $query->exists()))

```

## [​](#summarising-groups-of-rows)Summarising groups of rows

You can use summaries with [groups](./grouping) to display a summary of the records inside a group. This works automatically if you choose to add a summariser to a column in a grouped table.

### [​](#hiding-the-grouped-rows-and-showing-the-summary-only)Hiding the grouped rows and showing the summary only

You may hide the rows inside groups and just show the summary of each group using the `groupsOnly()` method. This is beneficial in many reporting scenarios.

Copy

```
use Filament\Tables\Columns\Summarizers\Sum;
use Filament\Tables\Columns\TextColumn;
use Filament\Tables\Table;

public function table(Table $table): Table
{
    return $table
        ->columns([
            TextColumn::make('views_count')
                ->summarize(Sum::make()),
            TextColumn::make('likes_count')
                ->summarize(Sum::make()),
        ])
        ->defaultGroup('category')
        ->groupsOnly();
}

```

## [​](#hiding-summary-rows)Hiding summary rows

By default, both the page summary and total summary rows are displayed when columns have summarizers. You can control which summary rows appear using the `summaries()` method on the table:

Copy

```
use Filament\Tables\Table;

public function table(Table $table): Table
{
    return $table
        ->summaries(
            pageCondition: false,
            allTableCondition: false
        );
}

```

`pageCondition` controls whether the “this page” summary row is shown, and `allTableCondition` controls whether the total summary row for the entire table is shown. This is useful when using [group summaries](#summarising-groups-of-rows) where you only want to display summaries per group, or when the page summary is redundant and you only need the total across all records.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/tables/docs/06-summaries.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[Your logo here](https://github.com/sponsors/danharrin)

[Layout](/docs/5.x/tables/layout)[Grouping rows](/docs/5.x/tables/grouping)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
