## [​](#introduction)Introduction

The toggle buttons input provides a group of buttons for selecting a single value, or multiple values, from a list of predefined options:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'scheduled' => 'Scheduled',
        'published' => 'Published'
    ])

```

**As well as allowing a static array, the `options()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#changing-the-color-of-option-buttons)Changing the color of option buttons

You can change the [color](../styling/colors) of the option buttons using the `colors()` method. Each key in the array should correspond to an option value:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'scheduled' => 'Scheduled',
        'published' => 'Published'
    ])
    ->colors([
        'draft' => 'info',
        'scheduled' => 'warning',
        'published' => 'success',
    ])

```

If you are using an enum for the options, you can use the [`HasColor` interface](../advanced/enums#enum-colors) to define colors instead.

**As well as allowing a static array, the `colors()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#adding-icons-to-option-buttons)Adding icons to option buttons

You can add [icon](../styling/icons) to the option buttons using the `icons()` method. Each key in the array should correspond to an option value, and the value may be any valid [icon](../styling/icons):

Copy

```
use Filament\Forms\Components\ToggleButtons;
use Filament\Support\Icons\Heroicon;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'scheduled' => 'Scheduled',
        'published' => 'Published'
    ])
    ->icons([
        'draft' => Heroicon::OutlinedPencil,
        'scheduled' => Heroicon::OutlinedClock,
        'published' => Heroicon::OutlinedCheckCircle,
    ])

```

**As well as allowing a static array, the `icons()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

If you are using an enum for the options, you can use the [`HasIcon` interface](../advanced/enums#enum-icons) to define icons instead. If you want to display only icons, you can use `hiddenButtonLabels()` to hide the option labels.

## [​](#adding-tooltips-to-option-buttons)Adding tooltips to option buttons

You can add different tooltips to each option button using the `tooltips()` method.

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'scheduled' => 'Scheduled',
        'published' => 'Published',
    ])
    ->tooltips([
        'draft' => 'Set as a draft before publishing.',
        'scheduled' => 'Schedule publishing on a specific date.',
        'published' => 'Publish now',
    ])

```

**As well as allowing a static array, the `tooltips()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/4.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#boolean-options)Boolean options

If you want a simple boolean toggle button group, with “Yes” and “No” options, you can use the `boolean()` method:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean()

```

The options will have [colors](#changing-the-color-of-option-buttons) and [icons](#adding-icons-to-option-buttons) set up automatically, but you can override these with `colors()` or `icons()`. To customize the “Yes” label, you can use the `trueLabel` argument on the `boolean()` method:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean(trueLabel: 'Absolutely!')

```

To customize the “No” label, you can use the `falseLabel` argument on the `boolean()` method:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean(falseLabel: 'Not at all!')

```

## [​](#positioning-the-options-inline-with-each-other)Positioning the options inline with each other

You may wish to display the buttons `inline()` with each other:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean()
    ->inline()

```

Optionally, you may pass a boolean value to control if the buttons should be inline or not:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean()
    ->inline(FeatureFlag::active())

```

**As well as allowing a static value, the `inline()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#grouping-option-buttons)Grouping option buttons

You may wish to group option buttons together so they are more compact, using the `grouped()` method. This also makes them appear horizontally inline with each other:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean()
    ->grouped()

```

Optionally, you may pass a boolean value to control if the buttons should be grouped or not:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('feedback')
    ->label('Like this post?')
    ->boolean()
    ->grouped(FeatureFlag::active())

```

**As well as allowing a static value, the `grouped()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#selecting-multiple-buttons)Selecting multiple buttons

The `multiple()` method on the `ToggleButtons` component allows you to select multiple values from the list of options:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('technologies')
    ->multiple()
    ->options([
        'tailwind' => 'Tailwind CSS',
        'alpine' => 'Alpine.js',
        'laravel' => 'Laravel',
        'livewire' => 'Laravel Livewire',
    ])

```

These options are returned in JSON format. If you’re saving them using Eloquent, you should be sure to add an `array` [cast](https://laravel.com/docs/eloquent-mutators#array-and-json-casting) to the model property:

Copy

```
use Illuminate\Database\Eloquent\Model;

class App extends Model
{
    /**
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'technologies' => 'array',
        ];
    }

    // ...
}

```

Optionally, you may pass a boolean value to control if the buttons should allow multiple selections or not:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('technologies')
    ->multiple(FeatureFlag::active())
    ->options([
        'tailwind' => 'Tailwind CSS',
        'alpine' => 'Alpine.js',
        'laravel' => 'Laravel',
        'livewire' => 'Laravel Livewire',
    ])

```

**As well as allowing a static value, the `multiple()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#splitting-options-into-columns)Splitting options into columns

You may split options into columns by using the `columns()` method:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('technologies')
    ->options([
        // ...
    ])
    ->columns(2)

```

**As well as allowing a static value, the `columns()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

This method accepts the same options as the `columns()` method of the [grid](../schemas/layouts#grid-system). This allows you to responsively customize the number of columns at various breakpoints.

### [​](#setting-the-grid-direction)Setting the grid direction

By default, when you arrange buttons into columns, they will be listed in order vertically. If you’d like to list them horizontally, you may use the `gridDirection(GridDirection::Row)` method:

Copy

```
use Filament\Forms\Components\ToggleButtons;
use Filament\Support\Enums\GridDirection;

ToggleButtons::make('technologies')
    ->options([
        // ...
    ])
    ->columns(2)
    ->gridDirection(GridDirection::Row)

```

**As well as allowing a static value, the `gridDirection()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

## [​](#disabling-specific-options)Disabling specific options

You can disable specific options using the `disableOptionWhen()` method. It accepts a closure, in which you can check if the option with a specific `$value` should be disabled:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'scheduled' => 'Scheduled',
        'published' => 'Published',
    ])
    ->disableOptionWhen(fn (string $value): bool => $value === 'published')

```

**You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/forms/overview#field-utility-injection)

Field

$component

Filament\Forms\Components\Field

The current field component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current form data. Validation is not run.

Option label

$label

string | Illuminate\Contracts\Support\Htmlable

The label of the option to disable.

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

Raw state

$rawState

mixed

The current value of the field, before state casts were applied. Validation is not run.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the field. Validation is not run.

Option value

$value

mixed

The value of the option to disable.

If you want to retrieve the options that have not been disabled, e.g. for validation purposes, you can do so using `getEnabledOptions()`:

Copy

```
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'scheduled' => 'Scheduled',
        'published' => 'Published',
    ])
    ->disableOptionWhen(fn (string $value): bool => $value === 'published')
    ->in(fn (ToggleButtons $component): array => array_keys($component->getEnabledOptions()))

```

For more information about the `in()` function, please see the [Validation documentation](./validation#in).

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/forms/docs/18-toggle-buttons.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Color picker](/docs/5.x/forms/color-picker)[Slider](/docs/5.x/forms/slider)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
