## [​](#introduction)Introduction

Notifications are sent using a `Notification` object that’s constructed through a fluent API. Calling the `send()` method on the `Notification` object will dispatch the notification and display it in your application. As the session is used to flash notifications, they can be sent from anywhere in your code, including JavaScript, not just Livewire components.

Copy

```
<?php

namespace App\Livewire;

use Filament\Notifications\Notification;
use Livewire\Component;

class EditPost extends Component
{
    public function save(): void
    {
        // ...

        Notification::make()
            ->title('Saved successfully')
            ->success()
            ->send();
    }
}

```

## [​](#setting-a-title)Setting a title

The main message of the notification is shown in the title. You can set the title as follows:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->send();

```

The title text can contain basic, safe HTML elements. To generate safe HTML with Markdown, you can use the [`Str::markdown()` helper](https://laravel.com/docs/strings#method-str-markdown): `title(Str::markdown('Saved **successfully**'))` Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .send()

```

## [​](#setting-an-icon)Setting an icon

Optionally, a notification can have an [icon](../styling/icons) that’s displayed in front of its content. You may also set a color for the icon, which is gray by default:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->icon('heroicon-o-document-text')
    ->iconColor('success')
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .icon('heroicon-o-document-text')
    .iconColor('success')
    .send()

```

Notifications often have a status like `success`, `warning`, `danger` or `info`. Instead of manually setting the corresponding [icons](../styling/icons) and [colors](../styling/colors), there’s a `status()` method which you can pass the status. You may also use the dedicated `success()`, `warning()`, `danger()` and `info()` methods instead. So, cleaning up the above example would look like this:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .send()

```

## [​](#setting-a-background-color)Setting a background color

Notifications have no background color by default. You may want to provide additional context to your notification by setting a color as follows:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->color('success')
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .color('success')
    .send()

```

## [​](#setting-a-duration)Setting a duration

By default, notifications are shown for 6 seconds before they’re automatically closed. You may specify a custom duration value in milliseconds as follows:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->duration(5000)
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .duration(5000)
    .send()

```

If you prefer setting a duration in seconds instead of milliseconds, you can do so:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->seconds(5)
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .seconds(5)
    .send()

```

You might want some notifications to not automatically close and require the user to close them manually. This can be achieved by making the notification persistent:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->persistent()
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .persistent()
    .send()

```

## [​](#setting-body-text)Setting body text

Additional notification text can be shown in the `body()`:

Copy

```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->send();

```

The body text can contain basic, safe HTML elements. To generate safe HTML with Markdown, you can use the [`Str::markdown()` helper](https://laravel.com/docs/strings#method-str-markdown): `body(Str::markdown('Changes to the **post** have been saved.'))` Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .body('Changes to the post have been saved.')
    .send()

```

## [​](#adding-actions-to-notifications)Adding actions to notifications

Notifications support [Actions](../actions/overview), which are buttons that render below the content of the notification. They can open a URL or dispatch a Livewire event. Actions can be defined as follows:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button(),
        Action::make('undo')
            ->color('gray'),
    ])
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .body('Changes to the post have been saved.')
    .actions([
        new FilamentNotificationAction('view')
            .button(),
        new FilamentNotificationAction('undo')
            .color('gray'),
    ])
    .send()

```

You can learn more about how to style action buttons [here](../actions/overview).

### [​](#opening-urls-from-notification-actions)Opening URLs from notification actions

You can open a URL, optionally in a new tab, when clicking on an action:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button()
            ->url(route('posts.show', $post), shouldOpenInNewTab: true),
        Action::make('undo')
            ->color('gray'),
    ])
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .body('Changes to the post have been saved.')
    .actions([
        new FilamentNotificationAction('view')
            .button()
            .url('/view')
            .openUrlInNewTab(),
        new FilamentNotificationAction('undo')
            .color('gray'),
    ])
    .send()

```

### [​](#dispatching-livewire-events-from-notification-actions)Dispatching Livewire events from notification actions

Sometimes you want to execute additional code when a notification action is clicked. This can be achieved by setting a Livewire event which should be dispatched on clicking the action. You may optionally pass an array of data, which will be available as parameters in the event listener on your Livewire component:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button()
            ->url(route('posts.show', $post), shouldOpenInNewTab: true),
        Action::make('undo')
            ->color('gray')
            ->dispatch('undoEditingPost', [$post->id]),
    ])
    ->send();

```

