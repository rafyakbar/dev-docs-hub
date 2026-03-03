## [​](#introduction)Introduction

Livewire components are PHP classes that have their state stored in the user’s browser. When a network request is made, the state is sent to the server, and filled into public properties on the Livewire component class, where it can be accessed in the same way as any other class property in PHP can be. Imagine you had a Livewire component with a public property called `$name`. You could bind that property to an input field in the HTML of the Livewire component in one of two ways: with the [`wire:model` attribute](https://livewire.laravel.com/docs/properties#data-binding), or by [entangling](https://livewire.laravel.com/docs/javascript#the-wire-object) it with an Alpine.js property:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    <input wire:model="name" />
  
    <!-- Or -->
  
  
        <input x-model="state" />

</x-dynamic-component>

```

When the user types into the input field, the `$name` property is updated in the Livewire component class. When the user submits the form, the `$name` property is sent to the server, where it can be saved. This is the basis of how fields work in Filament. Each field is assigned to a public property in the Livewire component class, which is where the state of the field is stored. We call the name of this property the “state path” of the field. You can access the state path of a field using the `$getStatePath()` function in the field’s view:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    <input wire:model="{{ $getStatePath() }}" />

    <!-- Or -->
  
  
        <input x-model="state" />

</x-dynamic-component>

```

If your component heavily relies on third party libraries, we advise that you asynchronously load the Alpine.js component using the Filament asset system. This ensures that the Alpine.js component is only loaded when it’s needed, and not on every page load. To find out how to do this, check out our [Assets documentation](../advanced/assets#asynchronous-alpinejs-components).

### [​](#custom-field-classes)Custom field classes

You may create your own custom field classes and views, which you can reuse across your project, and even release as a plugin to the community. To create a custom field class and view, you may use the following command:

Copy

```
php artisan make:filament-form-field LocationPicker

```

This will create the following component class:

Copy

```
use Filament\Forms\Components\Field;

class LocationPicker extends Field
{
    protected string $view = 'filament.forms.components.location-picker';
}

```

It will also create a view file at `resources/views/filament/forms/components/location-picker.blade.php`.

Filament form fields are **not** Livewire components. Defining public properties and methods on a form field class will not make them accessible in the Blade view.

## [​](#accessing-the-state-of-another-component-in-the-blade-view)Accessing the state of another component in the Blade view

Inside the Blade view, you may access the state of another component in the schema using the `$get()` function:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    {{ $get('email') }}
</x-dynamic-component>

```

Unless a form field is [reactive](../forms/overview#the-basics-of-reactivity), the Blade view will not refresh when the value of the field changes, only when the next user interaction occurs that makes a request to the server. If you need to react to changes in a field’s value, it should be `live()`.

## [​](#accessing-the-eloquent-record-in-the-blade-view)Accessing the Eloquent record in the Blade view

Inside the Blade view, you may access the current Eloquent record using the `$record` variable:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    {{ $record->name }}
</x-dynamic-component>

```

## [​](#accessing-the-current-operation-in-the-blade-view)Accessing the current operation in the Blade view

Inside the Blade view, you may access the current operation, usually `create`, `edit` or `view`, using the `$operation` variable:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    @if ($operation === 'create')
        This is a new conference.
    @else
        This is an existing conference.
    @endif
</x-dynamic-component>

```

## [​](#accessing-the-current-livewire-component-instance-in-the-blade-view)Accessing the current Livewire component instance in the Blade view

Inside the Blade view, you may access the current Livewire component instance using `$this`:

Copy

```
@php
    use Filament\Resources\Users\RelationManagers\ConferencesRelationManager;
@endphp

<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    @if ($this instanceof ConferencesRelationManager)
        You are editing conferences the of a user.
    @endif
</x-dynamic-component>

```

## [​](#accessing-the-current-field-instance-in-the-blade-view)Accessing the current field instance in the Blade view

Inside the Blade view, you may access the current field instance using `$field`. You can call public methods on this object to access other information that may not be available in variables:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    @if ($field->getState())
        This is a new conference.
    @endif
</x-dynamic-component>

```

## [​](#adding-a-configuration-method-to-a-custom-field-class)Adding a configuration method to a custom field class

You may add a public method to the custom field class that accepts a configuration value, stores it in a protected property, and returns it again from another public method:

Copy

```
use Filament\Forms\Components\Field;

class LocationPicker extends Field
{
    protected string $view = 'filament.forms.components.location-picker';
  
    protected ?float $zoom = null;

    public function zoom(?float $zoom): static
    {
        $this->zoom = $zoom;

        return $this;
    }

    public function getZoom(): ?float
    {
        return $this->zoom;
    }
}

```

Now, in the Blade view for the custom field, you may access the zoom using the `$getZoom()` function:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    {{ $getZoom() }}
</x-dynamic-component>

```

Any public method that you define on the custom field class can be accessed in the Blade view as a variable function in this way. To pass the configuration value to the custom field class, you may use the public method:

Copy

```
use App\Filament\Forms\Components\LocationPicker;

LocationPicker::make('location')
    ->zoom(0.5)

```

## [​](#allowing-utility-injection-in-a-custom-field-configuration-method)Allowing utility injection in a custom field configuration method

[Utility injection](./overview#field-utility-injection) is a powerful feature of Filament that allows users to configure a component using functions that can access various utilities. You can allow utility injection by ensuring that the parameter type and property type of the configuration allows the user to pass a `Closure`. In the getter method, you should pass the configuration value to the `$this->evaluate()` method, which will inject utilities into the user’s function if they pass one, or return the value if it is static:

Copy

```
use Closure;
use Filament\Forms\Components\Field;

class LocationPicker extends Field
{
    protected string $view = 'filament.forms.components.location-picker';
  
    protected float | Closure | null $zoom = null;

    public function zoom(float | Closure | null $zoom): static
    {
        $this->zoom = $zoom;

        return $this;
    }

    public function getZoom(): ?float
    {
        return $this->evaluate($this->zoom);
    }
}

```

Now, you can pass a static value or a function to the `zoom()` method, and [inject any utility](./overview#component-utility-injection) as a parameter:

Copy

```
use App\Filament\Forms\Components\LocationPicker;

LocationPicker::make('location')
    ->zoom(fn (Conference $record): float => $record->isGlobal() ? 1 : 0.5)

```

## [​](#obeying-state-binding-modifiers)Obeying state binding modifiers

When you bind a field to a state path, you may use the `defer` modifier to ensure that the state is only sent to the server when the user submits the form, or whenever the next Livewire request is made. This is the default behavior. However, you may use the [`live()`](./overview#the-basics-of-reactivity) on a field to ensure that the state is sent to the server immediately when the user interacts with the field. This allows for lots of advanced use cases as explained in the [reactivity](./overview#the-basics-of-reactivity) section of the documentation. Filament provides a `$applyStateBindingModifiers()` function that you may use in your view to apply any state binding modifiers to a `wire:model` or `$wire.$entangle()` binding:

Copy

```
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    <input {{ $applyStateBindingModifiers('wire:model') }}="{{ $getStatePath() }}" />

    <!-- Or -->

    <div x-data="{ state: $wire.{{ $applyStateBindingModifiers("\$entangle('{$getStatePath()}')") }} }">
        <input x-model="state" />

</x-dynamic-component>

```

## [​](#calling-field-methods-from-javascript)Calling field methods from JavaScript

Sometimes you need to call a method on the field class from JavaScript in the Blade view. For example, you might want to fetch data asynchronously, process a file upload, or perform some server-side computation. Filament provides a way to expose methods on your field class to JavaScript using the `#[ExposedLivewireMethod]` attribute.

### [​](#exposing-a-method)Exposing a method

To expose a method to JavaScript, add the `#[ExposedLivewireMethod]` attribute to a public method on your custom field class:

Copy

```
use Filament\Forms\Components\Field;
use Filament\Support\Components\Attributes\ExposedLivewireMethod;

class LocationPicker extends Field
{
    protected string $view = 'filament.forms.components.location-picker';

    #[ExposedLivewireMethod]
    public function geocodeAddress(string $address): array
    {
        // Perform geocoding logic...

        return [
            'latitude' => $latitude,
            'longitude' => $longitude,
        ];
    }
}

```

Only methods marked with `#[ExposedLivewireMethod]` can be called from JavaScript. This is a security measure to prevent arbitrary method execution.

### [​](#calling-the-method-from-javascript)Calling the method from JavaScript

In your Blade view, you may call the exposed method using `$wire.callSchemaComponentMethod()`. The first argument is the component’s key (available via `$getKey()`), and the second argument is the method name. You may pass arguments as a third argument:

Copy

```
@php
    $key = $getKey();
@endphp

<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
  
        <input type="text" x-model="address" />
        <button type="button" x-on:click="geocode">Geocode</button>

        <template x-if="coordinates">
            <p x-text="`${coordinates.latitude}, ${coordinates.longitude}`"></p>
        </template>

</x-dynamic-component>

```

### [​](#preventing-re-renders)Preventing re-renders

By default, calling an exposed method will trigger a re-render of the Livewire component. If your method doesn’t need to update the UI, you may add Livewire’s `#[Renderless]` attribute alongside `#[ExposedLivewireMethod]` to skip the re-render:

Copy

```
use Filament\Forms\Components\Field;
use Filament\Support\Components\Attributes\ExposedLivewireMethod;
use Livewire\Attributes\Renderless;

class LocationPicker extends Field
{
    protected string $view = 'filament.forms.components.location-picker';

    #[ExposedLivewireMethod]
    #[Renderless]
    public function geocodeAddress(string $address): array
    {
        // ...
    }
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/forms/docs/22-custom-fields.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[Hidden](/docs/5.x/forms/hidden)[Validation](/docs/5.x/forms/validation)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
