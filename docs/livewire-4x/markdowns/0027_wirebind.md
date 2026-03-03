# wire:bind

New Laracasts series

Master everything new in Livewire v4

[Start learning](https://laracasts.com/series/everything-new-in-livewire-4)

`wire:bind` is a directive that dynamically binds HTML attributes to component properties or expressions. Unlike using Blade's attribute syntax, `wire:bind` updates the attribute reactively on the client without requiring a full re-render.

If you are familiar with Alpine's `x-bind` directive, the two are essentially the same.

## [#](#basic-usage "Permalink")Basic usage

```
<input wire:model="message" wire:bind:class="message.length > 240 && 'text-red-500'">


```
As the user types, `wire:bind:class` reacts to the message length and applies the class instantly on the client.

## [#](#common-use-cases "Permalink")Common use cases

### [#](#binding-styles "Permalink")Binding styles

```
<div wire:bind:style="{ 'color': textColor, 'font-size': fontSize + 'px' }">

    Styled text

</div>


```


### [#](#binding-href "Permalink")Binding href

```
<a wire:bind:href="url">Dynamic link</a>


```


### [#](#binding-disabled-state "Permalink")Binding disabled state

```
<button wire:bind:disabled="isArchived">Delete</button>


```


### [#](#binding-data-attributes "Permalink")Binding data attributes

```
<div wire:bind:data-count="count">...</div>


```


## [#](#reference "Permalink")Reference

```
wire:bind:{attribute}="expression"


```
Replace `{attribute}` with any valid HTML attribute name (e.g., `class`, `style`, `href`, `disabled`, `data-*`).

This directive has no modifiers.
