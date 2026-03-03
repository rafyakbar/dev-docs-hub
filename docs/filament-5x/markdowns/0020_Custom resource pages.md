## [​](#introduction)Introduction

Filament allows you to create completely custom pages for resources. To create a new page, you can use:

Copy

```
php artisan make:filament-page SortUsers --resource=UserResource --type=custom

```

This command will create two files - a page class in the `/Pages` directory of your resource directory, and a view in the `/pages` directory of the resource views directory. You must register custom pages to a route in the static `getPages()` method of your resource:

Copy

```
public static function getPages(): array
{
    return [
        // ...
        'sort' => Pages\SortUsers::route('/sort'),
    ];
}

```

The order of pages registered in this method matters - any wildcard route segments that are defined before hard-coded ones will be matched by Laravel’s router first.

Any [parameters](https://laravel.com/docs/routing#route-parameters) defined in the route’s path will be available to the page class, in an identical way to [Livewire](https://livewire.laravel.com/docs/components#accessing-route-parameters).

## [​](#using-a-resource-record)Using a resource record

If you’d like to create a page that uses a record similar to the [Edit](./editing-records) or [View](./viewing-records) pages, you can use the `InteractsWithRecord` trait:

Copy

```
use Filament\Resources\Pages\Page;
use Filament\Resources\Pages\Concerns\InteractsWithRecord;

class ManageUser extends Page
{
    use InteractsWithRecord;
  
    public function mount(int | string $record): void
    {
        $this->record = $this->resolveRecord($record);
    }

    // ...
}

```

The `mount()` method should resolve the record from the URL and store it in `$this->record`. You can access the record at any time using `$this->getRecord()` in the class or view. To add the record to the route as a parameter, you must define `{record}` in `getPages()`:

Copy

```
public static function getPages(): array
{
    return [
        // ...
        'manage' => Pages\ManageUser::route('/{record}/manage'),
    ];
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/03-resources/12-custom-pages.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://baiz.ai](https://baiz.ai "Baiz.ai")[Your logo here](https://github.com/sponsors/danharrin)

[Using widgets on resource pages](/docs/5.x/resources/widgets)[Code quality tips](/docs/5.x/resources/code-quality-tips)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
