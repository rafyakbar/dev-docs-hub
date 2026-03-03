## [​](#introduction)Introduction

The dropdown component allows you to render a dropdown menu with a button that triggers it:

Copy

```
<x-filament::dropdown>
    <x-slot name="trigger">
        <x-filament::button>
            More actions
        </x-filament::button>
    </x-slot>
  
    <x-filament::dropdown.list>
        <x-filament::dropdown.list.item wire:click="openViewModal">
            View
        </x-filament::dropdown.list.item>
  
        <x-filament::dropdown.list.item wire:click="openEditModal">
            Edit
        </x-filament::dropdown.list.item>
  
        <x-filament::dropdown.list.item wire:click="openDeleteModal">
            Delete
        </x-filament::dropdown.list.item>
    </x-filament::dropdown.list>
</x-filament::dropdown>

```

## [​](#using-a-dropdown-item-as-an-anchor-link)Using a dropdown item as an anchor link

By default, a dropdown item’s underlying HTML tag is `<button>`. You can change it to be an `<a>` tag by using the `tag` attribute:

Copy

```
<x-filament::dropdown.list.item
    href="https://filamentphp.com"
    tag="a"
>
    Filament
</x-filament::dropdown.list.item>

```

## [​](#changing-the-color-of-a-dropdown-item)Changing the color of a dropdown item

By default, the color of a dropdown item is “gray”. You can change it to be `danger`, `info`, `primary`, `success` or `warning` by using the `color` attribute:

Copy

```
<x-filament::dropdown.list.item color="danger">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item color="info">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item color="primary">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item color="success">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item color="warning">
    Edit
</x-filament::dropdown.list.item>

```

## [​](#adding-an-icon-to-a-dropdown-item)Adding an icon to a dropdown item

You can add an [icon](../styling/icons) to a dropdown item by using the `icon` attribute:

Copy

```
<x-filament::dropdown.list.item icon="heroicon-m-pencil">
    Edit
</x-filament::dropdown.list.item>

```

### [​](#changing-the-icon-color-of-a-dropdown-item)Changing the icon color of a dropdown item

By default, the icon color uses the [same color as the item itself](#changing-the-color-of-a-dropdown-item). You can override it to be `danger`, `info`, `primary`, `success` or `warning` by using the `icon-color` attribute:

Copy

```
<x-filament::dropdown.list.item icon="heroicon-m-pencil" icon-color="danger">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item icon="heroicon-m-pencil" icon-color="info">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item icon="heroicon-m-pencil" icon-color="primary">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item icon="heroicon-m-pencil" icon-color="success">
    Edit
</x-filament::dropdown.list.item>

<x-filament::dropdown.list.item icon="heroicon-m-pencil" icon-color="warning">
    Edit
</x-filament::dropdown.list.item>

```

## [​](#adding-an-image-to-a-dropdown-item)Adding an image to a dropdown item

You can add a circular image to a dropdown item by using the `image` attribute:

Copy

```
<x-filament::dropdown.list.item image="https://filamentphp.com/dan.jpg">
    Dan Harrin
</x-filament::dropdown.list.item>

```

## [​](#adding-a-badge-to-a-dropdown-item)Adding a badge to a dropdown item

You can render a [badge](./badge) on top of a dropdown item by using the `badge` slot:

Copy

```
<x-filament::dropdown.list.item>
    Mark notifications as read
  
    <x-slot name="badge">
        3
    </x-slot>
</x-filament::dropdown.list.item>

```

You can [change the color](./badge#changing-the-color-of-the-badge) of the badge using the `badge-color` attribute:

Copy

```
<x-filament::dropdown.list.item badge-color="danger">
    Mark notifications as read
  
    <x-slot name="badge">
        3
    </x-slot>
</x-filament::dropdown.list.item>

```

## [​](#setting-the-placement-of-a-dropdown)Setting the placement of a dropdown

The dropdown may be positioned relative to the trigger button by using the `placement` attribute:

Copy

```
<x-filament::dropdown placement="top-start">
    {{-- Dropdown items --}}
</x-filament::dropdown>

```

## [​](#setting-the-width-of-a-dropdown)Setting the width of a dropdown

The dropdown may be set to a width by using the `width` attribute. Options correspond to [Tailwind’s max-width scale](https://tailwindcss.com/docs/max-width). The options are `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `3xl`, `4xl`, `5xl`, `6xl` and `7xl`:

Copy

```
<x-filament::dropdown width="xs">
    {{-- Dropdown items --}}
</x-filament::dropdown>

```

## [​](#controlling-the-maximum-height-of-a-dropdown)Controlling the maximum height of a dropdown

The dropdown content can have a maximum height using the `max-height` attribute, so that it scrolls. You can pass a [CSS length](https://developer.mozilla.org/en-US/docs/Web/CSS/length):

Copy

```
<x-filament::dropdown max-height="400px">
    {{-- Dropdown items --}}
</x-filament::dropdown>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/03-dropdown.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[Checkbox Blade component](/docs/5.x/components/checkbox)[Empty State Blade component](/docs/5.x/components/empty-state)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
