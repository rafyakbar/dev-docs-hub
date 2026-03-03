## [​](#introduction)Introduction

The button component is used to render a clickable button that can perform an action:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-plus"
    wire:click="openNewUserModal"
    label="New label"
/>

```

## [​](#using-an-icon-button-as-an-anchor-link)Using an icon button as an anchor link

By default, an icon button’s underlying HTML tag is `<button>`. You can change it to be an `<a>` tag by using the `tag` attribute:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-arrow-top-right-on-square"
    href="https://filamentphp.com"
    tag="a"
    label="Filament"
/>

```

## [​](#setting-the-size-of-an-icon-button)Setting the size of an icon button

By default, the size of an icon button is “medium”. You can make it “extra small”, “small”, “large” or “extra large” by using the `size` attribute:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-plus"
    size="xs"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-m-plus"
    size="sm"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-s-plus"
    size="lg"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-s-plus"
    size="xl"
    label="New label"
/>

```

## [​](#changing-the-color-of-an-icon-button)Changing the color of an icon button

By default, the color of an icon button is “primary”. You can change it to be `danger`, `gray`, `info`, `success` or `warning` by using the `color` attribute:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-plus"
    color="danger"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-m-plus"
    color="gray"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-m-plus"
    color="info"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-m-plus"
    color="success"
    label="New label"
/>

<x-filament::icon-button
    icon="heroicon-m-plus"
    color="warning"
    label="New label"
/>

```

## [​](#adding-a-tooltip-to-an-icon-button)Adding a tooltip to an icon button

You can add a tooltip to an icon button by using the `tooltip` attribute:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-plus"
    tooltip="Register a user"
    label="New label"
/>

```

## [​](#adding-a-badge-to-an-icon-button)Adding a badge to an icon button

You can render a [badge](./badge) on top of an icon button by using the `badge` slot:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-x-mark"
    label="Mark notifications as read"
>
    <x-slot name="badge">
        3
    </x-slot>
</x-filament::icon-button>

```

You can [change the color](./badge#changing-the-color-of-the-badge) of the badge using the `badge-color` attribute:

Copy

```
<x-filament::icon-button
    icon="heroicon-m-x-mark"
    label="Mark notifications as read"
    badge-color="danger"
>
    <x-slot name="badge">
        3
    </x-slot>
</x-filament::icon-button>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/03-icon-button.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[Fieldset Blade component](/docs/5.x/components/fieldset)[Input wrapper Blade component](/docs/5.x/components/input-wrapper)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
