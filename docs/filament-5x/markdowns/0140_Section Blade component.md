## [​](#introduction)Introduction

A section can be used to group content together, with an optional heading:

Copy

```
<x-filament::section>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

## [​](#adding-a-description-to-the-section)Adding a description to the section

You can add a description below the heading to the section by using the `description` slot:

Copy

```
<x-filament::section>
    <x-slot name="heading">
        User details
    </x-slot>

    <x-slot name="description">
        This is all the information we hold about the user.
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

## [​](#adding-an-icon-to-the-section-header)Adding an icon to the section header

You can add an [icon](../styling/icons) to a section by using the `icon` attribute:

Copy

```
<x-filament::section icon="heroicon-o-user">
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

### [​](#changing-the-color-of-the-section-icon)Changing the color of the section icon

By default, the color of the section icon is “gray”. You can change it to be `danger`, `info`, `primary`, `success` or `warning` by using the `icon-color` attribute:

Copy

```
<x-filament::section
    icon="heroicon-o-user"
    icon-color="info"
>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

### [​](#changing-the-size-of-the-section-icon)Changing the size of the section icon

By default, the size of the section icon is “large”. You can change it to be “small” or “medium” by using the `icon-size` attribute:

Copy

```
<x-filament::section
    icon="heroicon-m-user"
    icon-size="sm"
>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

<x-filament::section
    icon="heroicon-m-user"
    icon-size="md"
>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

## [​](#adding-content-to-the-end-of-the-header)Adding content to the end of the header

You may render additional content at the end of the header, next to the heading and description, using the `afterHeader` slot:

Copy

```
<x-filament::section>
    <x-slot name="heading">
        User details
    </x-slot>

    <x-slot name="afterHeader">
        {{-- Input to select the user's ID --}}
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

## [​](#making-a-section-collapsible)Making a section collapsible

You can make the content of a section collapsible by using the `collapsible` attribute:

Copy

```
<x-filament::section collapsible>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

### [​](#making-a-section-collapsed-by-default)Making a section collapsed by default

You can make a section collapsed by default by using the `collapsed` attribute:

Copy

```
<x-filament::section
    collapsible
    collapsed
>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

### [​](#persisting-collapsed-sections)Persisting collapsed sections

You can persist whether a section is collapsed in local storage using the `persist-collapsed` attribute, so it will remain collapsed when the user refreshes the page. You will also need a unique `id` attribute to identify the section from others, so that each section can persist its own collapse state:

Copy

```
<x-filament::section
    collapsible
    collapsed
    persist-collapsed
    id="user-details"
>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

## [​](#adding-the-section-header-aside-the-content-instead-of-above-it)Adding the section header aside the content instead of above it

You can change the position of the section header to be aside the content instead of above it by using the `aside` attribute:

Copy

```
<x-filament::section aside>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

### [​](#positioning-the-content-before-the-header)Positioning the content before the header

You can change the position of the content to be before the header instead of after it by using the `content-before` attribute:

Copy

```
<x-filament::section
    aside
    content-before
>
    <x-slot name="heading">
        User details
    </x-slot>

    {{-- Content --}}
</x-filament::section>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/03-section.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[Your logo here](https://github.com/sponsors/danharrin)

[Pagination Blade component](/docs/5.x/components/pagination)[Select Blade component](/docs/5.x/components/select)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
