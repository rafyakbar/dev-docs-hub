# Profile

Display a user's profile with an avatar and optional name in a compact, interactive component.









Copy to clipboard

```
<flux:profile avatar="https://unavatar.io/x/calebporzio" />
```



## [With name](#with-name)

Display a user's name next to their avatar.





Caleb Porzio







Copy to clipboard

```
<flux:profile name="Caleb Porzio" avatar="https://unavatar.io/x/calebporzio" />
```



## [Without chevron](#without-chevron)

Hide the chevron icon by setting the :chevron prop to false.









Copy to clipboard

```
<flux:profile :chevron="false" avatar="https://unavatar.io/x/calebporzio" />
```



## [Circle avatar](#circle-avatar)

Use the circle prop to display a circular avatar.





Caleb Porzio







Copy to clipboard

```
<flux:profile circle :chevron="false" avatar="https://unavatar.io/x/calebporzio" /><flux:profile circle name="Caleb Porzio" avatar="https://unavatar.io/x/calebporzio" />
```



## [Avatar with initials](#avatar-with-initials)

When no avatar image is provided, initials will be automatically generated from the name or they can be specified directly.





CP

Caleb Porzio



CP







Copy to clipboard

```
<!-- Automatically generates initials from name --><flux:profile name="Caleb Porzio" /><!-- Specify color... --><flux:profile name="Caleb Porzio" avatar:color="cyan" /><!-- Manually specify initials... --><flux:profile initials="CP" /><!-- Provide name only for avatar initial generation... --><flux:profile avatar:name="Caleb Porzio" />
```



## [Custom trailing icon](#custom-trailing-icon)

Replace the default chevron with a custom icon using the icon:trailing prop.





Caleb Porzio







Copy to clipboard

```
<flux:profile    icon:trailing="chevron-up-down"    avatar="https://unavatar.io/x/calebporzio"    name="Caleb Porzio"/>
```

## Examples



### [Profile menu](#profile-menu)









Copy to clipboard

```
<flux:dropdown align="end">    <flux:profile avatar="https://unavatar.io/x/calebporzio" />    <flux:navmenu class="max-w-[12rem]">        <div class="px-2 py-1.5">            <flux:text size="sm">Signed in as</flux:text>            <flux:heading class="mt-1! truncate">[[email protected]](/cdn-cgi/l/email-protection)</flux:heading>        </div>        <flux:navmenu.separator />        <div class="px-2 py-1.5">            <flux:text size="sm" class="pl-7">Teams</flux:text>        </div>        <flux:navmenu.item href="#" icon="check" class="text-zinc-800 dark:text-white truncate">Personal</flux:navmenu.item>        <flux:navmenu.item href="#" indent class="text-zinc-800 dark:text-white truncate">Wireable LLC</flux:navmenu.item>        <flux:navmenu.separator />        <flux:navmenu.item href="/dashboard" icon="key" class="text-zinc-800 dark:text-white">Licenses</flux:navmenu.item>        <flux:navmenu.item href="/account" icon="user" class="text-zinc-800 dark:text-white">Account</flux:navmenu.item>        <flux:navmenu.separator />        <flux:navmenu.item href="/logout" icon="arrow-right-start-on-rectangle" class="text-zinc-800 dark:text-white">Logout</flux:navmenu.item>    </flux:navmenu></flux:dropdown>
```



### [Profile switcher](#profile-switcher)





[*A* Acme Inc.](#)

Caleb Porzio



Caleb Porzio

Hugo Sainte-Marie

Josh Hanley

Logout





Copy to clipboard

```
<flux:dropdown position="top" align="start">    <flux:profile avatar="https://unavatar.io/x/calebporzio" name="Caleb Porzio" />    <flux:menu>        <flux:menu.radio.group>            <flux:menu.radio checked>Caleb Porzio</flux:menu.radio>            <flux:menu.radio>Hugo Sainte-Marie</flux:menu.radio>            <flux:menu.radio>Josh Hanley</flux:menu.radio>        </flux:menu.radio.group>        <flux:menu.separator />        <flux:menu.item icon="arrow-right-start-on-rectangle">Logout</flux:menu.item>    </flux:menu></flux:dropdown>
```

## Related components

[Avatar Display user profile images or fallback initials](/components/avatar) [Header Top navigation headers for your application](/layouts/header) [Brand Display your brand name and logo](/components/brand)

## Reference



### [flux:profile](#fluxprofile)

| Prop | Description |
| --- | --- |
| name | User's name to display next to the avatar. |
| avatar | URL to the image to display as avatar, or can pass content via avatar named slot. |
| avatar:name | Name to use for avatar initial generation. |
| avatar:color | Color to use for the avatar. (See [Avatar color documentation](/components/avatar#colors) for available options.) |
| circle | Whether to display a circular avatar. Default: false. |
| initials | Custom initials to display when no avatar image is provided. Automatically generated from name if not provided. |
| chevron | Whether to display a chevron icon (dropdown indicator). Default: true. |
| icon:trailing | Custom icon to display instead of the chevron. Accepts any icon name. |
| icon:variant | Icon variant to use for the trailing icon. Options: micro (default), outline. |

| Slot | Description |
| --- | --- |
| avatar | Custom content for the avatar section, typically containing a flux:avatar component. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)
