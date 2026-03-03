# Separator

Visually divide sections of content or groups of items.









Copy to clipboard

```
<flux:separator />
```



## [With text](#with-text)

Add text to the separator for a more descriptive element.





or





Copy to clipboard

```
<flux:separator text="or" />
```



## [Vertical](#vertical)

Seperate contents with a vertical seperator when horizontally stacked.





Switch to dark theme

Log in





Copy to clipboard

```
<flux:separator vertical />
```



## [Limited height](#limited-height)

You can limit the height of the vertical separator by adding vertical margin.





Switch to dark theme

Log in





Copy to clipboard

```
<flux:separator vertical class="my-2" />
```



## [Subtle](#subtle)

Flux offers a subtle variant for a separator that blends into the background.





Switch to dark theme

Log in





Copy to clipboard

```
<flux:separator vertical variant="subtle" />
```

## Reference



### [flux:separator](#fluxseparator)

| Prop | Description |
| --- | --- |
| vertical | Displays a vertical separator. Default is horizontal. |
| variant | Visual style variant. Options: subtle. Default: standard separator. |
| text | Optional text to display in the center of the separator. |
| orientation | Alternative to vertical prop. Options: horizontal, vertical. Default: horizontal. |

| Class | Description |
| --- | --- |
| my-* | Commonly used to shorten vertical separators. |

| Attribute | Description |
| --- | --- |
| data-flux-separator | Applied to the root element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)
