## [​](#introduction)Introduction

The code entry allows you to present a highlighted code snippet in your infolist. It uses [Phiki](https://github.com/phikiphp/phiki) for code highlighting on the server:

Copy

```
use Filament\Infolists\Components\CodeEntry;
use Phiki\Grammar\Grammar;

CodeEntry::make('code')
    ->grammar(Grammar::Php)

```

To use the code entry, you need to first install the [`phiki/phiki`](https://github.com/phikiphp/phiki) Composer package. Filament does not include it by default to allow you to choose which major version of Phiki to use explicitly, since major versions can have different grammars and themes available. You can install the latest version of Phiki using the following command:

Copy

```
composer require phiki/phiki

```

## [​](#changing-the-code’s-grammar-language)Changing the code’s grammar (language)

You may change the grammar (language) of the code using the `grammar()` method. Over 200 grammars are available, and you can open the `Phiki\Grammar\Grammar` enum class to see the full list. To switch to use JavaScript as the grammar, you can use the `Grammar::Javascript` enum value:

Copy

```
use Filament\Infolists\Components\CodeEntry;
use Phiki\Grammar\Grammar;

CodeEntry::make('code')
    ->grammar(Grammar::Javascript)

```

**As well as allowing a static value, the `grammar()` method also accepts a function to dynamically calculate it. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/infolists/overview#entry-utility-injection)

Entry

$component

Filament\Infolists\Components\Entry

The current entry component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current schema data. Validation is not run on form fields.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current schema.

Operation

$operation

string

The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the entry.

If your code entry’s content is a PHP array, it will automatically be converted to a JSON string, and the grammar will be set to `Grammar::Json`. You can customize the `JSON_` flags used during conversion with the `jsonFlags()` method.

## [​](#changing-the-code’s-theme-highlighting)Changing the code’s theme (highlighting)

You may change the theme of the code using the `lightTheme()` and `darkTheme()` methods. Over 50 themes are available, and you can open the `Phiki\Theme\Theme` enum class to see the full list. To use the popular `Dracula` theme, you can use the `Theme::Dracula` enum value:

Copy

```
use Filament\Infolists\Components\CodeEntry;
use Phiki\Theme\Theme;

CodeEntry::make('code')
    ->lightTheme(Theme::Dracula)
    ->darkTheme(Theme::Dracula)

```

**As well as allowing static values, the `lightTheme()` and `darkTheme()` methods also accept functions to dynamically calculate them. You can inject various utilities into the functions as parameters.**

[Learn more about utility injection.](/docs/5.x/infolists/overview#entry-utility-injection)

Entry

$component

Filament\Infolists\Components\Entry

The current entry component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current schema data. Validation is not run on form fields.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current schema.

Operation

$operation

string

The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the entry.

## [​](#allowing-the-code-to-be-copied-to-the-clipboard)Allowing the code to be copied to the clipboard

You may make the code copyable, such that clicking on it copies the code to the clipboard, and optionally specify a custom confirmation message and duration in milliseconds. This feature only works when SSL is enabled for the app.

Copy

```
use Filament\Infolists\Components\CodeEntry;

CodeEntry::make('code')
    ->copyable()
    ->copyMessage('Copied!')
    ->copyMessageDuration(1500)

```

Optionally, you may pass a boolean value to control if the code should be copyable or not:

Copy

```
use Filament\Infolists\Components\CodeEntry;

CodeEntry::make('code')
    ->copyable(FeatureFlag::active())

```

**As well as allowing static values, the `copyable()`, `copyMessage()`, and `copyMessageDuration()` methods also accept functions to dynamically calculate them. You can inject various utilities into the function as parameters.**

[Learn more about utility injection.](/docs/5.x/infolists/overview#entry-utility-injection)

Entry

$component

Filament\Infolists\Components\Entry

The current entry component instance.

Get function

$get

Filament\Schemas\Components\Utilities\Get

A function for retrieving values from the current schema data. Validation is not run on form fields.

Livewire

$livewire

Livewire\Component

The Livewire component instance.

Eloquent model FQN

$model

?string<Illuminate\Database\Eloquent\Model>

The Eloquent model FQN for the current schema.

Operation

$operation

string

The current operation being performed by the schema. Usually `create`, `edit`, or `view`.

Eloquent record

$record

?Illuminate\Database\Eloquent\Model

The Eloquent record for the current schema.

State

$state

mixed

The current value of the entry.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/infolists/docs/06-code-entry.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Color entry](/docs/5.x/infolists/color-entry)[Key-value entry](/docs/5.x/infolists/key-value-entry)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
