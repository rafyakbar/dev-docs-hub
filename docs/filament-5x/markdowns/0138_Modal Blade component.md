## [​](#introduction)Introduction

The modal component is able to open a dialog window or slide-over with any content:

Copy

```
<x-filament::modal>
    <x-slot name="trigger">
        <x-filament::button>
            Open modal
        </x-filament::button>
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#controlling-a-modal-from-javascript)Controlling a modal from JavaScript

You can use the `trigger` slot to render a button that opens the modal. However, this is not required. You have complete control over when the modal opens and closes through JavaScript. First, give the modal an ID so that you can reference it:

Copy

```
<x-filament::modal id="edit-user">
    {{-- Modal content --}}
</x-filament::modal>

```

Now, you can dispatch an `open-modal` or `close-modal` browser event, passing the modal’s ID, which will open or close the modal. For example, from a Livewire component:

Copy

```
$this->dispatch('open-modal', id: 'edit-user');

```

Or from Alpine.js:

Copy

```
$dispatch('open-modal', { id: 'edit-user' })

```

## [​](#adding-a-heading-to-a-modal)Adding a heading to a modal

You can add a heading to a modal by using the `heading` slot:

Copy

```
<x-filament::modal>
    <x-slot name="heading">
        Modal heading
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#adding-a-description-to-a-modal)Adding a description to a modal

You can add a description, below the heading, to a modal by using the `description` slot:

Copy

```
<x-filament::modal>
    <x-slot name="heading">
        Modal heading
    </x-slot>

    <x-slot name="description">
        Modal description
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#adding-an-icon-to-a-modal)Adding an icon to a modal

You can add an [icon](../styling/icons) to a modal by using the `icon` attribute:

Copy

```
<x-filament::modal icon="heroicon-o-information-circle">
    <x-slot name="heading">
        Modal heading
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

By default, the color of an icon is “primary”. You can change it to be `danger`, `gray`, `info`, `success` or `warning` by using the `icon-color` attribute:

Copy

```
<x-filament::modal
    icon="heroicon-o-exclamation-triangle"
    icon-color="danger"
>
    <x-slot name="heading">
        Modal heading
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#adding-a-footer-to-a-modal)Adding a footer to a modal

You can add a footer to a modal by using the `footer` slot:

Copy

```
<x-filament::modal>
    {{-- Modal content --}}
  
    <x-slot name="footer">
        {{-- Modal footer content --}}
    </x-slot>
</x-filament::modal>

```

Alternatively, you can add actions into the footer by using the `footerActions` slot:

Copy

```
<x-filament::modal>
    {{-- Modal content --}}
  
    <x-slot name="footerActions">
        {{-- Modal footer actions --}}
    </x-slot>
</x-filament::modal>

```

## [​](#changing-the-modal’s-alignment)Changing the modal’s alignment

By default, modal content will be aligned to the start, or centered if the modal is `xs` or `sm` in [width](#changing-the-modal-width). If you wish to change the alignment of content in a modal, you can use the `alignment` attribute and pass it `start` or `center`:

Copy

```
<x-filament::modal alignment="center">
    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#using-a-slide-over-instead-of-a-modal)Using a slide-over instead of a modal

You can open a “slide-over” dialog instead of a modal by using the `slide-over` attribute:

Copy

```
<x-filament::modal slide-over>
    {{-- Slide-over content --}}
</x-filament::modal>

```

## [​](#making-the-modal-header-sticky)Making the modal header sticky

The header of a modal scrolls out of view with the modal content when it overflows the modal size. However, slide-overs have a sticky modal that’s always visible. You may control this behavior using the `sticky-header` attribute:

Copy

```
<x-filament::modal sticky-header>
    <x-slot name="heading">
        Modal heading
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#making-the-modal-footer-sticky)Making the modal footer sticky

The footer of a modal is rendered inline after the content by default. Slide-overs, however, have a sticky footer that always shows when scrolling the content. You may enable this for a modal too using the `sticky-footer` attribute:

Copy

```
<x-filament::modal sticky-footer>
    {{-- Modal content --}}
  
    <x-slot name="footer">
        {{-- Modal footer content --}}
    </x-slot>
</x-filament::modal>

```

## [​](#changing-the-modal-width)Changing the modal width

You can change the width of the modal by using the `width` attribute. Options correspond to [Tailwind’s max-width scale](https://tailwindcss.com/docs/max-width). The options are `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `3xl`, `4xl`, `5xl`, `6xl`, `7xl`, and `screen`:

Copy

```
<x-filament::modal width="5xl">
    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#closing-the-modal-by-clicking-away)Closing the modal by clicking away

By default, when you click away from a modal, it will close itself. If you wish to disable this behavior for a specific action, you can use the `close-by-clicking-away` attribute:

Copy

```
<x-filament::modal :close-by-clicking-away="false">
    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#closing-the-modal-by-escaping)Closing the modal by escaping

By default, when you press escape on a modal, it will close itself. If you wish to disable this behavior for a specific action, you can use the `close-by-escaping` attribute:

Copy

```
<x-filament::modal :close-by-escaping="false">
    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#hiding-the-modal-close-button)Hiding the modal close button

By default, modals with a header have a close button in the top right corner. You can remove the close button from the modal by using the `close-button` attribute:

Copy

```
<x-filament::modal :close-button="false">
    <x-slot name="heading">
        Modal heading
    </x-slot>

    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#preventing-the-modal-from-autofocusing)Preventing the modal from autofocusing

By default, modals will autofocus on the first focusable element when opened. If you wish to disable this behavior, you can use the `autofocus` attribute:

Copy

```
<x-filament::modal :autofocus="false">
    {{-- Modal content --}}
</x-filament::modal>

```

## [​](#disabling-the-modal-trigger-button)Disabling the modal trigger button

By default, the trigger button will open the modal even if it is disabled, since the click event listener is registered on a wrapping element of the button itself. If you want to prevent the modal from opening, you should also use the `disabled` attribute on the trigger slot:

Copy

```
<x-filament::modal>
    <x-slot name="trigger" disabled>
        <x-filament::button :disabled="true">
            Open modal
        </x-filament::button>
    </x-slot>
    {{-- Modal content --}}
</x-filament::modal>

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/03-modal.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Loading indicator Blade component](/docs/5.x/components/loading-indicator)[Pagination Blade component](/docs/5.x/components/pagination)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
