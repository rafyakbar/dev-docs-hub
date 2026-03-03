# wire:click

New Laracasts series

Master everything new in Livewire v4

[Start learning](https://laracasts.com/series/everything-new-in-livewire-4)

Livewire provides a simple `wire:click` directive for calling component methods (aka actions) when a user clicks a specific element on the page.

For example, given the `ShowInvoice` component below:

```
<?php

 

namespace App\Livewire;

 

use Livewire\Component;

use App\Models\Invoice;

 

class ShowInvoice extends Component

{

    public Invoice $invoice;

 

    public function download()

    {

        return response()->download(

            $this->invoice->file_path, 'invoice.pdf'

        );

    }

}


```
You can trigger the `download()` method from the class above when a user clicks a "Download Invoice" button by adding `wire:click="download"`:

```
<button type="button" wire:click="download">

    Download Invoice

</button>


```


## [#](#passing-parameters "Permalink")Passing parameters

You can pass parameters to actions directly in the `wire:click` directive:

```
<button wire:click="delete({{ $post->id }})">Delete</button>


```
When the button is clicked, the `delete()` method will be called with the post's ID.

Don't trust action parameters

Action parameters should be treated like HTTP request input and should not be trusted. Always authorize ownership before updating data.

## [#](#using-on-links "Permalink")Using on links

When using `wire:click` on `<a>` tags, you must append `.prevent` to prevent the default link behavior. Otherwise, the browser will navigate to the provided `href`.

```
<a href="#" wire:click.prevent="show">View Details</a>


```


## [#](#preventing-re-renders "Permalink")Preventing re-renders

Use `.renderless` to skip re-rendering the component after the action completes. This is useful for actions that only perform side effects (like logging or analytics):

```
<button wire:click.renderless="trackClick">Track Event</button>


```


## [#](#preserving-scroll-position "Permalink")Preserving scroll position

By default, updating content may change the scroll position. Use `.preserve-scroll` to maintain the current scroll position:

```
<button wire:click.preserve-scroll="loadMore">Load More</button>


```


## [#](#parallel-execution "Permalink")Parallel execution

By default, Livewire queues actions within the same component. Use `.async` to allow actions to run in parallel:

```
<button wire:click.async="process">Process</button>


```


## [#](#going-deeper "Permalink")Going deeper

The `wire:click` directive is just one of many different available event listeners in Livewire. For full documentation on its (and other event listeners) capabilities, visit [the Livewire actions documentation page](/docs/4.x/actions).

## [#](#see-also "Permalink")See also

- **[Actions](/docs/4.x/actions)** — Complete guide to component actions
- **[Events](/docs/4.x/events)** — Dispatch events from click handlers
- **[wire:confirm](/docs/4.x/wire-confirm)** — Add confirmation dialogs to actions


## [#](#reference "Permalink")Reference

```
wire:click="methodName"

wire:click="methodName(param1, param2)"


```


### [#](#modifiers "Permalink")Modifiers

| Modifier | Description |
| --- | --- |
| `.prevent` | Prevents default browser behavior |
| `.stop` | Stops event propagation |
| `.self` | Only triggers if event originated on this element |
| `.once` | Ensures listener is only called once |
| `.debounce` | Debounces handler by 250ms (use `.debounce.500ms` for custom duration) |
| `.throttle` | Throttles handler to every 250ms minimum (use `.throttle.500ms` for custom) |
| `.window` | Listens for event on the `window` object |
| `.document` | Listens for event on the `document` object |
| `.outside` | Only listens for clicks outside the element |
| `.passive` | Won't block scroll performance |
| `.capture` | Listens during the capturing phase |
| `.camel` | Converts event name to camel case |
| `.dot` | Converts event name to dot notation |
| `.renderless` | Skips re-rendering after action completes |
| `.preserve-scroll` | Maintains scroll position during updates |
| `.async` | Executes action in parallel instead of queued |
