## [​](#introduction)Introduction

All examples in this guide will be written using [Pest](https://pestphp.com). To use Pest’s Livewire plugin for testing, you can follow the installation instructions in the Pest documentation on plugins: [Livewire plugin for Pest](https://pestphp.com/docs/plugins#livewire). However, you can easily adapt this to PHPUnit, mostly by switching out the `livewire()` function from Pest with the `Livewire::test()` method. Since all Filament components are mounted to a Livewire component, we’re just using Livewire testing helpers everywhere. If you’ve never tested Livewire components before, please read [this guide](https://livewire.laravel.com/docs/testing) from the Livewire docs.

## [​](#testing-guides)Testing guides

Looking for a full example on how to test a panel resource? Check out the [Testing resources](./testing-resources) section. If you would like to learn the different methods available to test tables, check out the [Testing tables](./testing-tables) section. If you need to test a schema, which encompasses both forms and infolists, check out the [Testing schemas](./testing-schemas) section. If you would like to test an action, including actions that exist in tables or in schemas, check out the [Testing actions](./testing-actions) section. If you would like to test a notification that you have sent, check out the [Testing notifications](./testing-notifications) section. If you would like to test a custom page in a panel, these are Livewire components with no special behavior, so you should visit the [testing](https://livewire.laravel.com/docs/testing) section of the Livewire documentation.

## [​](#what-is-a-livewire-component-when-using-filament)What is a Livewire component when using Filament?

When testing Filament, it is useful to understand which components are Livewire components and which aren’t. With this information, you know which classes to pass to the `livewire()` function in Pest or the `Livewire::test()` method in PHPUnit. Some examples of Livewire components are:

- Pages in a panel, including page classes in a resource’s `Pages` directory
- Relation managers in a resource
- WidgetsSome examples of classes that are not Livewire components are:

- Resource classes
- Schema components
- ActionsThese classes all interact with Livewire, but they are not Livewire components themselves. You can still test them, for example, by calling various methods and using the [Pest expectation API](https://pestphp.com/docs/expectations) to assert the expected behavior. However, the most useful tests will involve Livewire components, since they provide the best end-to-end testing coverage of your users’ experience.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/10-testing/01-overview.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[Modular architecture (DDD)](/docs/5.x/advanced/modular-architecture)[Testing resources](/docs/5.x/testing/testing-resources)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
