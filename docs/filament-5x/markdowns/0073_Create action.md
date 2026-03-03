## [​](#introduction)Introduction

Filament includes an action that is able to create Eloquent records. When the trigger button is clicked, a modal will open with a form inside. The user fills the form, and that data is validated and saved into the database. You may use it like so:

Copy

```
use Filament\Actions\CreateAction;
use Filament\Forms\Components\TextInput;

CreateAction::make()
    ->schema([
        TextInput::make('title')
            ->required()
            ->maxLength(255),
        // ...
    ])

```

## [​](#customizing-data-before-saving)Customizing data before saving

Sometimes, you may wish to modify form data before it is finally saved to the database. To do this, you may use the `mutateDataUsing()` method, which has access to the `$data` as an array, and returns the modified version:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->mutateDataUsing(function (array $data): array {
        $data['user_id'] = auth()->id();

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

## [​](#customizing-the-creation-process)Customizing the creation process

You can tweak how the record is created with the `using()` method:

Copy

```
use Filament\Actions\CreateAction;
use Illuminate\Database\Eloquent\Model;

CreateAction::make()
    ->using(function (array $data, string $model): Model {
        return $model::create($data);
    })

```

`$model` is the class name of the model, but you can replace this with your own hard-coded class if you wish.

**As well as `$data` and `$model`, the `using()` function can inject various utilities as parameters.**

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

## [​](#redirecting-after-creation)Redirecting after creation

You may set up a custom redirect when the form is submitted using the `successRedirectUrl()` method:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->successRedirectUrl(route('posts.list'))

```

If you want to redirect using the created record, use the `$record` parameter:

Copy

```
use Filament\Actions\CreateAction;
use Illuminate\Database\Eloquent\Model;

CreateAction::make()
    ->successRedirectUrl(fn (Model $record): string => route('posts.edit', [
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

When the record is successfully created, a notification is dispatched to the user, which indicates the success of their action. To customize the title of this notification, use the `successNotificationTitle()` method:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->successNotificationTitle('User registered')

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
use Filament\Actions\CreateAction;
use Filament\Notifications\Notification;

CreateAction::make()
    ->successNotification(
       Notification::make()
            ->success()
            ->title('User registered')
            ->body('The user has been created successfully.'),
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
use Filament\Actions\CreateAction;

CreateAction::make()
    ->successNotification(null)

```

## [​](#lifecycle-hooks)Lifecycle hooks

Hooks may be used to execute code at various points within the action’s lifecycle, like before a form is saved. There are several available hooks:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->beforeFormFilled(function () {
        // Runs before the form fields are populated with their default values.
    })
    ->afterFormFilled(function () {
        // Runs after the form fields are populated with their default values.
    })
    ->beforeFormValidated(function () {
        // Runs before the form fields are validated when the form is submitted.
    })
    ->afterFormValidated(function () {
        // Runs after the form fields are validated when the form is submitted.
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

## [​](#halting-the-creation-process)Halting the creation process

At any time, you may call `$action->halt()` from inside a lifecycle hook or mutation method, which will halt the entire creation process:

Copy

```
use App\Models\Post;
use Filament\Actions\Action;
use Filament\Actions\CreateAction;
use Filament\Notifications\Notification;

CreateAction::make()
    ->before(function (CreateAction $action, Post $record) {
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

## [​](#using-a-wizard)Using a wizard

You may easily transform the creation process into a multistep wizard. Instead of using a `schema()`, define a `steps()` array and pass your `Step` objects:

Copy

```
use Filament\Actions\CreateAction;
use Filament\Forms\Components\MarkdownEditor;
use Filament\Forms\Components\TextInput;
use Filament\Forms\Components\Toggle;
use Filament\Schemas\Components\Wizard\Step;

CreateAction::make()
    ->steps([
        Step::make('Name')
            ->description('Give the category a unique name')
            ->schema([
                TextInput::make('name')
                    ->required()
                    ->live()
                    ->afterStateUpdated(fn ($state, callable $set) => $set('slug', Str::slug($state))),
                TextInput::make('slug')
                    ->disabled()
                    ->required()
                    ->unique(Category::class, 'slug'),
            ])
            ->columns(2),
        Step::make('Description')
            ->description('Add some extra details')
            ->schema([
                MarkdownEditor::make('description'),
            ]),
        Step::make('Visibility')
            ->description('Control who can view it')
            ->schema([
                Toggle::make('is_visible')
                    ->label('Visible to customers.')
                    ->default(true),
            ]),
    ])

```

Now, create a new record to see your wizard in action! Edit will still use the form defined within the resource class. If you’d like to allow free navigation, so all the steps are skippable, use the `skippableSteps()` method:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->steps([
        // ...
    ])
    ->skippableSteps()

```

## [​](#creating-another-record)Creating another record

### [​](#modifying-the-create-another-action)Modifying the create another action

If you’d like to modify the “create another” action, you may use the `createAnotherAction()` method, passing a function that returns an action. All methods that are available to [customize action trigger buttons](./overview) can be used:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->createAnotherAction(fn (Action $action): Action => $action->label('Custom create another label'))

```

### [​](#disabling-create-another)Disabling create another

If you’d like to remove the “create another” button from the modal, you can use the `createAnother(false)` method:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->createAnother(false)

```

**As well as allowing a static value, the `createAnother()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

### [​](#preserving-data-when-creating-another)Preserving data when creating another

By default, when the user uses the “create and create another” feature, all the form data is cleared so the user can start fresh. If you’d like to preserve some of the data in the form, you may use the `preserveFormDataWhenCreatingAnother()` method, passing an array of fields to preserve:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->preserveFormDataWhenCreatingAnother(['is_admin', 'organization'])

```

Alternatively, you can define a function that returns an array of the `$data` to preserve:

Copy

```
use Filament\Actions\CreateAction;
use Illuminate\Support\Arr;

CreateAction::make()
    ->preserveFormDataWhenCreatingAnother(fn (array $data): array => Arr::only($data, ['is_admin', 'organization']))

```

To preserve all the data, return the entire `$data` array:

Copy

```
use Filament\Actions\CreateAction;

CreateAction::make()
    ->preserveFormDataWhenCreatingAnother(fn (array $data): array => $data)

```

**As well as allowing a static value, the `preserveFormDataWhenCreatingAnother()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/actions/docs/04-create.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[Your logo here](https://github.com/sponsors/danharrin)

[Grouping actions](/docs/5.x/actions/grouping-actions)[Edit action](/docs/5.x/actions/edit)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
