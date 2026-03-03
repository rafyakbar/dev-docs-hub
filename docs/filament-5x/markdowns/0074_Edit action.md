## [​](#introduction)Introduction

Filament includes an action that is able to edit Eloquent records. When the trigger button is clicked, a modal will open with a form inside. The user fills the form, and that data is validated and saved into the database. You may use it like so:

Copy

```
use Filament\Actions\EditAction;
use Filament\Forms\Components\TextInput;

EditAction::make()
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
use Filament\Actions\EditAction;

EditAction::make()
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

## [​](#customizing-data-before-saving)Customizing data before saving

Sometimes, you may wish to modify form data before it is finally saved to the database. To do this, you may use the `mutateDataUsing()` method, which has access to the `$data` as an array, and returns the modified version:

Copy

```
use Filament\Actions\EditAction;

EditAction::make()
    ->mutateDataUsing(function (array $data): array {
        $data['last_edited_by_id'] = auth()->id();

        return $data;
    })

```

**As well as `$data`, the `mutateDataUsing()` function can inject various utilities as parameters.**

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

## [​](#customizing-the-saving-process)Customizing the saving process

You can tweak how the record is updated with the `using()` method:

Copy

```
use Filament\Actions\EditAction;
use Illuminate\Database\Eloquent\Model;

EditAction::make()
    ->using(function (Model $record, array $data): Model {
        $record->update($data);

        return $record;
    })

```

**As well as `$record` and `$data`, the `using()` function can inject various utilities as parameters.**

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

## [​](#redirecting-after-saving)Redirecting after saving

You may set up a custom redirect when the form is submitted using the `successRedirectUrl()` method:

Copy

```
use Filament\Actions\EditAction;

EditAction::make()
    ->successRedirectUrl(route('posts.list'))

```

If you want to redirect using the created record, use the `$record` parameter:

Copy

```
use Filament\Actions\EditAction;
use Illuminate\Database\Eloquent\Model;

EditAction::make()
    ->successRedirectUrl(fn (Model $record): string => route('posts.view', [
        'post' => $record,
    ]))

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

## [​](#customizing-the-save-notification)Customizing the save notification

When the record is successfully updated, a notification is dispatched to the user, which indicates the success of their action. To customize the title of this notification, use the `successNotificationTitle()` method:

Copy

```
use Filament\Actions\EditAction;

EditAction::make()
    ->successNotificationTitle('User updated')

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
use Filament\Actions\EditAction;
use Filament\Notifications\Notification;

EditAction::make()
    ->successNotification(
       Notification::make()
            ->success()
            ->title('User updated')
            ->body('The user has been saved successfully.'),
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
use Filament\Actions\EditAction;

EditAction::make()
    ->successNotification(null)

```

## [​](#lifecycle-hooks)Lifecycle hooks

Hooks may be used to execute code at various points within the action’s lifecycle, like before a form is saved. There are several available hooks:

Copy

```
use Filament\Actions\EditAction;

EditAction::make()
    ->beforeFormFilled(function () {
        // Runs before the form fields are populated from the database.
    })
    ->afterFormFilled(function () {
        // Runs after the form fields are populated from the database.
    })
    ->beforeFormValidated(function () {
        // Runs before the form fields are validated when the form is saved.
    })
    ->afterFormValidated(function () {
        // Runs after the form fields are validated when the form is saved.
    })
    ->before(function () {
        // Runs before the form fields are saved to the database.
    })
    ->after(function () {
        // Runs after the form fields are saved to the database.
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

## [​](#halting-the-saving-process)Halting the saving process

At any time, you may call `$action->halt()` from inside a lifecycle hook or mutation method, which will halt the entire saving process:

Copy

```
use App\Models\Post;
use Filament\Actions\Action;
use Filament\Actions\EditAction;
use Filament\Notifications\Notification;

EditAction::make()
    ->before(function (EditAction $action, Post $record) {
        if (! $record->team->subscribed()) {
            Notification::make()
                ->warning()
                ->title('You don\'t have an active subscription!')
                ->body('Choose a plan to continue.')
                ->persistent()
                ->actions([
                    Action::make('subscribe')
                        ->button()
                        ->url(route('subscribe'), shouldOpenInNewTab: true),
                ])
                ->send();
  
            $action->halt();
        }
    })

```

If you’d like the action modal to close too, you can completely `cancel()` the action instead of halting it:

Copy

```
$action->cancel();

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/actions/docs/05-edit.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://baiz.ai](https://baiz.ai "Baiz.ai")[Your logo here](https://github.com/sponsors/danharrin)

[Create action](/docs/5.x/actions/create)[View action](/docs/5.x/actions/view)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
