## [​](#calling-an-action-in-a-test)Calling an action in a test

You can call an action by passing its name or class to `callAction()`:

Copy

```
use function Pest\Livewire\livewire;

it('can send invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->callAction('send');

    expect($invoice->refresh())
        ->isSent()->toBeTrue();
});

```

## [​](#testing-table-actions)Testing table actions

To test table actions, you can use a `TestAction` object with the `table()` method. This object receives the name of the action you want to test, and replaces the name of the action in any testing method you want to use. For example:

Copy

```
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoice = Invoice::factory()->create();

livewire(ListInvoices::class)
    ->callAction(TestAction::make('send')->table($invoice));

livewire(ListInvoices::class)
    ->assertActionVisible(TestAction::make('send')->table($invoice))

livewire(ListInvoices::class)
    ->assertActionExists(TestAction::make('send')->table($invoice))

```

### [​](#testing-table-header-actions)Testing table header actions

To test a header action, you can use the `table()` method without passing in a specific record to test with:

Copy

```
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

livewire(ListInvoices::class)
    ->callAction(TestAction::make('create')->table());

livewire(ListInvoices::class)
    ->assertActionVisible(TestAction::make('create')->table())

livewire(ListInvoices::class)
    ->assertActionExists(TestAction::make('create')->table())

```

### [​](#testing-table-bulk-actions)Testing table bulk actions

To test a bulk action, first call `selectTableRecords()` and pass in any records you want to select. Then, use the `TestAction`’s `bulk()` method to specify the action you want to test. For example:

Copy

```
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoices = Invoice::factory()->count(3)->create();

livewire(ListInvoices::class)
    ->selectTableRecords($invoices->pluck('id')->toArray())
    ->callAction(TestAction::make('send')->table()->bulk());

livewire(ListInvoices::class)
    ->assertActionVisible(TestAction::make('send')->table()->bulk())

livewire(ListInvoices::class)
    ->assertActionExists(TestAction::make('send')->table()->bulk())

```

## [​](#testing-actions-in-a-schema)Testing actions in a schema

If an action belongs to a component in a resource’s infolist, for example, if it is in the `belowContent()` method of an infolist entry, you can use the `TestAction` object with the `schemaComponent()` method. This object receives the name of the action you want to test and replaces the name of the action in any testing method you want to use. For example:

Copy

```
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoice = Invoice::factory()->create();

livewire(EditInvoice::class)
    ->callAction(TestAction::make('send')->schemaComponent('customer_id'));

livewire(EditInvoice::class)
    ->assertActionVisible(TestAction::make('send')->schemaComponent('customer_id'))

livewire(EditInvoice::class)
    ->assertActionExists(TestAction::make('send')->schemaComponent('customer_id'))

```

## [​](#testing-actions-inside-another-action’s-schema-/-form)Testing actions inside another action’s schema / form

If an action belongs to a component in another action’s `schema()` (or `form()`), for example, if it is in the `belowContent()` method of a form field in an action modal, you can use the `TestAction` object with the `schemaComponent()` method. This object receives the name of the action you want to test and replaces the name of the action in any testing method you want to use. You should pass an array of `TestAction` objects in order, for example:

Copy

```
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoice = Invoice::factory()->create();

livewire(ManageInvoices::class)
    ->callAction([
        TestAction::make('view')->table($invoice),
        TestAction::make('send')->schemaComponent('customer.name'),
    ]);
  
livewire(ManageInvoices::class)
    ->assertActionVisible([
        TestAction::make('view')->table($invoice),
        TestAction::make('send')->schemaComponent('customer.name'),
    ]);
  
livewire(ManageInvoices::class)
    ->assertActionExists([
        TestAction::make('view')->table($invoice),
        TestAction::make('send')->schemaComponent('customer.name'),
    ]);

```

## [​](#testing-resource-getformactions)Testing resource `getFormActions()`

