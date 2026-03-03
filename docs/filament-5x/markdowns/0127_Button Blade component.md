## [​](#introduction)Introduction

The button component is used to render a clickable button that can perform an action:

Copy

```
<x-filament::button wire:click="openNewUserModal">
    New user
</x-filament::button>

```

## [​](#using-a-button-as-an-anchor-link)Using a button as an anchor link

By default, a button’s underlying HTML tag is `<button>`. You can change it to be an `<a>` tag by using the `tag` attribute:

Copy

```
<x-filament::button
    href="https://filamentphp.com"
    tag="a"
>
    Filament
</x-filament::button>

```

## [​](#setting-the-size-of-a-button)Setting the size of a button

By default, the size of a button is “medium”. You can make it “extra small”, “small”, “large” or “extra large” by using the `size` attribute:

Copy

```
<x-filament::button size="xs">
    New user
</x-filament::button>

<x-filament::button size="sm">
    New user
</x-filament::button>

<x-filament::button size="lg">
    New user
</x-filament::button>

<x-filament::button size="xl">
    New user
</x-filament::button>

```

## [​](#changing-the-color-of-a-button)Changing the color of a button

By default, the color of a button is “primary”. You can change it to be `danger`, `gray`, `info`, `success` or `warning` by using the `color` attribute:

Copy

```
<x-filament::button color="danger">
    New user
</x-filament::button>

<x-filament::button color="gray">
    New user
</x-filament::button>

<x-filament::button color="info">
    New user
</x-filament::button>

<x-filament::button color="success">
    New user
</x-filament::button>

<x-filament::button color="warning">
    New user
</x-filament::button>

```

## [​](#adding-an-icon-to-a-button)Adding an icon to a button

You can add an [icon](../styling/icons) to a button by using the `icon` attribute:

Copy

```
<x-filament::button icon="heroicon-m-sparkles">
    New user
</x-filament::button>

```

You can also change the icon’s position to be after the text instead of before it, using the `icon-position` attribute:

Copy

```
<x-filament::button
    icon="heroicon-m-sparkles"
    icon-position="after"
>
    New user
</x-filament::button>

```

## [​](#making-a-button-outlined)Making a button outlined

You can make a button use an “outlined” design using the `outlined` attribute:

Copy

```
<x-filament::button outlined>
    New user
</x-filament::button>

```

## [​](#adding-a-tooltip-to-a-button)Adding a tooltip to a button

You can add a tooltip to a button by using the `tooltip` attribute:

Copy

```
<x-filament::button tooltip="Register a user">
    New user
</x-filament::button>

```

## [​](#adding-a-badge-to-a-button)Adding a badge to a button

You can render a [badge](./badge) on top of a button by using the `badge` slot:

Copy

```
<x-filament::button>
    Mark notifications as read
  
    <x-slot name="badge">
        3
    </x-slot>
</x-filament::button>

```

You can [change the color](./badge#changing-the-color-of-the-badge) of the badge using the `badge-color` attribute:

Copy

```
<x-filament::button badge-color="danger">
    Mark notifications as read
  
    <x-slot name="badge">
        3
    </x-slot>
</x-filament::button>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/03-button.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[Your logo here](https://github.com/sponsors/danharrin)

[Breadcrumbs Blade component](/docs/5.x/components/breadcrumbs)[Callout Blade component](/docs/5.x/components/callout)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
