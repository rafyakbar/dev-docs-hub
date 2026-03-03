## [​](#introduction)Introduction

The toggle component, similar to a [checkbox](./checkbox), allows you to interact a boolean value.

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('is_admin')

```

If you’re saving the boolean value using Eloquent, you should be sure to add a `boolean` [cast](https://laravel.com/docs/eloquent-mutators#attribute-casting) to the model property:

Copy

```
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'is_admin' => 'boolean',
        ];
    }

    // ...
}

```

## [​](#adding-icons-to-the-toggle-button)Adding icons to the toggle button

Toggles may also use an [icon](../styling/icons) to represent the “on” and “off” state of the button. To add an icon to the “on” state, use the `onIcon()` method. To add an icon to the “off” state, use the `offIcon()` method:

Copy

```
use Filament\Forms\Components\Toggle;
use Filament\Support\Icons\Heroicon;

Toggle::make('is_admin')
    ->onIcon(Heroicon::Bolt)
    ->offIcon(Heroicon::User)

```

**As well as allowing static values, the `onIcon()` and `offIcon()` methods also accept functions to dynamically calculate them. You can inject various utilities into the function as parameters.**

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

## [​](#customizing-the-color-of-the-toggle-button)Customizing the color of the toggle button

You may also customize the [color](../styling/colors) representing the “on” or “off” state of the toggle. To add a color to the “on” state, use the `onColor()` method. To add a color to the “off” state, use the `offColor()` method:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('is_admin')
    ->onColor('success')
    ->offColor('danger')

```

**As well as allowing static values, the `onColor()` and `offColor()` methods also accept functions to dynamically calculate them. You can inject various utilities into the function as parameters.**

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

## [​](#positioning-the-label-above)Positioning the label above

Toggle fields have two layout modes, inline and stacked. By default, they are inline. When the toggle is inline, its label is adjacent to it:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('is_admin')
    ->inline()

```

When the toggle is stacked, its label is above it:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('is_admin')
    ->inline(false)

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

## [​](#toggle-validation)Toggle validation

As well as all rules listed on the [validation](./validation) page, there are additional rules that are specific to toggles.

### [​](#accepted-validation)Accepted validation

You may ensure that the toggle is “on” using the `accepted()` method:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('terms_of_service')
    ->accepted()

```

Optionally, you may pass a boolean value to control if the validation rule should be applied or not:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('terms_of_service')
    ->accepted(FeatureFlag::active())

```

**As well as allowing a static value, the `accepted()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

### [​](#declined-validation)Declined validation

You may ensure that the toggle is “off” using the `declined()` method:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('is_under_18')
    ->declined()

```

Optionally, you may pass a boolean value to control if the validation rule should be applied or not:

Copy

```
use Filament\Forms\Components\Toggle;

Toggle::make('is_under_18')
    ->declined(FeatureFlag::active())

```

**As well as allowing a static value, the `declined()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/forms/docs/05-toggle.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[Your logo here](https://github.com/sponsors/danharrin)

[Checkbox](/docs/5.x/forms/checkbox)[Checkbox list](/docs/5.x/forms/checkbox-list)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