You can also `dispatchSelf` and `dispatchTo`:

Copy

```
Action::make('undo')
    ->color('gray')
    ->dispatchSelf('undoEditingPost', [$post->id])

Action::make('undo')
    ->color('gray')
    ->dispatchTo('another_component', 'undoEditingPost', [$post->id])

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .body('Changes to the post have been saved.')
    .actions([
        new FilamentNotificationAction('view')
            .button()
            .url('/view')
            .openUrlInNewTab(),
        new FilamentNotificationAction('undo')
            .color('gray')
            .dispatch('undoEditingPost'),
    ])
    .send()

```

Similarly, `dispatchSelf` and `dispatchTo` are also available:

Copy

```
new FilamentNotificationAction('undo')
    .color('gray')
    .dispatchSelf('undoEditingPost')

new FilamentNotificationAction('undo')
    .color('gray')
    .dispatchTo('another_component', 'undoEditingPost')

```

### [​](#closing-notifications-from-actions)Closing notifications from actions

After opening a URL or dispatching an event from your action, you may want to close the notification right away:

Copy

```
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button()
            ->url(route('posts.show', $post), shouldOpenInNewTab: true),
        Action::make('undo')
            ->color('gray')
            ->dispatch('undoEditingPost', [$post->id])
            ->close(),
    ])
    ->send();

```

Or with JavaScript:

Copy

```
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .body('Changes to the post have been saved.')
    .actions([
        new FilamentNotificationAction('view')
            .button()
            .url('/view')
            .openUrlInNewTab(),
        new FilamentNotificationAction('undo')
            .color('gray')
            .dispatch('undoEditingPost')
            .close(),
    ])
    .send()

```

## [​](#using-the-javascript-objects)Using the JavaScript objects

The JavaScript objects (`FilamentNotification` and `FilamentNotificationAction`) are assigned to `window.FilamentNotification` and `window.FilamentNotificationAction`, so they are available in on-page scripts. You may also import them in a bundled JavaScript file:

Copy

```
import { Notification, NotificationAction } from '../../vendor/filament/notifications/dist/index.js'


// ...

```

## [​](#closing-a-notification-with-javascript)Closing a notification with JavaScript

Once a notification has been sent, you can close it on demand by dispatching a browser event on the window called `close-notification`. The event needs to contain the ID of the notification you sent. To get the ID, you can use the `getId()` method on the `Notification` object:

Copy

```
use Filament\Notifications\Notification;

$notification = Notification::make()
    ->title('Hello')
    ->persistent()
    ->send()

$notificationId = $notification->getId()

```

To close the notification, you can dispatch the event from Livewire:

Copy

```
$this->dispatch('close-notification', id: $notificationId);

```

Or from JavaScript, in this case Alpine.js:

Copy

```
<button x-on:click="$dispatch('close-notification', { id: notificationId })" type="button">
    Close Notification
</button>

```

If you are able to retrieve the notification ID, persist it, and then use it to close the notification, that is the recommended approach, as IDs are generated uniquely, and you will not risk closing the wrong notification. However, if it is not possible to persist the random ID, you can pass in a custom ID when sending the notification:

Copy

```
use Filament\Notifications\Notification;

Notification::make('greeting')
    ->title('Hello')
    ->persistent()
    ->send()

```

In this case, you can close the notification by dispatching the event with the custom ID:

Copy

```
<button x-on:click="$dispatch('close-notification', { id: 'greeting' })" type="button">
    Close Notification
</button>

```

Please be aware that if you send multiple notifications with the same ID, you may experience unexpected side effects, so random IDs are recommended.

## [​](#positioning-notifications)Positioning notifications

You can configure the alignment of the notifications in a service provider or middleware, by calling `Notifications::alignment()` and `Notifications::verticalAlignment()`. You can pass `Alignment::Start`, `Alignment::Center`, `Alignment::End`, `VerticalAlignment::Start`, `VerticalAlignment::Center` or `VerticalAlignment::End`:

Copy

```
use Filament\Notifications\Livewire\Notifications;
use Filament\Support\Enums\Alignment;
use Filament\Support\Enums\VerticalAlignment;

Notifications::alignment(Alignment::Start);
Notifications::verticalAlignment(VerticalAlignment::End);

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/packages/notifications/docs/01-overview.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[Your logo here](https://github.com/sponsors/danharrin)

[Export action](/docs/5.x/actions/export)[Database notifications](/docs/5.x/notifications/database-notifications)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
