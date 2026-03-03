## [​](#introduction)Introduction

The link component is used to render a clickable link that can perform an action:

Copy

```
<x-filament::link :href="route('users.create')">
    New user
</x-filament::link>

```

## [​](#using-a-link-as-a-button)Using a link as a button

By default, a link’s underlying HTML tag is `<a>`. You can change it to be a `<button>` tag by using the `tag` attribute:

Copy

```
<x-filament::link
    wire:click="openNewUserModal"
    tag="button"
>
    New user
</x-filament::link>

```

## [​](#setting-the-size-of-a-link)Setting the size of a link

By default, the size of a link is “medium”. You can make it “small”, “large”, “extra large” or “extra extra large” by using the `size` attribute:

Copy

```
<x-filament::link size="sm">
    New user
</x-filament::link>

<x-filament::link size="lg">
    New user
</x-filament::link>

<x-filament::link size="xl">
    New user
</x-filament::link>

<x-filament::link size="2xl">
    New user
</x-filament::link>

```

## [​](#setting-the-font-weight-of-a-link)Setting the font weight of a link

By default, the font weight of links is `semibold`. You can make it `thin`, `extralight`, `light`, `normal`, `medium`, `bold`, `extrabold` or `black` by using the `weight` attribute:

Copy

```
<x-filament::link weight="thin">
    New user
</x-filament::link>

<x-filament::link weight="extralight">
    New user
</x-filament::link>

<x-filament::link weight="light">
    New user
</x-filament::link>

<x-filament::link weight="normal">
    New user
</x-filament::link>

<x-filament::link weight="medium">
    New user
</x-filament::link>

<x-filament::link weight="semibold">
    New user
</x-filament::link>
  
<x-filament::link weight="bold">
    New user
</x-filament::link>

<x-filament::link weight="black">
    New user
</x-filament::link>

```

Alternatively, you can pass in a custom CSS class to define the weight:

Copy

```
<x-filament::link weight="md:font-[650]">
    New user
</x-filament::link>

```

## [​](#changing-the-color-of-a-link)Changing the color of a link

By default, the color of a link is “primary”. You can change it to be `danger`, `gray`, `info`, `success` or `warning` by using the `color` attribute:

Copy

```
<x-filament::link color="danger">
    New user
</x-filament::link>

<x-filament::link color="gray">
    New user
</x-filament::link>

<x-filament::link color="info">
    New user
</x-filament::link>

<x-filament::link color="success">
    New user
</x-filament::link>

<x-filament::link color="warning">
    New user
</x-filament::link>

```

## [​](#adding-an-icon-to-a-link)Adding an icon to a link

You can add an [icon](../styling/icons) to a link by using the `icon` attribute:

Copy

```
<x-filament::link icon="heroicon-m-sparkles">
    New user
</x-filament::link>

```

You can also change the icon’s position to be after the text instead of before it, using the `icon-position` attribute:

Copy

```
<x-filament::link
    icon="heroicon-m-sparkles"
    icon-position="after"
>
    New user
</x-filament::link>

```

## [​](#adding-a-tooltip-to-a-link)Adding a tooltip to a link

You can add a tooltip to a link by using the `tooltip` attribute:

Copy

```
<x-filament::link tooltip="Register a user">
    New user
</x-filament::link>

```

## [​](#adding-a-badge-to-a-link)Adding a badge to a link

You can render a [badge](./badge) on top of a link by using the `badge` slot:

Copy

```
<x-filament::link>
    Mark notifications as read

    <x-slot name="badge">
        3
    </x-slot>
</x-filament::link>

```

You can [change the color](./badge#changing-the-color-of-the-badge) of the badge using the `badge-color` attribute:

Copy

```
<x-filament::link badge-color="danger">
    Mark notifications as read

    <x-slot name="badge">
        3
    </x-slot>
</x-filament::link>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/03-link.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[Your logo here](https://github.com/sponsors/danharrin)

[Input Blade component](/docs/5.x/components/input)[Loading indicator Blade component](/docs/5.x/components/loading-indicator)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
