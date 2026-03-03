## [​](#customizing-data-before-saving)Customizing data before saving

Sometimes, you may wish to modify form data before it is finally saved to the database. To do this, you may define a `mutateFormDataBeforeCreate()` method on the Create page class, which accepts the `$data` as an array, and returns the modified version:

Copy

```
protected function mutateFormDataBeforeCreate(array $data): array
{
    $data['user_id'] = auth()->id();

    return $data;
}

```

Alternatively, if you’re creating records in a modal action, check out the [Actions documentation](../actions/create#customizing-data-before-saving).

## [​](#customizing-the-creation-process)Customizing the creation process

You can tweak how the record is created using the `handleRecordCreation()` method on the Create page class:

Copy

```
use Illuminate\Database\Eloquent\Model;

protected function handleRecordCreation(array $data): Model
{
    return static::getModel()::create($data);
}

```

Alternatively, if you’re creating records in a modal action, check out the [Actions documentation](../actions/create#customizing-the-creation-process).

## [​](#customizing-redirects)Customizing redirects

By default, after saving the form, the user will be redirected to the [Edit page](./editing-records) of the resource, or the [View page](./viewing-records) if it is present. You may set up a custom redirect when the form is saved by overriding the `getRedirectUrl()` method on the Create page class. For example, the form can redirect back to the [List page](./listing-records):

Copy

```
protected function getRedirectUrl(): string
{
    return $this->getResource()::getUrl('index');
}

```

If you wish to be redirected to the previous page, else the index page:

Copy

```
protected function getRedirectUrl(): string
{
    return $this->previousUrl ?? $this->getResource()::getUrl('index');
}

```

You can also use the [configuration](../panel-configuration) to customize the default redirect page for all resources at once:

Copy

```
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->resourceCreatePageRedirect('index') // or
        ->resourceCreatePageRedirect('view') // or
        ->resourceCreatePageRedirect('edit');
}

```

## [​](#customizing-the-save-notification)Customizing the save notification

When the record is successfully created, a notification is dispatched to the user, which indicates the success of their action. To customize the title of this notification, define a `getCreatedNotificationTitle()` method on the create page class:

Copy

```
protected function getCreatedNotificationTitle(): ?string
{
    return 'User registered';
}

```

Alternatively, if you’re creating records in a modal action, check out the [Actions documentation](../actions/create#customizing-the-save-notification). You may customize the entire notification by overriding the `getCreatedNotification()` method on the create page class:

Copy

```
use Filament\Notifications\Notification;

protected function getCreatedNotification(): ?Notification
{
    return Notification::make()
        ->success()
        ->title('User registered')
        ->body('The user has been created successfully.');
}

```

To disable the notification altogether, return `null` from the `getCreatedNotification()` method on the create page class:

Copy

```
use Filament\Notifications\Notification;

protected function getCreatedNotification(): ?Notification
{
    return null;
}

```

## [​](#creating-another-record)Creating another record

### [​](#disabling-create-another)Disabling create another

To disable the “create and create another” feature, define the `$canCreateAnother` property as `false` on the Create page class:

Copy

```
protected static bool $canCreateAnother = false;

```

Alternatively, if you’d like to specify a dynamic condition when the feature is disabled, you may override the `canCreateAnother()` method on the Create page class:

Copy

```
public function canCreateAnother(): bool
{
    return false;
}

```

### [​](#preserving-data-when-creating-another)Preserving data when creating another

By default, when the user uses the “create and create another” feature, all the form data is cleared so the user can start fresh. If you’d like to preserve some of the data in the form, you may override the `preserveFormDataWhenCreatingAnother()` method on the Create page class, and return the part of the `$data` array that you’d like to keep:

Copy

```
use Illuminate\Support\Arr;

protected function preserveFormDataWhenCreatingAnother(array $data): array
{
    return Arr::only($data, ['is_admin', 'organization']);
}

```

To preserve all the data, return the entire `$data` array:

Copy

```
protected function preserveFormDataWhenCreatingAnother(array $data): array
{
    return $data;
}

```

## [​](#lifecycle-hooks)Lifecycle hooks

Hooks may be used to execute code at various points within a page’s lifecycle, like before a form is saved. To set up a hook, create a protected method on the Create page class with the name of the hook:

Copy

```
protected function beforeCreate(): void
{
    // ...
}

```

In this example, the code in the `beforeCreate()` method will be called before the data in the form is saved to the database. There are several available hooks for the Create page:

Copy

```
use Filament\Resources\Pages\CreateRecord;

class CreateUser extends CreateRecord
{
    // ...

    protected function beforeFill(): void
    {
        // Runs before the form fields are populated with their default values.
    }

    protected function afterFill(): void
    {
        // Runs after the form fields are populated with their default values.
    }

    protected function beforeValidate(): void
    {
        // Runs before the form fields are validated when the form is submitted.
    }

    protected function afterValidate(): void
    {
        // Runs after the form fields are validated when the form is submitted.
    }

    protected function beforeCreate(): void
    {
        // Runs before the form fields are saved to the database.
    }

    protected function afterCreate(): void
    {
        // Runs after the form fields are saved to the database.
    }
}

```

Alternatively, if you’re creating records in a modal action, check out the [Actions documentation](../actions/create#lifecycle-hooks).

## [​](#halting-the-creation-process)Halting the creation process

At any time, you may call `$this->halt()` from inside a lifecycle hook or mutation method, which will halt the entire creation process:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;

protected function beforeCreate(): void
{
    if (! auth()->user()->team->subscribed()) {
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
  
        $this->halt();
    }
}

```

Alternatively, if you’re creating records in a modal action, check out the [Actions documentation](../actions/create#halting-the-creation-process).

## [​](#authorization)Authorization

For authorization, Filament will observe any [model policies](https://laravel.com/docs/authorization#creating-policies) that are registered in your app. Users may access the Create page if the `create()` method of the model policy returns `true`.

## [​](#using-a-wizard)Using a wizard

You may easily transform the creation process into a multistep wizard. On the page class, add the corresponding `HasWizard` trait:

Copy

```
use App\Filament\Resources\Categories\CategoryResource;
use Filament\Resources\Pages\CreateRecord;

class CreateCategory extends CreateRecord
{
    use CreateRecord\Concerns\HasWizard;
  
    protected static string $resource = CategoryResource::class;

    protected function getSteps(): array
    {
        return [
            // ...
        ];
    }
}

```

Inside the `getSteps()` array, return your [wizard steps](../schemas/wizards):

Copy

```
use Filament\Forms\Components\MarkdownEditor;
use Filament\Forms\Components\TextInput;
use Filament\Forms\Components\Toggle;
use Filament\Schemas\Components\Wizard\Step;

protected function getSteps(): array
{
    return [
        Step::make('Name')
            ->description('Give the category a clear and unique name')
            ->schema([
                TextInput::make('name')
                    ->required()
                    ->live()
                    ->afterStateUpdated(fn ($state, callable $set) => $set('slug', Str::slug($state))),
                TextInput::make('slug')
                    ->disabled()
                    ->required()
                    ->unique(Category::class, 'slug', fn ($record) => $record),
            ]),
        Step::make('Description')
            ->description('Add some extra details')
            ->schema([
                MarkdownEditor::make('description')
                    ->columnSpan('full'),
            ]),
        Step::make('Visibility')
            ->description('Control who can view it')
            ->schema([
                Toggle::make('is_visible')
                    ->label('Visible to customers.')
                    ->default(true),
            ]),
    ];
}

```

Alternatively, if you’re creating records in a modal action, check out the [Actions documentation](../actions/create#using-a-wizard). Now, create a new record to see your wizard in action! Edit will still use the form defined within the resource class. If you’d like to allow free navigation, so all the steps are skippable, override the `hasSkippableSteps()` method:

Copy

```
public function hasSkippableSteps(): bool
{
    return true;
}

```

### [​](#sharing-fields-between-the-form-schema-and-wizards)Sharing fields between the form schema and wizards

If you’d like to reduce the amount of repetition between the resource form and wizard steps, it’s a good idea to extract public static form functions for your fields, where you can easily retrieve an instance of a field from the form schema or the wizard:

Copy

```
use Filament\Forms;
use Filament\Schemas\Schema;

class CategoryForm
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->components([
                static::getNameFormField(),
                static::getSlugFormField(),
                // ...
            ]);
    }
  
    public static function getNameFormField(): Forms\Components\TextInput
    {
        return TextInput::make('name')
            ->required()
            ->live()
            ->afterStateUpdated(fn ($state, callable $set) => $set('slug', Str::slug($state)));
    }
  
    public static function getSlugFormField(): Forms\Components\TextInput
    {
        return TextInput::make('slug')
            ->disabled()
            ->required()
            ->unique(Category::class, 'slug', fn ($record) => $record);
    }
}

```

Copy

```
use App\Filament\Resources\Categories\Schemas\CategoryForm;
use Filament\Resources\Pages\CreateRecord;

class CreateCategory extends CreateRecord
{
    use CreateRecord\Concerns\HasWizard;
  
    protected static string $resource = CategoryResource::class;

    protected function getSteps(): array
    {
        return [
            Step::make('Name')
                ->description('Give the category a clear and unique name')
                ->schema([
                    CategoryForm::getNameFormField(),
                    CategoryForm::getSlugFormField(),
                ]),
            // ...
        ];
    }
}

```

## [​](#importing-resource-records)Importing resource records

Filament includes an `ImportAction` that you can add to the `getHeaderActions()` of the [List page](./listing-records). It allows users to upload a CSV of data to import into the resource:

Copy

```
use App\Filament\Imports\ProductImporter;
use Filament\Actions;

protected function getHeaderActions(): array
{
    return [
        Actions\ImportAction::make()
            ->importer(ProductImporter::class),
        Actions\CreateAction::make(),
    ];
}

```

The “importer” class [needs to be created](../actions/import#creating-an-importer) to tell Filament how to import each row of the CSV. You can learn everything about the `ImportAction` in the [Actions documentation](../actions/import).

## [​](#custom-actions)Custom actions

“Actions” are buttons that are displayed on pages, which allow the user to run a Livewire method on the page or visit a URL. On resource pages, actions are usually in 2 places: in the top right of the page, and below the form. For example, you may add a new button action in the header of the Create page:

Copy

```
use App\Filament\Imports\UserImporter;
use Filament\Actions;
use Filament\Resources\Pages\CreateRecord;

class CreateUser extends CreateRecord
{
    // ...

    protected function getHeaderActions(): array
    {
        return [
            Actions\ImportAction::make()
                ->importer(UserImporter::class),
        ];
    }
}

```

Or, a new button next to “Create” below the form:

Copy

```
use Filament\Actions\Action;
use Filament\Resources\Pages\CreateRecord;

class CreateUser extends CreateRecord
{
    // ...

    protected function getFormActions(): array
    {
        return [
            ...parent::getFormActions(),
            Action::make('close')->action('createAndClose'),
        ];
    }

    public function createAndClose(): void
    {
        // ...
    }
}

```

To view the entire actions API, please visit the [pages section](../navigation/custom-pages#adding-actions-to-pages).

### [​](#adding-a-create-action-button-to-the-header)Adding a create action button to the header

The “Create” button can be moved to the header of the page by overriding the `getHeaderActions()` method and using `getCreateFormAction()`. You need to pass `formId()` to the action, to specify that the action should submit the form with the ID of `form`, which is the `<form>` ID used in the view of the page:

Copy

```
protected function getHeaderActions(): array
{
    return [
        $this->getCreateFormAction()
            ->formId('form'),
    ];
}

```

You may remove all actions from the form by overriding the `getFormActions()` method to return an empty array:

Copy

```
protected function getFormActions(): array
{
    return [];
}

```

## [​](#custom-page-content)Custom page content

Each page in Filament has its own [schema](../schemas), which defines the overall structure and content. You can override the schema for the page by defining a `content()` method on it. The `content()` method for the Create page contains the following components by default:

Copy

```
use Filament\Schemas\Schema;

public function content(Schema $schema): Schema
{
    return $schema
        ->components([
            $this->getFormContentComponent(), // This method returns a component to display the form that is defined in this resource
        ]);
}

```

Inside the `components()` array, you can insert any [schema component](../schemas). You can reorder the components by changing the order of the array or remove any of the components that are not needed.

### [​](#using-a-custom-blade-view)Using a custom Blade view

For further customization opportunities, you can override the static `$view` property on the page class to a custom view in your app:

Copy

```
protected string $view = 'filament.resources.users.pages.create-user';

```

This assumes that you have created a view at `resources/views/filament/resources/users/pages/create-user.blade.php`:

Copy

```
<x-filament-panels::page>
    {{ $this->content }} {{-- This will render the content of the page defined in the `content()` method, which can be removed if you want to start from scratch --}}
</x-filament-panels::page>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/03-resources/03-creating-records.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Listing records](/docs/5.x/resources/listing-records)[Editing records](/docs/5.x/resources/editing-records)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
