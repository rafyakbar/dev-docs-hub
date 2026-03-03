## [​](#introduction)Introduction

“Action” is a word that is used quite a bit within the Laravel community. Traditionally, action PHP classes handle “doing” something in your application’s business logic. For instance, logging a user in, sending an email, or creating a new user record in the database. In Filament, actions also handle “doing” something in your app. However, they are a bit different from traditional actions. They are designed to be used in the context of a user interface. For instance, you might have a button to delete a client record, which opens a modal to confirm your decision. When the user clicks the “Delete” button in the modal, the client is deleted. This whole workflow is an “action”.

Copy

```
use Filament\Actions\Action;

Action::make('delete')
    ->requiresConfirmation()
    ->action(fn () => $this->client->delete())

```

Actions can also collect extra information from the user. For instance, you might have a button to email a client. When the user clicks the button, a modal opens to collect the email subject and body. When the user clicks the “Send” button in the modal, the email is sent:

Copy

```
use Filament\Actions\Action;
use Filament\Forms\Components\RichEditor;
use Filament\Forms\Components\TextInput;
use Illuminate\Support\Facades\Mail;

Action::make('sendEmail')
    ->schema([
        TextInput::make('subject')->required(),
        RichEditor::make('body')->required(),
    ])
    ->action(function (array $data) {
        Mail::to($this->client)
            ->send(new GenericEmail(
                subject: $data['subject'],
                body: $data['body'],
            ));
    })

```

**As well as `$data`, the `action()` function can inject various utilities as parameters.**

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

Usually, actions get executed without redirecting the user away from the page. This is because we extensively use Livewire. However, actions can be much simpler, and don’t even need a modal. You can pass a URL to an action, and when the user clicks on the button, they are redirected to that page:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))

```

**As well as allowing a static value, the `url()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

The entire look of the action’s trigger button and the modal is customizable using fluent PHP methods. We provide a sensible and consistent styling for the UI, but all of this is customizable with CSS.

## [​](#available-actions)Available actions

Filament includes several actions that you can add to your app. Their aim is to simplify the most common Eloquent-related actions:

- [Create](./create)
- [Edit](./edit)
- [View](./view)
- [Delete](./delete)
- [Replicate](./replicate)
- [Force-delete](./force-delete)
- [Restore](./restore)
- [Import](./import)
- [Export](./export)You can also create your own actions to do anything, these are just common ones that we include out of the box.

## [​](#choosing-a-trigger-style)Choosing a trigger style

