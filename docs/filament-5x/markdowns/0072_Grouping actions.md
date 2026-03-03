## [​](#introduction)Introduction

You may group actions together into a dropdown menu by using an `ActionGroup` object. Groups may contain many actions, or other groups:

Copy

```
use Filament\Actions\Action;
use Filament\Actions\ActionGroup;

ActionGroup::make([
    Action::make('view'),
    Action::make('edit'),
    Action::make('delete'),
])

```

This page is about customizing the look of the group’s trigger button and dropdown.

## [​](#customizing-the-group-trigger-style)Customizing the group trigger style

The button which opens the dropdown may be customized in the same way as a normal action. [All the methods available for trigger buttons](./overview) may be used to customize the group trigger button:

Copy

```
use Filament\Actions\ActionGroup;
use Filament\Support\Enums\Size;

ActionGroup::make([
    // Array of actions
])
    ->label('More actions')
    ->icon('heroicon-m-ellipsis-vertical')
    ->size(Size::Small)
    ->color('primary')
    ->button()

```

### [​](#using-a-grouped-button-design)Using a grouped button design

Instead of a dropdown, an action group can render itself as a group of buttons. This design works with and without button labels. To use this feature, use the `buttonGroup()` method:

Copy

```
use Filament\Actions\Action;
use Filament\Actions\ActionGroup;
use Filament\Support\Icons\Heroicon;

ActionGroup::make([
    Action::make('edit')
        ->color('gray')
        ->icon(Heroicon::PencilSquare)
        ->hiddenLabel(),
    Action::make('delete')
        ->color('gray')
        ->icon(Heroicon::Trash)
        ->hiddenLabel(),
])
    ->buttonGroup()

```

## [​](#setting-the-placement-of-the-dropdown)Setting the placement of the dropdown

The dropdown may be positioned relative to the trigger button by using the `dropdownPlacement()` method:

Copy

```
use Filament\Actions\ActionGroup;

ActionGroup::make([
    // Array of actions
])
    ->dropdownPlacement('top-start')

```

**The `dropdownPlacement()` method also accepts a function to dynamically calculate the value. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/actions/overview#action-utility-injection)

Action group

$group

Filament\Actions\ActionGroup

The current action group instance.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current action group, if one is attached.

Mounted actions

$mountedActions

array<Filament\Actions\Action>

The array of actions that are currently mounted in the Livewire component. This is useful for accessing data from parent actions.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current action group, if one is attached.

Schema

$schema

Filament\Schemas\Schema

[Action groups in schemas only] The schema object that this action group belongs to.

Schema component

$schemaComponent

Filament\Schemas\Components\Component

[Action groups in schemas only] The schema component that this action group belongs to.

Schema component state

$schemaComponentState

mixed

[Action groups in schemas only] The current value of the schema component.

Schema get function

$schemaGet

Filament\Schemas\Components\Utilities\Get

[Action groups in schemas only] A function for retrieving values from the schema data. Validation is not run on form fields.

Schema operation

$schemaOperation

string

[Action groups in schemas only] The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Schema state

$schemaState

mixed

[Action groups in schemas only] The current value of the schema that this action group belongs to, like the current repeater item.

Table

$table

Filament\Tables\Table

[Action groups in tables only] The table object that this action group belongs to.

Alternatively, you may let the dropdown position be automatically determined based on the available space using the `dropdownAutoPlacement()` method:

Copy

```
use Filament\Actions\ActionGroup;

ActionGroup::make([
    // Array of actions
])
    ->dropdownAutoPlacement()

```

## [​](#adding-dividers-between-actions)Adding dividers between actions

You may add dividers between groups of actions by using nested `ActionGroup` objects:

Copy

```
use Filament\Actions\ActionGroup;

ActionGroup::make([
    ActionGroup::make([
        // Array of actions
    ])->dropdown(false),
    // Array of actions
])

```

The `dropdown(false)` method puts the actions inside the parent dropdown, instead of a new nested dropdown.

**The `dropdown()` method also accepts a function to dynamically calculate the value. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/actions/overview#action-utility-injection)

Action group

$group

Filament\Actions\ActionGroup

The current action group instance.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current action group, if one is attached.

Mounted actions

$mountedActions

array<Filament\Actions\Action>

The array of actions that are currently mounted in the Livewire component. This is useful for accessing data from parent actions.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current action group, if one is attached.

Schema

$schema

Filament\Schemas\Schema

[Action groups in schemas only] The schema object that this action group belongs to.

Schema component

$schemaComponent

Filament\Schemas\Components\Component

[Action groups in schemas only] The schema component that this action group belongs to.

Schema component state

$schemaComponentState

mixed

[Action groups in schemas only] The current value of the schema component.

Schema get function

$schemaGet

Filament\Schemas\Components\Utilities\Get

[Action groups in schemas only] A function for retrieving values from the schema data. Validation is not run on form fields.

Schema operation

$schemaOperation

string

[Action groups in schemas only] The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Schema state

$schemaState

mixed

[Action groups in schemas only] The current value of the schema that this action group belongs to, like the current repeater item.

Table

$table

Filament\Tables\Table

[Action groups in tables only] The table object that this action group belongs to.

## [​](#setting-the-width-of-the-dropdown)Setting the width of the dropdown

