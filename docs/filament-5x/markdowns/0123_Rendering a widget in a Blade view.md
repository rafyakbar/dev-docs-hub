Before proceeding, make sure `filament/widgets` is installed in your project. You can check by running:

Copy

```
composer show filament/widgets

```

If it’s not installed, consult the [installation guide](../introduction/installation#installing-the-individual-components) and configure the **individual components** according to the instructions.

## [​](#creating-a-widget)Creating a widget

Use the `make:filament-widget` command to generate a new widget. For details on customization and usage, see the [widgets section](../widgets).

## [​](#adding-the-widget)Adding the widget

Since widgets are Livewire components, you can easily render a widget in any Blade view using the `@livewire` directive:

Copy

```
<div>
    @livewire(\App\Livewire\Dashboard\PostsChart::class)


```

If you’re using a [table widget](../widgets/overview#table-widgets), make sure to install `filament/tables` as well.  
Refer to the [installation guide](../introduction/installation#installing-the-individual-components) and follow the steps to configure the **individual components** properly.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/12-components/02-widget.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Rendering a table in a Blade view](/docs/5.x/components/table)[Avatar Blade component](/docs/5.x/components/avatar)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
