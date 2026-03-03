## [​](#introduction)Introduction

The textarea allows you to interact with a multi-line string:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')

```

## [​](#resizing-the-textarea)Resizing the textarea

You may change the size of the textarea by defining the `rows()` and `cols()` methods:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->rows(10)
    ->cols(20)

```

**As well as allowing static values, the `rows()` and `cols()` methods also accept functions to dynamically calculate them. You can inject various utilities into the functions as parameters.**

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

### [​](#autosizing-the-textarea)Autosizing the textarea

You may allow the textarea to automatically resize to fit its content by setting the `autosize()` method:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->autosize()

```

Optionally, you may pass a boolean value to control if the textarea should be autosizeable or not:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->autosize(FeatureFlag::active())

```

**As well as allowing a static value, the `autosize()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#making-the-field-read-only)Making the field read-only

Not to be confused with [disabling the field](./overview#disabling-a-field), you may make the field “read-only” using the `readOnly()` method:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->readOnly()

```

There are a few differences, compared to [`disabled()`](./overview#disabling-a-field):

- When using `readOnly()`, the field will still be sent to the server when the form is submitted. It can be mutated with the browser console, or via JavaScript. You can use [`saved(false)`](./overview#preventing-a-field-from-being-saved) to prevent this.
- There are no styling changes, such as less opacity, when using `readOnly()`.
- The field is still focusable when using `readOnly()`.Optionally, you may pass a boolean value to control if the field should be read-only or not:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->readOnly(FeatureFlag::active())

```

**As well as allowing a static value, the `readOnly()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#disabling-grammarly-checks)Disabling Grammarly checks

If the user has Grammarly installed and you would like to prevent it from analyzing the contents of the textarea, you can use the `disableGrammarly()` method:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->disableGrammarly()

```

Optionally, you may pass a boolean value to control if the field should disable Grammarly checks or not:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->disableGrammarly(FeatureFlag::active())

```

**As well as allowing a static value, the `disableGrammarly()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#trimming-whitespace)Trimming whitespace

You can automatically trim whitespace from the beginning and end of the textarea value using the `trim()` method:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->trim()

```

You may want to enable trimming globally for all textareas, similar to Laravel’s `TrimStrings` middleware. You can do this in a service provider using the `configureUsing()` method:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::configureUsing(function (Textarea $component): void {
    $component->trim();
});

```

## [​](#textarea-validation)Textarea validation

As well as all rules listed on the [validation](./validation) page, there are additional rules that are specific to textareas.

### [​](#length-validation)Length validation

You may limit the length of the textarea by setting the `minLength()` and `maxLength()` methods. These methods add both frontend and backend validation:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('description')
    ->minLength(2)
    ->maxLength(1024)

```

You can also specify the exact length of the textarea by setting the `length()`. This method adds both frontend and backend validation:

Copy

```
use Filament\Forms\Components\Textarea;

Textarea::make('question')
    ->length(100)

```

**As well as allowing static values, the `minLength()`, `maxLength()` and `length()` methods also accept a function to dynamically calculate them. You can inject various utilities into the function as parameters.**

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

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/forms/docs/15-textarea.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[Tags input](/docs/5.x/forms/tags-input)[Key-value](/docs/5.x/forms/key-value)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