Out of the box, action triggers have 4 styles - “button”, “link”, “icon button”, and “badge”. “Button” triggers have a background color, label, and optionally an [icon](#setting-an-icon). Usually, this is the default button style, but you can use it manually with the `button()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->button()

```

“Link” triggers have no background color. They must have a label and optionally an [icon](#setting-an-icon). They look like a link that you might find embedded within text. You can switch to that style with the `link()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->link()

```

“Icon button” triggers are circular buttons with an [icon](#setting-an-icon) and no label. You can switch to that style with the `iconButton()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->icon('heroicon-m-pencil-square')
    ->iconButton()

```

“Badge” triggers have a background color, label, and optionally an [icon](#setting-an-icon). You can use a badge as trigger using the `badge()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->badge()

```

### [​](#using-an-icon-button-on-mobile-devices-only)Using an icon button on mobile devices only

You may want to use a button style with a label on desktop, but remove the label on mobile. This will transform it into an icon button. You can do this with the `labeledFrom()` method, passing in the responsive [breakpoint](https://tailwindcss.com/docs/responsive-design#overview) at which you want the label to be added to the button:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->icon('heroicon-m-pencil-square')
    ->button()
    ->labeledFrom('md')

```

## [​](#setting-a-label)Setting a label

By default, the label of the trigger button is generated from its name. You may customize this using the `label()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->label('Edit post')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))

```

**As well as allowing a static value, the `label()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#setting-a-color)Setting a color

Buttons may have a [color](../styling/colors) to indicate their significance:

Copy

```
use Filament\Actions\Action;

Action::make('delete')
    ->color('danger')

```

**As well as allowing a static value, the `color()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#setting-a-size)Setting a size

Buttons come in 3 sizes - `Size::Small`, `Size::Medium` or `Size::Large`. You can change the size of the action’s trigger using the `size()` method:

Copy

```
use Filament\Actions\Action;
use Filament\Support\Enums\Size;

Action::make('create')
    ->size(Size::Large)

```

**As well as allowing a static value, the `size()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#setting-an-icon)Setting an icon

Buttons may have an [icon](../styling/icons) to add more detail to the UI. You can set the icon using the `icon()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->icon('heroicon-m-pencil-square')

```

**As well as allowing a static value, the `icon()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

You can also change the icon’s position to be after the label instead of before it, using the `iconPosition()` method:

Copy

```
use Filament\Actions\Action;
use Filament\Support\Enums\IconPosition;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->icon('heroicon-m-pencil-square')
    ->iconPosition(IconPosition::After)

```

**As well as allowing a static value, the `iconPosition()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#authorization)Authorization

You may conditionally show or hide actions for certain users. To do this, you can use either the `visible()` or `hidden()` methods:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->visible(auth()->user()->can('update', $this->post))

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->hidden(! auth()->user()->can('update', $this->post))

```

This is useful for authorization of certain actions to only users who have permission.

**As well as allowing static values, the `visible()` and `hidden()` methods also accept functions to dynamically calculate them. You can inject various utilities into the functions as parameters.**

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

### [​](#authorization-using-a-policy)Authorization using a policy

You can use a policy to authorize an action. To do this, pass the name of the policy method to the `authorize()` method, and Filament will use the current Eloquent model for that action to find the correct policy:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->authorize('update')

```

If you’re using an action in a panel resource or relation manager, you don’t need to use the `authorize()` method, since Filament will automatically read the policy based on the resource model for the built-in actions like `CreateAction`, `EditAction` and `DeleteAction`. For more information, visit the [resource authorization](../resources/overview#authorization) section.

If your policy method returns a [response message](https://laravel.com/docs/authorization#policy-responses), you can disable the action instead of hiding it, and add a tooltip containing the message, using the `authorizationTooltip()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->authorize('update')
    ->authorizationTooltip()

```

You may instead allow the action to still be clickable even if the user is not authorized, but send a notification containing the response message, using the `authorizationNotification()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->authorize('update')
    ->authorizationNotification()

```

### [​](#disabling-a-button)Disabling a button

If you want to disable a button instead of hiding it, you can use the `disabled()` method:

Copy

```
use Filament\Actions\Action;

Action::make('delete')
    ->disabled()

```

You can conditionally disable a button by passing a boolean to it:

Copy

```
use Filament\Actions\Action;

Action::make('delete')
    ->disabled(! auth()->user()->can('delete', $this->post))

```

**As well as allowing a static value, the `disabled()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#registering-keybindings)Registering keybindings

You can attach keyboard shortcuts to trigger buttons. These use the same key codes as [Mousetrap](https://craig.is/killing/mice):

Copy

```
use Filament\Actions\Action;

Action::make('save')
    ->action(fn () => $this->save())
    ->keyBindings(['command+s', 'ctrl+s'])

```

**As well as allowing a static value, the `keyBindings()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#adding-a-badge-to-the-corner-of-the-button)Adding a badge to the corner of the button

You can add a badge to the corner of the button, to display whatever you want. It’s useful for displaying a count of something, or a status indicator:

Copy

```
use Filament\Actions\Action;

Action::make('filter')
    ->iconButton()
    ->icon('heroicon-m-funnel')
    ->badge(5)

```

**As well as allowing a static value, the `badge()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

You can also pass a [color](../styling/colors) to be used for the badge:

Copy

```
use Filament\Actions\Action;

Action::make('filter')
    ->iconButton()
    ->icon('heroicon-m-funnel')
    ->badge(5)
    ->badgeColor('success')

```

**As well as allowing a static value, the `badgeColor()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#outlined-button-style)Outlined button style

When you’re using the “button” trigger style, you might wish to make it less prominent. You could use a different [color](#setting-a-color), but sometimes you might want to make it outlined instead. You can do this with the `outlined()` method:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->button()
    ->outlined()

```

Optionally, you may pass a boolean value to control if the label should be hidden or not:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->button()
    ->outlined(FeatureFlag::active())

```

**As well as allowing a static value, the `outlined()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#adding-extra-html-attributes-to-an-action)Adding extra HTML attributes to an action

You can pass extra HTML attributes to the action via the `extraAttributes()` method, which will be merged onto its outer HTML element. The attributes should be represented by an array, where the key is the attribute name and the value is the attribute value:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->extraAttributes([
        'title' => 'Edit this post',
    ])

```

**As well as allowing a static value, the `extraAttributes()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

By default, calling `extraAttributes()` multiple times will overwrite the previous attributes. If you wish to merge the attributes instead, you can pass `merge: true` to the method.

## [​](#rate-limiting-actions)Rate limiting actions

You can rate limit actions by using the `rateLimit()` method. This method accepts the number of attempts per minute that a user IP address can make. If the user exceeds this limit, the action will not run and a notification will be shown:

Copy

```
use Filament\Actions\Action;

Action::make('delete')
    ->rateLimit(5)

```

If the action opens a modal, the rate limit will be applied when the modal is submitted. If an action is opened with arguments or for a specific Eloquent record, the rate limit will apply to each unique combination of arguments or record for each action. The rate limit is also unique to the current Livewire component / page in a panel.

**As well as allowing a static value, the `rateLimit()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

## [​](#customizing-the-rate-limited-notification)Customizing the rate limited notification

When an action is rate limited, a notification is dispatched to the user, which indicates the rate limit. To customize the title of this notification, use the `rateLimitedNotificationTitle()` method:

Copy

```
use Filament\Actions\DeleteAction;

DeleteAction::make()
    ->rateLimit(5)
    ->rateLimitedNotificationTitle('Slow down!')

```

**As well as allowing a static value, the `rateLimitedNotificationTitle()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

You may customize the entire notification using the `rateLimitedNotification()` method:

Copy

```
use DanHarrin\LivewireRateLimiting\Exceptions\TooManyRequestsException;
use Filament\Actions\DeleteAction;
use Filament\Notifications\Notification;

DeleteAction::make()
    ->rateLimit(5)
    ->rateLimitedNotification(
       fn (TooManyRequestsException $exception): Notification => Notification::make()
            ->warning()
            ->title('Slow down!')
            ->body("You can try deleting again in {$exception->secondsUntilAvailable} seconds."),
    )

```

**As well as allowing a static value, the `rateLimitedNotification()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

Exception

$exception

DanHarrin\LivewireRateLimiting\Exceptions\TooManyRequestsException

The exception encountered when the rate limit was hit.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Minutes until available

$minutes

int

The number of minutes until the rate limit will pass.

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

The default notification object for the rate limit, which could be a useful starting point for customization.

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

Seconds until available

$seconds

int

The number of seconds until the rate limit will pass.

Selected Eloquent records

$selectedRecords

Illuminate\Support\Collection

[Bulk actions only] The Eloquent records selected in the table.

Table

$table

Filament\Tables\Table

[Actions in tables only] The table object that this action belongs to.

### [​](#customizing-the-rate-limit-behavior)Customizing the rate limit behavior

If you wish to customize the rate limit behavior, you can use Laravel’s [rate limiting](https://laravel.com/docs/rate-limiting#basic-usage) features and Filament’s [flash notifications](../notifications/overview) together in the action. If you want to rate limit immediately when an action modal is opened, you can do so in the `mountUsing()` method:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;
use Illuminate\Support\Facades\RateLimiter;

Action::make('delete')
    ->mountUsing(function () {
        if (RateLimiter::tooManyAttempts(
            $rateLimitKey = 'delete:' . auth()->id(),
            maxAttempts: 5,
        )) {
            Notification::make()
                ->title('Too many attempts')
                ->body('Please try again in ' . RateLimiter::availableIn($rateLimitKey) . ' seconds.')
                ->danger()
                ->send();
  
            return;
        }
  
         RateLimiter::hit($rateLimitKey);
    })

```

If you want to rate limit when an action is run, you can do so in the `action()` method:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;
use Illuminate\Support\Facades\RateLimiter;

Action::make('delete')
    ->action(function () {
        if (RateLimiter::tooManyAttempts(
            $rateLimitKey = 'delete:' . auth()->id(),
            maxAttempts: 5,
        )) {
            Notification::make()
                ->title('Too many attempts')
                ->body('Please try again in ' . RateLimiter::availableIn($rateLimitKey) . ' seconds.')
                ->danger()
                ->send();
  
            return;
        }
  
         RateLimiter::hit($rateLimitKey);
  
        // ...
    })

```

## [​](#using-actions-in-schemas)Using actions in schemas

Action objects can be inserted anywhere in a [schema](../schemas/overview), such as in [form field slots](../forms/overview#adding-extra-content-to-a-field), [section headers and footers](../schemas/sections), or alongside [prime components](../schemas/primes). When an action is used in a schema, it has access to the schema’s state via [utility injection](#injecting-utilities-from-a-schema) - you can use `$schemaGet` and `$schemaSet` in closures to read and modify form field values.

Copy

```
use Filament\Actions\Action;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Utilities\Get;
use Filament\Schemas\Components\Utilities\Set;

TextInput::make('title')
    ->afterContent(
        Action::make('generateSlug')
            ->action(function (Get $schemaGet, Set $schemaSet) {
                $schemaSet('slug', str($schemaGet('title'))->slug());
            })
    )

TextInput::make('slug')

```

### [​](#running-javascript-when-an-action-is-clicked)Running JavaScript when an action is clicked

If you need a simple action that runs JavaScript directly in the browser without making a network request, you can use the `actionJs()` method. This is useful for simple interactions like updating form field values instantly:

Copy

```
use Filament\Actions\Action;
use Filament\Forms\Components\TextInput;

TextInput::make('title')
    ->live(onBlur: true)
    ->afterContent(
        Action::make('generateSlug')
            ->actionJs(<<<'JS'
                $set('slug', $get('title').toLowerCase().replaceAll(' ', '-'))
                JS)
    )

TextInput::make('slug')

```

The JavaScript string has access to `$get()` and `$set()` utilities, which allow you to read and modify the state of form fields in the schema.

**As well as allowing a static value, the `actionJs()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

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

When using `actionJs()`, the action cannot open a modal or perform any server-side processing. It is intended for simple client-side interactions only. If you need to run PHP code, use the `action()` method instead.

Any JavaScript string passed to the `actionJs()` method will be executed in the browser, so you should never add user input directly into the string, as it could lead to cross-site scripting (XSS) vulnerabilities. User input from `$get()` should never be evaluated as JavaScript code, but is safe to use as a string value.

## [​](#action-utility-injection)Action utility injection

The vast majority of methods used to configure actions accept functions as parameters instead of hardcoded values:

Copy

```
use Filament\Actions\Action;

Action::make('edit')
    ->label('Edit post')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))

```

This alone unlocks many customization possibilities. The package is also able to inject many utilities to use inside these functions, as parameters. All customization methods that accept functions as arguments can inject utilities. These injected utilities require specific parameter names to be used. Otherwise, Filament doesn’t know what to inject.

### [​](#injecting-the-current-modal-form-data)Injecting the current modal form data

If you wish to access the current [modal form data](./modals#rendering-a-form-in-a-modal), define a `$data` parameter:

Copy

```
function (array $data) {
    // ...
}

```

Be aware that this will be empty if the modal has not been submitted yet.

### [​](#injecting-the-eloquent-record)Injecting the Eloquent record

If your action is associated with an Eloquent record, for example if it is on a table row, you can inject the record using a `$record` parameter:

Copy

```
use Illuminate\Database\Eloquent\Model;

function (Model $record) {
    // ...
}

```

### [​](#injecting-the-current-arguments)Injecting the current arguments

If you wish to access the [current arguments](../components/action#passing-action-arguments) that have been passed to the action, define an `$arguments` parameter:

Copy

```
function (array $arguments) {
    // ...
}

```

### [​](#injecting-utilities-from-a-schema)Injecting utilities from a schema

You can access various additional utilities if your action is defined in a schema:

- `$schema` - The schema instance that the action belongs to.
- `$schemaComponent` - The schema component instance that the action belongs to.
- `$schemaComponentState` - The current value of the schema component.
- `$schemaState` - The current value of the schema that this action belongs to, like the current repeater item.
- `$schemaGet` - A function for retrieving values from the schema data. Validation is not run on form fields.
- `$schemaSet` - A function for setting values in the schema data.
- `$schemaOperation` - The current operation being performed by the schema. Usually `create`, `edit`, or `view`.For more information, please visit the [Schemas section](../schemas/overview#component-utility-injection).

### [​](#injecting-the-current-livewire-component-instance)Injecting the current Livewire component instance

If you wish to access the current Livewire component instance that the action belongs to, define a `$livewire` parameter:

Copy

```
use Livewire\Component;

function (Component $livewire) {
    // ...
}

```

### [​](#injecting-the-current-action-instance)Injecting the current action instance

If you wish to access the current action instance, define a `$action` parameter:

Copy

```
function (Action $action) {
    // ...
}

```

### [​](#injecting-multiple-utilities)Injecting multiple utilities

The parameters are injected dynamically using reflection, so you are able to combine multiple parameters in any order:

Copy

```
use Livewire\Component;

function (array $arguments, Component $livewire) {
    // ...
}

```

### [​](#injecting-dependencies-from-laravel’s-container)Injecting dependencies from Laravel’s container

You may inject anything from Laravel’s container like normal, alongside utilities:

Copy

```
use Illuminate\Http\Request;

function (Request $request, array $arguments) {
    // ...
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/actions/docs/01-overview.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Custom entries](/docs/5.x/infolists/custom-entries)[Modals](/docs/5.x/actions/modals)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