The dropdown may be set to a width by using the `dropdownWidth()` method. Options correspond to [Tailwind’s max-width scale](https://tailwindcss.com/docs/max-width). The options are `ExtraSmall`, `Small`, `Medium`, `Large`, `ExtraLarge`, `TwoExtraLarge`, `ThreeExtraLarge`, `FourExtraLarge`, `FiveExtraLarge`, `SixExtraLarge` and `SevenExtraLarge`:

Copy

```
use Filament\Actions\ActionGroup;
use Filament\Support\Enums\Width;

ActionGroup::make([
    // Array of actions
])
    ->dropdownWidth(Width::ExtraSmall)

```

**The `dropdownWidth()` method also accepts a function to dynamically calculate the value. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/actions/overview#action-utility-injection)

Action group

$group

Filament\Actions\ActionGroup

The current action group instance.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current action group, if one is attached.

Mounted actions

$mountedActions

array<Filament\Actions\Action>

The array of actions that are currently mounted in the Livewire component. This is useful for accessing data from parent actions.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current action group, if one is attached.

Schema

$schema

Filament\Schemas\Schema

[Action groups in schemas only] The schema object that this action group belongs to.

Schema component

$schemaComponent

Filament\Schemas\Components\Component

[Action groups in schemas only] The schema component that this action group belongs to.

Schema component state

$schemaComponentState

mixed

[Action groups in schemas only] The current value of the schema component.

Schema get function

$schemaGet

Filament\Schemas\Components\Utilities\Get

[Action groups in schemas only] A function for retrieving values from the schema data. Validation is not run on form fields.

Schema operation

$schemaOperation

string

[Action groups in schemas only] The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Schema state

$schemaState

mixed

[Action groups in schemas only] The current value of the schema that this action group belongs to, like the current repeater item.

Table

$table

Filament\Tables\Table

[Action groups in tables only] The table object that this action group belongs to.

## [​](#controlling-the-dropdown-offset)Controlling the dropdown offset

You may control the offset of the dropdown using the `dropdownOffset()` method, by default the offset is set to `8`.

Copy

```
use Filament\Actions\ActionGroup;

ActionGroup::make([
    // Array of actions
])
    ->dropdownOffset(16)

```

**The `dropdownOffset()` method also accepts a function to dynamically calculate the value. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/actions/overview#action-utility-injection)

Action group

$group

Filament\Actions\ActionGroup

The current action group instance.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current action group, if one is attached.

Mounted actions

$mountedActions

array<Filament\Actions\Action>

The array of actions that are currently mounted in the Livewire component. This is useful for accessing data from parent actions.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current action group, if one is attached.

Schema

$schema

Filament\Schemas\Schema

[Action groups in schemas only] The schema object that this action group belongs to.

Schema component

$schemaComponent

Filament\Schemas\Components\Component

[Action groups in schemas only] The schema component that this action group belongs to.

Schema component state

$schemaComponentState

mixed

[Action groups in schemas only] The current value of the schema component.

Schema get function

$schemaGet

Filament\Schemas\Components\Utilities\Get

[Action groups in schemas only] A function for retrieving values from the schema data. Validation is not run on form fields.

Schema operation

$schemaOperation

string

[Action groups in schemas only] The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Schema state

$schemaState

mixed

[Action groups in schemas only] The current value of the schema that this action group belongs to, like the current repeater item.

Table

$table

Filament\Tables\Table

[Action groups in tables only] The table object that this action group belongs to.

## [​](#controlling-the-maximum-height-of-the-dropdown)Controlling the maximum height of the dropdown

The dropdown content can have a maximum height using the `maxHeight()` method, so that it scrolls. You can pass a [CSS length](https://developer.mozilla.org/en-US/docs/Web/CSS/length):

Copy

```
use Filament\Actions\ActionGroup;

ActionGroup::make([
    // Array of actions
])
    ->maxHeight('400px')

```

**The `maxHeight()` method also accepts a function to dynamically calculate the value. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/actions/overview#action-utility-injection)

Action group

$group

Filament\Actions\ActionGroup

The current action group instance.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current action group, if one is attached.

Mounted actions

$mountedActions

array<Filament\Actions\Action>

The array of actions that are currently mounted in the Livewire component. This is useful for accessing data from parent actions.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current action group, if one is attached.

Schema

$schema

Filament\Schemas\Schema

[Action groups in schemas only] The schema object that this action group belongs to.

Schema component

$schemaComponent

Filament\Schemas\Components\Component

[Action groups in schemas only] The schema component that this action group belongs to.

Schema component state

$schemaComponentState

mixed

[Action groups in schemas only] The current value of the schema component.

Schema get function

$schemaGet

Filament\Schemas\Components\Utilities\Get

[Action groups in schemas only] A function for retrieving values from the schema data. Validation is not run on form fields.

Schema operation

$schemaOperation

string

[Action groups in schemas only] The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Schema state

$schemaState

mixed

[Action groups in schemas only] The current value of the schema that this action group belongs to, like the current repeater item.

Table

$table

Filament\Tables\Table

[Action groups in tables only] The table object that this action group belongs to.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/actions/docs/03-grouping-actions.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://baiz.ai](https://baiz.ai "Baiz.ai")[Your logo here](https://github.com/sponsors/danharrin)

[Modals](/docs/5.x/actions/modals)[Create action](/docs/5.x/actions/create)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
