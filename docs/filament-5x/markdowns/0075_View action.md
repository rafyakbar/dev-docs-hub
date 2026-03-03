## [​](#introduction)Introduction

Filament includes an action that is able to view Eloquent records. When the trigger button is clicked, a modal will open with information inside. Filament uses form fields to structure this information. All form fields are disabled, so they are not editable by the user. You may use it like so:

Copy

```
use Filament\Actions\ViewAction;
use Filament\Forms\Components\TextInput;

ViewAction::make()
    ->schema([
        TextInput::make('title')
            ->required()
            ->maxLength(255),
        // ...
    ])

```

## [​](#customizing-data-before-filling-the-form)Customizing data before filling the form

You may wish to modify the data from a record before it is filled into the form. To do this, you may use the `mutateRecordDataUsing()` method to modify the `$data` array, and return the modified version before it is filled into the form:

Copy

```
use Filament\Actions\ViewAction;

ViewAction::make()
    ->mutateRecordDataUsing(function (array $data): array {
        $data['user_id'] = auth()->id();

        return $data;
    })

```

**As well as `$data`, the `mutateRecordDataUsing()` function can inject various utilities as parameters.**

[Learn more about utility injection.](/docs/5.x/actions/overview#action-utility-injection)

Action

$action

Filament\Actions\Action

The current action instance.

Arguments

$arguments

array<string, mixed>

The array of arguments passed to the action when it was triggered.

Data

$data

array<string, mixed>

The array of data submitted from form fields in the action's modal. It will be empty before the modal form is submitted.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current action, if one is attached.

Mounted actions

$mountedActions

array<Filament\Actions\Action>

The array of actions that are currently mounted in the Livewire component. This is useful for accessing data from parent actions.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current action, if one is attached.

Schema

$schema

Filament\Schemas\Schema

[Actions in schemas only] The schema object that this action belongs to.

Schema component

$schemaComponent

Filament\Schemas\Components\Component

[Actions in schemas only] The schema component that this action belongs to.

Schema component state

$schemaComponentState

mixed

[Actions in schemas only] The current value of the schema component.

Schema get function

$schemaGet

Filament\Schemas\Components\Utilities\Get

[Actions in schemas only] A function for retrieving values from the schema data. Validation is not run on form fields.

Schema operation

$schemaOperation

string

[Actions in schemas only] The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Schema set function

$schemaSet

Filament\Schemas\Components\Utilities\Set

[Actions in schemas only] A function for setting values in the schema data.

Schema state

$schemaState

mixed

[Actions in schemas only] The current value of the schema that this action belongs to, like the current repeater item.

Selected Eloquent records

$selectedRecords

Illuminate\Support\Collection

[Bulk actions only] The Eloquent records selected in the table.

Table

$table

Filament\Tables\Table

[Actions in tables only] The table object that this action belongs to.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/actions/docs/06-view.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[Your logo here](https://github.com/sponsors/danharrin)

[Edit action](/docs/5.x/actions/edit)[Delete action](/docs/5.x/actions/delete)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
