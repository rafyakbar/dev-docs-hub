## [​](#introduction)Introduction

The repeatable entry allows you to repeat a set of entries and layout components for items in an array or relationship.

Copy

```
use Filament\Infolists\Components\RepeatableEntry;
use Filament\Infolists\Components\TextEntry;

RepeatableEntry::make('comments')
    ->schema([
        TextEntry::make('author.name'),
        TextEntry::make('title'),
        TextEntry::make('content')
            ->columnSpan(2),
    ])
    ->columns(2)

```

As you can see, the repeatable entry has an embedded `schema()` which gets repeated for each item. For example, the state of this entry might be represented as:

Copy

```
[
    [
        'author' => ['name' => 'Jane Doe'],
        'title' => 'Wow!',
        'content' => 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam euismod, nisl eget aliquam ultricies, nunc nisl aliquet nunc, quis aliquam nisl.',
    ],
    [
        'author' => ['name' => 'John Doe'],
        'title' => 'This isn\'t working. Help!',
        'content' => 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam euismod, nisl eget aliquam ultricies, nunc nisl aliquet nunc, quis aliquam nisl.',
    ],
]

```

Alternatively, `comments` and `author` could be Eloquent relationships, `title` and `content` could be attributes on the comment model, and `name` could be an attribute on the author model. Filament will automatically handle the relationship loading and display the data in the same way.

## [​](#grid-layout)Grid layout

You may organize repeatable items into columns by using the `grid()` method:

Copy

```
use Filament\Infolists\Components\RepeatableEntry;

RepeatableEntry::make('comments')
    ->schema([
        // ...
    ])
    ->grid(2)

```

This method accepts the same options as the `columns()` method of the [grid](../schemas/layouts#grid-system). This allows you to responsively customize the number of grid columns at various breakpoints.

**As well as allowing a static value, the `grid()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/infolists/overview#entry-utility-injection)

Entry

$component

Filament\Infolists\Components\Entry

The current entry component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current schema data. Validation is not run on form fields.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current schema.

Operation

$operation

string

The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the entry.

## [​](#removing-the-styled-container)Removing the styled container

By default, each item in a repeatable entry is wrapped in a container styled as a card. You may remove the styled container using `contained()`:

Copy

```
use Filament\Infolists\Components\RepeatableEntry;

RepeatableEntry::make('comments')
    ->schema([
        // ...
    ])
    ->contained(false)

```

**As well as allowing a static value, the `contained()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/infolists/overview#entry-utility-injection)

Entry

$component

Filament\Infolists\Components\Entry

The current entry component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current schema data. Validation is not run on form fields.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current schema.

Operation

$operation

string

The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the entry.

## [​](#table-repeatable-layout)Table repeatable layout

You can present repeatable items in a table format using the `table()` method, which accepts an array of `TableColumn` objects. These objects represent the columns of the table, which correspond to any components in the schema of the entry:

Copy

```
use Filament\Infolists\Components\IconEntry;
use Filament\Infolists\Components\RepeatableEntry;
use Filament\Infolists\Components\RepeatableEntry\TableColumn;
use Filament\Infolists\Components\TextEntry;

RepeatableEntry::make('comments')
    ->table([
        TableColumn::make('Author'),
        TableColumn::make('Title'),
        TableColumn::make('Published'),
    ])
    ->schema([
        TextEntry::make('author.name'),
        TextEntry::make('title'),
        IconEntry::make('is_published')
            ->boolean(),
    ])

```

The labels displayed in the header of the table are passed to the `TableColumn::make()` method. If you want to provide an accessible label for a column but do not wish to display it, you can use the `hiddenHeaderLabel()` method:

Copy

```
use Filament\Infolists\Components\RepeatableEntry\TableColumn;

TableColumn::make('Name')
    ->hiddenHeaderLabel()

```

You can enable wrapping of the column header using the `wrapHeader()` method:

Copy

```
use Filament\Infolists\Components\RepeatableEntry\TableColumn;

TableColumn::make('Name')
    ->wrapHeader()

```

You can also adjust the alignment of the column header using the `alignment()` method, passing an `Alignment` option of `Alignment::Start`, `Alignment::Center`, or `Alignment::End`:

Copy

```
use Filament\Infolists\Components\RepeatableEntry\TableColumn;
use Filament\Support\Enums\Alignment;

TableColumn::make('Name')
    ->alignment(Alignment::Center)

```

You can set a fixed column width using the `width()` method, passing a string value that represents the width of the column. This value is passed directly to the `style` attribute of the column header:

Copy

```
use Filament\Infolists\Components\RepeatableEntry\TableColumn;

TableColumn::make('Name')
    ->width('200px')

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/infolists/docs/08-repeatable-entry.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[Your logo here](https://github.com/sponsors/danharrin)

[Key-value entry](/docs/5.x/infolists/key-value-entry)[Custom entries](/docs/5.x/infolists/custom-entries)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