For details on how to test custom actions in the `getFormActions()` of a resource page, refer to the [Testing resources](./testing-resources#testing-create--edit-page-getformactions) documentation.

## [​](#testing-forms-in-action-modals)Testing forms in action modals

To pass an array of data into an action, use the `data` parameter:

Copy

```
use function Pest\Livewire\livewire;

it('can send invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->callAction('send', data: [
            'email' => $email = fake()->email(),
        ])
        ->assertHasNoFormErrors();

    expect($invoice->refresh())
        ->isSent()->toBeTrue()
        ->recipient_email->toBe($email);
});

```

If you ever need to only set an action’s data without immediately calling it, you can use `fillForm()`:

Copy

```
use function Pest\Livewire\livewire;

it('can send invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->mountAction('send')
        ->fillForm([
            'email' => $email = fake()->email(),
        ])
});

```

### [​](#testing-validation-errors-in-an-action-modal’s-form)Testing validation errors in an action modal’s form

`assertHasNoFormErrors()` is used to assert that no validation errors occurred when submitting the action form. To check if a validation error has occurred with the data, use `assertHasFormErrors()`, similar to `assertHasErrors()` in Livewire:

Copy

```
use function Pest\Livewire\livewire;

it('can validate invoice recipient email', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->callAction('send', data: [
            'email' => Str::random(),
        ])
        ->assertHasFormErrors(['email' => ['email']]);
});

```

To check if an action is pre-filled with data, you can use the `assertSchemaStateSet()` method:

Copy

```
use function Pest\Livewire\livewire;

it('can send invoices to the primary contact by default', function () {
    $invoice = Invoice::factory()->create();
    $recipientEmail = $invoice->company->primaryContact->email;

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->mountAction('send')
        ->assertSchemaStateSet([
            'email' => $recipientEmail,
        ])
        ->callMountedAction()
        ->assertHasNoFormErrors();

    expect($invoice->refresh())
        ->isSent()->toBeTrue()
        ->recipient_email->toBe($recipientEmail);
});

```

## [​](#testing-the-content-of-an-action-modal)Testing the content of an action modal

To assert the content of a modal, you should first mount the action (rather than call it which closes the modal). You can then use `assertMountedActionModalSee()`, `assertMountedActionModalDontSee()`, `assertMountedActionModalSeeHtml()` or `assertMountedActionModalDontSeeHtml()` to assert the modal contains the content that you expect it to:

Copy

```
use function Pest\Livewire\livewire;

it('confirms the target address before sending', function () {
    $invoice = Invoice::factory()->create();
    $recipientEmail = $invoice->company->primaryContact->email;

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->mountAction('send')
        ->assertMountedActionModalSee($recipientEmail);
});

```

## [​](#testing-the-existence-of-an-action)Testing the existence of an action

To ensure that an action exists or doesn’t, you can use the `assertActionExists()` or `assertActionDoesNotExist()` method:

Copy

```
use function Pest\Livewire\livewire;

it('can send but not unsend invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionExists('send')
        ->assertActionDoesNotExist('unsend');
});

```

You may pass a function as an additional argument to assert that an action passes a given “truth test”. This is useful for asserting that an action has a specific configuration:

Copy

```
use Filament\Actions\Action;
use function Pest\Livewire\livewire;

it('has the correct description', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionExists('send', function (Action $action): bool {
            return $action->getModalDescription() === 'This will send an email to the customer\'s primary address, with the invoice attached as a PDF';
        });
});

```

## [​](#testing-the-visibility-of-an-action)Testing the visibility of an action

To ensure an action is hidden or visible for a user, you can use the `assertActionHidden()` or `assertActionVisible()` methods:

Copy

```
use function Pest\Livewire\livewire;

it('can only print invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionHidden('send')
        ->assertActionVisible('print');
});

```

## [​](#testing-disabled-actions)Testing disabled actions

To ensure an action is enabled or disabled for a user, you can use the `assertActionEnabled()` or `assertActionDisabled()` methods:

Copy

```
use function Pest\Livewire\livewire;

it('can only print a sent invoice', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionDisabled('send')
        ->assertActionEnabled('print');
});

```

To ensure sets of actions exist in the correct order, you can use `assertActionListInOrder()`:

Copy

```
use function Pest\Livewire\livewire;

it('can have actions in order', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionListInOrder(['send', 'export']);
});

```

To check if an action is hidden to a user, you can use the `assertActionHidden()` method:

Copy

```
use function Pest\Livewire\livewire;

it('can not send invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionHidden('send');
});

```

## [​](#testing-the-label-of-an-action)Testing the label of an action

To ensure an action has the correct label, you can use `assertActionHasLabel()` and `assertActionDoesNotHaveLabel()`:

Copy

```
use function Pest\Livewire\livewire;

it('send action has correct label', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionHasLabel('send', 'Email Invoice')
        ->assertActionDoesNotHaveLabel('send', 'Send');
});

```

## [​](#testing-the-icon-of-an-action)Testing the icon of an action

To ensure an action’s button is showing the correct icon, you can use `assertActionHasIcon()` or `assertActionDoesNotHaveIcon()`:

Copy

```
use function Pest\Livewire\livewire;

it('when enabled the send button has correct icon', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionEnabled('send')
        ->assertActionHasIcon('send', 'envelope-open')
        ->assertActionDoesNotHaveIcon('send', 'envelope');
});

```

## [​](#testing-the-color-of-an-action)Testing the color of an action

To ensure that an action’s button is displaying the right color, you can use `assertActionHasColor()` or `assertActionDoesNotHaveColor()`:

Copy

```
use function Pest\Livewire\livewire;

it('actions display proper colors', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionHasColor('delete', 'danger')
        ->assertActionDoesNotHaveColor('print', 'danger');
});

```

## [​](#testing-the-url-of-an-action)Testing the URL of an action

To ensure an action has the correct URL, you can use `assertActionHasUrl()`, `assertActionDoesNotHaveUrl()`, `assertActionShouldOpenUrlInNewTab()`, and `assertActionShouldNotOpenUrlInNewTab()`:

Copy

```
use function Pest\Livewire\livewire;

it('links to the correct Filament sites', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->assertActionHasUrl('filament', 'https://filamentphp.com/')
        ->assertActionDoesNotHaveUrl('filament', 'https://github.com/filamentphp/filament')
        ->assertActionShouldOpenUrlInNewTab('filament')
        ->assertActionShouldNotOpenUrlInNewTab('github');
});

```

## [​](#testing-action-arguments)Testing action arguments

To test action arguments, you can use a `TestAction` object with the `arguments()` method. This object receives the name of the action you want to test and replaces the name of the action in any testing method you want to use. For example:

Copy

```
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoice = Invoice::factory()->create();

livewire(ManageInvoices::class)
    ->callAction(TestAction::make('send')->arguments(['invoice' => $invoice->getKey()]));

livewire(ManageInvoices::class)
    ->assertActionVisible(TestAction::make('send')->arguments(['invoice' => $invoice->getKey()]))

livewire(ManageInvoices::class)
    ->assertActionExists(TestAction::make('send')->arguments(['invoice' => $invoice->getKey()]))

```

## [​](#testing-if-an-action-has-been-halted)Testing if an action has been halted

To check if an action has been halted, you can use `assertActionHalted()`:

Copy

```
use function Pest\Livewire\livewire;

it('stops sending if invoice has no email address', function () {
    $invoice = Invoice::factory(['email' => null])->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->callAction('send')
        ->assertActionHalted('send');
});

```

## [​](#using-action-class-names-in-tests)Using action class names in tests

Filament includes a host of prebuilt actions such as `CreateAction`, `EditAction` and `DeleteAction`, and you can use these class names in your tests instead of action names, for example:

Copy

```
use Filament\Actions\CreateAction;
use function Pest\Livewire\livewire;

livewire(ManageInvoices::class)
    ->callAction(CreateAction::class)

```

If you have your own action classes in your app with a `make()` method, the name of your action is not discoverable by Filament unless it runs the `make()` method, which is not efficient. To use your own action class names in your tests, you can add an `#[ActionName]` attribute to your action class, which Filament can use to discover the name of your action. The name passed to the `#[ActionName]` attribute should be the same as the name of the action you would normally use in your tests. For example:

Copy

```
use Filament\Actions\Action;
use Filament\Actions\ActionName;

#[ActionName('send')]
class SendInvoiceAction
{
    public static function make(): Action
    {
        return Action::make('send')
            ->requiresConfirmation()
            ->action(function () {
                // ...
            });
    }
}

```

Now, you can use the class name in your tests:

Copy

```
use App\Filament\Resources\Invoices\Actions\SendInvoiceAction;
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoice = Invoice::factory()->create();

livewire(ManageInvoices::class)
    ->callAction(TestAction::make(SendInvoiceAction::class)->table($invoice);

```

If you have an action class that extends the `Action` class, you can add a `getDefaultName()` static method to the class, which will be used to discover the name of the action. It also allows users to omit the name of the action from the `make()` method when instantiating it. For example:

Copy

```
use Filament\Actions\Action;

class SendInvoiceAction extends Action
{
    public static function getDefaultName(): string
    {
        return 'send';
    }

    protected function setUp(): void
    {
        parent::setUp();
  
        $this
            ->requiresConfirmation()
            ->action(function () {
                // ...
            });
    }
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/10-testing/05-testing-actions.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Testing schemas](/docs/5.x/testing/testing-schemas)[Testing notifications](/docs/5.x/testing/testing-notifications)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
