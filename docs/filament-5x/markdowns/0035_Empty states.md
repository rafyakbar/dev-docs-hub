## [​](#introduction)Introduction

You can display an empty state in your schema to communicate that there is no content to show yet, and to guide the user towards the next action. An empty state requires a heading, but can also have a `description()`, [`icon()`](#adding-an-icon-to-the-empty-state) and [`footer()`](#inserting-actions-and-other-components-in-the-footer-of-an-empty-state):

Copy

```
use Filament\Actions\Action;
use Filament\Schemas\Components\EmptyState;
use Filament\Support\Icons\Heroicon;

EmptyState::make('No users yet')
    ->description('Get started by creating a new user.')
    ->icon(Heroicon::OutlinedUser)
    ->footer([
        Action::make('createUser')
            ->icon(Heroicon::Plus),
    ])

```

**As well as allowing static values, the `make()` and `description()` methods also accept functions to dynamically calculate them. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/schemas/overview#component-utility-injection)

Component

$component

Filament\Schemas\Components\Component

The current component instance.

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

## [​](#adding-an-icon-to-the-empty-state)Adding an icon to the empty state

You may add an [icon](../styling/icons) to the empty state using the `icon()` method:

Copy

```
use Filament\Schemas\Components\EmptyState;
use Filament\Support\Icons\Heroicon;

EmptyState::make('No users yet')
    ->description('Get started by creating a new user.')
    ->icon(Heroicon::OutlinedUser)

```

**As well as allowing a static value, the `icon()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/schemas/overview#component-utility-injection)

Component

$component

Filament\Schemas\Components\Component

The current component instance.

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

## [​](#inserting-actions-and-other-components-in-the-footer-of-an-empty-state)Inserting actions and other components in the footer of an empty state

You may insert [actions](../actions) and any other schema component (usually [prime components](./primes)) into the footer of an empty state by passing an array of components to the `footer()` method:

Copy

```
use Filament\Actions\Action;
use Filament\Schemas\Components\EmptyState;

EmptyState::make('No users yet')
    ->description('Get started by creating a new user.')
    ->footer([
        Action::make('createUser')
            ->icon(Heroicon::Plus),
    ])

```

**As well as allowing a static value, the `footer()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/schemas/overview#component-utility-injection)

Component

$component

Filament\Schemas\Components\Component

The current component instance.

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

## [​](#removing-the-empty-state-container)Removing the empty state container

By default, empty states have a background color, shadow and border. You may remove these styles and just render the content of the empty state without the container using `contained(false)`:

Copy

```
use Filament\Schemas\Components\EmptyState;

EmptyState::make('No users yet')
    ->description('Get started by creating a new user.')
    ->contained(false)

```

**As well as allowing a static value, the `contained()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/schemas/overview#component-utility-injection)

Component

$component

Filament\Schemas\Components\Component

The current component instance.

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

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/schemas/docs/07-empty-states.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[Your logo here](https://github.com/sponsors/danharrin)

[Callouts](/docs/5.x/schemas/callouts)[Prime components](/docs/5.x/schemas/primes)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
