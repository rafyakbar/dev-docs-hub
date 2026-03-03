## [​](#introduction)Introduction

Filament includes an action that is able to restore [soft-deleted](https://laravel.com/docs/eloquent#soft-deleting) Eloquent records. When the trigger button is clicked, a modal asks the user for confirmation. You may use it like so:

Copy

```
use Filament\Actions\RestoreAction;

RestoreAction::make()

```

Or if you want to add it as a table bulk action, so that the user can choose which rows to restore, use `Filament\Actions\RestoreBulkAction`:

Copy

```
use Filament\Actions\RestoreBulkAction;
use Filament\Tables\Table;

public function table(Table $table): Table
{
    return $table
        ->toolbarActions([
            RestoreBulkAction::make(),
        ]);
}

```

## [​](#redirecting-after-restoring)Redirecting after restoring

You may set up a custom redirect when the form is submitted using the `successRedirectUrl()` method:

Copy

```
use Filament\Actions\RestoreAction;

RestoreAction::make()
    ->successRedirectUrl(route('posts.list'))

```

**As well as `$record`, the `successRedirectUrl()` function can inject various utilities as parameters.**

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

## [​](#customizing-the-restore-notification)Customizing the restore notification

When the record is successfully restored, a notification is dispatched to the user, which indicates the success of their action. To customize the title of this notification, use the `successNotificationTitle()` method:

Copy

```
use Filament\Actions\RestoreAction;

RestoreAction::make()
    ->successNotificationTitle('User restored')

```

**As well as allowing a static value, the `successNotificationTitle()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

You may customize the entire notification using the `successNotification()` method:

Copy

```
use Filament\Actions\RestoreAction;
use Filament\Notifications\Notification;

RestoreAction::make()
    ->successNotification(
       Notification::make()
            ->success()
            ->title('User restored')
            ->body('The user has been restored successfully.'),
    )

```

**As well as allowing a static value, the `successNotification()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

Notification

$notification

Filament\Notifications\Notification

The default notification object, which could be a useful starting point for customization.

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

To disable the notification altogether, use the `successNotification(null)` method:

Copy

```
use Filament\Actions\RestoreAction;

RestoreAction::make()
    ->successNotification(null)

```

## [​](#lifecycle-hooks)Lifecycle hooks

You can use the `before()` and `after()` methods to execute code before and after a record is restored:

Copy

```
use Filament\Actions\RestoreAction;

RestoreAction::make()
    ->before(function () {
        // ...
    })
    ->after(function () {
        // ...
    })

```

**These hook functions can inject various utilities as parameters.**

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

## [​](#improving-the-performance-of-restore-bulk-actions)Improving the performance of restore bulk actions

By default, the `RestoreBulkAction` will load all Eloquent records into memory, before looping over them and restoring them one by one. If you are restoring a large number of records, you may want to use the `chunkSelectedRecords()` method to fetch a smaller number of records at a time. This will reduce the memory usage of your application:

Copy

```
use Filament\Actions\RestoreBulkAction;

RestoreBulkAction::make()
    ->chunkSelectedRecords(250)

```

Filament loads Eloquent records into memory before restoring them for two reasons:

- To allow individual records in the collection to be authorized with a model policy before restoration (using `authorizeIndividualRecords('restore')`, for example).
- To ensure that model events are run when restoring records, such as the `restoring` and `restored` events in a model observer.If you do not require individual record policy authorization and model events, you can use the `fetchSelectedRecords(false)` method, which will not fetch the records into memory before restoring them, and instead will restore them in a single query:

Copy

```
use Filament\Actions\RestoreBulkAction;

RestoreBulkAction::make()
    ->fetchSelectedRecords(false)

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/actions/docs/10-restore.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[Force-delete action](/docs/5.x/actions/force-delete)[Import action](/docs/5.x/actions/import)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
