

# 0001_Installation

# Installation

Flux is a robust, hand-crafted, UI component library for your Livewire applications. It's built using [Tailwind CSS](https://tailwindcss.com/) and provides a set of components that are easy to use and customize.

Starting a new project? Flux comes baked into the new [Livewire starter kit ->](https://laravel.com/docs/12.x/starter-kits#livewire)



## Prerequisites

Flux requires the following before installing:

[Laravel Version 10 or later](https://laravel.com/docs/11.x/installation) [Livewire Version 3.7.0 or later](https://livewire.laravel.com/docs/installation) [Tailwind CSS Version 4.1 or later](https://tailwindcss.com/docs/installation)



## Getting started

1

Install Flux

Flux can be installed via composer from your project root:

Copy to clipboard

```
composer require livewire/flux
```

2

Install Flux Pro (optional)

If you have purchased a Flux Pro license, you can install it using the following command:

Copy to clipboard

```
php artisan flux:activate
```

During the activation process, you will be prompted to enter an email and license key.

*If you haven't purchased a Flux Pro license, [you can purchase one here ->](/pricing).*

The above command will create an auth.json file in your project's root directory. This file contains your email and license key for downloading and installing Flux and should not be added to version control.

Because auth.json is not version controlled, you will need to manually recreate it in every new project environment. See below for [cloning an existing project](#cloning-an-existing-project) or how to [activate in CI](#activating-in-ci) or [activate using Laravel Forge](#activating-using-laravel-forge).

You can also view your [licenses and their associated install instructions here ->](/dashboard)

3

Include Flux assets

Now, add the @fluxAppearance and @fluxScripts Blade directives to your layout file:

Copy to clipboard

```
<head>    ...    @fluxAppearance</head><body>    ...    @livewireScripts    @fluxScripts</body>
```

4

Set up Tailwind CSS

The last step is to set up Tailwind CSS. Flux uses Tailwind CSS for its default styling.

*Flux v2.0 requires Tailwind CSS v4.1 or later.*

If you already have Tailwind installed in your project, just add the following configuration to your resources/css/app.css file:

Copy to clipboard

```
@import 'tailwindcss';@import '../../vendor/livewire/flux/dist/flux.css';@custom-variant dark (&:where(.dark, .dark *));
```

If you don't have Tailwind installed, you can learn how to install it on the [Tailwind website](https://tailwindcss.com/docs/guides/laravel).

5

Use the Inter font family

Although completely optional, we recommend using the [Inter font family](https://rsms.me/inter) for your application.

Add the following to the head tag in your layout file to ensure the font is loaded:

Copy to clipboard

```
<head>    ...    <link rel="preconnect" href="https://fonts.bunny.net">    <link href="https://fonts.bunny.net/css?family=inter:400,500,600&display=swap" rel="stylesheet" /></head>
```

You can configure Tailwind to use this font family in your resources/css/app.css file:

Copy to clipboard

```
@import 'tailwindcss';@import '../../vendor/livewire/flux/dist/flux.css';...@theme {    --font-sans: Inter, sans-serif;}
```



## Theming

We've meticulously designed Flux to look great out of the box, however, every project has its own identity. You can choose from our hand-picked color schemes or build your own theme by customizing CSS variables.

[Learn more about theming Flux ->](/docs/theming)



## Disable dark mode

By default, Flux will handle the appearance of your application by adding a dark class to the html element depending on the user's system preference or selected appearance.

[Learn more about dark mode ->](/docs/dark-mode)

If you don't want Flux to handle this for you, you can remove the @fluxAppearance directive from your layout file.

Copy to clipboard

```
<head>    ...--    @fluxAppearance</head>
```

Now you can handle the appearance of your application manually.



## Publishing components

To keep things simple, you can use the internal Flux components in your Blade files directly. However, if you'd like to customize a specific Flux component, you can publish its blade file(s) into your project using the following Artisan command:

Copy to clipboard

```
php artisan flux:publish
```

You will be prompted to search and select which components you want to publish. If you want to publish all components at once, you can use the --all flag.

[Learn more about customizing Flux ->](/docs/customization)



## Keeping Flux updated

To ensure you have the latest version of Flux, regularly update your composer dependencies:

Copy to clipboard

```
composer update livewire/flux livewire/flux-pro
```

If you've published Flux components, make sure to check the changelog for any breaking changes before updating:

[Flux release notes (changelog) ->](https://github.com/livewire/flux/releases)



## Cloning an existing project

If you're cloning an existing project that uses Flux Pro, you will need to authenticate your Flux Pro installation.

When running composer install, you will be prompted to provide a username and password:

- Enter your Flux account email as the username
- Enter your Flux license key as the password


To avoid manually typing these credentials, you can create a Composer auth.json file.

To do this, run the following command before you run composer install:

Copy to clipboard

```
composer config http-basic.composer.fluxui.dev your-email your-license-key
```

Make sure to replace `your-email` and `your-license-key` with your actual Flux account email and license key, which you can find on your [dashboard ->](/dashboard).

This will create an auth.json file in your project's root directory. This file contains your email and license key for downloading and installing Flux Pro and should not be added to version control.

You can now run composer install and it should automatically authenticate the Flux Pro installation.



## Activating using Laravel Forge

If you are using Laravel Forge, you can take advantage of their built in [Packages](https://forge.laravel.com/docs/sites/packages.html) feature for
authenticating private composer packages.

Laravel Forge allows you to manage packages on a server or site level. If you have multiple sites using Flux, then it's recommended to manage Packages
 on the server level.

To authenticate Flux, head over to the packages page on either the server or site. You will then see the following:

Click the "Add Credential" button to authenticate with a new private composer package and enter the following details:

- Enter composer.fluxui.dev as the Repository URL
- Enter your Flux account email as the username
- Enter your Flux license key as the password


Finally, click the "Save" button. You should now be authenticated with the Flux private composer server and be able
install Flux using composer require livewire/flux-pro

For more information, please refer to the [Laravel Forge Packages documentation](https://forge.laravel.com/docs/sites/packages.html).



## Activating using Laravel Cloud

If you are using Laravel Cloud, you will need to use their [Build Commands](https://cloud.laravel.com/docs/environments#build-commands) feature for authenticating private composer packages.

To authenticate Flux, open up the environment you wish to use Flux in and go to "Settings" and then "Deployments".

There you will find a "Build Commands" section. Add the following command above the existing composer install command:

Copy to clipboard

```
composer config http-basic.composer.fluxui.dev your-email your-license-key
```

Make sure to replace `your-email` and `your-license-key` with your actual Flux account email and license key, which you can find on your [dashboard ->](/dashboard).

Finally, click the "Save" button. You should now be authenticated with the Flux private composer server and be able deploy your application.

For more information, please refer to the [Laravel Cloud Private Composer Packages documentation](https://cloud.laravel.com/docs/environments#private-composer-packages).



## Activating in GitHub Actions

If you are using Flux in GitHub Actions, you will need to add Flux's license details to your repository's secrets and then configure your GitHub Actions workflows accordingly.

To add your Flux license details as secrets in your GitHub repository, first browse to your repository on GitHub and then go to **Settings > Secrets and variables > Actions**.

From here, click on "New repository secret":

You will need to add the following secrets:

- FLUX_USERNAME – Your Flux account email
- FLUX_LICENSE_KEY – Your Flux license key


Once you've added these secrets, if you're using Laravel's [Livewire Starter Kit](https://laravel.com/docs/12.x/starter-kits#livewire), everything else should already be configured for you.

If you are not using the Livewire Starter Kit, you will need to add the following configuration to your GitHub Actions workflows:

Copy to clipboard

```
- name: Add Flux license  run: composer config http-basic.composer.fluxui.dev "${{ secrets.FLUX_USERNAME }}" "${{ secrets.FLUX_LICENSE_KEY }}"
```

This should be placed before the step that runs composer install.

To see this in action, check out the GitHub Actions workflow included with the [Livewire starter kit ->](https://github.com/laravel/livewire-starter-kit/blob/4d2f09640b1829f542f3aa31b5180eaacc91febe/.github/workflows/tests.yml).

You can now run your GitHub Actions workflow again and it should successfully authenticate the Flux Pro installation.



## Activating in CI

If you are using Flux in a CI environment without an auth.json file, you can add the following environment variables and command to your CI script:

Copy to clipboard

```
composer config http-basic.composer.fluxui.dev "${FLUX_USERNAME}" "${FLUX_LICENSE_KEY}"
```



## Configuring nginx

If you run into problems loading Flux's JavaScript and CSS assets, you may need to configure your nginx server to allow for this.

By default, Flux exposes two routes in your application to serve its assets from: /flux/flux.js and /flux/flux.css.

This is fine for most applications, however, if you are using nginx with a custom configuration, you may receive a 404 from this endpoint.

To fix this issue, you can add the following to your nginx configuration:

Copy to clipboard

```
location ~* ^/flux/flux(\.min)?\.(js|css)$ {    expires off;    try_files $uri $uri/ /index.php?$query_string;}
```

This block should be placed before any other location blocks that match `.js` or `.css` files.

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0002_Upgrade guide

# Upgrade guide

Follow this guide to upgrade from Flux v1.x to v2.x.



## Prerequisites

Before upgrading to Flux v2, make sure you have the following:

- Laravel version 10 or later
- Livewire version 3.5.19 or later
- Tailwind CSS version 4 or later


Flux v2 is built on top of Tailwind CSS v4, so if you are using an older version of Tailwind CSS, you need to upgrade it to v4 or later by following the [Tailwind CSS upgrade guide](https://tailwindcss.com/docs/upgrade-guide).



## Update Flux

Run the following composer command to upgrade your application's Flux and Flux Pro dependencies to v2:

Copy to clipboard

```
composer require livewire/flux:^2.0 livewire/flux-pro:^2.0
```



## Rename @fluxStyles

In Flux v2, the @fluxStyles directive has been removed as these styles are now imported directly into your app.css file.

However, the @fluxAppearance directive has been added as a replacement to manage dark mode in your application—it controls the .dark class on the <html> element.

Copy to clipboard

```
<head>    ...--    @fluxStyles++    @fluxAppearance</head>
```



## Clear the view cache

Run the following Artisan command from your application's root directory to clear any cached/compiled Blade views:

Copy to clipboard

```
php artisan view:clear
```



## Tailwind Config

Because Flux's styles are no longer added via the @fluxStyles directive, you will need to import the Flux CSS file directly into your ./resources/css/app.css file like so:

Copy to clipboard

```
@import "tailwindcss";@import '../../vendor/livewire/flux/dist/flux.css';/* Required for dark mode in Flux... */@custom-variant dark (&:where(.dark, .dark *));...
```



## Migrating accent colors

If you had previously defined custom accent colors in your app.css and tailwind.config.js file, then you will need to update them in your app.css file.

Before, these were defined in a single @layer base block within your app.css file, but now they are defined as two separate blocks:

- default colors are now inside the @theme block
- dark mode colors are now inside the @layer theme block


Here's an example of defining sky as your application's accent color:

Copy to clipboard

```
@theme {    --color-accent: var(--color-sky-600);    --color-accent-content: var(--color-sky-600);    --color-accent-foreground: var(--color-white);}@layer theme {    .dark {        --color-accent: var(--color-sky-600);        --color-accent-content: var(--color-sky-400);        --color-accent-foreground: var(--color-white);    }}
```

If you're still using your old Tailwind config, you can now remove the following lines:

Copy to clipboard

```
export default {    ...    theme: {        extend: {            colors: {                ...--             accent: {--                  DEFAULT: 'var(--color-accent)',--                  content: 'var(--color-accent-content)',--                  foreground: 'var(--color-accent-foreground)',--              },            },        },    },};
```



## Re-assigning gray

If you had previously re-assigned Flux's gray of choice in your tailwind.config.js file, then you will need to move this to your app.css file.

Here's an example of re-assigning zinc to neutral:

Copy to clipboard

```
/* Re-assign Flux's gray of choice... */@theme {  --color-zinc-50: var(--color-neutral-50);  --color-zinc-100: var(--color-neutral-100);  --color-zinc-200: var(--color-neutral-200);  --color-zinc-300: var(--color-neutral-300);  --color-zinc-400: var(--color-neutral-400);  --color-zinc-500: var(--color-neutral-500);  --color-zinc-600: var(--color-neutral-600);  --color-zinc-700: var(--color-neutral-700);  --color-zinc-800: var(--color-neutral-800);  --color-zinc-900: var(--color-neutral-900);  --color-zinc-950: var(--color-neutral-950);}
```

If you are continuing to use your tailwind.config.js file in your application, then you can remove the following:

Copy to clipboard

```
-- import colors from 'tailwindcss/colors';export default {    ...    theme: {        extend: {            colors: {--              // Re-assign Flux's gray of choice...--              zinc: colors.neutral,                ...            },        },    },};
```



## Dark mode changes

If you had previously set darkMode: null in your tailwind.config.js file to prevent Flux from controlling the .dark class and handling dark mode automatically, you can now accomplish this by not including the @fluxAppearance directive in your layout file:

Copy to clipboard

```
<head>    ...--    @fluxAppearance</head>
```



## Rename components

In Flux v2, some components have been renamed. You will need to update your code accordingly:

| v1 | v2 |
| --- | --- |
| flux:options | flux:select.options |
| flux:option | flux:select.option |
| flux:cell | flux:table.cell |
| flux:columns | flux:table.columns |
| flux:column | flux:table.column |
| flux:rows | flux:table.rows |
| flux:row | flux:table.row |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0003_Principles

# Principles

Flux is not a *set* of UI Blade components, it's a *system* of them. The design of this system is guided by a set of principles that, when applied, result in a cleaner, more creative, and more intuitive, app-building experience.



## Simplicity

Above all else, simplicity is the quality Flux aims for in its syntax, implementation, and visuals.

Take for example, a basic input field written with Flux:

Copy to clipboard

```
<flux:input wire:model="email" label="Email" />
```

It's *simple*.

Now, consider a dystopian version of the same input field where simplicity is not valued as highly:

Copy to clipboard

```
<flux:form.field>    <flux:form.field.label>Email</flux:form.field.label>    <div>        <flux:form.field.text-input wire:model="email" />    </div>    @error('email')        <p class="mt-2 text-red-500 dark:text-red-400 text-xs">{{ $message }}</p>    @enderror</flux:form.field>
```

It's a *mess*.



## Complexity

Of course simplicity comes with trade-offs. It's harder to customize smaller parts of a single component that "does too much".

That's why Flux offers composable alternatives to overly *simple* components.

Consider the previous version of the input field:

Copy to clipboard

```
<flux:input wire:model="email" label="Email" />
```

If you want more control, you can *compose* the form field manually from its individual parts:

Copy to clipboard

```
<flux:field>    <flux:label>Email</flux:label>    <flux:input wire:model="email" />    <flux:error name="email" /></flux:field>
```

This gives you the best of both worlds. A short, succinct, syntax for the common case, and the ability to customize each part on an as-needed basis.



## Friendliness

When given the chance, Flux chooses familiar, friendly, names for its components instead of overly technical ones.

For example, you won't find words like "form controls" in Flux. Most developers use simple terminology like "form inputs" instead.

Another example is "accordion" instead of "disclosure" for collapsible sections. "disclosure" is the more acurate UI pattern, however, "accordion" is the more commonly used term amongst application developers.



## Composition

After simplicity, *composability* is the next highest value. Ideally, you learn a handful of core components, and then you mix and match them to create (or *compose*) more robust components.

For example, the following is a common Button component in Flux:

Copy to clipboard

```
<flux:button>Options</flux:button>
```

If you want to trigger a dropdown using that button, simply wrap it in <flux:dropdown>:

Copy to clipboard

```
<flux:dropdown>    <flux:button>Options</flux:button>    <flux:navmenu>        <!-- ... -->    </flux:navmenu></flux:dropdown>
```

Many other libraries force you into more rigid component shapes, dissalowing use of a simple button inside a dropdown and instead forcing you to use a more perscriptive alternative like <flux:dropdown.button>.

Because composition is a priority, you can turn this navigation dropdown into a "system menu" containing submenus, checkable items, and keyboard control by swapping navmenu for menu:

Copy to clipboard

```
<flux:dropdown>    <flux:button>Options</flux:button>    <flux:menu>        <!-- ... -->    </flux:menu></flux:dropdown>
```

Because <flux:menu> is a standalone component in its own right, you can use it to create a context menu that opens on right click instead using the <flux:context> component:

Copy to clipboard

```
<flux:context>    <flux:button>Options</flux:button>    <flux:menu>        <!-- ... -->    </flux:menu></flux:context>
```

*This* is the power of composition; the ability to combine independent components into new and more powerful ones.



## Consistency

Inconsistent naming, component structure, etc. leads to confusion and frustration. It robs from the intuitiveness of a system.

Therefore, you will find repeated syntax patterns all over Flux.

One simple example is the use of the word "heading" instead of "title" or "name" in many components.

This way, you can more easily memorize component terms without having to guess or look them up.

Here are a few examples of Flux components that use the word "heading":

Copy to clipboard

```
<flux:heading>...</flux:heading><flux:menu.submenu heading="..."><flux:accordion.heading>...</flux:accordion.heading>
```



## Brevity

Next to simplicity, brevity is another priority. Flux aims to be as brief as possible without sacrificing any of the above principles.

In general, we avoid compound words that require hyphens in Flux syntax. We also avoid too many levels of nested (dot-seperated) names.

For example, we use the simple word "input" instead of "text-input", "input-text", "form-input", or "form-control":

Copy to clipboard

```
<flux:input>
```

Composition helps with this quest for brevity. Consider the following dropdown menu component:

Copy to clipboard

```
<flux:dropdown>    <flux:button>Options</flux:button>    <flux:menu>        <!-- ... -->    </flux:menu></flux:dropdown>
```

Notice the simple, single-word names for the dropdown component.

Consider what it might look like if composability and brevity weren't as high a priority:

Copy to clipboard

```
<flux:dropdown-menu>    <flux:dropdown-menu.button>Options</flux:dropdown-menu.button>    <flux:dropdown-menu.items>        <!-- ... -->    </flux:dropdown-menu.items></flux:dropdown-menu>
```



## Use the browser

Modern browsers have a lot to offer. Flux aims to leverage this to its full potential.

When you use native browser features, you are depending on reliable behavior that you don't have to download any JavaScript libraries for.

For example, anytime you see a dropdown (popover) in Flux, it will likely by using the popover attribute under the hood. This is a relatively new, but widely supported, feature that solves many problems that plague hand-built dropdown menus:

Copy to clipboard

```
<div popover>    <!-- ... --></div>
```

[Read more about the popover attribute](https://developer.mozilla.org/en-US/docs/Web/API/Popover_API)

Another example is using the <dialog> element for modals instead of something hand written:

Copy to clipboard

```
<dialog>    <!-- ... --></dialog>
```

By using the native <dialog> element, you get a much more consistent and reliable modal experience with things like focus management, accessibility, and keyboard navigation out of the box.

[Read more about the dialog element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog)



## Use CSS

CSS is becoming a more and more powerful tool for authoring composable design systems. With new feature like :has(), :not() and :where(), things that historically required JavaScript, can be done with CSS alone.

When you peer into the source of a Flux component, you may notice some complicated Tailwind utilities being used.

This is a tradeoff in complexity. In Flux, if a component *can* use CSS to solve a problem, instead of using PHP or JavaScript, that component *will* use CSS.

For example, consider how the search icon in the flux:command.input component changes color when the input field is focused:

Copy to clipboard

```
<flux:command.input placeholder="Search..." />
```

When rendered in the browser, the search icon turns darker when the input is focused. This elegant interaction happens without any JavaScript.

It's accomplished using CSS's :has() selector. Here's the actual Tailwind utility used in the component:

Copy to clipboard

```
[&:has(+input:focus)]:text-zinc-800
```

The above selector will match any element that has a sibling input element with focus, and changes its text color to a darker shade. This is a simple but powerful example of using modern CSS to enhance the user experience without additional JavaScript.



## We style, you space

In general, Flux provides *styling* out of the box, and leaves *spacing* to you. Another, more practical way to put it is: We provide padding, you provide margins.

For example, take a look at the following "Create account" form:

Copy to clipboard

```
<form wire:submit="createAccount">    <div class="mb-6">        <flux:heading>Create an account</flux:heading>        <flux:text class="mt-2">We're excited to have you on board.</flux:text>    </div>    <flux:input class="mb-6" label="Email" wire:model="email" />    <div class="mb-6 flex *:w-1/2 gap-4">        <flux:input label="Password" wire:model="password" />        <flux:input label="Confirm password" wire:model="password_confirmation" />    </div>    <flux:button type="submit" variant="primary">Create account</flux:button></form>
```

Notice how Flux handles the styling of individual components, but leaves the spacing and layout to you.

The reason for this pattern is that *spacing* is contextual, and *styling* is less-so. Therefore, if we baked spacing into Flux, you would be constantly overriding it, or worse, preserving it and risking your app looking disjointed.

It takes slightly more work to manage spacing and layout yourself, however, the payoff in flexibility is well worth it.

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0004_Patterns

# Patterns

Every design decision in flux was carefully and intentionally made. Understanding these intentions will make your experience with flux more intuitive.


Ideally, after internalizing some of flux's design philosophy, you will be able to almost guess how to use a component you're unfamiliar with.



## Props vs attributes

Props and attributes are indistinguishable on the surface, however, we've found it helpful to make a distinction between flux-provided properties called "props" and bespoke "attributes" that will be forwarded directly to an underlying HTML element.

For example, the following component uses a prop called variant as well as a bespoke x-on:change.prevent attribute:

Copy to clipboard

```
<flux:button variant="primary" x-on:change.prevent="...">
```

When the component is rendered in the browser, the output HTML might will look something like this:

Copy to clipboard

```
<button type="button" class="bg-zinc-900 ..." x-on:change.prevent="...">
```

As you can see, the x-on:change.prevent attribute was forwarded directly to the underlying HTML element, while the variant prop was instead internally used to customize which classes were applied to the input.



## Class merging

Most flux components apply Tailwind classes to their underlying elements, however, you can also pass your own classes into components and they will be automatically merged with the classes applied by flux.

Here's an example of making a button full width by passing in the w-full Tailwind utility class:

Copy to clipboard

```
<flux:button class="w-full">
```

Now, when the component is rendered, the output HTML will contain both the w-full class and other classes applied by flux:

Copy to clipboard

```
<button type="button" class="w-full border border-zinc-200 ...">
```



## Dealing with class merging conflicts

Occasionally, you may run into conflicts when passing in a Tailwind utility that flux also applies internally.

For example, you may try to customize the background color of a button by passing in the bg-zinc-800 Tailwind utility class:

Copy to clipboard

```
<flux:button class="bg-zinc-800 hover:bg-zinc-700">
```

However, because flux applies it's own bg-* attributes, both classes will be rendered in the output HTML:

Copy to clipboard

```
<button type="button" class="bg-zinc-800 hover:bg-zinc-700 bg-white hover:bg-zinc-100...">
```

Because both classes exist on the element, the one defined last in CSS wins.

Tailwind's important (!) modifier is the simplest way to resolve these conflicts:

Copy to clipboard

```
<flux:button class="bg-zinc-800! hover:bg-zinc-700!">
```

The conflicting utilities will still both be rendered, however the user-defined ones with the ! modifier will take precedence.

Usage of the ! modifier can cause more problems than it solves. Below are a few alternatives to consider instead:

- Publishing the component and adding your own variant
- Globally customizing the component by styling the data attributes
- Writing a new component for your unique case


## Split attribute forwarding

In a perfect world, each flux component would directly render a single HTML element. However, in practice, some components are more complex than that.

For example, the flux:input component actually renders two HTML elements by default. A wrapping <div> and an underlying <input> element:

Copy to clipboard

```
<div class="...">    <input type="text" class="..."></div>
```

This presents a problem when passing bespoke Tailwind classes into the component: which element should receive the provided classes?

In these cases flux will often split up the forwarded attributes into two groups: styling related ones like class and behavioral ones like autofocus. It will then apply each to wherever is most appropriate.

For example consider passing in the following class and autofocus attributes:

Copy to clipboard

```
<flux:input class="w-full" autofocus>
```

Flux will apply the w-full class to the wrapping <div> element and the autofocus attribute to the underlying <input> element:

Copy to clipboard

```
<div class="w-full ...">    <input type="text" class="..." autofocus></div>
```



## Common props

Now that you've seen some of the nuances of attributes, let's look at some common prop patterns you will encounter as you use Flux.



## Variant

First up is "variant". Any component that offers an alternate visual style uses the variant prop to do so.

Here's a list of a few common component variants:

Copy to clipboard

```
<flux:button variant="primary" /><flux:input variant="filled" /><flux:modal variant="flyout" /><flux:badge variant="solid" /><flux:select variant="combobox" /><flux:separator variant="subtle" /><flux:tabs variant="segmented" />
```

If you find the need for a variant we don't offer, don't be afraid to [publish a component and add your own.](/docs/customization#publishing-components)



## Icon

Rather than manually adding, styling, and spacing icons inside component slots, you can simply pass the icon prop to any component that supports it.

Flux uses [Heroicons](https://heroicons.com/) for its icon collection. Heroicons is a set of beautiful and functional icons crafted by the fine folks at [Tailwind Labs](https://tailwindcss.com).

Here's a handful of components you can pass icons into:

Copy to clipboard

```
<flux:button icon="magnifying-glass" /><flux:input icon="magnifying-glass" /><flux:tab icon="cog-6-tooth" /><flux:badge icon="user" /><flux:breadcrumbs.item icon="home" /><flux:navlist.item icon="user" /><flux:navbar.item icon="user" /><flux:menu.item icon="plus" />
```

Occasionally, if a component supports adding an icon to the end of an element instead of the beginning by default, you can pass the icon:trailing prop as well:

Copy to clipboard

```
<flux:button icon:trailing="chevron-down" /><flux:input icon:trailing="credit-card" /><flux:badge icon:trailing="x-mark" /><flux:navbar.item icon:trailing="chevron-down" />
```



## Size

Some components offer size variations through the size prop.

Here are a few components that can be sized-down:

Copy to clipboard

```
<flux:button size="sm" /><flux:select size="sm" /><flux:input size="sm" /><flux:tabs size="sm" />
```

Here are a few that can be sized up for larger visual contexts:

Copy to clipboard

```
<flux:heading size="lg" /><flux:badge size="lg" />
```



## Keyboard hints

Similar to the icon prop, many components allow you to add decorative hints for keyboard shortcuts using the kbd prop:

Copy to clipboard

```
<flux:button kbd="⌘S" /><flux:tooltip kbd="D" /><flux:input kbd="⌘K" /><flux:menu.item kbd="⌘E" /><flux:command.item kbd="⌘N" />
```



## Inset

Certain components offer the inset prop which makes it easy to add the exact amount of negative margin needed to "inset" an element on any axis you specify.

This is extremely useful for putting a button or a badge inline with other text and not stretching the entire height of the container.

Copy to clipboard

```
<flux:badge inset="top bottom"><flux:button variant="ghost" inset="left">
```



## Prop forwarding

Occasionally, one component will wrap another and expose it as a simple prop.

For example, here is the Button component that allows you to set the icon using the simple icon prop instead of passing an entire Icon component into the Button as a child:

Copy to clipboard

```
<flux:button icon="bell" />
```

This is often a more desirable alternative to composing the entire component like so:

Copy to clipboard

```
<flux:button>   <flux:icon.bell /></flux:button>
```

However, when using the icon prop, you are unable to add additional props to the Icon component like variant.

In these cases, flux will often expose nested props via prefixes like so:

Copy to clipboard

```
<flux:button icon="bell" icon:variant="solid" />
```



## Opt-out props

Sometimes flux will turn a prop "on" by default, or manage its state internally. For example, the current prop on the navbar.item component.

However, you may want to enforce that its value remains false for a specific instance of the component.

In these cases, you can use Laravel's dynamic prop syntax (:) and pass in false.

Copy to clipboard

```
<flux:navbar.item :current="false">
```



## Shorthand props

Sometimes a component arrangement is both common and verbose enough that it warrants a shorthand syntax.

For example, here's a full input field:

Copy to clipboard

```
<flux:field>    <flux:label>Email</flux:label>    <flux:input wire:model="email" type="email" />    <flux:error name="email" /></flux:field>
```

This can be shortened to the following:

Copy to clipboard

```
<flux:input type="email" wire:model="email" label="Email" />
```

Internally, flux will expand the above into the full assembly of field, label, input, and error components.

This way you can keep syntax short and concise, but still have the ability to fully customize things if you'd like to use the full longform syntax.

You'll also encounter this pattern with tooltips and buttons.

Here's a long-form toolip:

Copy to clipboard

```
<flux:tooltip content="Settings">    <flux:button icon="cog-6-tooth" /></flux:tooltip>
```

Because the above is often repetitive, you can shorten it to a simple tooltip prop:

Copy to clipboard

```
<flux:button icon="cog-6-tooth" tooltip="Settings" />
```



## Data binding

In Livewire you are used to adding wire:model directly to input elements inside your forms.

In Flux, the experience is no different. Here are some common components you will often be adding wire:model to:

Copy to clipboard

```
<flux:input wire:model="email" /><flux:checkbox wire:model="terms" /><flux:switch wire:model.live="enabled" /><flux:textarea wire:model="content" /><flux:select wire:model="state" />
```

In addition to these common ones you'd expect, here are a few other components you can control via wire:model:

Copy to clipboard

```
<flux:checkbox.group wire:model="notifications"><flux:radio.group wire:model="payment"><flux:tabs wire:model="activeTab">
```

Of course, you can also pass x-model or x-on:change to any of these and they should behave exactly like native input elements.



## Component Groups

When a Flux component can be "grouped", but is otherwise a stand-alone component, its wrapper component has a .group suffix.

All of the following components can be used on their own, or grouped together:

Copy to clipboard

```
<flux:button.group>    <flux:button /></flux:button.group><flux:input.group>    <flux:input /></flux:input.group><flux:checkbox.group>    <flux:checkbox /></flux:checkbox.group><flux:radio.group>    <flux:radio /></flux:radio.group>
```

Alternatively, if a component can NOT be used on its own, but can be grouped, the wrapper will often be the main name of the component, and each child will have a .item suffix:

Copy to clipboard

```
<flux:accordion>    <flux:accordion.item /></flux:accordion><flux:menu>    <flux:menu.item /></flux:menu><flux:breadcrumbs>    <flux:breadcrumbs.item /></flux:breadcrumbs><flux:navbar>    <flux:navbar.item /></flux:navbar><flux:navlist>    <flux:navlist.item /></flux:navlist><flux:navmenu>    <flux:navmenu.item /></flux:navmenu><flux:command>    <flux:command.item /></flux:command><flux:autocomplete>    <flux:autocomplete.item /></flux:autocomplete>
```



# Root components

Most of the time, when a component can be composed of many sub-components, you will see compound names like the ones mentioned above.

However, for components that are larger or more "primitive" feeling than the others, they will lack a common prefix, and instead use the name of the component itself.

For example, this is flux's field component:

Copy to clipboard

```
<flux:field>    <flux:label></flux:label>    <flux:description></flux:description>    <flux:error></flux:error></flux:field>
```

You'll notice bare component names like flux:label, instead of flux:field.label.

The reasoning for this is to avoid overly verbose heirarchies in common components that would result in naming like: flux:field.label.badge.

You will also see this pattern with <flux:table>.



## Anomalies

As painful as it is, sometimes for something to "feel right", you have to abandon consistency for one reason or another.

For example, the flux:tabs component doesn't follow the aforementioned rules:

Copy to clipboard

```
<flux:tab.group>    <flux:tabs>        <flux:tab>    </flux:tabs>    <flux:tab.panel></flux:tab.group>
```



## Slots

In general, Flux prefers composing multiple components together rather than using slots.

However, there are times where there is no substitute and slots are the perfect solution.

To demonstrate, consider the following input component with an x-mark icon:

Copy to clipboard

```
<flux:input icon:trailing="x-mark" />
```

If you wanted to wrap the icon in a clickable button to perform an action there is no way to achieve that without slots (or without offering an extremely verbose, custom syntax).

Here is the above, rewritten with a wrapping button:

Copy to clipboard

```
<flux:input>    <x-slot name="iconTrailing">        <flux:button icon="x-mark" size="sm" variant="subtle" wire:click="clear" />    </x-slot></flux:input>
```



## Paper cuts

Here are a few gotchas that you might encounter while using Flux.



## Blade components vs HTML elements

When dealing with plain HTML elements in Blade, you are free to use expressions like @if inside opening tags.

However, those expressions are not supported inside the opening tag of a Blade or Flux component.

Instead, you must stay within the confines of the Blade component [dynamic attribute syntax](https://laravel.com/docs/12.x/blade#component-attributes):

Copy to clipboard

```
<!-- Conditional attributes: --><input @if ($disabled) disabled @endif><flux:input :disabled="$disabled">
```

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)  




# 0005_Theming

# Theming

We've meticulously designed Flux to look great out of the box, however, every project has its own identity. You can choose from our hand-picked color schemes or build your own theme by customizing CSS variables.

[Build your theme with our interactive theme builder ->](/themes)



## Base color

There are essentially two colors in a Flux project: the **base color** and the **accent color**.

The base color is the color of the majority of your application's content. It's used for things like text, backgrounds, borders, etc.

The accent color is the color of the primary action buttons and other interactive elements in your application.

Flux ships with "zinc" as the default base color, but you are free to use any shade of gray you'd like.

Because zinc is hard-coded throughout Flux's source code, you will need to redefine it in your CSS file if you'd like to use a different base color.

Here is an example of redefining "zinc" to "slate" in your CSS file:

Copy to clipboard

```
/* resources/css/app.css *//* Re-assign Flux's gray of choice... */@theme {  --color-zinc-50: var(--color-slate-50);  --color-zinc-100: var(--color-slate-100);  --color-zinc-200: var(--color-slate-200);  --color-zinc-300: var(--color-slate-300);  --color-zinc-400: var(--color-slate-400);  --color-zinc-500: var(--color-slate-500);  --color-zinc-600: var(--color-slate-600);  --color-zinc-700: var(--color-slate-700);  --color-zinc-800: var(--color-slate-800);  --color-zinc-900: var(--color-slate-900);  --color-zinc-950: var(--color-slate-950);}
```

Now, Flux will use "slate" as the base color instead of "zinc", and you can use "slate" inside your application utilities like you normally would:

Copy to clipboard

```
<flux:text class="text-slate-800 dark:text-white">...</flux:text>
```



## Accent color

Under the hood, flux uses CSS variables for its accent colors. This means that you can change the accent color to any color you'd like.

We recommend you use the [interactive theme builder](/themes) with pre-selected colors, however, if you'd like to use a different accent color, you can define the following CSS variables in your own css file:

Copy to clipboard

```
/* resources/css/app.css */@theme {    --color-accent: var(--color-red-500);    --color-accent-content: var(--color-red-600);    --color-accent-foreground: var(--color-white);}@layer theme {    .dark {        --color-accent: var(--color-red-500);        --color-accent-content: var(--color-red-400);        --color-accent-foreground: var(--color-white);    }}
```

You'll notice Flux uses three different hues in both light mode and dark mode for its accent color palette. Here are descriptions of each hue:

| Variable | Description |
| --- | --- |
| --color-accent | The main accent color used is the background for primary buttons. |
| --color-accent-content | A (typically) darker hue used for text content because it's more readable. |
| --color-accent-foreground | The color of (typically) text content on top of an accent colored background. |

Tailwind allows you to use reference CSS variable colors inline like so:

Copy to clipboard

```
<button class="bg-[var(--color-accent)] text-[var(--color-accent-foreground)]">
```

However, this is not a very ergonomic syntax. Instead you can use utility classes such as:

Copy to clipboard

```
<button class="bg-accent text-accent-foreground">
```



## Accent props

Certain design elements like tabs and links use the accent color by default. If you'd like to opt out of this behavior, and use the base color instead, you can use the :accent="false" prop:

Copy to clipboard

```
<!-- Link --><flux:link :accent="false">Profile</flux:tab><!-- Tabs --><flux:tabs>    <flux:tab :accent="false">Profile</flux:tab>    <flux:tab :accent="false">Account</flux:tab>    <flux:tab :accent="false">Billing</flux:tab></flux:tabs><!-- Navbar --><flux:navbar>    <flux:navbar.item :accent="false">Profile</flux:navbar.item>    <flux:navbar.item :accent="false">Account</flux:navbar.item>    <flux:navbar.item :accent="false">Billing</flux:navbar.item></flux:navbar><!-- Navlist --><flux:navlist>    <flux:navlist.item :accent="false">Profile</flux:navlist.item>    <flux:navlist.item :accent="false">Account</flux:navlist.item>    <flux:navlist.item :accent="false">Billing</flux:navlist.item></flux:navlist>
```

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0006_Dark mode

# Dark mode

Flux supports dark mode out of the box.





Light Dark System



## Set up Tailwind

To take full advantage of Flux's dark mode controls, you will need to ensure that Tailwind CSS is configured to use the selector strategy for dark mode by adding this to your resources/css/app.css file:

Copy to clipboard

```
@import "tailwindcss";@import '../../vendor/livewire/flux/dist/flux.css';@custom-variant dark (&:where(.dark, .dark *));
```

By doing this, Flux can now toggle on and off dark mode by adding/removing a .dark class to the <html> element of your application.



## Disabling dark mode handling

By default, Flux will handle the appearance of your application by adding a dark class to the html element depending on the user's system preference or selected appearance.

If you don't want Flux to handle this for you, you can remove the @fluxAppearance directive from your layout file.

Copy to clipboard

```
<head>    ...--    @fluxAppearance</head>
```

Now you can handle the appearance of your application manually.



## JavaScript utilities

Managing dark mode in your own application is cumbersome. Here are a few essential behaviors you have to implement:

- Add/remove the .dark class to the <html> element
- Store the users preference in local storage
- Honor the system preference if system is selected
- Listen for changes in the system preference after a page has loaded


To save you from this complexity, Flux provides two JavaScript/Alpine utilities for making it easy to manage dark mode:

Copy to clipboard

```
// Get/set a users color scheme preference...$flux.appearance = 'light|dark|system'// Get/set the current color scheme of your app...$flux.dark = 'true|false'
```

Given these two utilities, you can now use Alpine to easily build widgets to manage dark mode.

For example, here's how you would write a simple dark mode toggle button:

Copy to clipboard

```
<flux:button x-data x-on:click="$flux.dark = ! $flux.dark">Toggle</flux:button>
```

Or if you wanted to allow a user to choose their preferred color scheme, you could write:

Copy to clipboard

```
<flux:radio.group x-data x-model="$flux.appearance">    <flux:radio value="light">Light</flux:radio>    <flux:radio value="dark">Dark</flux:radio>    <flux:radio value="system">System</flux:radio></flux:radio.group>
```

If you want to use these utilities outside of Alpine, you can instead access .appearance and .dark on the global window.Flux JavaScript object from anywhere in your application:

Copy to clipboard

```
let button = document.querySelector('...')button.addEventListener('click', () => {    Flux.dark = ! Flux.dark})
```



## Examples

Rather than offer a one-size-fits-~~all~~none solution, Flux provides a few examples of how you can use these utilities to build your own dark mode controls.



## Toggle button

A simple toggle button to allow uesrs to control dark mode from something like a navbar or sidebar.









Copy to clipboard

```
<flux:button x-data x-on:click="$flux.dark = ! $flux.dark" icon="moon" variant="subtle" aria-label="Toggle dark mode" />
```



## Dropdown menu

More robust than a simple toggle button, this dropdown menu allows users to choose between light, dark, and system modes.





Light

Dark

System





Copy to clipboard

```
<flux:dropdown x-data align="end">    <flux:button variant="subtle" square class="group" aria-label="Preferred color scheme">        <flux:icon.sun x-show="$flux.appearance === 'light'" variant="mini" class="text-zinc-500 dark:text-white" />        <flux:icon.moon x-show="$flux.appearance === 'dark'" variant="mini" class="text-zinc-500 dark:text-white" />        <flux:icon.moon x-show="$flux.appearance === 'system' && $flux.dark" variant="mini" />        <flux:icon.sun x-show="$flux.appearance === 'system' && ! $flux.dark" variant="mini" />    </flux:button>    <flux:menu>        <flux:menu.item icon="sun" x-on:click="$flux.appearance = 'light'">Light</flux:menu.item>        <flux:menu.item icon="moon" x-on:click="$flux.appearance = 'dark'">Dark</flux:menu.item>        <flux:menu.item icon="computer-desktop" x-on:click="$flux.appearance = 'system'">System</flux:menu.item>    </flux:menu></flux:dropdown>
```



## Toggle switch

A simple toggle switch to allow users to control dark mode from something like a settings page.





 Dark mode





Copy to clipboard

```
<flux:switch x-data x-model="$flux.dark" label="Dark mode"  />
```



## Segmented radio

A simple toggle switch to allow users to control dark mode from something like a settings page.





Light Dark System





Copy to clipboard

```
<flux:radio.group x-data variant="segmented" x-model="$flux.appearance">    <flux:radio value="light" icon="sun">Light</flux:radio>    <flux:radio value="dark" icon="moon">Dark</flux:radio>    <flux:radio value="system" icon="computer-desktop">System</flux:radio></flux:radio.group>
```

Alternatively, you can use an icon-only variant to save horizontal space:









Copy to clipboard

```
<flux:radio.group x-data variant="segmented" x-model="$flux.appearance">    <flux:radio value="light" icon="sun" />    <flux:radio value="dark" icon="moon" />    <flux:radio value="system" icon="computer-desktop" /></flux:radio.group>
```

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0007_Customization

# Customization

Knowing how to customize components to your own needs is a crucial part of using Flux. Flux provides multiple levels of customization so that it doesn't have to be all or nothing.



## Tailwind overrides

The first level of customization is simply passing your own Tailwind classes into a component.

This often works well for things like custom width:

Copy to clipboard

```
<flux:select class="max-w-md">
```

However, there are times where your one-off Tailwind class conflicts with Flux's internal styling.

For example, here's how you might attempt to customize the background color of a button:

Copy to clipboard

```
<flux:button class="bg-zinc-800 hover:bg-zinc-700">
```

However, because flux applies its own bg-* attributes, both classes will be rendered in the output HTML, but only one will be applied:

Copy to clipboard

```
<button type="button" class="bg-zinc-800 hover:bg-zinc-700 bg-white hover:bg-zinc-100...">
```

The simplest way to resolve these conflicts is using Tailwind's important (!) modifier like so:

Copy to clipboard

```
<flux:button class="bg-zinc-800! hover:bg-zinc-700!">
```

The conflicting utilities will still both be rendered, however the user-defined ones with the ! modifier will take precedence.

Sometimes, using ! is necessary. Most times, you would be better served creating a new component or customizing the existing one with a new variant. More on that below.



## Publishing components

When you first install Flux, all the components are automatically available to be used inside any Blade file in your app.

If you wish, you can "publish" any given component into your project so that you own all the Blade files that make up that component.

At first, you might be hesitant to publish components because you won't receive automatic updates, howevever, this isn't as scary as it may first seem.
To publish a component, run the following Artisan command:

Copy to clipboard

```
php artisan flux:publish
```

You will be prompted to search and select which components you want to publish. If you want to publish all components at once, you can use the --all flag:

Copy to clipboard

```
php artisan flux:publish --all
```

Let's say you decided to publish the checkbox component into your project, you would find the component file in the following location:

Copy to clipboard

```
resources/    views/        flux/            checkbox.blade.php            ...
```

Now, you can continue using the checkbox component like normal, but the published Blade files will be used instead of the original ones. This means you can change anything you like about the component such as classes, slots and variants.



## Global style overrides

Most HTML elements used inside flux component have a data-flux-* attribute. You can use this attribute to override any styles you'd like to. Here's an example of using Tailwind's @apply directive to change the default background color of all buttons:

Copy to clipboard

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0008_Help

# Help

Our number one priority is to make Flux the best UI library for Livewire applications. If you're having trouble with Flux, please reach out to us for help.



## Found a bug?

Please create an isolated, succinct, snippet of code that we can use to reproduce your issue and submit it via a GitHub issue on the livewire/flux repository.

[-> Submit a bug report](https://github.com/livewire/flux/issues/new?template=bug_report.yml)



## Have a feature request?

Please submit your feature request via a GitHub discussion on the livewire/flux repository.

[-> Submit a feature request](https://github.com/livewire/flux/discussions/new?category=feature-requests)



## Need help with billing, licensing, etc.

If you have any questions related to purchases, refunds, licensing, discounts, etc., you can email our support inbox.

[-> Send us an email at [email protected]](/cdn-cgi/l/email-protection#087b7d7878677a7c486e647d707d61266c6d7e)

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0009_Accordion



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Accordion

Collapse and expand sections of content. Perfect for FAQs and content-heavy areas.





What's your refund policy?

If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.

Do you offer any discounts for bulk purchases?

Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.

How do I track my order?

Once your order is shipped, you will receive an email with a tracking number. Use this number to track your order on our website.





Copy to clipboard

```
<flux:accordion>    <flux:accordion.item>        <flux:accordion.heading>What's your refund policy?</flux:accordion.heading>        <flux:accordion.content>            If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.        </flux:accordion.content>    </flux:accordion.item>    <flux:accordion.item>        <flux:accordion.heading>Do you offer any discounts for bulk purchases?</flux:accordion.heading>        <flux:accordion.content>            Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.        </flux:accordion.content>    </flux:accordion.item>    <flux:accordion.item>        <flux:accordion.heading>How do I track my order?</flux:accordion.heading>        <flux:accordion.content>            Once your order is shipped, you will receive an email with a tracking number. Use this number to track your order on our website.        </flux:accordion.content>    </flux:accordion.item></flux:accordion>
```



## [Shorthand](#shorthand)

You can save on markup by passing the heading text as a prop directly.



Copy to clipboard

```
<flux:accordion.item heading="What's your refund policy?">    If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.</flux:accordion.item>
```



## [With transition](#with-transition)

Enable expanding transitions for smoother interactions.





What's your refund policy?

If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.

Do you offer any discounts for bulk purchases?

Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.

How do I track my order?

Once your order is shipped, you will receive an email with a tracking number. Use this number to track your order on our website.





Copy to clipboard

```
<flux:accordion transition>    <!-- ... --></flux:accordion>
```



## [Disabled](#disabled)

Restrict an accordion item from being expanded.





What's your refund policy?

It all depends how nice you are to me in your email.

Do you offer PPP discounts?

Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.

How do I track my order?

What do YOU think?





Copy to clipboard

```
<flux:accordion.item disabled>    <!-- ... --></flux:accordion.item>
```



## [Exclusive](#exclusive)

Enforce that only a single accordion item is expanded at a time.





What's your refund policy?

If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.

Do you offer any discounts for bulk purchases?

Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.

How do I track my order?

Once your order is shipped, you will receive an email with a tracking number. Use this number to track your order on our website.





Copy to clipboard

```
<flux:accordion exclusive>    <!-- ... --></flux:accordion>
```



## [Expanded](#expanded)

Expand a specific accordion by default.





What's your refund policy?

If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.

Do you offer any discounts for bulk purchases?

Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.

How do I track my order?

Once your order is shipped, you will receive an email with a tracking number. Use this number to track your order on our website.





Copy to clipboard

```
<flux:accordion.item expanded>    <!-- ... --></flux:accordion.item>
```



## [Leading icon](#leading-icon)

Display the icon before the heading instead of after it.





What's your refund policy?

If you are not satisfied with your purchase, we offer a 30-day money-back guarantee. Please contact our support team for assistance.

Do you offer any discounts for bulk purchases?

Yes, we offer special discounts for bulk orders. Please reach out to our sales team with your requirements.

How do I track my order?

Once your order is shipped, you will receive an email with a tracking number. Use this number to track your order on our website.





Copy to clipboard

```
<flux:accordion variant="reverse">    <!-- ... --></flux:accordion>
```

## Reference



### [flux:accordion](#fluxaccordion)

| Prop | Description |
| --- | --- |
| variant | When set to reverse, displays the icon before the heading instead of after it. |
| transition | If true, enables expanding transitions for smoother interactions. Default: false. |
| exclusive | If true, only one accordion item can be expanded at a time. Default: false. |



### [flux:accordion.item](#fluxaccordionitem)

| Prop | Description |
| --- | --- |
| heading | Shorthand for flux:accordion.heading content. |
| expanded | If true, the accordion item is expanded by default. Default: false. |
| disabled | If true, the accordion item cannot be expanded or collapsed. Default: false. |



### [flux:accordion.heading](#fluxaccordionheading)

| Slot | Description |
| --- | --- |
| default | The heading text. |



### [flux:accordion.content](#fluxaccordioncontent)

| Slot | Description |
| --- | --- |
| default | The content to display when the accordion item is expanded. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0010_Autocomplete



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Autocomplete

Enhance an input field with autocomplete suggestions.

Autocomplete suggests text as you type and inserts the selected suggestion directly into the input field. It does not support a value attribute.

If you need to show a label but store a value (e.g., showing a user's name but storing their ID), use a [combobox](/components/select#combobox) instead.





State of residence

Alabama Arkansas
California
Colorado
Connecticut
Delaware
Florida
Georgia
Hawaii
Idaho
Illinois
Indiana
Iowa
Kansas
Kentucky
Louisiana
Maine
Maryland
Massachusetts
Michigan
Minnesota
Mississippi
Missouri
Montana
Nebraska
Nevada
New Hampshire
New Jersey
New Mexico
New York
North Carolina
North Dakota
Ohio
Oklahoma
Oregon
Pennsylvania
Rhode Island
South Carolina
South Dakota
Tennessee
Texas
Utah
Vermont
Virginia
Washington
West Virginia
Wisconsin
Wyoming





Copy to clipboard

```
<flux:autocomplete wire:model="state" label="State of residence">    <flux:autocomplete.item>Alabama</flux:autocomplete.item>    <flux:autocomplete.item>Arkansas</flux:autocomplete.item>    <flux:autocomplete.item>California</flux:autocomplete.item>    <!-- ... --></flux:autocomplete>
```

## Related components

[Input Text fields for collecting user input](/components/input) [Select Display a dropdown menu for selecting one option from many](/components/select)

## Reference



### [flux:autocomplete](#fluxautocomplete)

| Prop | Description |
| --- | --- |
| wire:model | The name of the Livewire property to bind the input value to. |
| type | HTML input type (e.g., text, email, password, file, date). Default: text. |
| label | Label text displayed above the input. |
| description | Descriptive text displayed below the label. |
| placeholder | Placeholder text displayed when the input is empty. |
| size | Size of the input. Options: sm, xs. |
| variant | Visual style variant. Options: filled. Default: outline. |
| disabled | If true, prevents user interaction with the input. |
| readonly | If true, makes the input read-only. |
| invalid | If true, applies error styling to the input. |
| multiple | For file inputs, allows selecting multiple files. |
| mask | Input mask pattern using Alpine's mask plugin. Example: 99/99/9999. |
| icon | Name of the icon displayed at the start of the input. |
| icon:trailing | Name of the icon displayed at the end of the input. |
| kbd | Keyboard shortcut hint displayed at the end of the input. |
| clearable | If true, displays a clear button when the input has content. |
| copyable | If true, displays a copy button to copy the input's content. |
| viewable | For password inputs, if true, displays a toggle to show/hide the password. |
| as | Render the input as a different element. Options: button. Default: input. |
| container:class | Additional CSS classes applied to the autocomplete container. Useful for setting height constraints like max-h-80. |
| class:input | CSS classes applied directly to the input element instead of the input wrapper. |

| Slot | Description |
| --- | --- |
| icon | Custom content displayed at the start of the input (e.g., icons). |
| icon:leading | Custom content displayed at the start of the input (e.g., icons). |
| icon:trailing | Custom content displayed at the end of the input (e.g., buttons). |



### [flux:autocomplete.item](#fluxautocompleteitem)

| Prop | Description |
| --- | --- |
| disabled | If present or true, the item cannot be selected. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0011_Avatar

# Avatar

Display an image or initials as an avatar.









Copy to clipboard

```
<flux:avatar src="https://unavatar.io/x/calebporzio" />
```



## [Tooltip](#tooltip)

Use the tooltip prop to display a tooltip when hovering over the avatar.





Caleb Porzio





Copy to clipboard

```
<flux:avatar tooltip="Caleb Porzio" src="https://unavatar.io/x/calebporzio" /><!-- Or infer from the name prop... --><flux:avatar tooltip name="Caleb Porzio" src="https://unavatar.io/x/calebporzio" />
```



## [Initials](#initials)

When no src is provided, the name prop will be used to automatically generate initials. You can also use the initials prop directly.





CP

Ca

C





Copy to clipboard

```
<flux:avatar name="Caleb Porzio" /><flux:avatar name="calebporzio" /><flux:avatar name="calebporzio" initials:single /><!-- Or use the initials prop directly... --><flux:avatar initials="CP" />
```



## [Size](#size)

Use the size prop to change the size of the avatar.









Copy to clipboard

```
<!-- Extra large: size-16 (64px) --><flux:avatar size="xl" src="https://unavatar.io/x/calebporzio" /><!-- Large: size-12 (48px) --><flux:avatar size="lg" src="https://unavatar.io/x/calebporzio" /><!-- Default: size-10 (40px) --><flux:avatar src="https://unavatar.io/x/calebporzio" /><!-- Small: size-8 (32px) --><flux:avatar size="sm" src="https://unavatar.io/x/calebporzio" /><!-- Extra small: size-6 (24px) --><flux:avatar size="xs" src="https://unavatar.io/x/calebporzio" />
```



## [Icon](#icon)

Use the icon prop to display an icon instead of an image.









Copy to clipboard

```
<flux:avatar icon="user" /><flux:avatar icon="phone" /><flux:avatar icon="computer-desktop" />
```



## [Colors](#colors)

Use the color prop to change the color of the avatar.





CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP

CP





Copy to clipboard

```
<flux:avatar name="Caleb Porzio" color="red" /><flux:avatar name="Caleb Porzio" color="orange" /><flux:avatar name="Caleb Porzio" color="amber" /><flux:avatar name="Caleb Porzio" color="yellow" /><flux:avatar name="Caleb Porzio" color="lime" /><flux:avatar name="Caleb Porzio" color="green" /><flux:avatar name="Caleb Porzio" color="emerald" /><flux:avatar name="Caleb Porzio" color="teal" /><flux:avatar name="Caleb Porzio" color="cyan" /><flux:avatar name="Caleb Porzio" color="sky" /><flux:avatar name="Caleb Porzio" color="blue" /><flux:avatar name="Caleb Porzio" color="indigo" /><flux:avatar name="Caleb Porzio" color="violet" /><flux:avatar name="Caleb Porzio" color="purple" /><flux:avatar name="Caleb Porzio" color="fuchsia" /><flux:avatar name="Caleb Porzio" color="pink" /><flux:avatar name="Caleb Porzio" color="rose" />
```



## [Auto color](#auto-color)

Deterministically generate a color based on a user's name.





CP

MJ

KC

KN

KS

BP

AB





Copy to clipboard

```
<flux:avatar name="Caleb Porzio" color="auto" /><!-- Use color:seed to generate a consistent color based --><!-- on something unchanging like a user's ID... --><flux:avatar name="Caleb Porzio" color="auto" color:seed="{{ $user->id }}" />
```



## [Circle](#circle)

Use the circle prop to make the avatar circular.









Copy to clipboard

```
<flux:avatar circle src="https://unavatar.io/x/calebporzio" />
```



## [Badge](#badge)

Add badges to avatars in various ways. Use the badge prop by itself for a simple dot indicator, provide content like numbers or emojis, or even pass in custom HTML via a slot.





25

👍





Copy to clipboard

```
<flux:avatar badge badge:color="green" src="https://unavatar.io/x/calebporzio" /><flux:avatar badge badge:color="zinc" badge:position="top right" badge:circle badge:variant="outline" src="https://unavatar.io/x/calebporzio" /><flux:avatar badge="25" src="https://unavatar.io/x/calebporzio" /><flux:avatar circle badge="👍" badge:circle src="https://unavatar.io/x/calebporzio" /><flux:avatar circle src="https://unavatar.io/x/calebporzio">    <x-slot:badge>        <img class="size-3" src="https://unavatar.io/github/hugosaintemarie" />    </x-slot:badge></flux:avatar>
```



## [Groups](#groups)

Stack avatars together. By default, grouped avatars have rings that adapt to your theme - white in light mode and a dark color in dark mode. If you need to customize the ring color, to match a different background, you can do so by adding a custom class to the flux:avatar.group component.





3+

3+





Copy to clipboard

```
<flux:avatar.group>    <flux:avatar src="https://unavatar.io/x/calebporzio" />    <flux:avatar src="https://unavatar.io/github/hugosaintemarie" />    <flux:avatar src="https://unavatar.io/github/joshhanley" />    <flux:avatar>3+</flux:avatar></flux:avatar.group><!-- Adapt rings to custom background... --><flux:avatar.group class="**:ring-zinc-100 dark:**:ring-zinc-800">    <flux:avatar circle src="https://unavatar.io/x/calebporzio" />    <flux:avatar circle src="https://unavatar.io/github/hugosaintemarie" />    <flux:avatar circle src="https://unavatar.io/github/joshhanley" />    <flux:avatar circle>3+</flux:avatar></flux:avatar.group>
```



## [As button](#as-button)

Use the as prop to make the avatar a button.









Copy to clipboard

```
<flux:avatar as="button" src="https://unavatar.io/x/calebporzio" />
```



## [As link](#as-link)

Use the href prop to make the avatar a link.





[https://x.com/calebporzio](https://x.com/calebporzio)





Copy to clipboard

```
<flux:avatar href="https://x.com/calebporzio" src="https://unavatar.io/x/calebporzio" />
```

## Examples



### [Testimonial](#testimonial)





IMO Livewire takes Blade to the next level. It's basically what Blade should be by default. 🔥

Taylor Otwell

Creator of Laravel





Copy to clipboard

```
<div>    <div class="flex items-center gap-2">        <flux:icon.star variant="solid" />        <flux:icon.star variant="solid" />        <flux:icon.star variant="solid" />        <flux:icon.star variant="solid" />        <flux:icon.star variant="solid" />    </div>    <flux:heading size="xl" class="mt-4 italic">        <p>IMO Livewire takes Blade to the next level. It's basically what Blade should be by default. 🔥</p>    </flux:heading>    <div class="mt-6 flex items-center gap-4">        <flux:avatar size="lg" src="https://unavatar.io/x/taylorotwell" />        <div>            <flux:heading size="lg">Taylor Otwell</flux:heading>            <flux:text>Creator of Laravel</flux:text>        </div>    </div></div>
```



### [Grouped feature](#grouped-feature)





The Laravel Podcast

New

A podcast about Laravel, development best practices, and the PHP ecosystem—hosted by Jeffrey Way, Matt Stauffer, and Taylor Otwell, later joined by Adam Wathan.





Copy to clipboard

```
<div>    <flux:heading size="xl">The Laravel Podcast <flux:badge inset="top bottom" class="ml-1 max-sm:hidden">New</flux:badge></flux:heading>    <flux:text class="mt-2">        A podcast about Laravel, development best practices, and the PHP ecosystem—hosted by Jeffrey Way, Matt Stauffer, and Taylor Otwell, later joined by Adam Wathan.    </flux:text>    <flux:avatar.group class="mt-6">        <flux:avatar circle size="lg" src="https://unavatar.io/x/taylorotwell" />        <flux:avatar circle size="lg" src="https://unavatar.io/x/adamwathan" />        <flux:avatar circle size="lg" src="https://unavatar.io/x/jeffrey_way" />        <flux:avatar circle size="lg" src="https://unavatar.io/x/stauffermatt" />    </flux:avatar.group></div>
```



### [Members table](#members-table)

Include avatars in table rows to make user data more identifiable.





Team members

Invite

| Caleb Porzio     You <br>[[email protected]](/cdn-cgi/l/email-protection) | * Admin  Member  Guest |
| --- | --- |
| Hugo Sainte-Marie<br>[[email protected]](/cdn-cgi/l/email-protection) | Admin  * Member  Guest |
| Josh Hanley<br>[[email protected]](/cdn-cgi/l/email-protection) | Admin  * Member  Guest |





Copy to clipboard

```
<div class="flex justify-between items-center mb-4">    <flux:heading size="lg">Team members</flux:heading>    <flux:button size="sm" icon="plus">Invite</flux:button></div><flux:table>    <flux:table.rows>        <flux:table.row>            <flux:table.cell>                <div class="flex items-center gap-2 sm:gap-4">                    <flux:avatar circle size="lg" class="max-sm:size-8" src="https://unavatar.io/github/calebporzio" />                    <div class="flex flex-col">                        <flux:heading>Caleb Porzio <flux:badge size="sm" color="blue" class="ml-1 max-sm:hidden">You</flux:badge></flux:heading>                        <flux:text class="max-sm:hidden">[[email protected]](/cdn-cgi/l/email-protection)</flux:text>                    </div>                </div>            </flux:table.cell>            <flux:table.cell>                <div class="flex justify-end items-center gap-2">                    <flux:select size="sm" class="min-w-fit max-w-fit">                        <flux:select.option value="admin" selected>Admin</flux:select.option>                        <flux:select.option value="member">Member</flux:select.option>                        <flux:select.option value="guest">Guest</flux:select.option>                    </flux:select>                    <flux:button size="sm" variant="subtle" icon="trash" class="shrink-0" />                </div>            </flux:table.cell>        </flux:table.row>        <flux:table.row >            <flux:table.cell>                <div class="flex items-center gap-2 sm:gap-4">                    <flux:avatar circle size="lg" class="max-sm:size-8" src="https://unavatar.io/github/hugosaintemarie" />                    <div class="flex flex-col">                        <flux:heading>Hugo Sainte-Marie</flux:heading>                        <flux:text class="max-sm:hidden">[[email protected]](/cdn-cgi/l/email-protection)</flux:text>                    </div>                </div>            </flux:table.cell>            <flux:table.cell>                <div class="flex justify-end items-center gap-2">                    <flux:select size="sm" class="min-w-fit max-w-fit">                        <flux:select.option value="admin">Admin</flux:select.option>                        <flux:select.option value="member" selected>Member</flux:select.option>                        <flux:select.option value="guest">Guest</flux:select.option>                    </flux:select>                    <flux:button size="sm" variant="subtle" icon="trash" class="shrink-0" />                </div>            </flux:table.cell>        </flux:table.row>        <flux:table.row>            <flux:table.cell>                <div class="flex items-center gap-2 sm:gap-4">                    <flux:avatar circle size="lg" class="max-sm:size-8" src="https://unavatar.io/github/joshhanley" />                    <div class="flex flex-col">                        <flux:heading>Josh Hanley</flux:heading>                        <flux:text class="max-sm:hidden">[[email protected]](/cdn-cgi/l/email-protection)</flux:text>                    </div>                </div>            </flux:table.cell>            <flux:table.cell>                <div class="flex justify-end items-center gap-2">                    <flux:select size="sm" class="min-w-fit max-w-fit">                        <flux:select.option value="admin">Admin</flux:select.option>                        <flux:select.option value="member" selected>Member</flux:select.option>                        <flux:select.option value="guest">Guest</flux:select.option>                    </flux:select>                    <flux:button size="sm" variant="subtle" icon="trash" class="shrink-0" />                </div>            </flux:table.cell>        </flux:table.row>    </flux:table.rows></flux:table>
```



### [Assignees list](#assignees-list)

Include avatars in table rows to make user data more identifiable.





Assignees

- Caleb Porzio

- Hugo Sainte-Marie

- Josh Hanley

- Jason Beggs





Copy to clipboard

```
<flux:card>    <div class="flex justify-between items-center">        <flux:heading>Assignees</flux:heading>        <flux:button size="sm" variant="subtle" icon="plus" inset="top bottom" />    </div>    <flux:separator class="mt-2 mb-4" variant="subtle" />    <ul class="flex flex-col gap-3">        <li class="flex items-center gap-2">            <flux:avatar size="xs" src="https://unavatar.io/github/calebporzio" />            <flux:heading>Caleb Porzio</flux:heading>        </li>        <li class="flex items-center gap-2">            <flux:avatar size="xs" src="https://unavatar.io/github/hugosaintemarie" />            <flux:heading>Hugo Sainte-Marie</flux:heading>        </li>        <li class="flex items-center gap-2">            <flux:avatar size="xs" src="https://unavatar.io/github/joshhanley" />            <flux:heading>Josh Hanley</flux:heading>        </li>        <li class="flex items-center gap-2">            <flux:avatar size="xs" src="https://unavatar.io/github/jasonlbeggs" />            <flux:heading>Jason Beggs</flux:heading>        </li>    </ul></flux:card>
```



### [Select options](#select-options)

Enhance select options with avatars to make them more visually recognizable.





Assign to

Caleb Porzio

Hugo Sainte-Marie

Josh Hanley

Jason Beggs





Copy to clipboard

```
<flux:select variant="listbox" label="Assign to">    <flux:select.option selected>        <div class="flex items-center gap-2 whitespace-nowrap">            <flux:avatar circle size="xs" src="https://unavatar.io/github/calebporzio" /> Caleb Porzio        </div>    </flux:select.option>    <flux:select.option>        <div class="flex items-center gap-2 whitespace-nowrap">            <flux:avatar circle size="xs" src="https://unavatar.io/github/hugosaintemarie" /> Hugo Sainte-Marie        </div>    </flux:select.option>    <flux:select.option>        <div class="flex items-center gap-2 whitespace-nowrap">            <flux:avatar circle size="xs" src="https://unavatar.io/github/joshhanley" /> Josh Hanley        </div>    </flux:select.option>    <flux:select.option>        <div class="flex items-center gap-2 whitespace-nowrap">            <flux:avatar circle size="xs" src="https://unavatar.io/github/jasonlbeggs" /> Jason Beggs        </div>    </flux:select.option></flux:select>
```



### [User popover](#user-popover)

Display a user's profile information in a popover.





Follow back

Caleb Porzio

@calebporzio

Follows you

I'm a full stack developer with a passion for building web applications. Currently working on a new project called [Flux](https://fluxui.dev).

1.2k

Followers

1.2k

Following





Copy to clipboard

```
<flux:dropdown hover position="bottom center">    <flux:avatar as="button" name="calebporzio" src="https://unavatar.io/x/calebporzio" />    <flux:popover class="relative max-w-[15rem]">        <div class="absolute top-0 right-0 p-2">            <flux:button icon="user-plus" variant="filled" size="sm">Follow back</flux:button>        </div>        <flux:avatar size="xl" name="calebporzio" src="https://unavatar.io/x/calebporzio" />        <flux:heading class="mt-2">Caleb Porzio</flux:heading>        <flux:text>@calebporzio <flux:badge color="zinc" size="sm" inset="top bottom">Follows you</flux:badge></flux:text>        <flux:text class="mt-3">            I'm a full stack developer with a passion for building web applications. Currently working on a new project called <flux:link href="https://fluxui.dev">Flux</flux:link>.        </flux:text>        <div class="flex gap-4 mt-3">            <div class="flex gap-2 items-center">                <flux:heading>1.2k</flux:heading> <flux:text>Followers</flux:text>            </div>            <div class="flex gap-2 items-center">                <flux:heading>1.2k</flux:heading> <flux:text>Following</flux:text>            </div>        </div>    </flux:popover></flux:dropdown>
```

## Related components

[Profile Display a user's profile with avatar and optional name](/components/profile) [Tooltip Display informative tooltips when hovering over an element](/components/tooltip)

## Reference



### [flux:avatar](#fluxavatar)

| Prop | Description |
| --- | --- |
| name | User's name to display as initials. If provided without initials, this will be used to generate initials automatically. |
| src | URL to the image to display as avatar. |
| initials | Custom initials to display when no src is provided. Will override name if provided. |
| alt | Alternative text for the avatar image. (Default: name if provided) |
| size | Size of the avatar. Options: xs (24px), sm (32px), (default: 40px), lg (48px). |
| color | Background color when displaying initials or icons. Options: red, orange, amber, yellow, lime, green, emerald, teal, cyan, sky, blue, indigo, violet, purple, fuchsia, pink, rose, auto. Default: none (uses system colors). |
| color:seed | Value used when color="auto" to deterministically generate consistent colors. Useful for using user IDs to generate consistent colors. |
| circle | If present or true, makes the avatar fully circular instead of rounded corners. |
| icon | Name of the icon to display instead of an image or initials. |
| icon:variant | Icon variant to use. Options: outline, solid. Default: solid. |
| tooltip | Text to display in a tooltip when hovering over the avatar. If set to true, uses the name prop as tooltip content. |
| tooltip:position | Position of the tooltip. Options: top, right, bottom, left. Default: top. |
| badge | Content to display as a badge. Can be a string, boolean, or a slot. |
| badge:color | Color of the badge. Options: same color options as the color prop. |
| badge:circle | If present or true, makes the badge fully circular instead of slightly rounded corners. |
| badge:position | Position of the badge. Options: top left, top right, bottom left, bottom right. Default: bottom right. |
| badge:variant | Variant of the badge. Options: solid, outline. Default: solid. |
| as | Element to render the avatar as. Options: button, div (default). |
| href | URL to link to, making the avatar a link element. |

| Slot | Description |
| --- | --- |
| default | Custom content to display inside the avatar. Will override initials if provided. |
| badge | Custom content to display in the badge (for more complex badge content). |



### [flux:avatar.group](#fluxavatargroup)

| Prop | Description |
| --- | --- |
| class | CSS classes to apply to the group, including customizing ring colors using *:ring-{color} format. |

| Slot | Description |
| --- | --- |
| default | Place multiple flux:avatar components here to display them as a group. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0012_Badge

# Badge

Highlight information like status, category, or count.





New





Copy to clipboard

```
<flux:badge color="lime">New</flux:badge>
```



## [Sizes](#sizes)

Choose between three different sizes for your badges with the size prop.





Small

Default

Large





Copy to clipboard

```
<flux:badge size="sm">Small</flux:badge><flux:badge>Default</flux:badge><flux:badge size="lg">Large</flux:badge>
```



## [Icons](#icons)

Add icons to badges with the icon and icon:trailing props.





Users

Files

Videos





Copy to clipboard

```
<flux:badge icon="user-circle">Users</flux:badge><flux:badge icon="document-text">Files</flux:badge><flux:badge icon:trailing="video-camera">Videos</flux:badge>
```



## [Rounded](#rounded)

Display badges with a fully rounded border radius using the rounded prop.





Users





Copy to clipboard

```
<flux:badge rounded icon="user">Users</flux:badge>
```



## [As button](#as-button)

Make the entire badge clickable by wrapping it in a button element.





Amount





Copy to clipboard

```
<flux:badge as="button" rounded icon="plus" size="lg">Amount</flux:badge>
```



## [With close button](#with-close-button)

Make a badge removable by appending a close button.





Admin





Copy to clipboard

```
<flux:badge>    Admin <flux:badge.close /></flux:badge>
```



## [Colors](#colors)

Choose from an array of colors to differentiate between badges and convey emotion.





Zinc

Red

Orange

Amber

Yellow

Lime

Green

Emerald

Teal

Cyan

Sky

Blue

Indigo

Violet

Purple

Fuchsia

Pink

Rose





Copy to clipboard

```
<flux:badge color="zinc">Zinc</flux:badge><flux:badge color="red">Red</flux:badge><flux:badge color="orange">Orange</flux:badge><flux:badge color="amber">Amber</flux:badge><flux:badge color="yellow">Yellow</flux:badge><flux:badge color="lime">Lime</flux:badge><flux:badge color="green">Green</flux:badge><flux:badge color="emerald">Emerald</flux:badge><flux:badge color="teal">Teal</flux:badge><flux:badge color="cyan">Cyan</flux:badge><flux:badge color="sky">Sky</flux:badge><flux:badge color="blue">Blue</flux:badge><flux:badge color="indigo">Indigo</flux:badge><flux:badge color="violet">Violet</flux:badge><flux:badge color="purple">Purple</flux:badge><flux:badge color="fuchsia">Fuchsia</flux:badge><flux:badge color="pink">Pink</flux:badge><flux:badge color="rose">Rose</flux:badge>
```



## [Solid variant](#solid-variant)

Bold, high-contrast badges for more important status indicators or alerts.





Zinc

Red

Orange

Amber

Yellow

Lime

Green

Emerald

Teal

Cyan

Sky

Blue

Indigo

Violet

Purple

Fuchsia

Pink

Rose





Copy to clipboard

```
<flux:badge variant="solid" color="zinc">Zinc</flux:badge><flux:badge variant="solid" color="red">Red</flux:badge><flux:badge variant="solid" color="orange">Orange</flux:badge><flux:badge variant="solid" color="amber">Amber</flux:badge><flux:badge variant="solid" color="yellow">Yellow</flux:badge><flux:badge variant="solid" color="lime">Lime</flux:badge><flux:badge variant="solid" color="green">Green</flux:badge><flux:badge variant="solid" color="emerald">Emerald</flux:badge><flux:badge variant="solid" color="teal">Teal</flux:badge><flux:badge variant="solid" color="cyan">Cyan</flux:badge><flux:badge variant="solid" color="sky">Sky</flux:badge><flux:badge variant="solid" color="blue">Blue</flux:badge><flux:badge variant="solid" color="indigo">Indigo</flux:badge><flux:badge variant="solid" color="violet">Violet</flux:badge><flux:badge variant="solid" color="purple">Purple</flux:badge><flux:badge variant="solid" color="fuchsia">Fuchsia</flux:badge><flux:badge variant="solid" color="pink">Pink</flux:badge><flux:badge variant="solid" color="rose">Rose</flux:badge>
```



## [Inset](#inset)

If you're using badges alongside inline text, you might run into spacing issues because of the extra padding around the badge. Use the inset prop to add negative margins to the top and bottom of the badge to avoid this.





Page builder

New

Easily author new pages without leaving your browser.





Copy to clipboard

```
<flux:heading>    Page builder <flux:badge color="lime" inset="top bottom">New</flux:badge></flux:heading><flux:text class="mt-2">Easily author new pages without leaving your browser.</flux:text>
```

## Related components

[Avatar Display user profile images or fallback initials](/components/avatar) [Navbar Build responsive navigation bars with item badges](/components/navbar)

## Reference



### [flux:badge](#fluxbadge)

| Prop | Description |
| --- | --- |
| color | Badge color (e.g., zinc, red, blue). Default: zinc. |
| size | Badge size. Options: sm, lg. |
| rounded | If present or true, makes the badge fully rounded instead of slightly rounded corners. |
| variant | Badge style variant. Options: solid (depracated: pill, use rounded prop instead). |
| icon | Name of the icon to display before the badge text. |
| icon:trailing | Name of the icon to display after the badge text. |
| icon:variant | Icon variant. Options: outline, solid, mini, micro. Default: mini. |
| as | HTML element to render the badge as. Options: button. Default: div. |
| inset | Add negative margins to specific sides. Options: top, bottom, left, right, or any combination of the four. |



### [flux:badge.close](#fluxbadgeclose)

| Prop | Description |
| --- | --- |
| icon | Name of the icon to display. Default: x-mark. |
| icon:variant | Icon variant. Options: outline, solid, mini, micro. Default: mini. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0013_Brand

# Brand

Display your company or application's logo and name in a clean, consistent way across your interface.





[Acme Inc.](#) [Acme Inc.](#)





Copy to clipboard

```
<flux:brand href="#" logo="/img/demo/logo.png" name="Acme Inc." /><flux:brand href="#" name="Acme Inc.">    <x-slot name="logo">        <div class="size-6 rounded shrink-0 bg-accent text-accent-foreground flex items-center justify-center"><i class="font-serif font-bold">A</i></div>    </x-slot></flux:brand>
```



## [Logo slot](#logo-slot)

Use the logo slot to provide a custom logo for your brand.





[Launchpad](#)





Copy to clipboard

```
<flux:brand href="#" name="Launchpad">    <x-slot name="logo" class="size-6 rounded-full bg-cyan-500 text-white text-xs font-bold">        <flux:icon name="rocket-launch" variant="micro" />    </x-slot></flux:brand>
```



## [Logo only](#logo-only)

Display just the logo without the company name by omitting the name prop.





[#](#) [#](#)





Copy to clipboard

```
<flux:brand href="#" logo="/img/demo/logo.png" />
```

## Examples



### [Header with brand](#header-with-brand)









Copy to clipboard

```
<flux:header class="px-4! w-full bg-zinc-50 dark:bg-zinc-800 rounded-lg border border-zinc-100 dark:border-white/5">    <flux:brand href="#" name="Acme Inc.">        <x-slot name="logo" class="bg-accent text-accent-foreground">            <i class="font-serif font-bold">A</i>        </x-slot>    </flux:brand>    <flux:navbar variant="outline">        <flux:navbar.item href="#" current>Home</flux:navbar.item>        <flux:navbar.item badge="12" href="#">Inbox</flux:navbar.item>    </flux:navbar>    <flux:spacer class="min-w-24" />    <flux:profile circle :chevron="false" avatar="https://unavatar.io/x/calebporzio" /></flux:header>
```

## Related components

[Header Top navigation headers for your application](/layouts/header) [Sidebar Sidebar navigation for your application](/layouts/sidebar)

## Reference



### [flux:brand](#fluxbrand)

| Prop | Description |
| --- | --- |
| name | Company or application name to display next to the logo. |
| logo | URL to the image to display as logo, or can pass content via slot. |
| alt | Alternative text for the logo. |
| href | URL to navigate to when the brand is clicked. Default: '/'. |

| Slot | Description |
| --- | --- |
| logo | Custom content for the logo section, typically containing an image, SVG, or custom HTML. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0014_Button

# Button

A powerful and composable button component for your application.





Button





Copy to clipboard

```
<flux:button>Button</flux:button>
```



## [Variants](#variants)

Use the variant prop to change the visual style of the button.



Use primary buttons sparingly; mostly for form submissions.





Default

Primary

Filled

Danger

Ghost

Subtle





Copy to clipboard

```
<flux:button>Default</flux:button><flux:button variant="primary">Primary</flux:button><flux:button variant="filled">Filled</flux:button><flux:button variant="danger">Danger</flux:button><flux:button variant="ghost">Ghost</flux:button><flux:button variant="subtle">Subtle</flux:button>
```



## [Colors](#colors)

Use standard Tailwind color names with the color prop to control the color of the primary button.





Zinc

Red

Orange

Amber

Yellow

Lime

Green

Emerald

Teal

Cyan

Sky

Blue

Indigo

Violet

Purple

Fuchsia

Pink

Rose





Copy to clipboard

```
<flux:button variant="primary" color="zinc">Zinc</flux:button><flux:button variant="primary" color="red">Red</flux:button><flux:button variant="primary" color="orange">Orange</flux:button><flux:button variant="primary" color="amber">Amber</flux:button><flux:button variant="primary" color="yellow">Yellow</flux:button><flux:button variant="primary" color="lime">Lime</flux:button><flux:button variant="primary" color="green">Green</flux:button><flux:button variant="primary" color="emerald">Emerald</flux:button><flux:button variant="primary" color="teal">Teal</flux:button><flux:button variant="primary" color="cyan">Cyan</flux:button><flux:button variant="primary" color="sky">Sky</flux:button><flux:button variant="primary" color="blue">Blue</flux:button><flux:button variant="primary" color="indigo">Indigo</flux:button><flux:button variant="primary" color="violet">Violet</flux:button><flux:button variant="primary" color="purple">Purple</flux:button><flux:button variant="primary" color="fuchsia">Fuchsia</flux:button><flux:button variant="primary" color="pink">Pink</flux:button><flux:button variant="primary" color="rose">Rose</flux:button>
```



## [Sizes](#sizes)

The default button size works great for most cases, but here are some additional size options for unique situations.





Default

Small

Extra small





Copy to clipboard

```
<flux:button>Base</flux:button><flux:button size="sm">Small</flux:button><flux:button size="xs">Extra small</flux:button>
```



## [Icons](#icons)

Automatically sized and styled icons for your buttons.





Export

Open





Copy to clipboard

```
<flux:button icon="ellipsis-horizontal" /><flux:button icon="arrow-down-tray">Export</flux:button><flux:button icon:trailing="chevron-down">Open</flux:button><flux:button icon="x-mark" variant="subtle" />
```



## [Loading](#loading)

Buttons with wire:click or type="submit" will automatically show a loading indicator and disable pointer events during network requests.





Save changes





Copy to clipboard

```
<flux:button wire:click="save">    Save changes</flux:button>
```

You can disable this behavior using :loading="false".



Copy to clipboard

```
<flux:button wire:click="save" :loading="false">
```



## [Full width](#full-width)

A button that spans the full width of the container.





Send invite





Copy to clipboard

```
<flux:button variant="primary" class="w-full">Send invite</flux:button>
```



## [Button groups](#button-groups)

Fuse related buttons into a group with shared borders.





Oldest

Newest

Top





Copy to clipboard

```
<flux:button.group>    <flux:button>Oldest</flux:button>    <flux:button>Newest</flux:button>    <flux:button>Top</flux:button></flux:button.group>
```



## [Icon group](#icon-group)

Fuse multiple icon buttons into a visually-linked group.









Copy to clipboard

```
<flux:button.group>    <flux:button icon="bars-3-bottom-left"></flux:button>    <flux:button icon="bars-3"></flux:button>    <flux:button icon="bars-3-bottom-right"></flux:button></flux:button.group>
```



## [Attached button](#attached-button)

Append or prepend an icon button to another button to add additional functionality.





New product





Copy to clipboard

```
<flux:button.group>    <flux:button>New product</flux:button>    <flux:button icon="chevron-down"></flux:button></flux:button.group>
```



## [As a link](#as-a-link)

Display an HTML a tag as a button by passing the href prop.





[Visit Google](https://google.com)





Copy to clipboard

```
<flux:button    href="https://google.com"    icon:trailing="arrow-up-right">    Visit Google</flux:button>
```



## [As an input](#as-an-input)

To display a button as an input, pass as="button" to the [input component](/components/input).





Search...

⌘K







Copy to clipboard

```
<flux:input as="button" placeholder="Search..." icon="magnifying-glass" kbd="⌘K" />
```



## [Square](#square)

Make the height and width of a button equal. Flux does this automatically for icon-only buttons.





...





Copy to clipboard

```
<flux:button square>...</flux:button>
```



## [Inset](#inset)

When using ghost or subtle button variants, you can use the inset prop to negate any invisible padding for better alignment.





Post successfully created.





Copy to clipboard

```
<div class="flex justify-between">    <flux:heading>Post successfully created.</flux:heading>    <flux:button size="sm" icon="x-mark" variant="ghost" inset /></div>
```

## Related components

[Dropdown Display expandable menus for navigational options](/components/dropdown) [Icon Display icons for your application](/components/icon)

## Reference



### [flux:button](#fluxbutton)

| Prop | Description |
| --- | --- |
| as | The HTML tag to render the button as. Options: button (default), a, div. |
| href | The URL to link to when the button is used as an anchor tag. |
| type | The HTML type attribute of the button. Options: button (default), submit. |
| variant | Visual style of the button. Options: outline, primary, filled, danger, ghost, subtle. Default: outline. |
| size | Size of the button. Options: base (default), sm, xs. |
| icon | Name of the icon to display at the start of the button. |
| icon:variant | Visual style of the icon. Options: outline, solid, mini, micro. Default: micro. |
| icon:trailing | Name of the icon to display at the end of the button. |
| square | If true, makes the button square. (Useful for icon-only buttons.) |
| align | Alignment of the button content. Options: start, center, end. Default: center. |
| inset | Add negative margins to specific sides. Options: top, bottom, left, right, or any combination of the four. |
| loading | If true, shows a loading spinner and disables the button when used with wire:click or type="submit". If false, the button will not show a loading spinner at all. Default: true. |
| tooltip | Text to display in a tooltip when hovering over the button. |
| tooltip:position | Position of the tooltip. Options: top, bottom, left, right. Default: top. |
| tooltip:kbd | Text to display in a keyboard shortcut tooltip when hovering over the button. |
| kbd | Text to display in a keyboard shortcut tooltip when hovering over the button. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the button. Common use: w-full for full width. |

| Attribute | Description |
| --- | --- |
| data-flux-button | Applied to the root element for styling and identification. |



### [flux:button.group](#fluxbuttongroup)

A container component that groups multiple buttons together with shared borders.

| Slot | Description |
| --- | --- |
| default | The buttons to be grouped together. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0015_Breadcrumbs

# Breadcrumbs

Help users navigate and understand their place within your application.





[Home](#)

[Blog](#)

Post





Copy to clipboard

```
<flux:breadcrumbs>    <flux:breadcrumbs.item href="#">Home</flux:breadcrumbs.item>    <flux:breadcrumbs.item href="#">Blog</flux:breadcrumbs.item>    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item></flux:breadcrumbs>
```



## [With slashes](#with-slashes)

Use slashes instead of chevrons to separate breadcrumb items.





[Home](#)

[Blog](#)

Post





Copy to clipboard

```
<flux:breadcrumbs>    <flux:breadcrumbs.item href="#" separator="slash">Home</flux:breadcrumbs.item>    <flux:breadcrumbs.item href="#" separator="slash">Blog</flux:breadcrumbs.item>    <flux:breadcrumbs.item separator="slash">Post</flux:breadcrumbs.item></flux:breadcrumbs>
```



## [With icon](#with-icon)

Use an icon instead of text for a particular breadcrumb item.





[#](#)

[Blog](#)

Post





Copy to clipboard

```
<flux:breadcrumbs>    <flux:breadcrumbs.item href="#" icon="home" />    <flux:breadcrumbs.item href="#">Blog</flux:breadcrumbs.item>    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item></flux:breadcrumbs>
```



## [With ellipsis](#with-ellipsis)

Truncate a long breadcrumb list with an ellipsis.





[#](#)

Post





Copy to clipboard

```
<flux:breadcrumbs>    <flux:breadcrumbs.item href="#" icon="home" />    <flux:breadcrumbs.item icon="ellipsis-horizontal" />    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item></flux:breadcrumbs>
```



## [With ellipsis dropdown](#with-ellipsis-dropdown)

Truncate a long breadcrumb list into a single ellipsis dropdown.





[#](#)

Post





Copy to clipboard

```
<flux:breadcrumbs>    <flux:breadcrumbs.item href="#" icon="home" />    <flux:breadcrumbs.item>        <flux:dropdown>            <flux:button icon="ellipsis-horizontal" variant="ghost" size="sm" />            <flux:navmenu>                <flux:navmenu.item>Client</flux:navmenu.item>                <flux:navmenu.item icon="arrow-turn-down-right">Team</flux:navmenu.item>                <flux:navmenu.item icon="arrow-turn-down-right">User</flux:navmenu.item>            </flux:navmenu>        </flux:dropdown>    </flux:breadcrumbs.item>    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item></flux:breadcrumbs>
```

## Reference



### [flux:breadcrumbs](#fluxbreadcrumbs)

| Slot | Description |
| --- | --- |
| default | The breadcrumb items to display. |



### [flux:breadcrumbs.item](#fluxbreadcrumbsitem)

| Prop | Description |
| --- | --- |
| href | URL the breadcrumb item links to. If omitted, renders as non-clickable text. |
| icon | Name of the icon to display before the badge text. |
| icon:variant | Icon variant. Options: outline, solid, mini, micro. Default: mini. |
| separator | Name of the icon to display as the separator. Default: chevron-right. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0016_Calendar



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Calendar

A flexible calendar component for date selection. Supports single dates, multiple dates, and date ranges. Perfect for scheduling and booking systems.









Copy to clipboard

```
<flux:calendar />
```



## Basic Usage

Set the initial selected date using the value prop with a Y-m-d formatted date string:

Copy to clipboard

```
<flux:calendar value="2026-03-03" />
```

You can also bind the selection to a Livewire property using wire:model:

Copy to clipboard

```
<flux:calendar wire:model="date" />
```

Now you can access the selected date from your Livewire component using either a Carbon instance or a Y-m-d formatted string:

Copy to clipboard

```
<?phpuse Illuminate\Support\Carbon;use Livewire\Component;class BookAppointment extends Component {    public Carbon $date;    public function mount() {        $this->date = now();    }}
```



## [Multiple dates](#multiple-dates)

Select multiple non-consecutive dates.









Copy to clipboard

```
<flux:calendar multiple />
```

Set multiple selected dates using a comma-separated list in the value prop:

Copy to clipboard

```
<flux:calendar    multiple    value="2026-03-02,2026-03-05,2026-03-15"/>
```

You can also bind the selection to a Livewire property using wire:model:

Copy to clipboard

```
<flux:calendar multiple wire:model="dates" />
```

You can access the selected dates in your Livewire component using an array of Y-m-d formatted date strings:

Copy to clipboard

```
<?phpuse Illuminate\Support\Carbon;use Livewire\Component;class RequestTimeOff extends Component {    public array $dates = [];    public function mount() {        $this->dates = [            now()->format('Y-m-d'),            now()->addDays(1)->format('Y-m-d'),        ];    }}
```



## [Date range](#date-range)

Select a range of dates.









Copy to clipboard

```
<flux:calendar mode="range" />
```

Set the initial range using the value prop with a start and end date separated by a forward slash:

Copy to clipboard

```
<flux:calendar mode="range" value="2026-03-02/2026-03-06" />
```

You can also bind the selection to a Livewire property using wire:model:

Copy to clipboard

```
<flux:calendar mode="range" wire:model="range" />
```

Now you can access the selected range from your Livewire component using an associative array of Y-m-d formatted date strings:

Copy to clipboard

```
<?phpuse Livewire\Component;class BookFlight extends Component {    public ?array $range;    public function book() {        // ...        $flight->depart_on = $this->range['start'];        $flight->return_on = $this->range['end'];        // ...    }}
```

Alternatively, you can use the specialized DateRange object for enhanced functionality:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class BookFlight extends Component {    public ?DateRange $range;    public function book() {        // ...        $flight->depart_on = $this->range->start();        $flight->return_on = $this->range->end();        // ...    }}
```

We highly recommend using the DateRange object for range selection, it provides a lot of useful functionality.

[Check out everything you can do with the DateRange object ->](#the-daterange-object)



## Range Configuration

Control range behavior with these props:

Copy to clipboard

```
<!-- Set minimum and maximum range limits --><flux:calendar mode="range" min-range="3" max-range="10" /><!-- Control number of months shown --><flux:calendar mode="range" months="2" />
```



## [Size](#size)

Adjust the calendar's size to fit your layout. Available sizes include xs, sm, lg, xl, and 2xl.









Copy to clipboard

```
<flux:calendar size="xl" />
```



## [Static](#static)

Create a non-interactive calendar for display purposes.









Copy to clipboard

```
<flux:calendar    static    value="2026-03-03"    size="xs"    :navigation="false"/>
```



## [Min/max dates](#minmax-dates)

Restrict the selectable date range by setting minimum and maximum boundaries.









Copy to clipboard

```
<flux:calendar max="2026-03-03" />
```

You can also use the convenient "today" shorthand:

Copy to clipboard

```
<!-- Prevent selection before today... --><flux:calendar min="today" /><!-- Prevent selection after today... --><flux:calendar max="today" />
```



## [Unavailable dates](#unavailable-dates)

Disable specific dates from being selected. Useful for blocking out holidays, showing booked dates, or indicating unavailable time slots.









Copy to clipboard

```
<flux:calendar unavailable="2026-03-02,2026-03-04" />
```



## [With today shortcut](#with-today-shortcut)

Add a shortcut button to quickly navigate to today's date. When viewing a different month, it jumps to the current month. When already viewing the current month, it selects today's date.









Copy to clipboard

```
<flux:calendar with-today />
```



## [Selectable header](#selectable-header)

Enable quick navigation by making the month and year in the header selectable.









Copy to clipboard

```
<flux:calendar selectable-header />
```



## [Fixed weeks](#fixed-weeks)

Display a consistent number of weeks in every month. Prevents layout shifts when navigating between months with different numbers of weeks.









Copy to clipboard

```
<flux:calendar fixed-weeks />
```



## [Start day](#start-day)

By default, the first day of the week will be automatically set based on the user's locale. You can override this by setting the start-day attribute to any day of the week.









Copy to clipboard

```
<flux:calendar start-day="1" />
```



## [Open to](#open-to)

Set the date that the calendar will open to, if there is no selected date.









Copy to clipboard

```
<flux:calendar open-to="2027-04-01" />
```

If you want the calendar to always use the open-to date, you can add the force-open-to attribute.







Copy to clipboard

```
<flux:calendar open-to="2027-04-01" force-open-to />
```



## [Week numbers](#week-numbers)

Display the week number for each week.









Copy to clipboard

```
<flux:calendar week-numbers />
```



## [Localization](#localization)

By default, the calendar will use the browser's locale (e.g. navigator.language).

You can override this behavior by setting the locale attribute to any valid locale string (e.g. fr for French, en-US for English, etc.):









Copy to clipboard

```
<flux:calendar locale="ja-JP" />
```



## The DateRange object

Flux provides a specialized Flux\DateRange object that extends the native CarbonPeriod class. This object provides a number of convenience methods to easily create and manage date ranges.

First, it's worth noting that most of the time, you will want to use wire:model.live to bind the range property to a DateRange object. This will automatically update the range property whenever the user selects a date range:

Copy to clipboard

```
<flux:calendar wire:model.live="range" />
```

Now, in your component, you can type hint the range property as a DateRange object:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    public DateRange $range;}
```



## Instantiation

You can initialize a DateRange object by passing a start and end date to the DateRange constructor from something like the mount method:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    public DateRange $range;    public function mount() {        $this->range = new DateRange(now(), now()->addDays(7));    }}
```



## Persisting to the session

You can persist a DateRange object in the user's session by using the #[Session] attribute:

Copy to clipboard

```
<?phpuse Livewire\Attributes\Session;use Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    #[Session]    public DateRange $range;}
```



## Using with Eloquent

You can use the DateRange object with Eloquent's whereBetween() method to filter queries by date range:

Copy to clipboard

```
<?phpuse Livewire\Attributes\Computed;use Livewire\Component;use App\Models\Order;use Flux\DateRange;class Dashboard extends Component {    public ?DateRange $range;    #[Computed]    public function orders() {        return $this->range            ? Order::whereBetween('created_at', $this->range)->get()            : Order::all();    }}
```



## Available methods

The DateRange object extends the native CarbonPeriod class, so it inherits all of its methods. Here are a few examples:

Copy to clipboard

```
$range = new Flux\DateRange(    now()->subDays(1),    now()->addDays(1),);// Get the start and end dates as Carbon instances...$start = $range->start();$end = $range->end();// Check if the range contains a date...$range->contains(now());// Get the number of days in the range...$range->length();// Loop over the range by day...foreach ($range as $date) {    // $date is a Carbon instance...}// Get the range as an array of Carbon instances representing each day in the range...$range->toArray();
```

You can also use it anywhere Eloquent utilities expect a CarbonPeriod instance:

Copy to clipboard

```
$orders = Order::whereBetween('created_at', $range)->get();
```

## Reference



### [flux:calendar](#fluxcalendar)

| Prop | Description |
| --- | --- |
| wire:model | Binds the calendar to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| value | Selected date(s). Format depends on mode: single date (Y-m-d), multiple dates (comma-separated Y-m-d), or range (Y-m-d/Y-m-d). |
| mode | Selection mode. Options: single (default), multiple, range. |
| min | Earliest selectable date. Can be a date string or "today". |
| max | Latest selectable date. Can be a date string or "today". |
| size | Calendar size. Options: base (default), xs, sm, lg, xl, 2xl. |
| start-day | The day of the week to start the calendar on. Options: 0 (Sunday) to 6 (Saturday). Default: based on the user's locale. |
| months | Number of months to display. Default: 1 for single/multiple modes, 2 for range mode. |
| min-range | Minimum number of days that can be selected in range mode. |
| max-range | Maximum number of days that can be selected in range mode. |
| open-to | Set the date that the calendar will open to, if there is no selected date. |
| force-open-to | If true, forces the calendar to open to the open-to date regardless of the selected date. Default: false. |
| navigation | If false, hides month navigation controls. Default: true. |
| static | If true, makes the calendar non-interactive (display-only). Default: false. |
| multiple | If true, enables multiple date selection mode. Default: false. |
| week-numbers | If true, displays week numbers in the calendar. Default: false. |
| selectable-header | If true, displays month and year dropdowns for quick navigation. Default: false. |
| with-today | If true, displays a button to quickly navigate to today's date. Default: false. |
| with-inputs | If true, displays date inputs at the top of the calendar for manual date entry. Default: false. |
| locale | Set the locale for the calendar. Examples: fr, en-US, ja-JP. |

| Attribute | Description |
| --- | --- |
| data-flux-calendar | Applied to the root element for styling and identification. |



### [DateRange Object](#daterange-object)

A specialized object for handling date ranges when using `mode="range"`.

| Method | Description |
| --- | --- |
| $range->start() | Get the start date as a Carbon instance. |
| $range->end() | Get the end date as a Carbon instance. |
| $range->days() | Get the number of days in the range. |
| $range->contains(date) | Check if the range contains a specific date. |
| $range->length() | Get the length of the range in days. |
| $range->toArray() | Get the range as an array with start and end keys. |
| $range->preset() | Get the current preset as a DateRangePreset enum value, if any. |

| Static Method | Description |
| --- | --- |
| DateRange::today() | Create a DateRange for today. |
| DateRange::yesterday() | Create a DateRange for yesterday. |
| DateRange::thisWeek() | Create a DateRange for the current week. |
| DateRange::lastWeek() | Create a DateRange for the previous week. |
| DateRange::last7Days() | Create a DateRange for the last 7 days. |
| DateRange::thisMonth() | Create a DateRange for the current month. |
| DateRange::lastMonth() | Create a DateRange for the previous month. |
| DateRange::thisYear() | Create a DateRange for the current year. |
| DateRange::lastYear() | Create a DateRange for the previous year. |
| DateRange::yearToDate() | Create a DateRange from January 1st to today. |
| DateRange::tomorrow() | Create a DateRange for tomorrow. |
| DateRange::nextWeek() | Create a DateRange for next week. |
| DateRange::next7Days() | Create a DateRange for the next 7 days. |
| DateRange::next30Days() | Create a DateRange for the next 30 days. |
| DateRange::nextMonth() | Create a DateRange for next month. |
| DateRange::nextQuarter() | Create a DateRange for next quarter. |
| DateRange::nextYear() | Create a DateRange for next year. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0017_Callout

# Callout

Highlight important information or guide users toward key actions.





Upcoming maintenance

Our servers will be undergoing scheduled maintenance this Sunday from 2 AM - 5 AM UTC. Some services may be temporarily unavailable. [Learn more](#)





Copy to clipboard

```
<flux:callout icon="clock">    <flux:callout.heading>Upcoming maintenance</flux:callout.heading>    <flux:callout.text>        Our servers will be undergoing scheduled maintenance this Sunday from 2 AM - 5 AM UTC. Some services may be temporarily unavailable.        <flux:callout.link href="#">Learn more</flux:callout.link>    </flux:callout.text></flux:callout>
```



## [Icon inside heading](#icon-inside-heading)

For a more compact layout, place the icon inside the heading by adding the icon prop to flux:callout.heading instead of the root flux:callout component.





Policy update

We've updated our Terms of Service and Privacy Policy. Please review them to stay informed.





Copy to clipboard

```
<flux:callout>    <flux:callout.heading icon="newspaper">Policy update</flux:callout.heading>    <flux:callout.text>We've updated our Terms of Service and Privacy Policy. Please review them to stay informed.</flux:callout.text></flux:callout>
```



## [With actions](#with-actions)

Add action buttons to your callout to provide users with clear next steps.





Subscription expiring soon

Your current plan will expire in 3 days. Renew now to avoid service interruption and continue accessing premium features.

Renew now

[View plans](#)





Copy to clipboard

```
<flux:callout icon="clock">    <flux:callout.heading>Subscription expiring soon</flux:callout.heading>    <flux:callout.text>Your current plan will expire in 3 days. Renew now to avoid service interruption and continue accessing premium features.</flux:callout.text>    <x-slot name="actions">        <flux:button>Renew now</flux:button>        <flux:button variant="ghost" href="/pricing">View plans</flux:button>    </x-slot></flux:callout>
```



## [Inline actions](#inline-actions)

Use the inline prop to display actions inline with the callout.





Your package is delayed

Track order ->

Reschedule

Payment issue detected

Your last payment attempt failed. Update your billing details to prevent service interruption.

Update billing





Copy to clipboard

```
<flux:callout icon="cube" variant="secondary" inline>    <flux:callout.heading>Your package is delayed</flux:callout.heading>    <x-slot name="actions">        <flux:button>Track order -></flux:button>        <flux:button variant="ghost">Reschedule</flux:button>    </x-slot></flux:callout><flux:callout icon="exclamation-triangle" variant="secondary" inline>    <flux:callout.heading>Payment issue detected</flux:callout.heading>    <flux:callout.text>Your last payment attempt failed. Update your billing details to prevent service interruption.</flux:callout.text>    <x-slot name="actions">        <flux:button>Update billing</flux:button>    </x-slot></flux:callout>
```



## [Dismissible](#dismissible)

Add a close button, using the controls slot, to allow users to dismiss callouts they no longer care to see.

Callouts do not include built-in dismiss functionality. This is intentional—dismissal behavior depends on your app’s needs. You might want to remove it from the DOM on the frontend or persist the dismissal in a backend database.





Upcoming meeting

10:00 AM

Unusual login attempt

We detected a login from a new device in New York, USA. If this was you, no action is needed. If not, secure your account immediately.

Change password

Review activity





Copy to clipboard

```
<flux:callout icon="bell" variant="secondary" inline x-data="{ visible: true }" x-show="visible">    <flux:callout.heading class="flex gap-2 @max-md:flex-col items-start">Upcoming meeting <flux:text>10:00 AM</flux:text></flux:callout.heading>    <x-slot name="controls">        <flux:button icon="x-mark" variant="ghost" x-on:click="visible = false" />    </x-slot></flux:callout><!-- Wrapping divs to add smooth exist transition... --><div x-data="{ visible: true }" x-show="visible" x-collapse>    <div x-show="visible" x-transition>        <flux:callout icon="finger-print" variant="secondary">            <flux:callout.heading>Unusual login attempt</flux:callout.heading>            <flux:callout.text>We detected a login from a new device in <span class="font-medium text-zinc-800 dark:text-white">New York, USA</span>. If this was you, no action is needed. If not, secure your account immediately.</flux:callout.text>            <x-slot name="actions">                <flux:button>Change password</flux:button>                <flux:button variant="ghost">Review activity</flux:button>            </x-slot>            <x-slot name="controls">                <flux:button icon="x-mark" variant="ghost" x-on:click="visible = false" />            </x-slot>        </flux:callout>    </div></div>
```



## [Variants](#variants)

Use predefined variants to convey a specific tone or level of urgency.





Your account has been successfully created.

Your account is verified and ready to use.

Please verify your account to unlock all features.

Something went wrong. Try again or contact support.





Copy to clipboard

```
<flux:callout variant="secondary" icon="information-circle" heading="Your account has been successfully created." /><flux:callout variant="success" icon="check-circle" heading="Your account is verified and ready to use." /><flux:callout variant="warning" icon="exclamation-circle" heading="Please verify your account to unlock all features." /><flux:callout variant="danger" icon="x-circle" heading="Something went wrong. Try again or contact support." />
```



## [Colors](#colors)

Use the color prop to change the color of the callout to match your use case.







You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message

You've received a new message.

View message





Copy to clipboard

```
<flux:callout color="zinc" ... /><flux:callout color="red" ... /><flux:callout color="orange" ... /><flux:callout color="amber" ... /><flux:callout color="yellow" ... /><flux:callout color="lime" ... /><flux:callout color="green" ... /><flux:callout color="emerald" ... /><flux:callout color="teal" ... /><flux:callout color="cyan" ... /><flux:callout color="sky" ... /><flux:callout color="blue" ... /><flux:callout color="indigo" ... /><flux:callout color="violet" ... /><flux:callout color="purple" ... /><flux:callout color="fuchsia" ... /><flux:callout color="pink" ... /><flux:callout color="rose" ... />
```



## [Custom icon](#custom-icon)

Use a custom icon to match your brand or specific use case using the icon slot.





Notification system updated

We've improved our notification system to deliver alerts faster and more reliably.





Copy to clipboard

```
<flux:callout>    <x-slot name="icon">        <!-- Custom icon: https://lucide.dev/icons/alarm-clock -->        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-alarm-clock"><circle cx="12" cy="13" r="8"/><path d="M12 9v4l2 2"/><path d="M5 3 2 6"/><path d="m22 6-3-3"/><path d="M6.38 18.7 4 21"/><path d="M17.64 18.67 20 21"/></svg>    </x-slot>    <flux:callout.heading>Notification system updated</flux:callout.heading>    <flux:callout.text>        <p>We've improved our notification system to deliver alerts faster and more reliably.</p>    </flux:callout.text></flux:callout>
```

## Examples



### [Feature spotlight](#feature-spotlight)

Call attention to a new feature or update.





Have a question?

Try our new AI assistant, Jeffrey. Let him handle tasks and answer questions for you. [Learn more](#)





Copy to clipboard

```
<flux:callout icon="sparkles" color="purple">    <flux:callout.heading>Have a question?</flux:callout.heading>    <flux:callout.text>        Try our new AI assistant, Jeffrey. Let him handle tasks and answer questions for you.        <flux:callout.link href="#">Learn more</flux:callout.link>    </flux:callout.text></flux:callout>
```



### [Premium upsell](#premium-upsell)

Encourage users to upgrade.





API access is restricted

Get access to all of our premium features and benefits.

Upgrade to Pro ->





Copy to clipboard

```
<flux:callout icon="shield-check" color="blue" inline>    <flux:callout.heading>API access is restricted</flux:callout.heading>    <flux:callout.text>Get access to all of our premium features and benefits.</flux:callout.text>    <x-slot name="actions" class="@md:h-full m-0!">        <flux:button>Upgrade to Pro -></flux:button>    </x-slot></flux:callout>
```



### [Upgrade offer](#upgrade-offer)

Compact reminders to take advantage of special offers.





You could save $4,900/yr on annual billing.

Switch now ->





Copy to clipboard

```
<flux:callout icon="banknotes" color="lime" inline>    <flux:callout.heading>You could save $4,900/yr on annual billing.</flux:callout.heading>    <x-slot name="actions">        <flux:button>Switch now -></flux:button>    </x-slot></flux:callout>
```



### [Engagement prompt](#engagement-prompt)

Nudge users toward an action or feature.





Team collaboration

Available with Pro

Share projects, manage permissions, and collaborate in real time with your team. Upgrade now to access these features.

Invite member

Manage team





Copy to clipboard

```
<flux:callout variant="secondary" icon="user-group">    <flux:callout.heading>        Team collaboration <flux:badge color="purple" size="sm" inset="top bottom">Available with Pro</flux:badge>    </flux:callout.heading>    <flux:callout.text>        <p>Share projects, manage permissions, and collaborate in real time with your team. Upgrade now to access these features.</p>    </flux:callout.text>    <x-slot name="actions">        <flux:button>Invite member</flux:button>        <flux:button variant="ghost" class="@max-md:hidden">Manage team</flux:button>    </x-slot></flux:callout>
```

## Related components

[Toast Display temporary notifications with a toast](/components/toast) [Card Display content in a card component](/components/card)

## Reference



### [flux:callout](#fluxcallout)

| Prop | Description |
| --- | --- |
| icon | Name of the icon displayed next to the heading (e.g., clock). [Explore icons](/components/icon) |
| icon:variant | Variant of the icon displayed next to the heading (e.g., outline). [Explore icon variants](/components/icon#variants) |
| variant | Options: secondary, success, warning, danger. Default: secondary |
| color | Custom color (e.g., red, blue). [View available Tailwind colors ->](https://tailwindcss.com/docs/colors) |
| inline | If true, actions appear inline. Default: false. |
| heading | Shorthand for flux:callout.heading. |
| text | Shorthand for flux:callout.text. |

| Slot | Description |
| --- | --- |
| icon | Custom icon displayed next to the heading. |
| actions | Buttons or links inside the callout (flux:callout.button). |
| controls | Extra UI elements placed at the top right of the callout (e.g., close button). |



### [flux:callout.heading](#fluxcalloutheading)

| Prop | Description |
| --- | --- |
| icon | Moves the icon inside the heading instead of the callout root. |
| icon:variant | Variant of the icon displayed next to the heading (e.g., outline). [Explore icon variants](/components/icon#variants) |

| Slot | Description |
| --- | --- |
| icon | Custom icon displayed next to the heading. |



### [flux:callout.text](#fluxcallouttext)

| Slot | Description |
| --- | --- |
| default | Text content inside the callout. |



### [flux:callout.link](#fluxcalloutlink)

| Prop | Description |
| --- | --- |
| href | The URL the link points to. |
| external | If true, the link opens in a new tab. Default: false. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0018_Card

# Card

A container for related content, such as a form, alert, or data list.





Log in to your account

Welcome back!

Email

Password [Forgot password?](#)

Log in

Sign up for a new account





Copy to clipboard

```
<flux:card class="space-y-6">    <div>        <flux:heading size="lg">Log in to your account</flux:heading>        <flux:text class="mt-2">Welcome back!</flux:text>    </div>    <div class="space-y-6">        <flux:input label="Email" type="email" placeholder="Your email address" />        <flux:field>            <div class="mb-3 flex justify-between">                <flux:label>Password</flux:label>                <flux:link href="#" variant="subtle" class="text-sm">Forgot password?</flux:link>            </div>            <flux:input type="password" placeholder="Your password" />            <flux:error name="password" />        </flux:field>    </div>    <div class="space-y-2">        <flux:button variant="primary" class="w-full">Log in</flux:button>        <flux:button variant="ghost" class="w-full">Sign up for a new account</flux:button>    </div></flux:card>
```



## [Small card](#small-card)

Use the small card variant for compact content like notifications, alerts, or brief summaries.





[Latest on our blog Stay up to date with our latest insights, tutorials, and product updates.](#)





Copy to clipboard

```
<a href="#" aria-label="Latest on our blog">    <flux:card size="sm" class="hover:bg-zinc-50 dark:hover:bg-zinc-700">        <flux:heading class="flex items-center gap-2">Latest on our blog <flux:icon name="arrow-up-right" class="ml-auto text-zinc-400" variant="micro" /></flux:heading>        <flux:text class="mt-2">Stay up to date with our latest insights, tutorials, and product updates.</flux:text>    </flux:card></a>
```



## [Header actions](#header-actions)

Use the [button component](/components/button) to add actions to the header.





Are you sure?

Your post will be deleted permanently.  
This action cannot be undone.

Undo

Delete





Copy to clipboard

```
<flux:card class="space-y-6">    <div class="flex">        <div class="flex-1">            <flux:heading size="lg">Are you sure?</flux:heading>            <flux:text class="mt-2">                Your post will be deleted permanently.<br>                This action cannot be undone.            </flux:text>        </div>        <div class="-mx-2 -mt-2">            <flux:button variant="ghost" size="sm" icon="x-mark" inset="top right bottom" />        </div>    </div>    <div class="flex gap-4">        <flux:spacer />        <flux:button variant="ghost">Undo</flux:button>        <flux:button variant="danger">Delete</flux:button>    </div></flux:card>
```



## [Simple card](#simple-card)

Let's be honest, a card is just a div with a border and some padding.





Are you sure?

Your post will be deleted permanently.  
This action cannot be undone.

Delete





Copy to clipboard

```
<flux:card>    <flux:heading size="lg">Are you sure?</flux:heading>    <flux:text class="mt-2 mb-4">        Your post will be deleted permanently.<br>        This action cannot be undone.    </flux:text>    <flux:button variant="danger">Delete</flux:button></flux:card>
```

## Related components

[Heading Create hierarchical section headings for content](/components/heading) [Text Format paragraphs and textual content with consistent styling](/components/text)

## Reference



### [flux:card](#fluxcard)

| Slot | Description |
| --- | --- |
| default | Content to display within the card. Can include headings, text, forms, buttons, and other components. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the card. Common uses: space-y-6 for spacing between child elements, max-w-md for width control, p-0 to remove padding. |

| Attribute | Description |
| --- | --- |
| data-flux-card | Applied to the root element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)  




# 0019_Chart



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Chart

Flux's Chart component is a lightweight, zero-dependency tool for building charts in your Livewire applications. It is designed to be simple but extremely flexible, so that you can assemble and style your charts exactly as you need them.









Copy to clipboard

```
<flux:chart wire:model="data" class="aspect-3/1">    <flux:chart.svg>        <flux:chart.line field="visitors" class="text-pink-500 dark:text-pink-400" />        <flux:chart.axis axis="x" field="date">            <flux:chart.axis.line />            <flux:chart.axis.tick />        </flux:chart.axis>        <flux:chart.axis axis="y">            <flux:chart.axis.grid />            <flux:chart.axis.tick />        </flux:chart.axis>        <flux:chart.cursor />    </flux:chart.svg>    <flux:chart.tooltip>        <flux:chart.tooltip.heading field="date" :format="['year' => 'numeric', 'month' => 'numeric', 'day' => 'numeric']" />        <flux:chart.tooltip.value field="visitors" label="Visitors" />    </flux:chart.tooltip></flux:chart>
```



## Data structure

Flux charts expect a structured array of data, typically provided via wire:model or passed as a value prop. Each data point should be an associative array with named fields:

Copy to clipboard

```
<?phpuse Livewire\Component;class Dashboard extends Component{    public array $data = [        ['date' => '2026-03-03', 'visitors' => 267],        ['date' => '2026-03-02', 'visitors' => 259],        ['date' => '2026-03-01', 'visitors' => 269],        // ...    ];}
```

If you've stored this data as a public property, you can use wire:model to bind the data to the chart:

Copy to clipboard

```
<flux:chart wire:model="data" />
```

Otherwise, you can pass data in any form directly into the :value prop:

Copy to clipboard

```
<flux:chart :value="$this->data" />
```

For things like simple line charts with no axes, you can pass a single array of values as well:

Copy to clipboard

```
<flux:chart :value="[1, 2, 3, 4, 5]" />
```



## Examples



## Line chart

To create a line chart, you can include the <flux:chart.line> component in the <flux:chart.svg> component:





Memory usage





Copy to clipboard

```
<flux:chart wire:model="data" class="aspect-[3/1]">    <flux:chart.svg>        <flux:chart.line field="memory" class="text-pink-500" />        <flux:chart.point field="memory" class="text-pink-400" />        <flux:chart.axis axis="x" field="date">            <flux:chart.axis.tick />            <flux:chart.axis.line />        </flux:chart.axis>        <flux:chart.axis axis="y" tick-values="[0, 128, 256, 384, 512]" :format="['style' => 'unit', 'unit' => 'megabyte']">            <flux:chart.axis.grid />            <flux:chart.axis.tick />        </flux:chart.axis>    </flux:chart.svg></flux:chart>
```

As you can see above, you can also render circular points on top of the line using the <flux:chart.point> component.



## Area chart

Similar to a line chart but with a filled area beneath the line. Great for showing cumulative values or emphasizing volume.





Stock price





Copy to clipboard

```
<flux:chart wire:model="data" class="aspect-3/1">    <flux:chart.svg>        <flux:chart.line field="stock" class="text-blue-500 dark:text-blue-400" curve="none" />        <flux:chart.area field="stock" class="text-blue-200/50 dark:text-blue-400/30" curve="none" />        <flux:chart.axis axis="y" position="right" tick-prefix="$" :format="[            'notation' => 'compact',            'compactDisplay' => 'short',            'maximumFractionDigits' => 1,        ]">            <flux:chart.axis.grid />            <flux:chart.axis.tick />        </flux:chart.axis>        <flux:chart.axis axis="x" field="date">            <flux:chart.axis.tick />            <flux:chart.axis.line />        </flux:chart.axis>    </flux:chart.svg></flux:chart>
```



## Multiple lines

You can plot multiple lines in the same chart by including multiple <flux:chart.line> components. This helps compare different data series against each other.







Instagram



Twitter



Facebook





Copy to clipboard

```
<flux:chart wire:model="data">    <flux:chart.viewport class="min-h-[20rem]" >        <flux:chart.svg>            <flux:chart.line field="twitter" class="text-blue-500" curve="none" />            <flux:chart.point field="twitter" class="text-blue-500" r="6" stroke-width="3" />            <flux:chart.line field="facebook" class="text-red-500" curve="none" />            <flux:chart.point field="facebook" class="text-red-500" r="6" stroke-width="3" />            <flux:chart.line field="instagram" class="text-green-500" curve="none" />            <flux:chart.point field="instagram" class="text-green-500" r="6" stroke-width="3" />            <flux:chart.axis axis="x" field="date">                <flux:chart.axis.tick />                <flux:chart.axis.line />            </flux:chart.axis>            <flux:chart.axis axis="y" tick-start="0" tick-end="1" :format="[                'style' => 'percent',                'minimumFractionDigits' => 0,                'maximumFractionDigits' => 0,            ]">                <flux:chart.axis.grid />                <flux:chart.axis.tick />            </flux:chart.axis>        </flux:chart.svg>    </flux:chart.viewport>    <div class="flex justify-center gap-4 pt-4">        <flux:chart.legend label="Instagram">            <flux:chart.legend.indicator class="bg-green-400" />        </flux:chart.legend>        <flux:chart.legend label="Twitter">            <flux:chart.legend.indicator class="bg-blue-400" />        </flux:chart.legend>        <flux:chart.legend label="Facebook">            <flux:chart.legend.indicator class="bg-red-400" />        </flux:chart.legend>    </div></flux:chart>
```

You might have noticed that the above example includes a <flux:chart.viewport> component. This is used to constrain the chart SVG within the chart component so that you can render siblings like legends or summaries above or below it.



## Bar chart

To create a bar chart, you can include the <flux:chart.bar> component in the <flux:chart.svg> component:





Revenue





Copy to clipboard

```
<flux:chart wire:model="data" class="aspect-[3/1]">    <flux:chart.svg>        <flux:chart.bar field="revenue" class="text-blue-500" radius="0" width="85%" />        <flux:chart.axis axis="x" field="date" tick-count="10">            <flux:chart.axis.tick />            <flux:chart.axis.line />        </flux:chart.axis>        <flux:chart.axis axis="y" :format="['useGrouping' => true]" tick-prefix="$">            <flux:chart.axis.grid />            <flux:chart.axis.tick />        </flux:chart.axis>        <flux:chart.cursor type="area" />    </flux:chart.svg>    <flux:chart.tooltip>        <flux:chart.tooltip.heading field="date" />        <flux:chart.tooltip.value field="revenue" label="Revenue" :format="['useGrouping' => true]" prefix="$" />    </flux:chart.tooltip></flux:chart>
```





Support tickets





Copy to clipboard

```
<flux:chart wire:model="data" class="aspect-[3/1]">    <flux:chart.svg>        <flux:chart.bar field="tickets" class="text-blue-300 dark:text-blue-700" />        <flux:chart.axis axis="x" field="month">            <flux:chart.axis.tick />        </flux:chart.axis>        <flux:chart.axis axis="y">            <flux:chart.axis.grid />            <flux:chart.axis.tick />        </flux:chart.axis>    </flux:chart.svg>    <flux:chart.tooltip>        <flux:chart.tooltip.value field="tickets" label="Tickets" />    </flux:chart.tooltip></flux:chart>
```



## Grouped bar chart

To create a grouped bar chart, you can wrap multiple <flux:chart.bar> components inside a single <flux:chart.group> component:





Browser usage



Chrome





Firefox





Safari





Copy to clipboard

```
<flux:chart wire:model="data">    <flux:chart.viewport class="aspect-[3/1]">        <flux:chart.svg>            <flux:chart.group>                <flux:chart.bar field="chrome" class="text-blue-600" />                <flux:chart.bar field="firefox" class="text-blue-500" />                <flux:chart.bar field="safari" class="text-blue-300" />            </flux:chart.group>            <flux:chart.axis axis="x" field="year">                <flux:chart.axis.tick />                <flux:chart.axis.line />            </flux:chart.axis>            <flux:chart.axis axis="y">                <flux:chart.axis.grid />                <flux:chart.axis.tick />            </flux:chart.axis>        </flux:chart.svg>    </flux:chart.viewport>    <div class="flex justify-center gap-4 pt-4">        <flux:chart.legend label="Chrome">            <flux:chart.legend.indicator class="bg-blue-600" />        </flux:chart.legend>        <flux:chart.legend label="Firefox">            <flux:chart.legend.indicator class="bg-blue-500" />        </flux:chart.legend>        <flux:chart.legend label="Safari">            <flux:chart.legend.indicator class="bg-blue-300" />        </flux:chart.legend>    </div></flux:chart>
```



## Stacked bar chart

To create a stacked bar chart, you can wrap multiple <flux:chart.bar> components inside a single <flux:chart.stack> component:





Number of orders



Online





Retail





Wholesale





Copy to clipboard

```
<flux:chart wire:model="data">    <flux:chart.viewport class="aspect-[3/1]">        <flux:chart.svg>            <flux:chart.stack width="65%">                <flux:chart.bar field="online" class="text-blue-600" />                <flux:chart.bar field="retail" class="text-blue-400" />                <flux:chart.bar field="wholesale" class="text-blue-300" radius="4 0" />            </flux:chart.stack>            <flux:chart.axis axis="x" field="category">                <flux:chart.axis.tick />                <flux:chart.axis.line />            </flux:chart.axis>            <flux:chart.axis axis="y">                <flux:chart.axis.grid />                <flux:chart.axis.tick />            </flux:chart.axis>        </flux:chart.svg>    </flux:chart.viewport>    <div class="flex justify-center gap-4 pt-4">        <flux:chart.legend label="Online">            <flux:chart.legend.indicator class="bg-blue-600" />        </flux:chart.legend>        <flux:chart.legend label="Retail">            <flux:chart.legend.indicator class="bg-blue-400" />        </flux:chart.legend>        <flux:chart.legend label="Wholesale">            <flux:chart.legend.indicator class="bg-blue-300" />        </flux:chart.legend>    </div></flux:chart>
```



## Live summary

Flux charts support live summaries, which are updated as the user hovers over the chart. To enable this feature, you can include the <flux:chart.summary> component in the <flux:chart> component:









Copy to clipboard

```
<flux:card>    <flux:chart class="grid gap-6" wire:model="data">        <flux:chart.summary class="flex gap-12">            <div>                <flux:text>Today</flux:text>                <flux:heading size="xl" class="mt-2 tabular-nums">                    <flux:chart.summary.value field="sales" :format="['style' => 'currency', 'currency' => 'USD']" />                </flux:heading>                <flux:text class="mt-2 tabular-nums">                    <flux:chart.summary.value field="date" :format="['hour' => 'numeric', 'minute' => 'numeric', 'hour12' => true]" />                </flux:text>            </div>            <div>                <flux:text>Yesterday</flux:text>                <flux:heading size="lg" class="mt-2 tabular-nums">                    <flux:chart.summary.value field="yesterday" :format="['style' => 'currency', 'currency' => 'USD']" />                </flux:heading>            </div>        </flux:chart.summary>        <flux:chart.viewport class="aspect-[3/1]">            <flux:chart.svg>                <flux:chart.line field="yesterday" class="text-zinc-300 dark:text-white/40" stroke-dasharray="4 4" curve="none" />                <flux:chart.line field="sales" class="text-sky-500 dark:text-sky-400" curve="none" />                <flux:chart.axis axis="x" field="date">                    <flux:chart.axis.grid />                    <flux:chart.axis.tick />                    <flux:chart.axis.line />                </flux:chart.axis>                <flux:chart.axis axis="y">                    <flux:chart.axis.tick />                </flux:chart.axis>                <flux:chart.cursor />            </flux:chart.svg>        </flux:chart.viewport>    </flux:chart></flux:card>
```



## Sparkline

A compact, single-line chart used in tables or dashboards for quick visual insights. Ideal for stock prices, memory usage, or other small-scale trends.





| Stock | Price | Change | Trend |
| --- | --- | --- | --- |
| AAPL | $193.45 | +2.4% |  |
| MSFT | $338.12 | +1.8% |  |
| TSLA | $242.68 | -3.2% |  |
| GOOGL | $129.87 | +0.9% |  |





Copy to clipboard

```
<flux:chart :value="[15, 18, 16, 19, 22, 25, 28, 25, 29, 28, 32, 35]" class="w-[5rem] aspect-[3/1]">    <flux:chart.svg gutter="0">        <flux:chart.line class="text-green-500 dark:text-green-400" />    </flux:chart.svg></flux:chart>
```

You might have noticed the gutter attribute on the <flux:chart.svg> component. This is because by default, the chart will be rendered with a padding of 8px on all sides. This is to prevent overflowing contents of the chart (like tick labels or stroke lines) from being cut off at the edges of the container.

For simple charts like a sparkline, you don't want that extra padding, so you can set the gutter to 0 to remove it.

[Read more about the gutter prop ->](#chart-padding)



## Dashboard stat

A small card displaying a key metric with an embedded chart in the background. Useful for KPIs like revenue, active users, or system health.





Revenue

$12,345





Copy to clipboard

```
<flux:card class="overflow-hidden min-w-[12rem]">    <flux:text>Revenue</flux:text>    <flux:heading size="xl" class="mt-2 tabular-nums">$12,345</flux:heading>    <flux:chart class="-mx-8 -mb-8 h-[3rem]" :value="[10, 12, 11, 13, 15, 14, 16, 18, 17, 19, 21, 20]">        <flux:chart.svg gutter="0">            <flux:chart.line class="text-sky-200 dark:text-sky-400" />            <flux:chart.area class="text-sky-100 dark:text-sky-400/30" />        </flux:chart.svg>    </flux:chart></flux:card>
```



## Chart padding

By default, the chart will be rendered with a padding of 8px on all sides. This is to prevent overflowing contents of the chart (like tick labels or stroke lines) from being cut off at the edges of the container.

You can control this by setting the gutter attribute on the <flux:chart.svg> component:

Here's an example of adding the following padding to the chart:

Copy to clipboard

```
<flux:chart>    <flux:chart.svg gutter="12 0 12 8">        <!-- ... -->    </flux:chart.svg></flux:chart>
```

The gutter attribute accepts between one and four values, which correspond to the top, right, bottom, and left padding respectively. Similar to the padding property shorthand in CSS.

The example above will result in the following padding:

- **Top:** 12px
- **Right:** 0px
- **Bottom:** 12px
- **Left:** 8px


## Axis scale

You can configure the scale of an axis and its ticks by setting the scale attribute on the <flux:chart.axis> component:

Copy to clipboard

```
<flux:chart.axis axis="y" scale="linear">    <!-- ... --></flux:chart.axis>
```

There are three available types of scales:

- categorical: For categorical data like names or categories.
- linear: For numeric data like stock prices or temperatures.
- time: For date and time data


The "y" axis is linear by default, but you can change it to a time axis by setting the scale attribute to time.

The "x" axis will automatically use a time scale if the data is date or time values. Otherwise, it will use a categorical scale.



## Axis lines

By default, axes do not include a visible baseline. You can add an axis line using <flux:chart.axis.line> inside the corresponding axis:

Copy to clipboard

```
<flux:chart.svg>    <!-- ... -->    <flux:chart.axis axis="x">        <!-- Horizontal "X" axis line: -->        <flux:chart.axis.line />    </flux:chart.axis>    <flux:chart.axis axis="y">        <!-- Vertical "Y" axis line: -->        <flux:chart.axis.line />    </flux:chart.axis></flux:chart.svg>
```

**Styling axis lines**

Because the axis line is rendered as a <line> element, you can style it using any of the SVG attributes that are available for the <line> element.

Copy to clipboard

```
<!-- A dark gray axis line that is 2px wide and has a gray color: --><flux:chart.axis.line class="text-zinc-800" stroke-width="2" />
```



## Zero line

The zero line is the line that represents the zero value on the axis. It will only be visible if the axis includes a negative value.

Copy to clipboard

```
<flux:chart.svg>    <!-- ... -->    <!-- Zero line: -->    <flux:chart.zero-line /></flux:chart.svg>
```

**Styling the zero line**

Because the zero line is rendered as a <line> element, you can style it using any of the SVG attributes that are available for the <line> element.

Copy to clipboard

```
<!-- A dark gray zero line that is 2px wide and has a gray color: --><flux:chart.zero-line class="text-zinc-800" stroke-width="2" />
```



## Grid lines

You can render horizontal and vertical grid lines by adding the <flux:chart.axis.grid> component to the appropriate axis:

Copy to clipboard

```
<flux:chart.svg>    <!-- ... -->    <flux:chart.axis axis="x">        <!-- Vertical grid lines: -->        <flux:chart.axis.grid />    </flux:chart.axis>    <flux:chart.axis axis="y">        <!-- Horizontal grid lines: -->        <flux:chart.axis.grid />    </flux:chart.axis></flux:chart.svg>
```

**Styling grid lines**

Because the grid lines are rendered as a <line> element, you can style them using any of the SVG attributes that are available for the <line> element.

Copy to clipboard

```
<!-- A dashed grid line that is 2px wide and has a gray color: --><flux:chart.axis.grid class="text-zinc-200/50" stroke-width="2" stroke-dasharray="4,4" />
```



## Ticks

You can render tick mark lines and labels by adding the <flux:chart.axis.mark> and/or <flux:chart.axis.tick> components to the appropriate axis:

Copy to clipboard

```
<flux:chart.svg>    <!-- ... -->    <flux:chart.axis axis="x">        <!-- X axis tick mark lines: -->        <flux:chart.axis.mark />        <!-- X axis tick labels: -->        <flux:chart.axis.tick />    </flux:chart.axis>    <flux:chart.axis axis="y">        <!-- Y axis tick mark lines: -->        <flux:chart.axis.mark />        <!-- Y axis tick labels: -->        <flux:chart.axis.tick />    </flux:chart.axis></flux:chart.svg>
```

**Styling tick mark lines**

The tick mark component is a simple wrapper around the <line> SVG element. You can customize the length, width, and color of the tick mark lines using plain CSS and SVG attributes:

Copy to clipboard

```
<!-- A tick mark line that is 10px long, 2px wide, and has a gray color: --><flux:chart.axis.mark class="text-zinc-300" stroke-width="2" y1="0" y2="10" />
```

**Styling tick labels**

The <flux:chart.axis.tick> component is a simple wrapper around the <text> SVG element. You can customize the font size, color, and position of the tick labels using plain CSS and SVG attributes:

Copy to clipboard

```
<!-- A tick label that is 12px, has a blue color, is center aligned, and is 2.5rem from the axis line: --><flux:chart.axis.tick class="text-xs text-blue-500" text-anchor="middle" dy="2.5rem"  />
```



## Tick frequency

You can influence the number of ticks on an axis by setting the tick-count attribute:

**Setting the tick count**

Copy to clipboard

```
<flux:chart.axis axis="y" tick-count="5">    <!-- ... --></flux:chart.axis>
```

Note that the tick-count attribute is only a target number, and the actual number of ticks may vary based on the range of values on the axis.

**Setting the tick start**

By default, the tick marks will start at zero, unless negative values are present. You can override this by setting the tick-start attribute:

Copy to clipboard

```
<flux:chart.axis axis="y" tick-start="min">    <!-- ... --></flux:chart.axis>
```

The available values for tick-start are:

- auto: Automatically determine the starting tick value.
- min: Start at the minimum value on the axis.
- 0: Start at zero.
- 123: Start at 123 (or any other number).


**Setting the tick end**

By default, the tick marks will end at the next tick mark after the maximum value on the axis. You can override this by setting the tick-end attribute:

Copy to clipboard

```
<flux:chart.axis axis="y" tick-end="max">    <!-- ... --></flux:chart.axis>
```

The available values for tick-end are:

- auto: Automatically determine the ending tick value.
- max: End at the maximum value on the axis.
- 123: End at 123 (or any other number).


**Setting explicit tick values**

You can also set explicit tick values by passing an array of values to the tick-values attribute:

Copy to clipboard

```
<flux:chart.axis axis="y" tick-values="[0, 128, 256, 384, 512]" tick-suffix="MB">    <!-- ... --></flux:chart.axis>
```



## Tick formatting

The tick labels can be formatted using the format attribute.

Under-the-hood, the format attribute is passed to the Intl.NumberFormat constructor.

This means that you can use any of the formatting options that are available for the Intl.NumberFormat constructor.

[See the MDN documentation for more information on the formatting options ->](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat)

Copy to clipboard

```
<flux:chart.svg>    <!-- ... -->    <!-- Format the X axis tick labels to display the month and day: -->    <flux:chart.axis axis="x" :format="['month' => 'long', 'day' => 'numeric']">        <!-- X axis tick labels: -->        <flux:chart.axis.tick />    </flux:chart.axis>    <!-- Format the Y axis tick labels to display the value in USD: -->    <flux:chart.axis axis="y" :format="['style' => 'currency', 'currency' => 'USD']">        <!-- Y axis tick labels: -->        <flux:chart.axis.tick />    </flux:chart.axis></flux:chart.svg>
```

**Setting a tick prefix**

You can set a tick prefix by passing a string to the tick-prefix attribute:

Copy to clipboard

```
<flux:chart.axis axis="y" tick-prefix="$">    <!-- ... --></flux:chart.axis>
```

**Setting a tick suffix**

You can set a tick suffix by passing a string to the tick-suffix attribute:

Copy to clipboard

```
<flux:chart.axis axis="y" tick-suffix="MB">    <!-- ... --></flux:chart.axis>
```



## Cursor

Adds a vertical guide when hovering over the chart to highlight values at specific points. Customizable with stroke styles, colors, and dash patterns.

To enable a cursor, simply include <flux:chart.cursor> inside <flux:chart.svg>:

Copy to clipboard

```
<flux:chart.svg>    <!-- ... -->    <flux:chart.cursor /></flux:chart.svg>
```

**Styling the cursor**

Because the cursor is rendered as a <line> element, you can style it using any of the SVG attributes that are available for the <line> element.

Copy to clipboard

```
<!-- A dashed, black cursor that is 1px wide: --><flux:chart.cursor class="text-zinc-800" stroke-width="1" stroke-dasharray="4,4" />
```



## Tooltip

Displays contextual data on hover. Supports multiple values and custom formatting for better readability.

To enable tooltips, include <flux:chart.tooltip> inside <flux:chart>:

Copy to clipboard

```
<flux:chart>    <flux:chart.svg>        <!-- ... -->    </flux:chart.svg>    <flux:chart.tooltip>        <flux:chart.tooltip.heading field="date" />        <flux:chart.tooltip.value field="visitors" label="Visitors" />        <flux:chart.tooltip.value field="views" label="Views" :format="['notation' => 'compact']" />    </flux:chart.tooltip></flux:chart>
```

**Customizing tooltip content**

You can display multiple values and format numbers dynamically.

Copy to clipboard

```
<flux:chart.tooltip>    <flux:chart.tooltip.heading field="date" />    <flux:chart.tooltip.value field="visitors" label="Visitors" />    <flux:chart.tooltip.value field="views" label="Page Views" :format="['notation' => 'compact']" /></flux:chart.tooltip>
```



## Legend

Identifies multiple data series in the chart. Each legend item corresponds to a different dataset.

When using a legend, you will need to include a <flux:chart.viewport> component to wrap the <flux:chart.svg> component so that the legend is rendered outside of the chart:

Copy to clipboard

```
<flux:chart wire:model="data">    <flux:chart.viewport class="aspect-3/1">        <flux:chart.svg>            <flux:chart.line class="text-blue-500" field="visitors" />            <flux:chart.line class="text-red-500" field="views" />        </flux:chart.svg>    </flux:chart.viewport>    <div class="flex justify-center gap-4 pt-4">        <flux:chart.legend label="Visitors">            <flux:chart.legend.indicator class="bg-blue-400" />        </flux:chart.legend>        <flux:chart.legend label="Views">            <flux:chart.legend.indicator class="bg-red-400" />        </flux:chart.legend>    </div></flux:chart>
```



## Summary

Displays a single value from the dataset in a bold, easy-to-read format. Great for key performance indicators.

To enable a summary, include <flux:chart.summary> inside <flux:chart>:

Copy to clipboard

```
<flux:chart wire:model="data">    <flux:chart.summary>        <flux:chart.summary.value field="visitors" :format="['notation' => 'compact']" />    </flux:chart.summary>    <flux:chart.viewport class="aspect-[3/1]">        <!-- ... -->    </flux:chart.viewport></flux:chart>
```

Notice that you will need to include a <flux:chart.viewport> component to wrap the <flux:chart.svg> component so that the summary is rendered outside of the chart.

**Setting a fallback value**

You can set a fallback value by passing a string to the fallback attribute:

Copy to clipboard

```
<flux:chart.summary.value field="visitors" fallback="1200" />
```

This will be the value that is displayed if a data point is not being hovered over.



## Formatting

You can customize how numbers and dates appear in your charts to make them more readable. Whether it's formatting currency, percentages, or large numbers, Flux charts let you easily control how values are displayed using the :format prop.

Flux handles formatting for you behind the scenes using the Intl.NumberFormat and Intl.DateTimeFormat API, a built-in browser feature that ensures numbers and dates are displayed consistently based on locale and formatting rules. Just pass your desired format options to the :format prop, and Flux will apply them for you.



## Formatting numbers

You can format numbers by passing an array of formatting options to the :format prop.

Copy to clipboard

```
<flux:chart.axis axis="y" :format="['style' => 'currency', 'currency' => 'USD']" />
```

**Commonly used formatting options**

Here are some commonly used number formatting options you will likely need:

| Description | Example Input | Example Output | Format Array |
| --- | --- | --- | --- |
| Currency (USD) | 1234.56 |  | ['style' => 'currency', 'currency' => 'USD'] |
| Currency (EUR) | 1234.56 |  | ['style' => 'currency', 'currency' => 'EUR'] |
| Percent | 0.85 |  | ['style' => 'percent'] |
| Compact Number | 1000000 |  | ['notation' => 'compact'] |
| Scientific | 123456789 |  | ['notation' => 'scientific'] |
| Fixed Decimal | 3.1415926535 |  | ['maximumFractionDigits' => 2] |
| Thousands Separator | 1234567 |  | ['useGrouping' => true] |
| Custom Unit | 50 |  | ['style' => 'unit', 'unit' => 'megabyte'] |



## Formatting dates

You can format dates by passing an array of formatting options to the :format prop.

Copy to clipboard

```
<flux:chart.axis axis="x" field="date" :format="['month' => 'long', 'day' => 'numeric']" />
```

**Commonly used date formatting options**

Here are some commonly used date formatting options you will likely need:

| Description | Example Input | Example Output | Format Array |
| --- | --- | --- | --- |
| Full Date | 2024-03-15 |  | ['dateStyle' => 'full'] |
| Month and Day | 2024-03-15 |  | ['month' => 'long', 'day' => 'numeric'] |
| Short Month | 2024-03-15 |  | ['month' => 'short', 'day' => 'numeric'] |
| Time Only | 2024-03-15 14:30 |  | ['hour' => 'numeric', 'minute' => 'numeric', 'hour12' => true] |
| 24-hour Time | 2024-03-15 14:30 |  | ['hour' => '2-digit', 'minute' => '2-digit', 'hour12' => false] |
| Weekday | 2024-03-15 |  | ['weekday' => 'long'] |
| Short Date | 2024-03-15 |  | ['month' => '2-digit', 'day' => '2-digit', 'year' => '2-digit'] |
| Year Only | 2024-03-15 |  | ['year' => 'numeric'] |



## Additional resources

For more detailed information about formatting options, refer to:

- [MDN Documentation on Intl.DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat)
- [MDN Documentation on Intl.NumberFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat)

## Reference



### [flux:chart](#fluxchart)

| Prop | Description |
| --- | --- |
| wire:model | Binds the chart to a Livewire property containing the data to display. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| value | Array of data points for the chart. Each point should be an associative array with named fields. Used when not binding with wire:model. |
| curve | Default line curve type for all lines in the chart. Options: smooth (default), none. |

| Slot | Description |
| --- | --- |
| default | Chart components to render. Typically contains a flux:chart.svg component that defines the chart structure. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the chart container. Common uses: aspect-3/1 for aspect ratio, h-64 for fixed height. |

| Attribute | Description |
| --- | --- |
| data-flux-chart | Applied to the root element for styling and identification. |



### [flux:chart.svg](#fluxchartsvg)

Container for the chart's SVG elements. This component must be included within a `flux:chart` to render the chart.

| Slot | Description |
| --- | --- |
| default | Chart visualization components like lines, areas, axes, and interactive elements. |



### [flux:chart.line](#fluxchartline)

| Prop | Description |
| --- | --- |
| field | Name of the data field to plot on the y-axis. Required. |
| curve | Line curve type. Options: smooth (default), none. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the line. Common use: text-{color} for line color. |



### [flux:chart.area](#fluxchartarea)

| Prop | Description |
| --- | --- |
| field | Name of the data field to plot on the y-axis. Required. |
| curve | Area curve type. Options: smooth (default), none. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the area. Common use: fill-{color}/20 for fill color. |



### [flux:chart.point](#fluxchartpoint)

Adds points (dots) to mark data points on a line or area chart.

| Prop | Description |
| --- | --- |
| field | Name of the data field to plot points for. Required. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the points. Common use: fill-{color} for point fill color, r attribute for point radius. |



### [flux:chart.axis](#fluxchartaxis)

| Prop | Description |
| --- | --- |
| axis | Axis to configure. Options: x, y. Required. |
| field | For x-axis, the data field to use for labels. |
| format | Date/number formatting options for axis labels. See [Formatting](#formatting) for more details. |



### [flux:chart.axis.mark](#fluxchartaxismark)

Adds tick marks to the chart. Must be used within a `flux:chart.axis` component.

| Prop | Description |
| --- | --- |
| position | Position of the tick marks. Options: top, bottom, left, right. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the tick marks. Common use: text-{color} for line color, stroke-width="1" for line thickness. |



### [flux:chart.axis.line](#fluxchartaxisline)

Adds an axis line to the chart. Must be used within a `flux:chart.axis` component.

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the axis line. Common use: text-{color} for line color, stroke-width="1" for line thickness. |



### [flux:chart.axis.grid](#fluxchartaxisgrid)

Adds gridlines to the chart. Must be used within a `flux:chart.axis` component.

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the gridlines. Common use: text-{color} for line color, stroke-width="{width}" for line thickness. |



### [flux:chart.axis.tick](#fluxchartaxistick)

Adds tick marks and labels to an axis. Must be used within a `flux:chart.axis` component.

| Prop | Description |
| --- | --- |
| format | Date/number formatting options for tick labels. See [Formatting](#formatting) for more details. |

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the tick marks and labels. Common use: text-{color} for label color, font-{weight} for label weight. |



### [flux:chart.zero-line](#fluxchartzero-line)

Adds a horizontal line at y=0. Useful for charts that contain both positive and negative values.

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the zero line. Common use: text-{color} for line color, stroke-width="{width}" for line thickness. |



### [flux:chart.tooltip](#fluxcharttooltip)

| Prop | Description |
| --- | --- |
| field | Data field to display in the tooltip. |
| format | Date/number formatting options for tooltip values. |



### [flux:chart.tooltip.heading](#fluxcharttooltipheading)

| Prop | Description |
| --- | --- |
| field | Data field to display in the tooltip heading. |
| format | Date/number formatting options for tooltip values. See [Formatting](#formatting) for more details. |



### [flux:chart.tooltip.value](#fluxcharttooltipvalue)

| Prop | Description |
| --- | --- |
| field | Data field to display in the tooltip. |
| format | Date/number formatting options for tooltip values. See [Formatting](#formatting) for more details. |



### [flux:chart.cursor](#fluxchartcursor)

Adds an interactive cursor that follows mouse movement over the chart. Activates tooltips when present.

| CSS | Description |
| --- | --- |
| class | Additional CSS classes applied to the cursor line. |



### [flux:chart.summary](#fluxchartsummary)

Adds a summary section typically shown above the chart. Shows the latest values or values at cursor position.

| Slot | Description |
| --- | --- |
| default | Content to display in the summary section. Can include flux:chart.value components to display specific data values. |



### [flux:chart.summaryvalue](#fluxchartsummaryvalue)

Displays a specific data value, typically used within a `flux:chart.summary` component.

| Prop | Description |
| --- | --- |
| field | Data field to display. |
| fallback | Fallback text to display if the value is not found or cannot be formatted. |
| format | Date/number formatting options. See [Formatting](#formatting) for more details. |



### [flux:chart.legend](#fluxchartlegend)

| Prop | Description |
| --- | --- |
| field | Data field this legend item represents. |
| label | Label text for the legend item. |
| format | Date/number formatting options. See [Formatting](#formatting) for more details. |

| Slot | Description |
| --- | --- |
| default | Content to display in the legend. Can include arbitrary content, including flux:chart.legend.indicator components. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0020_Checkbox

# Checkbox

Select one or multiple options from a set.





I agree to the terms and conditions





Copy to clipboard

```
<flux:field variant="inline">    <flux:checkbox wire:model="terms" />    <flux:label>I agree to the terms and conditions</flux:label>    <flux:error name="terms" /></flux:field>
```



## [Checkbox group](#checkbox-group)

Organize a list of related checkboxes vertically.



When using checkbox groups, you can add wire:model to the group element or the individual checkboxes.





Notifications
Push notifications

Email

In-app alerts

SMS





Copy to clipboard

```
<flux:checkbox.group wire:model="notifications" label="Notifications">    <flux:checkbox label="Push notifications" value="push" checked />    <flux:checkbox label="Email" value="email" checked />    <flux:checkbox label="In-app alerts" value="app" />    <flux:checkbox label="SMS" value="sms" /></flux:checkbox.group>
```



## [With descriptions](#with-descriptions)

Align descriptions for each checkbox directly below its label.





Subscription preferences
Newsletter Receive our monthly newsletter with the latest updates and offers.


Product updates Stay informed about new features and product updates.


Event invitations Get invitations to our exclusive events and webinars.






Copy to clipboard

```
<flux:checkbox.group wire:model="subscription" label="Subscription preferences">    <flux:checkbox checked        value="newsletter"        label="Newsletter"        description="Receive our monthly newsletter with the latest updates and offers."    />    <flux:checkbox        value="updates"        label="Product updates"        description="Stay informed about new features and product updates."    />    <flux:checkbox        value="invitations"        label="Event invitations"        description="Get invitations to our exclusive events and webinars."    /></flux:checkbox.group>
```



## [Horizontal fieldset](#horizontal-fieldset)

Organize a group of related checkboxes horizontally.





Languages
Choose the languages you want to support.


English

Spanish

French

German





Copy to clipboard

```
<flux:fieldset>    <flux:legend>Languages</flux:legend>    <flux:description>Choose the languages you want to support.</flux:description>    <div class="flex gap-4 *:gap-x-2">        <flux:checkbox checked value="english" label="English" />        <flux:checkbox checked value="spanish" label="Spanish" />        <flux:checkbox value="french" label="French" />        <flux:checkbox value="german" label="German" />    </div></flux:fieldset>
```



## [Check-all](#check-all)

Control a group of checkboxes with a single checkbox.





|  | Name |
| --- | --- |
|  | Caleb Porzio |
|  | Hugo Sainte-Marie |
|  | Keith Damiani |





Copy to clipboard

```
<flux:checkbox.group>    <flux:checkbox.all />    <flux:checkbox checked />    <flux:checkbox />    <flux:checkbox /></flux:checkbox.group>
```



## [Checked](#checked)

Mark a checkbox as checked by default.





Enable notifications





Copy to clipboard

```
<flux:checkbox checked />
```



## [Disabled](#disabled)

Prevent users from interacting with and modifying a checkbox.





Read and write





Copy to clipboard

```
<flux:checkbox disabled />
```



## [Checkbox cards](#checkbox-cards)

A bordered alternative to standard checkboxes.





Subscription preferences

Newsletter

Get the latest updates and offers.

Product updates

Learn about new features and products.

Event invitations

Invitatations to exclusive events.





Copy to clipboard

```
<flux:checkbox.group wire:model="subscription" label="Subscription preferences" variant="cards" class="max-sm:flex-col">    <flux:checkbox checked        value="newsletter"        label="Newsletter"        description="Get the latest updates and offers."    />    <flux:checkbox        value="updates"        label="Product updates"        description="Learn about new features and products."    />    <flux:checkbox        value="invitations"        label="Event invitations"        description="Invitatations to exclusive events."    /></flux:checkbox.group>
```

You can swap between vertical and horizontal card layouts by conditionally applying flex-col based on the viewport.



Copy to clipboard

```
<flux:checkbox.group ... class="max-sm:flex-col">    <!-- ... --></flux:checkbox.group>
```



## [Vertical cards](#vertical-cards)

You can arrange a set of checkbox cards vertically by simply adding the flex-col class to the group container.





Subscription preferences

Newsletter

Get the latest updates and offers.

Product updates

Learn about new features and products.

Event invitations

Invitatations to exclusive events.





Copy to clipboard

```
<flux:checkbox.group label="Subscription preferences" variant="cards" class="flex-col">    <flux:checkbox checked        value="newsletter"        label="Newsletter"        description="Get the latest updates and offers."    />    <flux:checkbox        value="updates"        label="Product updates"        description="Learn about new features and products."    />    <flux:checkbox        value="invitations"        label="Event invitations"        description="Invitatations to exclusive events."    /></flux:checkbox.group>
```



## [Cards with icons](#cards-with-icons)

You can arrange a set of checkbox cards vertically by simply adding the flex-col class to the group container.





Subscription preferences

Newsletter

Get the latest updates and offers.

Product updates

Learn about new features and products.

Event invitations

Invitatations to exclusive events.





Copy to clipboard

```
<flux:checkbox.group label="Subscription preferences" variant="cards" class="flex-col">    <flux:checkbox checked        value="newsletter"        icon="newspaper"        label="Newsletter"        description="Get the latest updates and offers."    />    <flux:checkbox        value="updates"        icon="cube"        label="Product updates"        description="Learn about new features and products."    />    <flux:checkbox        value="invitations"        icon="calendar"        label="Event invitations"        description="Invitatations to exclusive events."    /></flux:checkbox.group>
```



## [Custom card content](#custom-card-content)

You can compose your own custom cards through the flux:checkbox component slot.





Subscription preferences

Newsletter

Get the latest updates and offers.

Product updates

Learn about new features and products.

Event invitations

Invitatations to exclusive events.





Copy to clipboard

```
<flux:checkbox.group label="Subscription preferences" variant="cards" class="flex-col">    <flux:checkbox checked value="newsletter">        <flux:checkbox.indicator />        <div class="flex-1">            <flux:heading class="leading-4">Newsletter</flux:heading>            <flux:text size="sm" class="mt-2">Get the latest updates and offers.</flux:text>        </div>    </flux:checkbox>    <flux:checkbox value="updates">        <flux:checkbox.indicator />        <div class="flex-1">            <flux:heading class="leading-4">Product updates</flux:heading>            <flux:text size="sm" class="mt-2">Learn about new features and products.</flux:text>        </div>    </flux:checkbox>    <flux:checkbox value="invitations">        <flux:checkbox.indicator />        <div class="flex-1">            <flux:heading class="leading-4">Event invitations</flux:heading>            <flux:text size="sm" class="mt-2">Invitatations to exclusive events.</flux:text>        </div>    </flux:checkbox></flux:checkbox.group>
```



## [Pills](#pills)

Compact, rounded checkboxes that look like tags or badges. Perfect for filters, categories, and any time you want lightweight selectable options.





Categories Fantasy
Science fiction
Horror
Mystery
Romance
Autobiography
Thriller
Poetry
Children






Copy to clipboard

```
<flux:checkbox.group wire:model="categories" label="Categories" variant="pills">    <flux:checkbox value="fantasy" label="Fantasy" />    <flux:checkbox value="science-fiction" label="Science fiction" />    <flux:checkbox value="horror" label="Horror" />    <flux:checkbox value="mystery" label="Mystery" />    <flux:checkbox value="romance" label="Romance" />    <flux:checkbox value="autobiography" label="Autobiography" />    <flux:checkbox value="thriller" label="Thriller" />    <flux:checkbox value="poetry" label="Poetry" />    <flux:checkbox value="children" label="Children" /></flux:checkbox.group>
```



## [Buttons](#buttons)

Button-style checkbox options that look like a toolbar. Perfect for toggle controls and feature selections where you want a more prominent visual style.





Features  Notifications  Analytics  Backups





Copy to clipboard

```
<flux:checkbox.group wire:model="features" label="Features" variant="buttons">    <flux:checkbox value="notifications" icon="bell" label="Notifications" />    <flux:checkbox value="analytics" icon="chart-bar" label="Analytics" />    <flux:checkbox value="backups" icon="cloud-arrow-up" label="Backups" /></flux:checkbox.group>
```

## Related components

[Switch Toggle switches for selecting one or multiple options](/components/switch) [Radio Radio button controls for selecting one option from many](/components/radio) [Field Structured form field with label and validation states](/components/field)

## Reference



### [flux:checkbox](#fluxcheckbox)

| Prop | Description |
| --- | --- |
| wire:model | Binds the checkbox to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| label | Label text displayed next to the checkbox. When provided, wraps the checkbox in a structure with an adjacent label. |
| description | Help text displayed below the checkbox. When provided alongside label, appears between the label and checkbox. |
| value | Value associated with the checkbox when used in a group. When the checkbox is checked, this value will be included in the array returned by the group's wire:model. |
| checked | Sets the checkbox to be checked by default. |
| indeterminate | Sets the checkbox to an indeterminate state, represented by a dash instead of a checkmark. Useful for "select all" checkboxes when only some items are selected. |
| disabled | Prevents user interaction with the checkbox. |
| invalid | Applies error styling to the checkbox. |

| Attribute | Description |
| --- | --- |
| data-flux-checkbox | Applied to the root element for styling and identification. |
| data-checked | Applied when the checkbox is checked. |
| data-indeterminate | Applied when the checkbox is in an indeterminate state. |



### [flux:checkbox.group](#fluxcheckboxgroup)

| Prop | Description |
| --- | --- |
| wire:model | Binds the checkbox group to a Livewire property. The value will be an array of the selected checkboxes' values. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| label | Label text displayed above the checkbox group. When provided, wraps the group in a flux:field component with an adjacent flux:label component. |
| description | Help text displayed below the group label. When provided alongside label, appears between the label and the checkboxes. |
| variant | Visual style of the group. Options: default, cards (Pro), pills (Pro), buttons (Pro). |
| disabled | Prevents user interaction with all checkboxes in the group. |
| invalid | Applies error styling to all checkboxes in the group. |

| Slot | Description |
| --- | --- |
| default | The checkboxes to be grouped together. Can include flux:checkbox, flux:checkbox.all, and other elements. |



### [flux:checkbox.all](#fluxcheckboxall)

A special checkbox that controls all checkboxes within its group. It becomes checked when all checkboxes are checked, unchecked when none are checked, and indeterminate when some (but not all) are checked.

| Prop | Description |
| --- | --- |
| label | Text label displayed next to the checkbox. |
| description | Help text displayed below the checkbox. |
| disabled | Prevents user interaction with the checkbox. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0021_Command



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Command palette

A searchable list of commands.





Assign to…

⌘A

Create new file

Create new project

⌘⇧N

Documentation

Changelog

Settings

⌘,

No results found





Copy to clipboard

```
<flux:command>    <flux:command.input placeholder="Search..." />    <flux:command.items>        <flux:command.item wire:click="..." icon="user-plus" kbd="⌘A">Assign to…</flux:command.item>        <flux:command.item wire:click="..." icon="document-plus">Create new file</flux:command.item>        <flux:command.item wire:click="..." icon="folder-plus" kbd="⌘⇧N">Create new project</flux:command.item>        <flux:command.item wire:click="..." icon="book-open">Documentation</flux:command.item>        <flux:command.item wire:click="..." icon="newspaper">Changelog</flux:command.item>        <flux:command.item wire:click="..." icon="cog-6-tooth" kbd="⌘,">Settings</flux:command.item>    </flux:command.items></flux:command>
```



## [As a modal](#as-a-modal)

Open a command palette as a modal for quick access to frequently used commands.





Search...

⌘K



Assign to…

⌘A

Create new file

Create new project

⌘⇧N

Documentation

Changelog

Settings

⌘,

No results found





Copy to clipboard

```
<flux:modal.trigger name="search" shortcut="cmd.k">    <flux:input as="button" placeholder="Search..." icon="magnifying-glass" kbd="⌘K" /></flux:modal.trigger><flux:modal name="search" variant="bare" class="w-full max-w-[30rem] my-[12vh] max-h-screen overflow-y-hidden">    <flux:command class="border-none shadow-lg inline-flex flex-col max-h-[76vh]">        <flux:command.input placeholder="Search..." closable />        <flux:command.items>            <flux:command.item icon="user-plus" kbd="⌘A">Assign to…</flux:command.item>            <flux:command.item icon="document-plus">Create new file</flux:command.item>            <flux:command.item icon="folder-plus" kbd="⌘⇧N">Create new project</flux:command.item>            <flux:command.item icon="book-open">Documentation</flux:command.item>            <flux:command.item icon="newspaper">Changelog</flux:command.item>            <flux:command.item icon="cog-6-tooth" kbd="⌘,">Settings</flux:command.item>        </flux:command.items>    </flux:command></flux:modal>
```

## Reference



### [flux:command](#fluxcommand)

The root command palette component that wraps the input and items.

| Attribute | Description |
| --- | --- |
| data-flux-command | Applied to the root element for styling and identification. |



### [flux:command.input](#fluxcommandinput)

| Prop | Description |
| --- | --- |
| clearable | If true, displays a clear button when the input has content. |
| closable | If true, displays a close button to dismiss the command palette. |
| icon | Name of the icon displayed at the start of the input. Default: magnifying-glass. |
| placeholder | Placeholder text displayed when the input is empty. |



### [flux:command.items](#fluxcommanditems)

Container for command items. No props available.



### [flux:command.item](#fluxcommanditem)

| Prop | Description |
| --- | --- |
| icon | Name of the icon displayed at the start of the item. |
| icon:variant | Visual style of the icon. Options: outline (default), solid, mini, micro. |
| kbd | Keyboard shortcut hint displayed at the end of the item (e.g., ⌘K). |

| Attribute | Description |
| --- | --- |
| data-flux-command-item | Applied to the item element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0022_Context



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Context menu

Dropdown menus that open when right clicking a designated area.

Learn more about the menu component on the [dropdown page ->](/components/dropdown)





Right click

New post

Sort by



Name

Date

Popularity

Filter



Draft

Published

Archived

Delete





Copy to clipboard

```
<flux:context>    <flux:card class="border-dashed border-2 px-16">        <flux:text>Right click</flux:text>    </flux:card>    <flux:menu>        <flux:menu.item icon="plus">New post</flux:menu.item>        <flux:menu.separator />        <flux:menu.submenu heading="Sort by">            <flux:menu.radio.group>                <flux:menu.radio checked>Name</flux:menu.radio>                <flux:menu.radio>Date</flux:menu.radio>                <flux:menu.radio>Popularity</flux:menu.radio>            </flux:menu.radio.group>        </flux:menu.submenu>        <flux:menu.submenu heading="Filter">            <flux:menu.checkbox checked>Draft</flux:menu.checkbox>            <flux:menu.checkbox checked>Published</flux:menu.checkbox>            <flux:menu.checkbox>Archived</flux:menu.checkbox>        </flux:menu.submenu>        <flux:menu.separator />        <flux:menu.item variant="danger" icon="trash">Delete</flux:menu.item>    </flux:menu></flux:context>
```

## Related components

[Dropdown Display expandable menus for navigational options](/components/dropdown) [Command palette Execute actions with keyboard shortcuts](/components/command)

## Reference



### [flux:context](#fluxcontext)

A wrapper component that enables right-click context menu functionality.

| Prop | Description |
| --- | --- |
| wire:model | Binds the context menu's state to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| position | Controls the position of the menu relative to the click position. Format: [vertical] [horizontal]. Vertical options: top, bottom (default). Horizontal options: start, center, end (default). |
| gap | Distance in pixels between the menu and the click position. Default: 4. |
| offset | Additional offset in pixels along both axes. Format: [x] [y]. |
| target | ID of an external element to use as the menu. Use this when you need the menu to be outside the context element's DOM tree. |
| detail | Custom value to be stored in the menu's data-detail attribute, useful for adding custom styling or behavior based on the source of the context menu. |
| disabled | Prevents the context menu from being shown when right-clicking. |

| Slot | Description |
| --- | --- |
| default | The first child element functions as the trigger area, which will show the context menu when right-clicked. The second child element should be a flux:menu component that will appear as the context menu. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0023_ComposerNew



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Composer

A configurable message input with support for action buttons and rich text. Ideal for chat interfaces and AI prompts.





Prompt Enter your prompt here






Copy to clipboard

```
<form wire:submit="send">    <flux:composer wire:model="prompt" label="Prompt" label:sr-only placeholder="How can I help you today?">        <x-slot name="actionsLeading">            <flux:button size="sm" variant="subtle" icon="paper-clip" />            <flux:button size="sm" variant="subtle" icon="slash" />            <flux:button size="sm" variant="subtle" icon="adjustments-horizontal" />        </x-slot>        <x-slot name="actionsTrailing">            <flux:button size="sm" variant="filled" icon="microphone" />            <flux:button type="submit" size="sm" variant="primary" icon="paper-airplane" />        </x-slot>    </flux:composer></form>
```



## [With header](#with-header)

Display file previews or other content above the input area using the header slot.









Copy to clipboard

```
<flux:composer wire:model="prompt" label="Prompt" label:sr-only placeholder="How can I help you today?">    <x-slot name="header">        <!-- Header content... -->        <div class="relative border border-zinc-200 dark:border-zinc-700 rounded-lg overflow-hidden">            <img src="https://fluxui.dev/img/demo/caleb.png" alt="Profile picture" class="size-14">            <div class="absolute top-0 right-0 p-1">                <button type="button" class="p-0.5 rounded-full bg-zinc-900/50 hover:bg-zinc-900/70 flex justify-center items-center">                    <flux:icon icon="x-mark" variant="micro" class="text-white" />                </button>            </div>        </div>    </x-slot>    <x-slot name="actionsLeading">        <!-- ... -->    </x-slot>    <x-slot name="actionsTrailing">        <!-- ... -->    </x-slot></flux:composer>
```



## [Inline](#inline)

Place action buttons alongside the input in a single row for a more compact layout.









Copy to clipboard

```
<flux:composer wire:model="prompt" rows="1" inline label="Prompt" label:sr-only placeholder="How can I help you today?">    <x-slot name="actionsLeading">        <flux:button size="sm" variant="ghost" icon="plus" />    </x-slot>    <x-slot name="actionsTrailing">        <flux:button size="sm" variant="filled" icon="microphone" />        <flux:button type="submit" size="sm" variant="primary" icon="paper-airplane" />    </x-slot></flux:composer>
```



## [Input variant](#input-variant)

Use the variant="input" prop to render the composer with border radiuses that match other form inputs.





Name

Message


Send





Copy to clipboard

```
<flux:composer variant="input" label="Message" placeholder="What's on your mind?">    <!-- ... --></flux:composer>
```



## [Height](#height)

Set the initial and maximum height of the input area using rows and max-rows.









Copy to clipboard

```
<flux:composer rows="4" max-rows="8" ...>    <!-- ... --></flux:composer>
```



## [Submit behavior](#submit-behavior)

By default, the form submits when pressing `Ctrl`/`Cmd` + `Enter`. Set submit="enter" to submit on `Enter` alone.









Copy to clipboard

```
<form wire:submit="send">    <flux:composer wire:model="prompt" submit="enter" ...>        <!-- ... -->    </flux:composer></form>
```



## [Rich text](#rich-text)

Enable rich text formatting by passing an editor component to the input slot.





Bold ⌘B

Italic ⌘I

Bullet list

Ordered list

Insert link ⌘K

Insert link

Unlink

Left



Align

Left

Center

Right





Copy to clipboard

```
<flux:composer wire:model="prompt" rows="3" label="Prompt" label:sr-only placeholder="How can I help you today?">    <x-slot name="input">        <flux:editor variant="borderless" toolbar="bold italic bullet ordered | link | align" />    </x-slot>    <x-slot name="actionsLeading">        <flux:button size="sm" variant="subtle" icon="paper-clip" />        <flux:button size="sm" variant="subtle" icon="slash" />        <flux:button size="sm" variant="subtle" icon="adjustments-horizontal" />    </x-slot>    <x-slot name="actionsTrailing">        <flux:button size="sm" variant="filled" icon="microphone" />        <flux:button type="submit" size="sm" variant="primary" icon="paper-airplane" />    </x-slot></flux:composer>
```



## [Disabled](#disabled)

Prevent user interaction with the composer by adding the disabled attribute.









Copy to clipboard

```
<flux:composer disabled ...>    <!-- ... --></flux:composer>
```



## [Invalid](#invalid)

When paired with a name or wire:model attribute alongside a label prop, validation errors will automatically apply invalid styling to the composer.





Message


The prompt field is required.





Copy to clipboard

```
<flux:composer wire:model="prompt" label="Prompt" label:sr-only ...>    <!-- ... --></flux:composer>
```

## Related components

[Field Structured form field with label](/components/field) [Input Text fields for collecting user input](/components/input)

## Reference



### [flux:composer](#fluxcomposer)

| Prop | Description |
| --- | --- |
| wire:model | Binds the composer to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| name | Name attribute for the composer. Used for validation error detection. |
| placeholder | Placeholder text displayed when the input is empty. |
| label | Label text for the composer. When provided, wraps the composer in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| label:sr-only | Visually hides the label while keeping it accessible to screen readers. |
| description | Help text displayed near the composer. See the [field component](/components/field). |
| description:sr-only | Visually hides the description while keeping it accessible to screen readers. |
| rows | Number of visible text lines for the input area. Default: 2. |
| max-rows | Maximum number of rows the input can expand to as content grows. |
| inline | Displays action buttons alongside the input in a single row. |
| submit | Keyboard behavior for form submission. Options: cmd+enter (default), enter. |
| disabled | Prevents user interaction with the composer. |
| invalid | If true, applies error styling to the composer. |

| Slot | Description |
| --- | --- |
| input | Custom input content. Use this slot to replace the default textarea with a rich text editor. |
| header | Content displayed above the input area. Useful for file previews or uploads. |
| footer | Content displayed below the input area. |
| actionsLeading | Buttons or actions displayed at the start of the action bar. |
| actionsTrailing | Buttons or actions displayed at the end of the action bar, typically including the submit button. |

| Attribute | Description |
| --- | --- |
| data-flux-composer | Applied to the root element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0024_Date picker



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Date picker

Allow users to select dates or date ranges via a calendar overlay. Perfect for filtering data or scheduling events.

Use date inputs instead of date pickers for far-future or past events such as birthdates.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker />
```



## Basic usage

Set the initial selected date using the value prop with a Y-m-d formatted date string:

Copy to clipboard

```
<flux:date-picker value="2026-03-03" />
```

You can also bind the selection to a Livewire property using wire:model:

Copy to clipboard

```
<flux:date-picker wire:model="date" />
```

Now you can access the selected date from your Livewire component using either a Carbon instance or a Y-m-d formatted string:

Copy to clipboard

```
<?phpuse Illuminate\Support\Carbon;use Livewire\Component;use App\Models\Post;class CreatePost extends Component {    public ?Carbon $date;    public function save()    {        Post::create([            // ...            'published_at' => $this->date,        ])        // ...    }}
```



## [Input trigger](#input-trigger)

Attach the date picker to a date input for more precise date selection control.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker wire:model="date">    <x-slot name="trigger">        <flux:date-picker.input />    </x-slot></flux:date-picker>
```



## [Range picker](#range-picker)

Enable selection of date ranges for reporting, booking systems, or any scenario requiring a start and end date.





Cancel

Select range





Copy to clipboard

```
<flux:date-picker mode="range" />
```

Set the initial range using the value prop with a start and end date separated by a forward slash:

Copy to clipboard

```
<flux:date-picker mode="range" value="2026-03-02/2026-03-06" />
```

You can also bind the selection to a Livewire property using wire:model:

Copy to clipboard

```
<flux:date-picker mode="range" wire:model="range" />
```

Now you can access the selected range from your Livewire component using an associative array of Y-m-d formatted date strings:

Copy to clipboard

```
<?phpuse Illuminate\Support\Carbon;use Livewire\Component;class Dashboard extends Component {    public array $range;    public function mount() {        $this->range = [            'start' => now()->subMonth()->format('Y-m-d'),            'end' => now()->format('Y-m-d'),        ];    }}
```

Alternatively, you can use the specialized DateRange object for enhanced functionality:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    public DateRange $range;    public function mount() {        $this->range = new DateRange(now()->subMonth(), now());    }}
```

We highly recommend using the DateRange object for range selection, it provides a lot of useful functionality.

[Check out everything you can do with the DateRange object ->](#the-daterange-object)



## [Range limits](#range-limits)

Control the allowed range of dates that can be selected.





Cancel

Select range





Copy to clipboard

```
<flux:date-picker mode="range" min-range="3" />
```





Cancel

Select range





Copy to clipboard

```
<flux:date-picker mode="range" max-range="10" />
```



## [Range with inputs](#range-with-inputs)

Use separate inputs for start and end dates to provide a clearer interface for date range selection.





Start

End

Cancel

Select range





Copy to clipboard

```
<flux:date-picker mode="range">    <x-slot name="trigger">        <div class="flex flex-col sm:flex-row gap-6 sm:gap-4">            <flux:date-picker.input label="Start" />            <flux:date-picker.input label="End" />        </div>    </x-slot></flux:date-picker>
```



## [Presets](#presets)

Allow users to select from frequently used ranges like "Last 7 days" or "This month".





 TodayYesterdayThis WeekLast 7 DaysThis MonthYear to DateAll TimeCustom

* Choose predefined range...
 Today
Yesterday
This Week
Last 7 Days
This Month
Year to Date
All Time
Custom



Cancel

Select range





Copy to clipboard

```
<flux:date-picker mode="range" with-presets />
```

You can also specify which presets to show, and in which order, using the presets prop:

Copy to clipboard

```
<flux:date-picker    mode="range"    presets="today yesterday thisWeek last7Days thisMonth yearToDate allTime"/>
```



## Available presets

Below is a list of all available presets.

| Key | Label | Constructor | Date Range |
| --- | --- | --- | --- |
| today | Today | DateRange::today() | Current day |
| yesterday | Yesterday | DateRange::yesterday() | Previous day |
| thisWeek | This Week | DateRange::thisWeek() | Current week |
| lastWeek | Last Week | DateRange::lastWeek() | Previous week |
| last7Days | Last 7 Days | DateRange::last7Days() | Previous 7 days |
| thisMonth | This Month | DateRange::thisMonth() | Current month |
| lastMonth | Last Month | DateRange::lastMonth() | Previous month |
| thisQuarter | This Quarter | DateRange::thisQuarter() | Current quarter |
| lastQuarter | Last Quarter | DateRange::lastQuarter() | Previous quarter |
| thisYear | This Year | DateRange::thisYear() | Current year |
| lastYear | Last Year | DateRange::lastYear() | Previous year |
| last14Days | Last 14 Days | DateRange::last14Days() | Previous 14 days |
| last30Days | Last 30 Days | DateRange::last30Days() | Previous 30 days |
| last3Months | Last 3 Months | DateRange::last3Months() | Previous 3 months |
| last6Months | Last 6 Months | DateRange::last6Months() | Previous 6 months |
| yearToDate | Year to Date | DateRange::yearToDate() | January 1st to today |
| tomorrow | Tomorrow | DateRange::tomorrow() | Next day |
| nextWeek | Next Week | DateRange::nextWeek() | Next week |
| next7Days | Next 7 Days | DateRange::next7Days() | Next 7 days from today |
| nextMonth | Next Month | DateRange::nextMonth() | Next month |
| nextQuarter | Next Quarter | DateRange::nextQuarter() | Next quarter |
| nextYear | Next Year | DateRange::nextYear() | Next year |
| next14Days | Next 14 Days | DateRange::next14Days() | Next 14 days from today |
| next30Days | Next 30 Days | DateRange::next30Days() | Next 30 days from today |
| next3Months | Next 3 Months | DateRange::next3Months() | Next 3 months from today |
| next6Months | Next 6 Months | DateRange::next6Months() | Next 6 months from today |
| allTime | All Time | DateRange::allTime($start) | Minimum supplied date to today |
| custom | Custom Range | DateRange::custom() | User-defined date range |



## All time

When using the allTime preset, you must specify a minimum date using the min prop. This minimum date will be used as the start date of the "All Time" range. Today's date will be used as the end date:

Copy to clipboard

```
<flux:date-picker    mode="range"    presets="... allTime"    :min="auth()->user()->created_at->format('Y-m-d')"/>
```

If you need to construct this via the DateRange object from Livewire, you can do so like this:

Copy to clipboard

```
use Flux\DateRange;$this->range = DateRange::allTime(start: auth()->user()->created_at);
```

If you are using this date range to filter data, you may want to remove "where" constraints from the query when allTime is selected:

Copy to clipboard

```
$orders = Order::when($this->range->isNotAllTime(), function ($query) => {    $query->whereBetween('created_at', $this->range);})->get();
```



## Custom range preset

When a user selects a custom date range that doesn't match any other preset, the picker will automatically switch to the custom preset if it is included in the presets prop.

Copy to clipboard

```
<flux:date-picker mode="range" presets="... custom" />
```



## [Unavailable dates](#unavailable-dates)

Disable specific dates from being selected. Useful for blocking out holidays, showing booked dates, or indicating unavailable time slots.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker unavailable="2026-03-02,2026-03-04" />
```



## [With today shortcut](#with-today-shortcut)

Add a shortcut button to quickly navigate to today's date. When viewing a different month, it jumps to the current month. When already viewing the current month, it selects today's date.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker with-today />
```



## [Selectable header](#selectable-header)

Enable quick navigation by making the month and year in the header selectable.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker selectable-header />
```



## [Fixed weeks](#fixed-weeks)

Display a consistent number of weeks in every month. Prevents layout shifts when navigating between months with different numbers of weeks.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker fixed-weeks />
```



## [Start day](#start-day)

By deafult the first day of the week will be automatically set based on the user's locale. You can override this by setting the start-day attribute to any day of the week.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker start-day="1" />
```



## [Open to](#open-to)

Set the date that the date picker will open to, if there is no selected date.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker open-to="2027-04-01" />
```

If you want the date picker to always use the open-to date, you can add the force-open-to attribute.







Copy to clipboard

```
<flux:date-picker open-to="2027-04-01" force-open-to />
```



## [Week numbers](#week-numbers)

Display the week number for each week.





Cancel

Select date





Copy to clipboard

```
<flux:date-picker week-numbers />
```



## [Localization](#localization)

By default, the date picker will use the browser's locale (e.g. navigator.language).

You can override this behavior by setting the locale attribute to any valid locale string (e.g. fr for French, en-US for English, etc.):





Cancel

Select date





Copy to clipboard

```
<flux:date-picker locale="ja-JP" />
```



## The DateRange object

Flux provides a specialized Flux\DateRange object that extends the native CarbonPeriod class. This object provides a number of convenience methods to easily create and manage date ranges.

First, it's worth noting that most of the time, you will want to use wire:model.live to bind the range property to a DateRange object. This will automatically update the range property whenever the user selects a date range:

Copy to clipboard

```
<flux:calendar wire:model.live="range" />
```

Now, in your component, you can type hint the range property as a DateRange object:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    public DateRange $range;}
```



## Instantiation

You can initialize a DateRange object by passing a start and end date to the DateRange constructor from something like the mount method:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    public DateRange $range;    public function mount() {        $this->range = new DateRange(now(), now()->addDays(7));    }}
```



## Persisting to the session

You can persist a DateRange object in the user's session by using the #[Session] attribute:

Copy to clipboard

```
<?phpuse Livewire\Attributes\Session;use Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    #[Session]    public DateRange $range;}
```



## Using with Eloquent

You can use the DateRange object with Eloquent's whereBetween() method to filter queries by date range:

Copy to clipboard

```
<?phpuse Livewire\Attributes\Computed;use Livewire\Component;use App\Models\Order;use Flux\DateRange;class Dashboard extends Component {    public ?DateRange $range;    #[Computed]    public function orders() {        return $this->range            ? Order::whereBetween('created_at', $this->range)->get()            : Order::all();    }}
```



## Available methods

The DateRange object extends the native CarbonPeriod class, so it inherits all of its methods. Here are a few examples:

Copy to clipboard

```
$range = new Flux\DateRange(    now()->subDays(1),    now()->addDays(1),);// Get the start and end dates as Carbon instances...$start = $range->start();$end = $range->end();// Check if the range contains a date...$range->contains(now());// Get the number of days in the range...$range->length();// Loop over the range by day...foreach ($range as $date) {    // $date is a Carbon instance...}// Get the range as an array of Carbon instances representing each day in the range...$range->toArray();
```

You can also use it anywhere Eloquent utilities expect a CarbonPeriod instance:

Copy to clipboard

```
$orders = Order::whereBetween('created_at', $range)->get();
```



## Range presets

When using the presets prop, the calendar will get/set an associative array of dates as well as a preset key:

Copy to clipboard

```
[    'start' => null,    'end' => null,    'preset' => 'lastMonth',]
```

You can directly get/set the preset string through a simple array binding:

Copy to clipboard

```
<?phpuse Livewire\Component;class Dashboard extends Component {    public array $range;    public function mount() {        $this->range = [            'start' => null,            'end' => null,            'preset' => 'lastMonth',        ];    }}
```

However, the DateRange object is equipped to manage the preset internally.

For example, you can create a range using the lastMonth() method:

Copy to clipboard

```
<?phpuse Livewire\Component;use Flux\DateRange;class Dashboard extends Component {    public DateRange $range;    public function mount() {        $this->range = DateRange::lastMonth();    }}
```

[View the complete list of available presets ->](#available-presets)

You can access the preset as an enum value via the preset() method:

Copy to clipboard

```
$this->range->preset();// This will return a value like `DateRangePreset::LastMonth`...
```

## Related components

[Calendar Displays a calendar interface for selecting dates](/components/calendar) [Input Text fields for collecting user input](/components/input)

## Reference



### [flux:date-picker](#fluxdate-picker)

| Prop | Description |
| --- | --- |
| wire:model | Binds the date picker to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| value | Selected date(s). Format depends on mode: single date (Y-m-d) or range (Y-m-d/Y-m-d). |
| mode | Selection mode. Options: single (default), range. |
| min-range | Minimum number of days that can be selected in range mode. |
| max-range | Maximum number of days that can be selected in range mode. |
| min | Earliest selectable date. Can be a date string or "today". |
| max | Latest selectable date. Can be a date string or "today". |
| open-to | Set the date that the date picker will open to, if there is no selected date. |
| force-open-to | If true, forces the date picker to open to the open-to date regardless of the selected date. Default: false. |
| months | Number of months to display. Default: 1 in single mode, 2 in range mode. |
| label | Label text displayed above the date picker. When provided, wraps the component in a flux:field with an adjacent flux:label. |
| description | Help text displayed below the date picker. When provided alongside label, appears between the label and date picker within the flux:field wrapper. |
| description:trailing | The description provided will be displayed below the date picker instead of above it. |
| badge | Badge text displayed at the end of the flux:label component when the label prop is provided. |
| placeholder | Placeholder text displayed when no date is selected. Default depends on mode. |
| size | Size of the calendar day cells. Options: sm, default, lg, xl, 2xl. |
| start-day | The day of the week to start the calendar on. Options: 0 (Sunday) to 6 (Saturday). Default: based on the user's locale. |
| week-numbers | If true, displays week numbers in the calendar. |
| selectable-header | If true, displays month and year dropdowns for quick navigation. |
| with-today | If true, displays a button to quickly navigate to today's date. |
| with-inputs | If true, displays date inputs at the top of the calendar for manual date entry. |
| with-confirmation | If true, requires confirmation before applying the selected date(s). |
| with-presets | If true, displays preset date ranges. Use with presets to customize available options. |
| presets | Space-separated list of preset date ranges to display. Default: today yesterday thisWeek last7Days thisMonth yearToDate allTime. |
| clearable | Displays a clear button when a date is selected. |
| disabled | Prevents user interaction with the date picker. |
| invalid | Applies error styling to the date picker. |
| locale | Set the locale for the date picker. Examples: fr, en-US, ja-JP. |

| Slot | Description |
| --- | --- |
| trigger | Custom trigger element to open the date picker. Usually a flux:date-picker.input or flux:date-picker.button. |

| Attribute | Description |
| --- | --- |
| data-flux-date-picker | Applied to the root element for styling and identification. |



### [flux:date-picker.input](#fluxdate-pickerinput)

| Prop | Description |
| --- | --- |
| label | Label text displayed above the input. When provided, wraps the input in a flux:field component with an adjacent flux:label component. |
| description | Help text displayed below the input. When provided alongside label, appears between the label and input within the flux:field wrapper. |
| placeholder | Placeholder text displayed when no date is selected. |
| clearable | Displays a clear button when a date is selected. |
| disabled | Prevents user interaction with the input. |
| invalid | Applies error styling to the input. |



### [flux:date-picker.button](#fluxdate-pickerbutton)

| Prop | Description |
| --- | --- |
| placeholder | Text displayed when no date is selected. |
| size | Size of the button. Options: sm, xs. |
| clearable | Displays a clear button when a date is selected. |
| disabled | Prevents user interaction with the button. |
| invalid | Applies error styling to the button. |



### [DateRange Object](#daterange-object)

A specialized object for handling date ranges when using mode="range".

| Method | Description |
| --- | --- |
| $range->start() | Get the start date as a Carbon instance. |
| $range->end() | Get the end date as a Carbon instance. |
| $range->days() | Get the number of days in the range. |
| $range->preset() | Get the current preset as a DateRangePreset enum value. |
| $range->toArray() | Get the range as an array with start and end keys. |

| Static Method | Description |
| --- | --- |
| DateRange::today() | Create a DateRange for today. |
| DateRange::yesterday() | Create a DateRange for yesterday. |
| DateRange::thisWeek() | Create a DateRange for the current week. |
| DateRange::lastWeek() | Create a DateRange for the previous week. |
| DateRange::last7Days() | Create a DateRange for the last 7 days. |
| DateRange::last30Days() | Create a DateRange for the last 30 days. |
| DateRange::thisMonth() | Create a DateRange for the current month. |
| DateRange::lastMonth() | Create a DateRange for the previous month. |
| DateRange::thisQuarter() | Create a DateRange for the current quarter. |
| DateRange::lastQuarter() | Create a DateRange for the previous quarter. |
| DateRange::thisYear() | Create a DateRange for the current year. |
| DateRange::lastYear() | Create a DateRange for the previous year. |
| DateRange::yearToDate() | Create a DateRange from January 1st to today. |
| DateRange::tomorrow() | Create a DateRange for tomorrow. |
| DateRange::nextWeek() | Create a DateRange for next week. |
| DateRange::next7Days() | Create a DateRange for the next 7 days. |
| DateRange::next30Days() | Create a DateRange for the next 30 days. |
| DateRange::nextMonth() | Create a DateRange for next month. |
| DateRange::nextQuarter() | Create a DateRange for next quarter. |
| DateRange::nextYear() | Create a DateRange for next year. |
| DateRange::allTime() | Create a DateRange with no limits. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0025_Dropdown

# Dropdown

A composable dropdown component that can handle both simple navigation menus as well as complex action menus with checkboxes, radios, and submenus.





Options

New post

Sort by



Name

Date

Popularity

Filter



Draft

Published

Archived

Delete





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Options</flux:button>    <flux:menu>        <flux:menu.item icon="plus">New post</flux:menu.item>        <flux:menu.separator />        <flux:menu.submenu heading="Sort by">            <flux:menu.radio.group>                <flux:menu.radio checked>Name</flux:menu.radio>                <flux:menu.radio>Date</flux:menu.radio>                <flux:menu.radio>Popularity</flux:menu.radio>            </flux:menu.radio.group>        </flux:menu.submenu>        <flux:menu.submenu heading="Filter">            <flux:menu.checkbox checked>Draft</flux:menu.checkbox>            <flux:menu.checkbox checked>Published</flux:menu.checkbox>            <flux:menu.checkbox>Archived</flux:menu.checkbox>        </flux:menu.submenu>        <flux:menu.separator />        <flux:menu.item variant="danger" icon="trash">Delete</flux:menu.item>    </flux:menu></flux:dropdown>
```



## [Navigation menus](#navigation-menus)

Display a simple set of links in a dropdown menu.



Use the navmenu component for a simple collections of links. Otherwise, use the menu component for action menus that require keyboard navigation, submenus, etc.





Olivia Martin







Copy to clipboard

```
<flux:dropdown position="bottom" align="end">    <flux:profile avatar="/img/demo/user.png" name="Olivia Martin" />    <flux:navmenu>        <flux:navmenu.item href="#" icon="user">Account</flux:navmenu.item>        <flux:navmenu.item href="#" icon="building-storefront">Profile</flux:navmenu.item>        <flux:navmenu.item href="#" icon="credit-card">Billing</flux:navmenu.item>        <flux:navmenu.item href="#" icon="arrow-right-start-on-rectangle">Logout</flux:navmenu.item>        <flux:navmenu.item href="#" icon="trash" variant="danger">Delete</flux:navmenu.item>    </flux:navmenu></flux:dropdown>
```



## [Positioning](#positioning)

Customize the position of the dropdown menu via the position and align props. You can first pass the base position: top, bottom, left, and right, then an alignment modifier like start, center, or end.









Copy to clipboard

```
<flux:dropdown position="top" align="start"><!-- More positions... --><flux:dropdown position="right" align="center"><flux:dropdown position="bottom" align="center"><flux:dropdown position="left" align="end">
```



## [Offset & gap](#offset-gap)

Customize the offset/gap of the dropdown menu via the offset and gap props. These properties accept values in pixels.









Copy to clipboard

```
<flux:dropdown offset="-15" gap="2">
```



## [Keyboard hints](#keyboard-hints)

Add keyboard shortcut hints to menu items to teach users how to navigate your app faster.





Options

Save

⌘S



Duplicate

⌘D



Delete

⌘⌫







Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Options</flux:button>    <flux:menu>        <flux:menu.item icon="pencil-square" kbd="⌘S">Save</flux:menu.item>        <flux:menu.item icon="document-duplicate" kbd="⌘D">Duplicate</flux:menu.item>        <flux:menu.item icon="trash" variant="danger" kbd="⌘⌫">Delete</flux:menu.item>    </flux:menu></flux:dropdown>
```



## [Checkbox items](#checkbox-items)

Select one or many menu options.





Permissions

Read

Write

Delete





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Permissions</flux:button>    <flux:menu>        <flux:menu.checkbox wire:model="read" checked>Read</flux:menu.checkbox>        <flux:menu.checkbox wire:model="write" checked>Write</flux:menu.checkbox>        <flux:menu.checkbox wire:model="delete">Delete</flux:menu.checkbox>    </flux:menu></flux:dropdown>
```



## [Radio items](#radio-items)

Select a single menu option.





Sort by

Latest activity

Date created

Most popular





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Sort by</flux:button>    <flux:menu>        <flux:menu.radio.group wire:model="sortBy">            <flux:menu.radio checked>Latest activity</flux:menu.radio>            <flux:menu.radio>Date created</flux:menu.radio>            <flux:menu.radio>Most popular</flux:menu.radio>        </flux:menu.radio.group>    </flux:menu></flux:dropdown>
```



## [Groups](#groups)

Visually group related menu items with a separator line.





Options

View

Transfer

Publish

Share

Delete





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Options</flux:button>    <flux:menu>        <flux:menu.item>View</flux:menu.item>        <flux:menu.item>Transfer</flux:menu.item>        <flux:menu.separator />        <flux:menu.item>Publish</flux:menu.item>        <flux:menu.item>Share</flux:menu.item>        <flux:menu.separator />        <flux:menu.item variant="danger">Delete</flux:menu.item>    </flux:menu></flux:dropdown>
```



## [Groups with headings](#groups-with-headings)

Group options under headings to make them more discoverable.





Options

Account

Profile

Permissions

Billing

Transactions

Payouts

Refunds

Logout





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Options</flux:button>    <flux:menu>        <flux:menu.group heading="Account">            <flux:menu.item>Profile</flux:menu.item>            <flux:menu.item>Permissions</flux:menu.item>        </flux:menu.group>        <flux:menu.group heading="Billing">            <flux:menu.item>Transactions</flux:menu.item>            <flux:menu.item>Payouts</flux:menu.item>            <flux:menu.item>Refunds</flux:menu.item>        </flux:menu.group>        <flux:menu.item>Logout</flux:menu.item>    </flux:menu></flux:dropdown>
```



## [Submenus](#submenus)

Nest submenus for more condensed menus.





Options

Sort by



Name

Date

Popularity

Filter



Draft

Published

Archived

Delete





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Options</flux:button>    <flux:menu>        <flux:menu.submenu heading="Sort by">            <flux:menu.radio checked>Name</flux:menu.radio>            <flux:menu.radio>Date</flux:menu.radio>            <flux:menu.radio>Popularity</flux:menu.radio>        </flux:menu.submenu>        <flux:menu.submenu heading="Filter">            <flux:menu.checkbox checked>Draft</flux:menu.checkbox>            <flux:menu.checkbox checked>Published</flux:menu.checkbox>            <flux:menu.checkbox>Archived</flux:menu.checkbox>        </flux:menu.submenu>        <flux:menu.separator />        <flux:menu.item variant="danger">Delete</flux:menu.item>    </flux:menu></flux:dropdown>
```



## [Keep open](#keep-open)

Menus typically close when an item is clicked, however, you can add the keep-open attribute to the menu component to keep it open.





Filter

Draft

Published

Archived





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Filter</flux:button>    <flux:menu keep-open>        <flux:menu.checkbox checked>Draft</flux:menu.checkbox>        <flux:menu.checkbox checked>Published</flux:menu.checkbox>        <flux:menu.checkbox>Archived</flux:menu.checkbox>    </flux:menu></flux:dropdown>
```

If you want the menu to only stay open when a specific item is clicked, you can add the keep-open attribute to the item instead. This works with:

- menu.item
- menu.checkbox
- menu.radio
- menu.radio.group
- menu.submenu





Filters

Draft

Published

Archived

Clear





Copy to clipboard

```
<flux:dropdown>    <flux:button icon:trailing="chevron-down">Filters</flux:button>    <flux:menu >        <flux:menu.checkbox keep-open checked>Draft</flux:menu.checkbox>        <flux:menu.checkbox keep-open checked>Published</flux:menu.checkbox>        <flux:menu.checkbox keep-open>Archived</flux:menu.checkbox>        <flux:menu.separator />        <flux:menu.item variant="danger">Clear</flux:menu.item>    </flux:menu></flux:dropdown>
```

## Related components

[Navbar Build responsive navigation bars with dropdown menus](/components/navbar) [Profile Show user avatars and profile information](/components/profile) [Button Interactive controls for forms and UI actions](/components/button)

## Reference



### [flux:dropdown](#fluxdropdown)

| Prop | Description |
| --- | --- |
| position | Position of the dropdown menu. Options: top, right, bottom (default), left. |
| align | Alignment of the dropdown menu. Options: start, center, end. Default: start. |
| offset | Offset in pixels from the trigger element. Default: 0. |
| gap | Gap in pixels between trigger and menu. Default: 4. |

| Attribute | Description |
| --- | --- |
| data-flux-dropdown | Applied to the root element for styling and identification. |



### [flux:menu](#fluxmenu)

A complex menu component that supports keyboard navigation, submenus, checkboxes, and radio buttons.

| Prop | Description |
| --- | --- |
| keep-open | Prevents the menu from closing when any item inside of it is clicked. |

| Slot | Description |
| --- | --- |
| default | The menu items, separators, and submenus. |

| Attribute | Description |
| --- | --- |
| data-flux-menu | Applied to the root element for styling and identification. |



### [flux:menu.item](#fluxmenuitem)

| Prop | Description |
| --- | --- |
| icon | Name of the icon to display at the start of the item. |
| icon:trailing | Name of the icon to display at the end of the item. |
| icon:variant | Variant of the icon. Options: outline, solid, mini, micro. |
| kbd | Keyboard shortcut hint displayed at the end of the item. |
| suffix | Text displayed at the end of the item. |
| variant | Visual style of the item. Options: default, danger. |
| disabled | If true, prevents interaction with the menu item. |
| keep-open | Prevents the menu from closing when this item is selected. |

| Attribute | Description |
| --- | --- |
| data-flux-menu-item | Applied to the root element for styling and identification. |
| data-active | Applied when the item is hovered/active. |



### [flux:menu.submenu](#fluxmenusubmenu)

| Prop | Description |
| --- | --- |
| heading | Text displayed as the submenu heading. |
| icon | Name of the icon to display at the start of the submenu. |
| icon:trailing | Name of the icon to display at the end of the submenu. |
| icon:variant | Variant of the icon. Options: outline, solid, mini, micro. |
| keep-open | Prevents the submenu from closing when any item inside of it is selected. |

| Slot | Description |
| --- | --- |
| default | The submenu items (checkboxes, radio buttons, etc.). |



### [flux:menu.separator](#fluxmenuseparator)

A horizontal line that separates menu items.



### [flux:menu.checkbox.group](#fluxmenucheckboxgroup)

| Prop | Description |
| --- | --- |
| wire:model | Binds the checkbox group to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |

| Slot | Description |
| --- | --- |
| default | The checkboxes. |



### [flux:menu.checkbox](#fluxmenucheckbox)

| Prop | Description |
| --- | --- |
| wire:model | Binds the checkbox to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| checked | If true, the checkbox is checked by default. |
| disabled | If true, prevents interaction with the checkbox. |
| keep-open | Prevents the menu from closing when this checkbox is selected. |

| Attribute | Description |
| --- | --- |
| data-active | Applied when the checkbox is hovered/active. |
| data-checked | Applied when the checkbox is checked. |



### [flux:menu.radio.group](#fluxmenuradiogroup)

| Prop | Description |
| --- | --- |
| wire:model | Binds the radio group to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| keep-open | Prevents the menu from closing when any radio button in this group is selected. |

| Slot | Description |
| --- | --- |
| default | The radio buttons. |



### [flux:menu.radio](#fluxmenuradio)

| Prop | Description |
| --- | --- |
| checked | If true, the radio button is selected by default. |
| disabled | If true, prevents interaction with the radio button. |
| keep-open | Prevents the menu from closing when this radio button is selected. |

| Attribute | Description |
| --- | --- |
| data-active | Applied when the radio button is hovered/active. |
| data-checked | Applied when the radio button is selected. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0026_Editor



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Rich text editor

A basic rich text editor for your application. Built using [ProseMirror](https://prosemirror.net) and [Tiptap](https://tiptap.dev/).

Because of large external dependencies, the editor's JavaScript is not included in the core Flux bundle. It will be loaded on-the-fly as a separate JS file when you use the flux:editor component.





Release notes Explain what's new in this release.


Text



Styles

Text

Heading 1

Heading 2

Heading 3

Bold ⌘B

Italic ⌘I

Strikethrough ⌘+Shift+S

Bullet list

Ordered list

Blockquote ⌘+Shift+B

Insert link ⌘K

Insert link

Unlink

Left



Align

Left

Center

Right

### What's changed

- Markdown notation support
- Accessible toolbar
- Shortcut keys
**Full changelog:** [v1.0.25...v1.0.26](https://github.com/livewire/flux/compare/v1.0.25...v1.0.26)





Copy to clipboard

```
<flux:editor wire:model="content" label="…" description="…" />
```



## [Toolbar](#toolbar)

Flux's editor toolbar is both keyboard/screen-reader accessible and completely customizable to suit your application's needs.



## Configuring items

You can configure which toolbar items are visible, and in what order, by passing in a space-separated list of items to the toolbar prop.





Text



Styles

Text

Heading 1

Heading 2

Heading 3

Bold ⌘B

Italic ⌘I

Underline ⌘U

Left



Align

Left

Center

Right

Undo ⌘Z

Redo ⌘+Shift+Z





Copy to clipboard

```
<flux:editor toolbar="heading | bold italic underline | align ~ undo redo" />
```

You may have noticed the | and ~ characters in the toolbar configuration. These are shorthand for separator and spacer respectively.

The following toolbar items are available:

- heading
- bold
- italic
- strike
- underline
- bullet
- ordered
- blockquote
- subscript
- superscript
- highlight
- link
- code
- undo
- redo



## Custom items

You can add your own toolbar items by adding new files to the resources/views/flux/editor directory in your project.

```
- resources    - views        - flux            - editor                - copy.blade.php
```

Here's an example of what a custom "Copy to clipboard" item in a blade file might look like:



Copy to clipboard

```
<flux:tooltip content="{{ __('Copy to clipboard') }}" class="contents">    <flux:editor.button x-on:click="navigator.clipboard?.writeText($el.closest('[data-flux-editor]').value); $el.setAttribute('data-copied', ''); setTimeout(() => $el.removeAttribute('data-copied'), 2000)">        <flux:icon.clipboard variant="outline" class="[[data-copied]_&]:hidden size-5!" />        <flux:icon.clipboard-document-check variant="outline" class="hidden [[data-copied]_&]:block size-5!" />    </flux:editor.button></flux:tooltip>
```

Now you can reference your new component by name in any toolbar configuration like so:





Text



Styles

Text

Heading 1

Heading 2

Heading 3

Bold ⌘B

Italic ⌘I

Strikethrough ⌘+Shift+S

Bullet list

Ordered list

Blockquote ⌘+Shift+B

Insert link ⌘K

Insert link

Unlink

Left



Align

Left

Center

Right

Copy to clipboard





Copy to clipboard

```
<flux:editor toolbar="heading | […] | align ~ copy" />
```



## Customization

If you have deeper customization needs, you can compose your own editor component. Here's an example of putting a custom dropdown menu in an editor's toolbar:





Text



Styles

Text

Heading 1

Heading 2

Heading 3

Bold ⌘B

Italic ⌘I

Strikethrough ⌘+Shift+S

Bullet list

Ordered list

Blockquote ⌘+Shift+B

Insert link ⌘K

Insert link

Unlink

Left



Align

Left

Center

Right

More

Preview

Export

Share





Copy to clipboard

```
<flux:editor>    <flux:editor.toolbar>        <flux:editor.heading />        <flux:editor.separator />        <flux:editor.bold />        <flux:editor.italic />        <flux:editor.strike />        <flux:editor.separator />        <flux:editor.bullet />        <flux:editor.ordered />        <flux:editor.blockquote />        <flux:editor.separator />        <flux:editor.link />        <flux:editor.separator />        <flux:editor.align />        <flux:editor.spacer />        <flux:dropdown position="bottom end" offset="-15">            <flux:editor.button icon="ellipsis-horizontal" tooltip="More" />            <flux:menu>                <flux:menu.item wire:click="…" icon="arrow-top-right-on-square">Preview</flux:menu.item>                <flux:menu.item wire:click="…" icon="arrow-down-tray">Export</flux:menu.item>                <flux:menu.item wire:click="…" icon="share">Share</flux:menu.item>            </flux:menu>        </flux:dropdown>    </flux:editor.toolbar>    <flux:editor.content /></flux:editor>
```



## [Height](#height)

By default, the editor will have a minimum height of 200px, and a maximum height of 500px. If you want to customize this behavior, you can use Tailwind utilties to target the content slot and set your own min/max height and overflow behavior.





Text



Styles

Text

Heading 1

Heading 2

Heading 3

Bold ⌘B

Italic ⌘I

Strikethrough ⌘+Shift+S

Bullet list

Ordered list

Blockquote ⌘+Shift+B

Insert link ⌘K

Insert link

Unlink

Left



Align

Left

Center

Right





Copy to clipboard

```
<flux:editor class="**:data-[slot=content]:min-h-[100px]!" />
```

The [&_[data-slot=content]]: selector targets a child element with a data-slot="content" attribute.

This is an advanced Tailwind technique used to style a nested element inline without needing direct access to it.



## [Shortcut keys](#shortcut-keys)

Flux's editor uses Tiptap's default shortcut keys which are common amongst most rich text editors.

| Operation | Windows/Linux | Mac |
| --- | --- | --- |
| Apply paragraph style | Ctrl+Alt+0 | Cmd+Alt+0 |
| Apply heading level 1 | Ctrl+Alt+1 | Cmd+Alt+1 |
| Apply heading level 2 | Ctrl+Alt+2 | Cmd+Alt+2 |
| Apply heading level 3 | Ctrl+Alt+3 | Cmd+Alt+3 |
| Bold | Ctrl+B | Cmd+B |
| Italic | Ctrl+I | Cmd+I |
| Underline | Ctrl+U | Cmd+U |
| Strikethrough | Ctrl+Shift+X | Cmd+Shift+X |
| Bullet list | Ctrl+Shift+8 | Cmd+Shift+8 |
| Ordered list | Ctrl+Shift+7 | Cmd+Shift+7 |
| Blockquote | Ctrl+Shift+B | Cmd+Shift+B |
| Code | Ctrl+E | Cmd+E |
| Highlight | Ctrl+Shift+H | Cmd+Shift+H |
| Align left | Ctrl+Shift+L | Cmd+Shift+L |
| Align center | Ctrl+Shift+E | Cmd+Shift+E |
| Align right | Ctrl+Shift+R | Cmd+Shift+R |
| Paste without formatting | Ctrl+Shift+V | Cmd+Shift+V |
| Add a line break | Ctrl+Shift+Enter | Cmd+Shift+Enter |
| Undo | Ctrl+Z | Cmd+Z |
| Redo | Ctrl+Shift+Z | Cmd+Shift+Z |



## [Markdown syntax](#markdown-syntax)

Although Flux's editor isn't a markdown editor itself, it allows you to use markdown syntax to trigger styling changes while authoring your content.

| Markdown | Operation |
| --- | --- |
| # | Apply heading level 1 |
| ## | Apply heading level 2 |
| ### | Apply heading level 3 |
| ** | Bold |
| * | Italic |
| ~~ | Strikethrough |
| - | Bullet list |
| 1. | Ordered list |
| > | Blockquote |
| ` | Inline code |
| ``` | Code block |
| ```? | Code block (with class="language-?") |
| --- | Horizontal rule |



## [Localization](#localization)

If you need to localize the editor's aria-label or tooltip copy, you'll need to register the following translation keys in one of your app's lang files.

Here's an example of supporting Spanish localization:

```
// lang/es.json{    "Rich text editor": "Editor de texto enriquecido",    "Formatting": "Formato",    "Text": "Texto",    "Heading 1": "Encabezado 1",    "Heading 2": "Encabezado 2",    "Heading 3": "Encabezado 3",    "Styles": "Estilos",    "Bold": "Negrita",    "Italic": "Cursiva",    "Underline": "Subrayado",    "Strikethrough": "Tachado",    "Subscript": "Subíndice",    "Superscript": "Superíndice",    "Highlight": "Resaltar",    "Code": "Código",    "Bullet list": "Lista con viñetas",    "Ordered list": "Lista numerada",    "Blockquote": "Cita",    "Insert link": "Insertar enlace",    "Unlink": "Quitar enlace",    "Align": "Alinear",    "Left": "Izquierda",    "Center": "Centro",    "Right": "Derecha",    "Undo": "Deshacer",    "Redo": "Rehacer"}
```



## [Extensions](#extensions)

Tiptap has a wide range of extensions that can be used to add custom functionality to the editor.

The following extensions are already installed:

- Highlight
- Link
- Placeholder
- StarterKit
- Superscript
- Subscript
- TextAlign
- Underline

But you can also add your own extensions, disable built-in extensions, or modify the behavior of the editor.



## Set up listener

To do this, you'll first need to create a listener for the flux:editor event in the <head> tag in your layout.



Copy to clipboard

```
<head>    ...    </head>
```

Or you can add the listener to your app.js file.



Copy to clipboard

```
...document.addEventListener('flux:editor', (e) => {    ...})
```



## Registering extensions

Once you have the listener set up, you can add extensions by passing an array of extensions to the registerExtensions method supplied by the flux:editor event.

If an extension already exists, it will be replaced.



Copy to clipboard

```
import Youtube from 'https://cdn.jsdelivr.net/npm/@tiptap/[[email protected]](/cdn-cgi/l/email-protection)/+esm'document.addEventListener('flux:editor', (e) => {    e.detail.registerExtensions([        Youtube.configure({            controls: false,            nocookie: true,        }),    ])})
```



## Disabling extensions

If you need to disable an extension that comes with the editor, you can disable an extension by calling the disableExtension method supplied by the flux:editor event and passing through the name of the extension.



Copy to clipboard

```
document.addEventListener('flux:editor', (e) => {    e.detail.disableExtension('underline')})
```



## Accessing the instance

Sometimes you may need to access the Tiptap instance directly to register event listeners or otherwise interact with with the instance.

You can do so by passing a callback to the init method supplied by the flux:editor event and accessing the editor instance from within the callback.

The init callback will be called when Tiptap's beforeCreate event is fired. You can find more details about Tiptap's events in the [Tiptap documentation](https://tiptap.dev/docs/editor/api/events).



Copy to clipboard

```
document.addEventListener('flux:editor', (e) => {    e.detail.init(({ editor }) => {        editor.on('create', () => {})        editor.on('update', () => {})        editor.on('selectionUpdate', () => {})        editor.on('transaction', () => {})        editor.on('focus', () => {})        editor.on('blur', () => {})        editor.on('destroy', () => {})        editor.on('drop', () => {})        editor.on('paste', () => {})        editor.on('contentError', () => {})    })})
```

## Related components

[Field Structured form field with label](/components/field) [Textarea Multi-line text input areas for longer form content](/components/textarea)

## Reference



### [flux:editor](#fluxeditor)

| Prop | Description |
| --- | --- |
| wire:model | Binds the editor to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| value | Initial content for the editor. Used when not binding with wire:model. |
| label | Label text displayed above the editor. When provided, wraps the editor in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the editor. When provided alongside label, appears between the label and editor within the flux:field wrapper. See the [field component](/components/field). |
| description:trailing | The description provided will be displayed below the editor instead of above it. |
| badge | Badge text displayed at the end of the flux:label component when the label prop is provided. |
| placeholder | Placeholder text displayed when the editor is empty. |
| toolbar | Space-separated list of toolbar items to display. Use \| for separator and ~ for spacer. By default, includes heading, bold, italic, strike, bullet, ordered, blockquote, link, and align tools. |
| disabled | Prevents user interaction with the editor. |
| invalid | Applies error styling to the editor. |

| Slot | Description |
| --- | --- |
| default | The editor content and toolbar components. If omitted, the standard toolbar and an empty content area will be used. |

| Attribute | Description |
| --- | --- |
| data-flux-editor | Applied to the root element for styling and identification. |



### [flux:editor.toolbar](#fluxeditortoolbar)

Container for editor toolbar items. Can be used for custom toolbar layouts.

| Prop | Description |
| --- | --- |
| items | Space-separated list of toolbar items to display. Use \| for separator and ~ for spacer. If not provided, displays the default toolbar. |

| Slot | Description |
| --- | --- |
| default | The toolbar items, separators, and spacers. Use this slot to create a completely custom toolbar. |



### [flux:editor.button](#fluxeditorbutton)

| Prop | Description |
| --- | --- |
| icon | Name of the icon to display in the button. |
| iconVariant | The variant of the icon to display. Options: mini, micro, outline. Default: mini (without slot) or micro (with slot). |
| tooltip | Text to display in a tooltip when hovering over the button. |
| disabled | Prevents interaction with the button. |

| Slot | Description |
| --- | --- |
| default | Content to display inside the button. If provided alongside an icon, the icon will be displayed before this content. |



### [flux:editor.content](#fluxeditorcontent)

Container for the editor's editable content. Typically used when creating a custom editor layout.

| Slot | Description |
| --- | --- |
| default | The initial HTML content for the editor. This content will be processed and managed by the editor. |



### [Toolbar Items](#toolbar-items)

Available toolbar items that can be referenced in the `toolbar` prop or used directly in a custom toolbar.

| Component | Description |
| --- | --- |
| heading | Heading level selector. |
| bold | Bold text formatting. |
| italic | Italic text formatting. |
| strike | Strikethrough text formatting. |
| underline | Underline text formatting. |
| bullet | Bulleted list. |
| ordered | Numbered list. |
| blockquote | Block quote formatting. |
| code | Code block formatting. |
| link | Link insertion. |
| align | Text alignment options. |
| undo | Undo last action. |
| redo | Redo last action. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0027_Field

# Field

Encapsulate input elements with labels, descriptions, and validation.

Explore the [input component ->](/components/input)





Email





Copy to clipboard

```
<flux:field>    <flux:label>Email</flux:label>    <flux:input wire:model="email" type="email" />    <flux:error name="email" /></flux:field>
```



## [Shorthand props](#shorthand-props)

Because using the field component in its full form can be verbose and repetitive, all form controls in flux allow you pass a label and a description parameter directly. Under the hood, they will be wrapped in a field with an error component automatically.



Copy to clipboard

```
<flux:input wire:model="email" label="Email" type="email" />
```



## [With trailing description](#with-trailing-description)

Position the field description directly below the input.





Password

Must be at least 8 characters long, include an uppercase letter, a number, and a special character.





Copy to clipboard

```
<flux:field>    <flux:label>Password</flux:label>    <flux:input type="password" />    <flux:error name="password" />    <flux:description>Must be at least 8 characters long, include an uppercase letter, a number, and a special character.</flux:description></flux:field><!-- Alternative shorthand syntax... --><flux:input    type="password"    label="Password"    description:trailing="Must be at least 8 characters long, include an uppercase letter, a number, and a special character."/>
```



## [With badge](#with-badge)

Badges allow you to enhance a field with additional information such as being "required" or "optional" when it might not be expected.





Email Required

Phone number Optional





Copy to clipboard

```
<flux:field>    <flux:label badge="Required">Email</flux:label>    <flux:input type="email" required />    <flux:error name="email" /></flux:field><flux:field>    <flux:label badge="Optional">Phone number</flux:label>    <flux:input type="phone" placeholder="(555) 555-5555" mask="(999) 999-9999"  />    <flux:error name="phone" /></flux:field>
```



## [Split layout](#split-layout)

Display multiple fields horizontally in the same row.





First name

Last name





Copy to clipboard

```
<div class="grid grid-cols-2 gap-4">    <flux:input label="First name" placeholder="River" />    <flux:input label="Last name" placeholder="Porzio" /></div>
```



## [Fieldset](#fieldset)

Group related fields using the fieldset and legend component.





Shipping address


Street address line 1

Street address line 2

City

State / Province

Postal / Zip code

Country * United States





Copy to clipboard

```
<flux:fieldset>    <flux:legend>Shipping address</flux:legend>    <div class="space-y-6">        <flux:input label="Street address line 1" placeholder="123 Main St" class="max-w-sm" />        <flux:input label="Street address line 2" placeholder="Apartment, studio, or floor" class="max-w-sm" />        <div class="grid grid-cols-2 gap-x-4 gap-y-6">            <flux:input label="City" placeholder="San Francisco" />            <flux:input label="State / Province" placeholder="CA" />            <flux:input label="Postal / Zip code" placeholder="12345" />            <flux:select label="Country">                <option selected>United States</option>                <!-- ... -->            </flux:select>        </div>    </div></flux:fieldset>
```

## Related components

[Input Text fields for collecting user input](/components/input) [Textarea Multi-line text input areas for longer form content](/components/textarea) [Switch Toggleable input control for making selections](/components/switch)

## Reference



### [flux:field](#fluxfield)

A container component that provides structure for form inputs with labels, descriptions, and error messages.

| Prop | Description |
| --- | --- |
| variant | Visual style variant. Options: block, inline. Default: block. |

| Slot | Description |
| --- | --- |
| default | The form control elements (input, select, etc.) and their associated labels, descriptions, and error messages. |

| Attribute | Description |
| --- | --- |
| data-flux-field | Applied to the root element for styling and identification. |



### [flux:label](#fluxlabel)

| Prop | Description |
| --- | --- |
| badge | Optional text to display as a badge (e.g., "Required", "Optional"). |

| Slot | Description |
| --- | --- |
| default | The label text content. |
| trailing | Optional text to display at the end of the label. |



### [flux:description](#fluxdescription)

| Slot | Description |
| --- | --- |
| default | The descriptive text content. |



### [flux:error](#fluxerror)

| Prop | Description |
| --- | --- |
| name | The name of the field to display validation errors for. |
| message | Custom error message content (optional). |
| bag | The error bag to get the error from. Default: default. |
| deep | Whether to look for validation errors in nested array fields (e.g., fields.*). If false, only shows errors for the exact field name specified. Default: true. |
| icon | The icon to display inline with the error message. Default: exclamation-triangle. Set to false to hide the icon. |

| Slot | Description |
| --- | --- |
| default | Custom error message content (optional). |



### [flux:fieldset](#fluxfieldset)

| Prop | Description |
| --- | --- |
| legend | The fieldset's heading text. |
| description | Optional description text for the fieldset. |

| Slot | Description |
| --- | --- |
| default | The grouped form fields and their associated legend. |



### [flux:legend](#fluxlegend)

| Slot | Description |
| --- | --- |
| default | The fieldset's heading text. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0028_File upload



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# File upload

A flexible file upload component with built-in drag-and-drop support, file previews, and Livewire integration for handling file uploads in your application.





Upload files

Drop files here or click to browse

JPG, PNG, GIF up to 10MB

Profile_pic.jpg

159 KB





Copy to clipboard

```
<flux:file-upload wire:model="photos" multiple label="Upload files">    <flux:file-upload.dropzone        heading="Drop files here or click to browse"        text="JPG, PNG, GIF up to 10MB"    /></flux:file-upload><div class="mt-4 flex flex-col gap-2">    <flux:file-item        heading="Profile_pic.jpg"        image="https://fluxui.dev/img/demo/user.png"        size="162400"    >        <x-slot name="actions">            <flux:file-item.remove />        </x-slot>    </flux:file-item></div>
```



## [Inline layout](#inline-layout)

For a more compact interface, use the inline prop on the dropzone to create a horizontal layout that takes up less vertical space.





Upload files

Drop files or click to browse

JPG, PNG, GIF up to 10MB

Profile_pic.jpg

Brand_banner.jpg





Copy to clipboard

```
<flux:file-upload wire:model="photos" multiple label="Upload files">    <flux:file-upload.dropzone        heading="Drop files or click to browse"        text="JPG, PNG, GIF up to 10MB"        inline    /></flux:file-upload><div class="mt-3 flex flex-col gap-2">    <flux:file-item heading="Profile_pic.jpg">        <x-slot name="actions">            <flux:file-item.remove />        </x-slot>    </flux:file-item>    <flux:file-item heading="Brand_banner.jpg">        <x-slot name="actions">            <flux:file-item.remove />        </x-slot>    </flux:file-item></div>
```



## [Progress indicator](#progress-indicator)

Use the with-progress on the dropzone to show a progress indicator while the file is uploading.

The text prop is required with the progress indicator.





Upload files

Drop files or click to browse



JPG, PNG, GIF up to 10MB





Copy to clipboard

```
<flux:file-upload wire:model="photos" multiple label="Upload files">    <flux:file-upload.dropzone        heading="Drop files or click to browse"        text="JPG, PNG, GIF up to 10MB"        with-progress        inline    /></flux:file-upload>
```

When using with-progress, the component provides two CSS variables that you can use for custom progress implementations:

- --flux-file-upload-progress - The progress percentage as a decimal (e.g., "42%")
- --flux-file-upload-progress-as-string - The progress percentage as a quoted string (e.g., "'42%'")


These variables are automatically updated during upload and can be used in your custom CSS to create progress bars, circular indicators, or any other visual feedback you need.



## [Disabled state](#disabled-state)

Use the disabled prop to prevent user interaction with the file upload component. When disabled, the dropzone becomes unclickable, drag-and-drop is disabled, and the UI appears in a muted state to indicate it's inactive.





Upload files

Drop files or click to browse

JPG, PNG, GIF up to 10MB





Copy to clipboard

```
<flux:file-upload wire:model="photos" multiple label="Upload files" disabled>    <flux:file-upload.dropzone        heading="Drop files or click to browse"        text="JPG, PNG, GIF up to 10MB"        inline    /></flux:file-upload>
```



## [Custom uploader](#custom-uploader)

The flux:file-upload wrapper handles all the complex file upload functionality - drag and drop, file selection, and upload progress. You can place any custom HTML inside it to completely customize the appearance while maintaining all the upload behavior.

Here's an example of a custom avatar uploader:









Copy to clipboard

```
<flux:file-upload wire:model="photo">    <!-- Custom avatar uploader -->    <div class="        relative flex items-center justify-center size-20 rounded-full transition-colors cursor-pointer        border border-zinc-200 dark:border-white/10 hover:border-zinc-300 dark:hover:border-white/10        bg-zinc-100 hover:bg-zinc-200 dark:bg-white/10 hover:dark:bg-white/15 in-data-dragging:dark:bg-white/15    ">        <!-- Show the uploaded file if it exists -->        @if ($photo)            <img src="{{ $photo?->temporaryUrl() }}" class="size-full object-cover rounded-full" />        @else            <!-- Show the default icon if no file is uploaded -->            <flux:icon name="user" variant="solid" class="text-zinc-500 dark:text-zinc-400" />        @endif        <!-- Corner upload icon -->        <div class="absolute bottom-0 right-0 bg-white dark:bg-zinc-800 rounded-full">            <flux:icon name="arrow-up-circle" variant="solid" class="text-zinc-500 dark:text-zinc-400" />        </div>    </div></flux:file-upload>
```

The file upload wrapper automatically provides data attributes you can use to style your custom uploader:

- data-dragging - Present when a file is being dragged over the upload area
- data-loading - Present while files are being uploaded


These attributes can be targeted with CSS using the in-data-dragging: and in-data-loading: utility prefixes to create dynamic visual feedback during drag and upload states.



## [Livewire integration](#livewire-integration)

The file upload component seamlessly integrates with Livewire's file upload functionality. Use the wire:model directive to bind uploaded files to your Livewire component properties.

### [Single file upload](#single-file)

For single file uploads, bind directly to a property and handle the uploaded file display and removal.



Copy to clipboard

```
use Livewire\Component;use Livewire\WithFileUploads;use Livewire\Attributes\Validate;class FileUpload extends Component {    use WithFileUploads;    #[Validate('image|max:10240')] // 10MB Max    public $photo;    public function removePhoto()    {        $this->photo->delete();        $this->photo = null;    }    public function save()    {        $this->photo->store(path: 'photos');        return $this->redirect('...');    }}
```



Copy to clipboard

```
<!-- Blade view: --><form wire:submit="save">    <flux:file-upload wire:model="photo" label="Upload file">        <flux:file-upload.dropzone heading="Drop file here or click to browse" text="JPG, PNG, GIF up to 10MB" />    </flux:file-upload>    <div class="mt-3 flex flex-col gap-2">        @if ($photo)            <flux:file-item                :heading="$photo->getClientOriginalName()"                :image="$photo->temporaryUrl()"                :size="$photo->getSize()"            >                <x-slot name="actions">                    <flux:file-item.remove wire:click="removePhoto" aria-label="{{ 'Remove file: ' . $photo->getClientOriginalName() }}" />                </x-slot>            </flux:file-item>        @endif    </div>    <flux:button type="submit">Save</flux:button></form>
```

### [Multiple files upload](#multiple-files)

Handle multiple file uploads by using an array property and the multiple attribute.



Copy to clipboard

```
use Livewire\Component;use Livewire\WithFileUploads;use Livewire\Attributes\Validate;class FileUpload extends Component {    use WithFileUploads;    #[Validate(['photos.*' => 'image|max:1024'])]    public $photos = [];    public function removePhoto($index)    {        $photo = $this->photos[$index];        $photo->delete();        unset($this->photos[$index]);        $this->photos = array_values($this->photos);    }    public function save()    {        foreach ($this->photos as $photo) {            $photo->store(path: 'photos');        }        return $this->redirect('...');    }}
```



Copy to clipboard

```
<!-- Blade view: --><form wire:submit="save">    <flux:file-upload wire:model="photos" label="Upload files" multiple>        <flux:file-upload.dropzone heading="Drop files here or click to browse" text="JPG, PNG, GIF up to 10MB" />    </flux:file-upload>    <div class="mt-3 flex flex-col gap-2">        @foreach ($photos as $index => $photo)            <flux:file-item                :heading="$photo->getClientOriginalName()"                :image="$photo->temporaryUrl()"                :size="$photo->getSize()"            >                <x-slot name="actions">                    <flux:file-item.remove wire:click="removePhoto({{ $index }})" aria-label="{{ 'Remove file: ' . $photo->getClientOriginalName() }}" />                </x-slot>            </flux:file-item>        @endforeach    </div>    <flux:button type="submit">Save</flux:button></form>
```

## Related components

[Input Text fields for collecting user input](/components/input) [Field Structured form field with label and validation states](/components/field)

## Reference



### [flux:file-upload](#fluxfile-upload)

The main file upload container component that wraps the upload functionality and integrates with form fields.

| Prop | Description |
| --- | --- |
| name | The input name attribute for form submissions. |
| multiple | If present, allows selecting and uploading multiple files. Default: false. |
| label | Field label text displayed above the upload area. |
| description | Helper text displayed below the field. |
| error | Error message to display for validation failures. |
| disabled | If present, prevents user interaction with the file upload. Default: false. |

| Livewire directive | Description |
| --- | --- |
| wire:model | Binds the file upload to a Livewire property for handling uploaded files. |

| Data attributes | Description |
| --- | --- |
| data-dragging | Automatically added when files are being dragged over the component. Use with Tailwind's in-data-dragging: prefix for styling. |
| data-loading | Automatically added while files are being uploaded. Use with Tailwind's in-data-loading: prefix for styling. |



### [flux:file-upload.dropzone](#fluxfile-uploaddropzone)

The visual drop zone area where users can drag and drop files or click to browse for files.

| Prop | Description |
| --- | --- |
| heading | Main text displayed in the dropzone area. |
| text | Supporting text displayed below the heading (e.g., file type and size restrictions). |
| icon | Icon name to display in the dropzone. Default: cloud-arrow-up. |
| inline | If present, displays the dropzone in a compact horizontal layout. Default: false. |
| with-progress | If present, shows a progress bar during file uploads instead of just a loading spinner. Requires the text prop to be defined. Default: false. |

| CSS variables | Description |
| --- | --- |
| --flux-file-upload-progress | The upload progress percentage (e.g., "42%"). Available when using with-progress. |
| --flux-file-upload-progress-as-string | The upload progress as a quoted string (e.g., "'42%'"). Available when using with-progress. |

| Data attributes | Description |
| --- | --- |
| data-dragging | Present on the file upload element when files are being dragged over the drop zone. |
| data-loading | Present on the file upload element while files are being uploaded. |



### [flux:file-item](#fluxfile-item)

Displays an uploaded file with optional preview image, file details, and actions.

| Prop | Description |
| --- | --- |
| heading | The file name or title to display. |
| text | Additional text to display (automatically calculated from size if not provided). |
| image | URL or path to a preview image for the file. |
| size | File size in bytes. Automatically formatted to B, KB, MB, or GB. |
| icon | Icon to display when no image is provided. Default: document. |
| invalid | If present, displays the file item in an error state. Default: false. |

| Slot | Description |
| --- | --- |
| actions | Slot for action buttons like remove, download, or preview. |



### [flux:file-item.remove](#fluxfile-itemremove)

A pre-styled remove button for file items that can be wired to removal actions.

| Livewire directive | Description |
| --- | --- |
| wire:click | Triggers a Livewire method to remove the file when clicked. |
| aria-label | The aria-label to use for the remove button. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0029_Heading

# Heading

A consistent heading component for your application.





User profile

This information will be displayed publicly.





Copy to clipboard

```
<flux:heading>User profile</flux:heading><flux:text class="mt-2">This information will be displayed publicly.</flux:text>
```



## [Sizes](#sizes)

Flux offers three different heading sizes that should cover most use cases in your app.





Default

14px · Use liberally—think input and toast labels.

Large

16px · Use sparingly—think modal and card headings.

Extra large

24px · Use rarely—think hero text.





Copy to clipboard

```
<flux:heading>Default</flux:heading><flux:heading size="lg">Large</flux:heading><flux:heading size="xl">Extra large</flux:heading>
```



## [Heading level](#heading-level)

Control the heading level: h1, h2, h3, that will be used for the heading element. Without a level prop, the heading will default to a div.





### User profile

This information will be displayed publicly.





Copy to clipboard

```
<flux:heading level="3">User profile</flux:heading><flux:text class="mt-2">This information will be displayed publicly.</flux:text>
```

## Examples



### [Leading subheading](#leading-subheading)

Subheadings can be placed above headings for a more interesting arrangment.





Year to date

$7,532.16

15.2%





Copy to clipboard

```
<div>    <flux:text>Year to date</flux:text>    <flux:heading size="xl" class="mb-1">$7,532.16</flux:heading>    <div class="flex items-center gap-2">        <flux:icon.arrow-trending-up variant="micro" class="text-green-600 dark:text-green-500" />        <span class="text-sm text-green-600 dark:text-green-500">15.2%</span>    </div></div>
```

## Related components

[Text Format paragraphs and textual content with consistent styling](/components/text) [Card Containers for content with consistent styling](/components/card)

## Reference



### [flux:heading](#fluxheading)

| Prop | Description |
| --- | --- |
| size | Size of the heading. Options: base, lg, xl. Default: base. |
| level | HTML heading level. Options: 1, 2, 3, 4. Default: renders as a div if not specified. |
| accent | If true, applies accent color styling to the heading. |



### [flux:text](#fluxtext)

| Prop | Description |
| --- | --- |
| size | Size of the text. Options: sm, base, lg, xl. Default: base. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0030_Icon

# Icon

Flux uses the excellent Heroicons project for its icon collection. Heroicons is a set of beautiful and functional icons crafted by the fine folks at [Tailwind Labs](https://tailwindcss.com)

Search for the exact icon you need over at [Heroicons](https://heroicons.com/)









Copy to clipboard

```
<flux:icon.bolt />
```



## [Variants](#variants)

There are four variants for each icon: outline (default), solid, mini, and micro.









Copy to clipboard

```
<flux:icon.bolt />                  <!-- 24px, outline --><flux:icon.bolt variant="solid" />  <!-- 24px, filled --><flux:icon.bolt variant="mini" />   <!-- 20px, filled --><flux:icon.bolt variant="micro" />  <!-- 16px, filled -->
```



## [Sizes](#sizes)

Control the size (height/width) of an icon using the size-* Tailwind utility.



Avoid tweaking icon sizes. Each variant is specifically designed for its default size.









Copy to clipboard

```
<flux:icon.bolt class="size-12" /><flux:icon.bolt class="size-10" /><flux:icon.bolt class="size-8" />
```



## [Color](#color)

You can customize the color of an icon using Tailwind's [text color utilities](https://tailwindcss.com/docs/text-color)









Copy to clipboard

```
<flux:icon.bolt variant="solid" class="text-amber-500 dark:text-amber-300" />
```



## [Loading spinner](#loading-spinner)

Flux has a special loading spinner icon that isn't part of the Heroicons collection. You can use this special icon anywhere you would normally use a standard icon.









Copy to clipboard

```
<flux:icon.loading />
```



## [Dynamic icons](#dynamic-icons)

If you need to dynamically set an icon, you can use the flux:icon component and pass in the icon name as a prop.









Copy to clipboard

```
<flux:icon name="bolt" />
```



## [Lucide icons](#lucide-icons)

We love Heroicons, but we acknowledge that it's a fairly limited icon set. If you need more icons, we recommend using [Lucide](https://lucide.dev/) instead.

To make it trivial to use Lucide icons, Flux provides a convenient artisan command to import them into your project:

```
php artisan flux:icon
```

This command will prompt you to select which icons you want to import. You can also manually specify the icons you want to import by passing in their names as arguments to the command:

```
php artisan flux:icon crown grip-vertical github
```









Copy to clipboard

```
<flux:icon.crown /><flux:icon.grip-vertical /><flux:icon.github />
```



## [Custom icons](#custom-icons)

For full control over your icons, you can create your own Blade files in the resources/views/flux/icon directory in your project.

```
- resources    - views        - flux            - icon                - wink.blade.php
```

You can simply paste SVG code directly into the Blade file, however we recommend using the following template structure to ensure compatibility with other components:



Copy to clipboard

```
@php $attributes = $unescapedForwardedAttributes ?? $attributes; @endphp@props([    'variant' => 'outline',])@php$classes = Flux::classes('shrink-0')    ->add(match($variant) {        'outline' => '[:where(&)]:size-6',        'solid' => '[:where(&)]:size-6',        'mini' => '[:where(&)]:size-5',        'micro' => '[:where(&)]:size-4',    });@endphp{{-- Your SVG code here: --}}<svg {{ $attributes->class($classes) }} data-flux-icon aria-hidden="true" ... >    ...</svg>
```









Copy to clipboard

```
<flux:icon.wink />
```

## Related components

[Button Interactive controls with integrated icons](/components/button) [Input Text fields with leading or trailing icons](/components/input) [Badge Small indicators with optional icon content](/components/badge)

## Reference



### [flux:icon.*](#fluxicon)

All icon components (e.g., flux:icon.bolt, flux:icon.loading) share the same props and behavior.

| Prop | Description |
| --- | --- |
| variant | Visual style of the icon. Options: outline (default), solid, mini, micro. |

| Class | Description |
| --- | --- |
| size-* | Control the size of the icon using Tailwind's size utilities (e.g., size-8, size-12). |
| text-* | Control the color of the icon using Tailwind's text color utilities (e.g., text-blue-500). |

| Attribute | Description |
| --- | --- |
| data-flux-icon | Applied to the root SVG element for styling and identification. |



### [Icon sizes](#icon-sizes)

| Size | Description |
| --- | --- |
| outline | 24x24 pixels (default) |
| solid | 24x24 pixels |
| mini | 20x20 pixels |
| micro | 16x16 pixels |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0031_Input

# Input

Capture user data with various forms of text input.





Username This will be publicly displayed.






Copy to clipboard

```
<flux:field>    <flux:label>Username</flux:label>    <flux:description>This will be publicly displayed.</flux:description>    <flux:input />    <flux:error name="username" /></flux:field>
```



## [Shorthand](#shorthand)

Because using the field component in its full form can be verbose and repetitive, all form controls in flux allow you pass a label and a description parameter directly. Under the hood, they will be wrapped in a field with an error component automatically.



Copy to clipboard

```
<flux:input label="Username" description="This will be publicly displayed." />
```



## [Class targeting](#class-targeting)

Unlike other form components, Flux's input component is composed of two underlying elements: an input element and a wrapper div. The wrapper div is there to add padding where icons should go.

This is typically fine, however, if you need to pass classes into the input component and have them directly applied to the input element, you can do so using the class:input attribute instead of simply class:



Copy to clipboard

```
<flux:input class="max-w-xs" class:input="font-mono" />
```



## [Types](#types)

Use the browser's various input types for different situations: text, email, password, etc.





Email

Password

Date





Copy to clipboard

```
<flux:input type="email" label="Email" /><flux:input type="password" label="Password" /><flux:input type="date" max="2999-12-31" label="Date" />
```



## [File](#file)

Flux provides a special input component for file uploads. It's a simple wrapper around the native input[type="file"] element.





Logo

Choose file

No file chosen

Attachments

Choose files

No file chosen





Copy to clipboard

```
<flux:input type="file" wire:model="logo" label="Logo"/><flux:input type="file" wire:model="attachments" label="Attachments" multiple />
```



## [Smaller](#smaller)

Use the size prop to make the input's height more compact.









Copy to clipboard

```
<flux:input size="sm" placeholder="Filter by..." />
```



## [Disabled](#disabled)

Prevent users from interacting with an input by disabling it.





Email





Copy to clipboard

```
<flux:input disabled label="Email" />
```



## [Readonly](#readonly)

Useful for locking an input during a form submission.





Public API key





Copy to clipboard

```
<flux:input readonly variant="filled" />
```



## [Invalid](#invalid)

Signal to users that the contents of an input are invalid.









Copy to clipboard

```
<flux:input invalid />
```



## [Input masking](#input-masking)

Restrict the formatting of text content for unique cases by using [Alpine's mask plugin](https://alpinejs.dev/plugins/mask)









Copy to clipboard

```
<flux:input mask="(999) 999-9999" value="7161234567" /><flux:input mask:dynamic="$money($input)" value="1234.56" />
```



## [Icons](#icons)

Append or prepend an icon to the inside of a form input.









Copy to clipboard

```
<flux:input icon="magnifying-glass" placeholder="Search orders" /><flux:input icon:trailing="credit-card" placeholder="4444-4444-4444-4444" /><flux:input icon:trailing="loading" placeholder="Search transactions" />
```



## [Icon buttons](#icon-buttons)

Append a button to the inside of an input to provide associated functionality.









Copy to clipboard

```
<flux:input placeholder="Search orders">    <x-slot name="iconTrailing">        <flux:button size="sm" variant="subtle" icon="x-mark" class="-mr-1" />    </x-slot></flux:input><flux:input type="password" value="password">    <x-slot name="iconTrailing">        <flux:button size="sm" variant="subtle" icon="eye" class="-mr-1" />    </x-slot></flux:input>
```



## [Clearable, copyable, and viewable inputs](#clearable-copyable-and-viewable-inputs)

Flux provides three special input properties to configure common input button behaviors. clearable for clearing contents, copyable for copying contents, and viewable for toggling password visibility.









Copy to clipboard

```
<flux:input placeholder="Search orders" clearable /><flux:input type="password" value="password" viewable /><flux:input icon="key" value="FLUX-1234-5678-ABCD-EFGH" readonly copyable />
```



## [Keyboard hint](#keyboard-hint)

Hint to users what keyboard shortcuts they can use with this input.





⌘K





Copy to clipboard

```
<flux:input kbd="⌘K" icon="magnifying-glass" placeholder="Search..."/>
```



## [As a button](#as-a-button)

To render an input using a button element, pass "button" into the as prop.





Search...

⌘K







Copy to clipboard

```
<flux:input as="button" placeholder="Search..." icon="magnifying-glass" kbd="⌘K" />
```



## [With buttons](#with-buttons)

Attach buttons to the beginning or end of an input element.





New post

* USD
 EUR
 GBP
 CAD
 AUD
 JPY
 CNY
 INR





Copy to clipboard

```
<flux:input.group>    <flux:input placeholder="Post title" />    <flux:button icon="plus">New post</flux:button></flux:input.group><flux:input.group>    <flux:select class="max-w-fit">        <flux:select.option selected>USD</flux:select.option>        <!-- ... -->    </flux:select>    <flux:input placeholder="$99.99" /></flux:input.group>
```



## [Text prefixes and suffixes](#text-prefixes-and-suffixes)

Append text inside a form input.





https://

.brand.com





Copy to clipboard

```
<flux:input.group>    <flux:input.group.prefix>https://</flux:input.group.prefix>    <flux:input placeholder="example.com" /></flux:input.group><flux:input.group>    <flux:input placeholder="chunky-spaceship" />    <flux:input.group.suffix>.brand.com</flux:input.group.suffix></flux:input.group>
```



## [Input group labels](#input-group-labels)

If you want to use an input group in a form field with a label, you will need to wrap the input group in a field component.





Website

https://





Copy to clipboard

```
<flux:field>    <flux:label>Website</flux:label>    <flux:input.group>        <flux:input.group.prefix>https://</flux:input.group.prefix>        <flux:input wire:model="website" placeholder="example.com" />    </flux:input.group>    <flux:error name="website" /></flux:field>
```

## Related components

[Field Structured form field with label and validation states](/components/field) [Textarea Multi-line text input areas for longer form content](/components/textarea) [Autocomplete Enhanced text input with predictive suggestions](/components/autocomplete)

## Reference



### [flux:input](#fluxinput)

| Prop | Description |
| --- | --- |
| wire:model | Binds the input to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| label | Label text displayed above the input. When provided, wraps the input in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed above the input. When provided alongside label, appears between the label and input within the flux:field wrapper. See the [field component](/components/field). |
| description:trailing | Help text displayed below the input. When provided alongside label, appears below the label and input within the flux:field wrapper. See the [field component](/components/field). |
| placeholder | Placeholder text displayed when the input is empty. |
| size | Size of the input. Options: sm, xs. |
| variant | Visual style variant. Options: filled. Default: outline. |
| disabled | Prevents user interaction with the input. |
| readonly | Makes the input read-only. |
| invalid | Applies error styling to the input. |
| multiple | For file inputs, allows selecting multiple files. |
| mask | Input mask pattern using Alpine's mask plugin. Example: 99/99/9999. |
| mask:dynamic | Dynamic input mask pattern using Alpine's mask plugin. Example: $money($input). |
| icon | Name of the icon displayed at the start of the input. |
| icon:trailing | Name of the icon displayed at the end of the input. |
| kbd | Keyboard shortcut hint displayed at the end of the input. |
| clearable | If true, displays a clear button when the input has content. |
| copyable | If true, displays a copy button to copy the input's content (https only). |
| viewable | For password inputs, displays a toggle to show/hide the password. |
| as | Render the input as a different element. Options: button. Default: input. |
| class:input | CSS classes applied directly to the input element instead of the wrapper. |

| Slot | Description |
| --- | --- |
| icon | Custom content displayed at the start of the input (e.g., icons). |
| icon:leading | Custom content displayed at the start of the input (e.g., icons). |
| icon:trailing | Custom content displayed at the end of the input (e.g., buttons). |

| Attribute | Description |
| --- | --- |
| data-flux-input | Applied to the root element for styling and identification. |



### [flux:input.group](#fluxinputgroup)

| Slot | Description |
| --- | --- |
| default | The input group content, typically containing an input and prefix/suffix elements. |



### [flux:input.group.prefix](#fluxinputgroupprefix)

| Slot | Description |
| --- | --- |
| default | Content displayed before the input (e.g., icons, text, buttons). |



### [flux:input.group.suffix](#fluxinputgroupsuffix)

| Slot | Description |
| --- | --- |
| default | Content displayed after the input (e.g., icons, text, buttons). |

See the [field component documentation](/components/field) for more information.

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0032_KanbanNew



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Kanban

A collection of cards arranged in columns, representing different stages of a workflow.









Planned



6





Update privacy policy in app

Search bar suggestions broken

Improve loading spinner visuals

Date picker keyboard input fails

Admin panel permissions broken

Broken image links in gallery





In Progress



5





Mobile responsive improvements

Data table sorting broken

API error codes inconsistent

Accessibility audit in progress

User dashboard redesign





In review



3





Button double-click issue

Crash on large file upload

API concurrent request handling



 





Copy to clipboard

```
<flux:kanban>    @foreach ($this->columns as $column)        <flux:kanban.column>            <flux:kanban.column.header :heading="$column->title" :count="count($column->cards)" />            <flux:kanban.column.cards>                @foreach ($column->cards as $card)                    <flux:kanban.card :heading="$card->title" />                @endforeach            </flux:kanban.column.cards>        </flux:kanban.column>    @endforeach</flux:kanban>
```



## [Column actions](#column-actions)

Add actions to the column header.









Planned



4

New card

Archive column

Delete











Copy to clipboard

```
<flux:kanban.column>    <flux:kanban.column.header :heading="$column->title" :count="count($column->cards)">        <x-slot name="actions">            <flux:dropdown>                <flux:button variant="subtle" icon="ellipsis-horizontal" size="sm" />                <flux:menu>                    <flux:menu.item icon="plus">New card</flux:menu.item>                    <flux:menu.item icon="archive-box">Archive column</flux:menu.item>                    <flux:menu.separator />                    <flux:menu.item variant="danger" icon="trash">Delete</flux:menu.item>                </flux:menu>            </flux:dropdown>            <flux:button variant="subtle" icon="plus" size="sm" />        </x-slot>    </flux:kanban.column.header>    <flux:kanban.column.cards>        <!-- ... -->    </flux:kanban.column.cards></flux:kanban.column>
```



## [Column subheading](#column-subheading)

Add a subheading to the column header using the subheading prop.







Blacklog



Ideas and suggestions











Copy to clipboard

```
<flux:kanban.column>    <flux:kanban.column.header heading="Blacklog" subheading="Ideas and suggestions" />    <flux:kanban.column.cards>        <!-- ... -->    </flux:kanban.column.cards></flux:kanban.column>
```



## [Column footer](#column-footer)

Add a footer to the column using the flux:kanban.column.footer component to display additional information or actions like a "New card" button.









Planned





Add

New card





Copy to clipboard

```
<flux:kanban.column>    <flux:kanban.column.header :heading="$column['title']" count="5" />    <flux:kanban.column.cards>        <!-- ... -->    </flux:kanban.column.cards>    <flux:kanban.column.footer>        <form>            <flux:kanban.card>                <div class="flex items-center gap-1">                    <flux:heading class="flex-1">                        <input class="w-full outline-none" placeholder="New card...">                    </flux:heading>                    <flux:button type="submit" variant="filled" size="sm" inset="top bottom" class="-me-1.5">Add</flux:button>                </div>            </flux:kanban.card>        </form>        <flux:button variant="subtle" icon="plus" size="sm" align="start">            New card        </flux:button>    </flux:kanban.column.footer></flux:kanban.column>
```



## [Card as button](#card-as-button)

Make a card clickable by passing the as="button" prop to the flux:kanban.card component.

Now you can use the wire:click or x-on:click directives to handle the click event.









Planned

Update privacy policy in app





Copy to clipboard

```
<flux:kanban.card as="button" wire:click="edit" heading="Update privacy policy in app" />
```



## [Card header](#card-header)

Add a header to the card using the <x-slot name="header"> slot to display additional information or actions.









Planned



UI

Backend

Bug

Update privacy policy in app





Copy to clipboard

```
<flux:kanban.card as="button" heading="Update privacy policy in app">    <x-slot name="header">        <div class="flex gap-2">            <flux:badge color="blue" size="sm">UI</flux:badge>            <flux:badge color="green" size="sm">Backend</flux:badge>            <flux:badge color="red" size="sm">Bug</flux:badge>        </div>    </x-slot></flux:kanban.card>
```



## [Card footer](#card-footer)

Add a footer to the card using the <x-slot name="footer"> slot to display additional information or actions.







Planned

Update privacy policy in app



3+





Copy to clipboard

```
<flux:kanban.card as="button" heading="Update privacy policy in app">    <x-slot name="footer">        <flux:icon name="bars-3-bottom-left" variant="micro" class="text-zinc-400" />        <flux:avatar.group>            <flux:avatar circle size="xs" src="https://unavatar.io/x/calebporzio" />            <flux:avatar circle size="xs" src="https://unavatar.io/github/hugosaintemarie" />            <flux:avatar circle size="xs" src="https://unavatar.io/github/joshhanley" />            <flux:avatar circle size="xs">3+</flux:avatar>        </flux:avatar.group>    </x-slot></flux:kanban.card>
```

## Reference



### [flux:kanban](#fluxkanban)

| Slot | Description |
| --- | --- |
| default | Place multiple flux:kanban.column components here to create columns in the kanban board. |



### [flux:kanban.column](#fluxkanbancolumn)

| Slot | Description |
| --- | --- |
| default | Should contain a flux:kanban.column.header, a flux:kanban.column.cards, and optionally a flux:kanban.column.footer component. |



### [flux:kanban.column.header](#fluxkanbancolumnheader)

| Prop | Description |
| --- | --- |
| heading | The title text to display in the column header. |
| subheading | Optional secondary text to display below the column header. |
| count | Optional number to display next to the heading, typically showing the number of cards in the column. |
| badge | Optional badge text or content to display next to the heading. Supports badge:* attributes for customization. |

| Slot | Description |
| --- | --- |
| default | Custom content to display in the header. Will override the heading and count props if provided. |
| actions | Optional slot for action buttons or dropdowns that appear on the right side of the column header. |



### [flux:kanban.column.cards](#fluxkanbancolumncards)

| Slot | Description |
| --- | --- |
| default | Place multiple flux:kanban.card components here to populate the column with cards. |



### [flux:kanban.column.footer](#fluxkanbancolumnfooter)

| Slot | Description |
| --- | --- |
| default | Custom content to display at the bottom of the column, commonly used for "Add card" buttons or forms. |



### [flux:kanban.card](#fluxkanbancard)

| Prop | Description |
| --- | --- |
| heading | The title text to display in the card. |
| as | Element to render the card as. Options: button, div (default). When set to button, the card becomes clickable. |

| Slot | Description |
| --- | --- |
| default | Custom content to display in the card body. Will override the heading prop if provided. |
| header | Optional content to display above the card heading, commonly used for badges or tags. |
| footer | Optional content to display below the card heading, commonly used for icons, avatars, or metadata. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0033_Modal

# Modal

Display content in a layer above the main page. Ideal for confirmations, alerts, and forms.





Edit profile

Update profile

Make changes to your personal details.

Name

Date of birth

Save changes





Copy to clipboard

```
<flux:modal.trigger name="edit-profile">    <flux:button>Edit profile</flux:button></flux:modal.trigger><flux:modal name="edit-profile" class="md:w-96">    <div class="space-y-6">        <div>            <flux:heading size="lg">Update profile</flux:heading>            <flux:text class="mt-2">Make changes to your personal details.</flux:text>        </div>        <flux:input label="Name" placeholder="Your name" />        <flux:input label="Date of birth" type="date" />        <div class="flex">            <flux:spacer />            <flux:button type="submit" variant="primary">Save changes</flux:button>        </div>    </div></flux:modal>
```



## [Unique modal names](#unique-modal-names)

If you are placing modals inside a loop, ensure that you are dynamically generating unique modal names. Otherwise, one modal trigger, will trigger all modals of that name on the page causing unexpected behavior.



Copy to clipboard

```
@foreach ($users as $user)    <flux:modal :name="'edit-profile-'.$user->id">        ...    </flux:modal>@endforeach
```



## [Livewire methods](#livewire-methods)

In addition to triggering modals in your Blade templates, you can also control them directly from Livewire.

Consider a "confirm" modal in your Blade template like so:



Copy to clipboard

```
<flux:modal name="confirm">    <!-- ... --></flux:modal>
```

You can now open and close this modal from your Livewire component using the following methods:



Copy to clipboard

```
<?phpclass ShowPost extends \Livewire\Component {    public function delete() {        // Control "confirm" modals anywhere on the page...        Flux::modal('confirm')->show();        Flux::modal('confirm')->close();        // Control "confirm" modals within this Livewire component...        $this->modal('confirm')->show();        $this->modal('confirm')->close();        // Closes all modals on the page...        Flux::modals()->close();    }}
```



## [JavaScript methods](#javascript-methods)

You can also control modals from Alpine directly using Flux's magic methods:



Copy to clipboard

```
<button x-on:click="$flux.modal('confirm').show()">    Open modal</button><button x-on:click="$flux.modal('confirm').close()">    Close modal</button><button x-on:click="$flux.modals().close()">    Close all modals</button>
```

Or you can use the window.Flux global object to control modals from any JavaScript in your application:



Copy to clipboard

```
// Control "confirm" modals anywhere on the page...Flux.modal('confirm').show()Flux.modal('confirm').close()// Closes all modals on the page...Flux.modals().close()
```



## [Data binding](#data-binding)

If you prefer, you can bind a Livewire property directly to a modal to control its states from your Livewire component.

Consider a confirmation modal in your Blade template like so:



Copy to clipboard

```
<flux:modal wire:model.self="showConfirmModal">    <!-- ... --></flux:modal>
```

It's important to add the .self modifier to the wire:model attribute to prevent nested elements from dispatching input events that would interfere with the state of the modal.

You can now open and close this modal from your Livewire component by toggling the wire:model property.



Copy to clipboard

```
<?phpclass ShowPost extends \Livewire\Component {    public $showConfirmModal = false;    public function delete() {        $this->showConfirmModal = true;    }}
```

One advantage of this approach is being able to control the state of the modal directly from the browser without making a server roundtrip:



Copy to clipboard

```
<flux:button x-on:click="$wire.showConfirmModal = true">Delete post</flux:button>
```



## [Close events](#close-events)

If you need to perform some logic after a modal closes, you can register a close listener like so:



Copy to clipboard

```
<flux:modal @close="someLivewireAction">    <!-- ... --></flux:modal>
```

You can also use wire:close or x-on:close if you prefer those syntaxes.



## [Cancel events](#cancel-events)

If you need to perform some logic after a modal is cancelled by clicking outside or pressing escape, you can register a cancel listener like so:



Copy to clipboard

```
<flux:modal @cancel="someLivewireAction">    <!-- ... --></flux:modal>
```

You can also use wire:cancel or x-on:cancel if you prefer those syntaxes.



## [Disable click outside](#disable-click-outside)

By default, clicking outside the modal will close it. If you want to disable this behavior, you can use the :dismissible="false" prop.



Copy to clipboard

```
<flux:modal :dismissible="false">    <!-- ... --></flux:modal>
```



## [Confirmation](#confirmation)

Prompt a user for confirmation before performing a dangerous action.





Delete

Delete project?

You're about to delete this project.  
This action cannot be reversed.

Cancel

Delete project





Copy to clipboard

```
<flux:modal.trigger name="delete-profile">    <flux:button variant="danger">Delete</flux:button></flux:modal.trigger><flux:modal name="delete-profile" class="min-w-[22rem]">    <div class="space-y-6">        <div>            <flux:heading size="lg">Delete project?</flux:heading>            <flux:text class="mt-2">                You're about to delete this project.<br>                This action cannot be reversed.            </flux:text>        </div>        <div class="flex gap-2">            <flux:spacer />            <flux:modal.close>                <flux:button variant="ghost">Cancel</flux:button>            </flux:modal.close>            <flux:button type="submit" variant="danger">Delete project</flux:button>        </div>    </div></flux:modal>
```



## [Flyout](#flyout)

Use the flyout prop for a more anchored and long-form dialog.





Edit profile

Update profile

Make changes to your personal details.

Name

Date of birth

Save changes





Copy to clipboard

```
<flux:modal.trigger name="edit-profile">    <flux:button>Edit profile</flux:button></flux:modal.trigger><flux:modal name="edit-profile" flyout>    <div class="space-y-6">        <div>            <flux:heading size="lg">Update profile</flux:heading>            <flux:text class="mt-2">Make changes to your personal details.</flux:text>        </div>        <flux:input label="Name" placeholder="Your name" />        <flux:input label="Date of birth" type="date" />        <div class="flex">            <flux:spacer />            <flux:button type="submit" variant="primary">Save changes</flux:button>        </div>    </div></flux:modal>
```



## Flyout positioning

By default, flyouts will open from the right. You can change this behavior by passing "left", or "bottom" into the position prop.

Copy to clipboard

```
<flux:modal flyout position="left">    <!-- ... --></flux:modal>
```



### [Floating flyout](#floating-flyout)

Use the "floating" variant to give your flyout modal a floating appearance.





Edit profile

Update profile

Make changes to your personal details.

Name

Date of birth





Copy to clipboard

```
<flux:modal.trigger name="edit-profile">    <flux:button>Edit profile</flux:button></flux:modal.trigger><flux:modal name="edit-profile" flyout variant="floating" class="md:w-lg">    <div class="space-y-6">        <flux:heading size="lg">Update profile</flux:heading>        <flux:subheading>Make changes to your personal details.</flux:subheading>        <flux:input label="Name" placeholder="Your name" />        <flux:input label="Date of birth" type="date" />    </div>    <x-slot name="footer" class="flex items-center justify-end gap-2">        <flux:modal.close>            <flux:button variant="filled">Cancel</flux:button>        </flux:modal.close>        <flux:button type="submit" variant="primary">Save changes</flux:button>    </x-slot></flux:modal>
```

## Related components

[Dropdown Display expandable action or navigation menus](/components/dropdown) [Command Keyboard command palettes for application navigation](/components/command)

## Reference



### [flux:modal](#fluxmodal)

| Prop | Description |
| --- | --- |
| name | Unique identifier for the modal. Required when using triggers. |
| flyout | If true, the modal will open as a flyout. |
| variant | Visual style of the modal. Options: default, floating, bare (legacy: flyout). |
| position | For flyout modals, the direction they open from. Options: right (default), left, bottom. |
| dismissible | If false, prevents closing the modal by clicking outside. Default: true. |
| closable | If false, hides the close button. Default: true. |
| wire:model | Optional Livewire property to bind the modal's open state to. |

| Event | Description |
| --- | --- |
| close | Triggered when the modal is closed by any means. |
| cancel | Triggered when the modal is closed by clicking outside or pressing escape. |

| Slot | Description |
| --- | --- |
| default | The modal content. |

| Class | Description |
| --- | --- |
| w-* | Common use: md:w-96 for width. |



### [flux:modal.trigger](#fluxmodaltrigger)

| Prop | Description |
| --- | --- |
| name | Name of the modal to trigger. Must match the modal's name. |
| shortcut | Keyboard shortcut to open the modal (e.g., cmd.k). |

| Slot | Description |
| --- | --- |
| default | The trigger element (e.g., button). |



### [flux:modal.close](#fluxmodalclose)

| Slot | Description |
| --- | --- |
| default | The close trigger element (e.g., button). |



### [Flux::modal()](#fluxmodal)

PHP method for controlling modals from Livewire components.

| Parameter | Description |
| --- | --- |
| default\|name | Name of the modal to control. |

| Method | Description |
| --- | --- |
| close() | Closes the modal. |



### [Flux::modals()](#fluxmodals)

PHP method for controlling all modals on the page.

| Method | Description |
| --- | --- |
| close() | Closes all modals on the page. |



### [$flux.modal()](#fluxmodal)

Alpine.js magic method for controlling modals.

| Parameter | Description |
| --- | --- |
| default\|name | Name of the modal to control. |

| Method | Description |
| --- | --- |
| show() | Shows the modal. |
| close() | Closes the modal. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)  




# 0034_Navbar

# Navbar

Arrange navigation links vertically or horizontally.

Discover more about the navbar on the [layout documentation ->](/layouts/sidebar)









Copy to clipboard

```
<flux:navbar>    <flux:navbar.item href="#">Home</flux:navbar.item>    <flux:navbar.item href="#">Features</flux:navbar.item>    <flux:navbar.item href="#">Pricing</flux:navbar.item>    <flux:navbar.item href="#">About</flux:navbar.item></flux:navbar>
```



## [Detecting the current page](#detecting-the-current-page)

Navbars and navlists will try to automatically detect and mark the current page based on the href attribute passed in. However, if you need full control, you can pass the current prop to the item directly.



Copy to clipboard

```
<flux:navbar.item href="/" current>Home</flux:navbar.item><flux:navbar.item href="/" :current="false">Home</flux:navbar.item><flux:navbar.item href="/" :current="request()->is('/')">Home</flux:navbar.item>
```



## [With icons](#with-icons)

Add a leading icons for visual context.









Copy to clipboard

```
<flux:navbar>    <flux:navbar.item href="#" icon="home">Home</flux:navbar.item>    <flux:navbar.item href="#" icon="puzzle-piece">Features</flux:navbar.item>    <flux:navbar.item href="#" icon="currency-dollar">Pricing</flux:navbar.item>    <flux:navbar.item href="#" icon="user">About</flux:navbar.item></flux:navbar>
```



## [With badges](#with-badges)

Add a trailing badge to a navbar item using the badge prop.









Copy to clipboard

```
<flux:navbar>    <flux:navbar.item href="#">Home</flux:navbar.item>    <flux:navbar.item href="#" badge="12">Inbox</flux:navbar.item>    <flux:navbar.item href="#">Contacts</flux:navbar.item>    <flux:navbar.item href="#" badge="Pro" badge:color="lime">Calendar</flux:navbar.item></flux:navbar>
```



## [Dropdown navigation](#dropdown-navigation)

Condense multiple navigation items into a single dropdown menu to save on space and group related items.









Copy to clipboard

```
<flux:navbar>    <flux:navbar.item href="#">Dashboard</flux:navbar.item>    <flux:navbar.item href="#">Transactions</flux:navbar.item>    <flux:dropdown>        <flux:navbar.item icon:trailing="chevron-down">Account</flux:navbar.item>        <flux:navmenu>            <flux:navmenu.item href="#">Profile</flux:navmenu.item>            <flux:navmenu.item href="#">Settings</flux:navmenu.item>            <flux:navmenu.item href="#">Billing</flux:navmenu.item>        </flux:navmenu>    </flux:dropdown></flux:navbar>
```



## [Navlist (sidebar)](#navlist-sidebar)

Arrange your navbar vertically using the navlist component.









Copy to clipboard

```
<flux:navlist class="w-64">    <flux:navlist.item href="#" icon="home">Home</flux:navlist.item>    <flux:navlist.item href="#" icon="puzzle-piece">Features</flux:navlist.item>    <flux:navlist.item href="#" icon="currency-dollar">Pricing</flux:navlist.item>    <flux:navlist.item href="#" icon="user">About</flux:navlist.item></flux:navlist>
```



## [Navlist group](#navlist-group)

Group related navigation items.









Copy to clipboard

```
<flux:navlist>    <flux:navlist.group heading="Account" class="mt-4">        <flux:navlist.item href="#">Profile</flux:navlist.item>        <flux:navlist.item href="#">Settings</flux:navlist.item>        <flux:navlist.item href="#">Billing</flux:navlist.item>    </flux:navlist.group></flux:navlist>
```



## [Collapsible groups](#collapsible-groups)

Group related navigation items into collapsible sections using the expandable prop.









Copy to clipboard

```
<flux:navlist class="w-64">    <flux:navlist.item href="#" icon="home">Dashboard</flux:navlist.item>    <flux:navlist.item href="#" icon="list-bullet">Transactions</flux:navlist.item>    <flux:navlist.group heading="Account" expandable>        <flux:navlist.item href="#">Profile</flux:navlist.item>        <flux:navlist.item href="#">Settings</flux:navlist.item>        <flux:navlist.item href="#">Billing</flux:navlist.item>    </flux:navlist.group></flux:navlist>
```

If you want a group to be collapsed by default, you can use the expanded prop:



Copy to clipboard

```
<flux:navlist.group heading="Account" expandable :expanded="false">
```



## [Navlist badges](#navlist-badges)

Show additional information related to a navlist item using the badge prop.









Copy to clipboard

```
<flux:navlist class="w-64">    <flux:navlist.item href="#" icon="home">Home</flux:navlist.item>    <flux:navlist.item href="#" icon="envelope" badge="12">Inbox</flux:navlist.item>    <flux:navlist.item href="#" icon="user-group">Contacts</flux:navlist.item>    <flux:navlist.item href="#" icon="calendar-days" badge="Pro" badge:color="lime">Calendar</flux:navlist.item></flux:navlist>
```

## Related components

[Tabs Organize content into separate panels](/components/tabs) [Header Top navigation headers for your application](/layouts/header) [Sidebar Primary or secondary navigation sidebars](/layouts/sidebar)

## Reference



### [flux:navbar](#fluxnavbar)

A horizontal navigation container.

| Slot | Description |
| --- | --- |
| default | The navigation items. |

| Attribute | Description |
| --- | --- |
| data-flux-navbar | Applied to the root element for styling and identification. |



### [flux:navbar.item](#fluxnavbaritem)

| Prop | Description |
| --- | --- |
| href | URL the item links to. |
| current | If true, applies active styling to the item. Auto-detected based on current URL if not specified. |
| icon | Name of the icon to display at the start of the item. |
| icon:trailing | Name of the icon to display at the end of the item. |
| badge | Content to display as a badge. Can be a string, boolean, or a slot. |
| badge:color | Color of the badge. Options: same color options as the color prop on the badge component. |
| badge:variant | Variant of the badge. Options: solid, outline. Default: solid. |

| Attribute | Description |
| --- | --- |
| data-current | Applied when the item is active/current. |



### [flux:navlist](#fluxnavlist)

A vertical navigation container (sidebar).

| Slot | Description |
| --- | --- |
| default | The navigation items and groups. |

| Attribute | Description |
| --- | --- |
| data-flux-navlist | Applied to the root element for styling and identification. |



### [flux:navlist.item](#fluxnavlistitem)

| Prop | Description |
| --- | --- |
| href | URL the item links to. |
| current | If true, applies active styling to the item. Auto-detected based on current URL if not specified. |
| icon | Name of the icon to display at the start of the item. |
| badge | Content to display as a badge. Can be a string, boolean, or a slot. |
| badge:color | Color of the badge. Options: same color options as the color prop on the badge component. |
| badge:variant | Variant of the badge. Options: solid, outline. Default: solid. |

| Attribute | Description |
| --- | --- |
| data-current | Applied when the item is active/current. |



### [flux:navlist.group](#fluxnavlistgroup)

| Prop | Description |
| --- | --- |
| heading | Text displayed as the group heading. |
| expandable | If true, makes the group collapsible. |
| expanded | If true, expands the group by default when expandable. |

| Slot | Description |
| --- | --- |
| default | The group's navigation items. |



### [Profile switcher](#profile-switcher)

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0035_OTP InputNew

# OTP Input

Capture one-time passwords with a series of individual input fields.









Copy to clipboard

```
<flux:otp wire:model="code" length="6" />
```



## [Example usage](#example-usage)

Display a form for verifying one-time passwords.





Verify your account

Please enter a one-time password from the authenticator app.

OTP Code


Verify

Resend code





Copy to clipboard

```
<flux:card>    <form wire:submit="verify" class="space-y-8">        <div class="max-w-64 mx-auto space-y-2">            <flux:heading size="lg" class="text-center">Verify your account</flux:heading>            <flux:text class="text-center">Please enter a one-time password from the authenticator app.</flux:text>        </div>        <flux:otp wire:model="code" length="6" label="OTP Code" label:sr-only :error:icon="false" error:class="text-center" class="mx-auto" />        <div class="space-y-4">            <flux:button variant="primary" type="submit" class="w-full">Verify</flux:button>            <flux:button wire:click="resend" class="w-full">Resend code</flux:button>        </div>    </form></flux:card>
```



## [Autosubmit](#autosubmit)

Use the submit="auto" prop to automatically submit the form once all input fields are filled.





Verify your account

Please enter a one-time password from the authenticator app.





Copy to clipboard

```
<form wire:submit="verify" class="space-y-8">    <div class="max-w-64 mx-auto space-y-2">        <flux:heading size="lg" class="text-center">Verify your account</flux:heading>        <flux:text class="text-center">Please enter a one-time password from the authenticator app.</flux:text>    </div>    <div class="space-y-6">        <flux:otp wire:model="code" length="6" submit="auto" class="mx-auto" />    </div></form>
```



## [Alphanumeric](#alphanumeric)

Allow non-numeric characters by setting the mode to alphanumeric or alpha.





License key


Enter the license key printed on the installation disc





Copy to clipboard

```
<flux:otp wire:model="licenseKey" length="10" mode="alphanumeric" label="License key" description:trailing="Enter the license key printed on the installation disc" />
```



## [Private](#private)

To mask sensitive input values, use the private prop.





PIN Code






Copy to clipboard

```
<flux:otp wire:model="pin" length="4" private label="PIN Code" />
```



## [Separator](#separator)

Use the default slot to render input fields with a separator in between them.





—







Copy to clipboard

```
<flux:otp wire:model="code">    <flux:otp.input />    <flux:otp.input />    <flux:otp.input />    <flux:otp.separator />    <flux:otp.input />    <flux:otp.input />    <flux:otp.input /></flux:otp>
```



## [Group](#group)

Group all input fields together using the flux:otp.group component.









Copy to clipboard

```
<flux:otp wire:model="code">    <flux:otp.group>        <flux:otp.input />        <flux:otp.input />        <flux:otp.input />        <flux:otp.input />        <flux:otp.input />        <flux:otp.input />    </flux:otp.group></flux:otp>
```



## [Group separator](#group-separator)

Add a separator between groups of input fields using the flux:otp.separator component.





—





Copy to clipboard

```
<flux:otp wire:model="code">    <flux:otp.group>        <flux:otp.input />        <flux:otp.input />        <flux:otp.input />    </flux:otp.group>    <flux:otp.separator />    <flux:otp.group>        <flux:otp.input />        <flux:otp.input />        <flux:otp.input />    </flux:otp.group></flux:otp>
```

## Related components

[Field Structured form field with label and validation](/components/field) [Input Text fields for collecting user input](/components/input)

## Reference



### [flux:otp](#fluxotp)

| Prop | Description |
| --- | --- |
| wire:model | Binds the value to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| value | The current value as a string. |
| length | The number of input fields to display. |
| mode | The input mode. Can be numeric (default), alphanumeric, or alpha. |
| private | Sets the input fields to private type to mask the input values. |
| submit | Keyboard behavior for form submission. Options: (default), auto to submit when all fields are filled. |
| autocomplete | Sets the autocomplete attribute for the first input field. Use off to disable browser autofill. Default: one-time-code. |

| Slot | Description |
| --- | --- |
| default | Custom input fields and separators. When used, the length prop is ignored. |



### [flux:otp.input](#fluxotpinput)

| Prop | Description |
| --- | --- |
| — | — |



### [flux:otp.separator](#fluxotpseparator)

| Prop | Description |
| --- | --- |
| — | — |



### [flux:otp.group](#fluxotpgroup)

| Slot | Description |
| --- | --- |
| Default | The input fields to include in the group. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0036_Pagination

# Pagination

Display a series of buttons to navigate through a list of items.









Showing 1 to 5 of 24 results







1   2

  3

  4

  5





Copy to clipboard

```
<!-- $orders = Order::paginate() --><flux:pagination :paginator="$orders" />
```



## [Simple paginator](#simple-paginator)

Use the simple paginator when working with large datasets where counting the total number of results would be expensive. The simple paginator provides "Previous" and "Next" buttons without displaying the total number of pages or records.















Copy to clipboard

```
<!-- $orders = Order::simplePaginate() --><flux:pagination :paginator="$orders" />
```



## [Large result set](#large-result-set)

When working with large result sets, the pagination component automatically adapts to show a reasonable number of page links. It shows the first and last pages, along with a window of pages around the current page, and adds ellipses for any gaps to ensure efficient navigation through numerous pages.









Showing 1 to 75 of 1000 results







1   2

  3

  4

  5

  6

  7

  8

  9

  10



...

   66

  67





Copy to clipboard

```
<!-- $orders = Order::paginate(5) --><flux:pagination :paginator="$orders" />
```

## Related components

[Table Display tabular data](/components/table)

## Reference



### [flux:pagination](#fluxpagination)

| Prop | Description |
| --- | --- |
| paginator | The paginator instance to display. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0037_PillboxNew



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Pillbox

A multi-select component that displays selected items as removable "pills" that expand the input area as needed.





Design

Development

Marketing

Sales

Support

Engineering

Product

Operations





Copy to clipboard

```
<flux:pillbox wire:model="selectedTags" multiple placeholder="Choose tags...">    <flux:pillbox.option value="design">Design</flux:pillbox.option>    <flux:pillbox.option value="development">Development</flux:pillbox.option>    <flux:pillbox.option value="marketing">Marketing</flux:pillbox.option>    <flux:pillbox.option value="sales">Sales</flux:pillbox.option>    <flux:pillbox.option value="support">Support</flux:pillbox.option>    <flux:pillbox.option value="engineering">Engineering</flux:pillbox.option>    <flux:pillbox.option value="product">Product</flux:pillbox.option>    <flux:pillbox.option value="operations">Operations</flux:pillbox.option></flux:pillbox>
```



## [Small](#small)

A smaller pillbox element for more compact layouts.





Design

Development

Marketing

Sales

Support

Engineering

Product

Operations





Copy to clipboard

```
<flux:pillbox size="sm" multiple placeholder="Choose tags...">    <flux:pillbox.option value="design">Design</flux:pillbox.option>    <flux:pillbox.option value="development">Development</flux:pillbox.option>    <flux:pillbox.option value="marketing">Marketing</flux:pillbox.option>    <flux:pillbox.option value="sales">Sales</flux:pillbox.option>    <flux:pillbox.option value="support">Support</flux:pillbox.option>    <flux:pillbox.option value="engineering">Engineering</flux:pillbox.option>    <flux:pillbox.option value="product">Product</flux:pillbox.option>    <flux:pillbox.option value="operations">Operations</flux:pillbox.option></flux:pillbox>
```



## [Searchable](#searchable)

Add a search input to filter through large lists of options.





No results found

JavaScript

TypeScript

PHP

Python

Ruby

Go

Rust

Java

C#

Swift





Copy to clipboard

```
<flux:pillbox multiple searchable placeholder="Choose skills...">    <flux:pillbox.option value="javascript">JavaScript</flux:pillbox.option>    <flux:pillbox.option value="typescript">TypeScript</flux:pillbox.option>    <flux:pillbox.option value="php">PHP</flux:pillbox.option>    <flux:pillbox.option value="python">Python</flux:pillbox.option>    <flux:pillbox.option value="ruby">Ruby</flux:pillbox.option>    <flux:pillbox.option value="go">Go</flux:pillbox.option>    <flux:pillbox.option value="rust">Rust</flux:pillbox.option>    <flux:pillbox.option value="java">Java</flux:pillbox.option>    <flux:pillbox.option value="csharp">C#</flux:pillbox.option>    <flux:pillbox.option value="swift">Swift</flux:pillbox.option></flux:pillbox>
```



## Custom search placeholder

You can customize the search input placeholder:

Copy to clipboard

```
<flux:pillbox multiple searchable search:placeholder="Filter skills...">    ...</flux:pillbox>
```



## [With icons](#with-icons)

Add icons to options for better visual recognition.





GitHub



GitLab



Bitbucket





Copy to clipboard

```
<flux:pillbox multiple placeholder="Choose platforms...">    <flux:pillbox.option value="github">        <div class="flex items-center gap-2">            <flux:icon.code-bracket variant="mini" class="text-zinc-400" /> GitHub        </div>    </flux:pillbox.option>    <flux:pillbox.option value="gitlab">        <div class="flex items-center gap-2">            <flux:icon.server variant="mini" class="text-zinc-400" /> GitLab        </div>    </flux:pillbox.option>    <flux:pillbox.option value="bitbucket">        <div class="flex items-center gap-2">            <flux:icon.cloud variant="mini" class="text-zinc-400" /> Bitbucket        </div>    </flux:pillbox.option></flux:pillbox>
```



## [Combobox](#combobox)

Display an input directly within the pillbox.





No results found

JavaScript

TypeScript

PHP

Python

Ruby

Go

Rust

Java

C#

Swift





Copy to clipboard

```
<flux:pillbox variant="combobox" multiple placeholder="Choose skills...">    <flux:pillbox.option value="javascript">JavaScript</flux:pillbox.option>    <flux:pillbox.option value="typescript">TypeScript</flux:pillbox.option>    <flux:pillbox.option value="php">PHP</flux:pillbox.option>    <flux:pillbox.option value="python">Python</flux:pillbox.option>    <flux:pillbox.option value="ruby">Ruby</flux:pillbox.option>    <flux:pillbox.option value="go">Go</flux:pillbox.option>    <flux:pillbox.option value="rust">Rust</flux:pillbox.option>    <flux:pillbox.option value="java">Java</flux:pillbox.option>    <flux:pillbox.option value="csharp">C#</flux:pillbox.option>    <flux:pillbox.option value="swift">Swift</flux:pillbox.option></flux:pillbox>
```



## [Create option](#create-option)

Allow users to the create new options using the <flux:pillbox.option.create> component.

Flux will automatically hide the create option when the search input matches an existing item in the list. You can also specify the minimum number of characters required for the create option to appear using the min-length prop.





No results found

Design

Development

Marketing

Sales

Support

Engineering

Product

Operations

Create new ""





Copy to clipboard

```
<flux:pillbox wire:model="selectedTags" variant="combobox" multiple>    <x-slot name="input">        <flux:pillbox.input wire:model="search" placeholder="Choose tags..." />    </x-slot>    @foreach ($this->tags as $tag)        <flux:pillbox.option :value="$tag->id">{{ $tag->name }}</flux:pillbox.option>    @endforeach    <flux:pillbox.option.create wire:click="createTag" min-length="2">        Create new "<span wire:text="search"></span>"    </flux:pillbox.option.create></flux:pillbox><!--public $search = '';public $selectedTags = [];public function createProject(){    $tag = Tag::create([        'name' => $this->search,    ]);    $this->selectedTags[] = $tag->id;    $this->search = '';}-->
```



### [With backend search](#with-backend-search)

If you're using :filter="false", make sure to adjust your query to always include the newly created item when the search input is cleared.

Flux will automatically disable the create option during requests to prevent duplicate entries and when the list is updated, it performs a uniqueness check on the frontend.





No results found

Design

Development

Marketing

Sales

Support

Engineering

Product

Operations

Create ""





Copy to clipboard

```
<flux:pillbox wire:model.live="selectedTags" variant="combobox" multiple :filter="false">    <x-slot name="input">        <flux:pillbox.input wire:model.live="search" placeholder="Choose tags..." />    </x-slot>    @foreach($this->tags as $tag)        <flux:pillbox.option :value="$tag->id">{{ $tag->name }}</flux:pillbox.option>    @endforeach    <flux:pillbox.option.create wire:click="createTag" min-length="2">        Create "<span wire:text="search"></span>"    </flux:pillbox.option.create></flux:pillbox><!--#[\Livewire\Attributes\Computed]public function tags() {    return \App\Models\Tag::query()        ->where('name', 'like', '%' . trim($this->search) . '%')        ->limit(20)->get()        ->when(blank($this->search) && $this->selectedTags, function ($results) {            return \App\Models\Tag::query()                ->whereIn('id', $this->selectedTags)                ->whereNotIn('id', $results->pluck('id'))                ->get()->merge($results);        });}-->
```



## Loading message

When then create option is hidden by the frontend but new results aren't available yet, Flux displays a special "Loading..." message. To customize this message, use the when-loading prop on the <flux:pillbox.option.empty> component.

Copy to clipboard

```
<flux:pillbox wire:model="selectedTags" variant="combobox" multiple :filter="false">    ...    <x-slot name="empty">        <flux:pillbox.option.empty when-loading="Loading tags...">            No tags found.        </flux:pillbox.option.empty>    </x-slot></flux:pillbox>
```



### [With validation](#with-validation)

When you perform additional validation on the backend, the search input will indicate an invalid state when there are validation errors present. Make sure to reset the error bag when the user updates the input.





No results found

Design

Development

Marketing

Sales

Support

Engineering

Product

Operations

Create ""





Copy to clipboard

```
<flux:pillbox wire:model.live="selectedTags" variant="combobox" multiple placeholder="Choose tags..." :filter="false">    <x-slot name="input">        <flux:pillbox.input wire:model.live="search" placeholder="Choose tags..." />    </x-slot>        ...    <flux:pillbox.option.create wire:click="createTag" min-length="2">        Create "<span wire:text="search"></span>"    </flux:pillbox.option.create></flux:pillbox><!--public function createTag() {    $this->validate(['search' => 'required|unique:tags,name']);    // Create logic...}public function updatedSearch() {    $this->resetErrorBag('search');}-->
```



### [With modal](#with-modal)

Use the modal prop to specify a name of a modal and handle more complex creation workflows inside a form.





Create new

Design

Development

Marketing

Sales

Support

Engineering

Product

Operations  

Create new tag

Enter the name of the new tag.

Name

Create





Copy to clipboard

```
<flux:pillbox wire:model="projectId" variant="combobox" placeholder="Choose project...">    <flux:pillbox.option.create modal="create-tag">Create new</flux:pillbox.option>    @foreach($this->tags as $tag)        <flux:pillbox.option :value="$tag->id">{{ $tag->name }}</flux:pillbox.option>    @endforeach</flux:pillbox><flux:modal name="create-tag" class="md:w-96">    <form wire:submit="createTag" class="space-y-6">        <div>            <flux:heading size="lg">Create new tag</flux:heading>            <flux:text class="mt-2">Enter the name of the new tag.</flux:text>        </div>        <flux:input wire:model="newTagName" label="Name" placeholder="e.g. 'Research'" />        <div class="flex">            <flux:spacer />            <flux:button type="submit" variant="primary">Create</flux:button>        </div>    </form></flux:modal>
```

## Related components

[Select Single and multi-select dropdowns](/components/select) [Field Structured form field with label and validation states](/components/field) [Autocomplete Enhanced text input with predictive suggestions](/components/autocomplete)

## Reference



### [flux:pillbox](#fluxpillbox)

| Prop | Description |
| --- | --- |
| wire:model | Binds the pillbox to a Livewire property. The model should be an array to store multiple selected values. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| placeholder | Text displayed when no pills are selected. |
| label | Label text displayed above the pillbox. When provided, wraps the pillbox in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the pillbox. When provided alongside label, appears between the label and pillbox within the flux:field wrapper. |
| size | Size of the pillbox. Options: sm. |
| searchable | Adds a search input inside the dropdown to filter options. |
| search:placeholder | Custom placeholder text for the search input when searchable is true. |
| filter | If false, disables client-side filtering for dynamic server-side options. |
| disabled | Prevents user interaction with the pillbox. |
| invalid | Applies error styling to the pillbox border. |

| Slot | Description |
| --- | --- |
| default | The pillbox options. Should contain flux:pillbox.option components. |
| trigger | Custom trigger element for the dropdown. Replaces the default pill container. |
| search | Custom search input for the dropdown. Used when you need to wire up custom search behavior. |
| empty | Content shown when no options match the search query. Typically the pillbox.option.empty component. |

| Attribute | Description |
| --- | --- |
| data-flux-pillbox | Applied to the root element for styling and JavaScript behavior. |



### [flux:pillbox.option](#fluxpillboxoption)

| Prop | Description |
| --- | --- |
| value | The value associated with this option. This is what gets stored in the model array when selected. |
| label | Text content displayed for the option. |
| selected-label | Text content displayed when the option is selected. |
| disabled | Prevents this option from being selected. |
| filterable | If false, this option won't be hidden by the search filter. Useful for "no results" messages. |

| Slot | Description |
| --- | --- |
| default | The option content. Can include text, icons, images, or any custom HTML. |



### [flux:pillbox.option.create](#fluxpillboxoptioncreate)

| Prop | Description |
| --- | --- |
| min-length | Minimum number of characters required in the search input before displaying the create option. |
| modal | Name of the modal to open when the option is selected. |
| wire:click | Livewire action to call when the option is selected. |



### [flux:pillbox.option.empty](#fluxpillboxoptionempty)

| Prop | Description |
| --- | --- |
| when-loading | Message displayed when options are loading. |

| Slot | Description |
| --- | --- |
| default | Message displayed when no options are found. |



### [flux:pillbox.search](#fluxpillboxsearch)

| Prop | Description |
| --- | --- |
| placeholder | Placeholder text for the search input. Defaults to "Search...". |
| icon | Icon to display in the search input. Defaults to magnifying glass. |
| clearable | If true, shows a clear button when the search input has text. Default: true. |



### [flux:pillbox.trigger](#fluxpillboxtrigger)

| Prop | Description |
| --- | --- |
| placeholder | Text displayed when no pills are selected. |
| invalid | Applies error styling to the trigger element. |
| size | Size of the trigger. Options: sm. |
| clearable | Shows a clear all button in the trigger. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0038_Popover



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Popover

Show extra content in a popup on click or hover.

This component is for generic popover content. Use it only if the [Dropdown menu](/components/dropdown) component doesn't fit your needs.





Options

Sort by
Recently active

Date posted

View as
List

Gallery

Reset to default





Copy to clipboard

```
<flux:dropdown>    <flux:button        icon="adjustments-horizontal"        icon:variant="micro"        icon:class="text-zinc-400"        icon-trailing="chevron-down"        icon-trailing:variant="micro"        icon-trailing:class="text-zinc-400"    >        Options    </flux:button>    <flux:popover class="flex flex-col gap-4">        <flux:radio.group wire:model="sort" label="Sort by" label:class="text-zinc-500 dark:text-zinc-400">            <flux:radio value="active" label="Recently active" />            <flux:radio value="posted" label="Date posted" checked />        </flux:radio.group>        <flux:separator variant="subtle" />        <flux:radio.group wire:model="view" label="View as" label:class="text-zinc-500 dark:text-zinc-400">            <flux:radio value="list" label="List" checked />            <flux:radio value="gallery" label="Gallery" />        </flux:radio.group>        <flux:separator variant="subtle" />        <flux:button variant="subtle" size="sm" class="justify-start -m-2 px-2!">Reset to default</flux:button>    </flux:popover></flux:dropdown>
```



## [Hover trigger](#hover-trigger)

Use the hover prop on the dropdown to show the popover when hovering over the trigger element.

Currently, you can only use the button element as the trigger element.





Caleb Porzio



Caleb Porzio

@calebporzio



Follows you

775

following







50.2k

followers



Following

Message



```
<flux:dropdown hover position="bottom" align="start" offset="-16" gap="10">    <button type="button" class="flex items-center gap-3">        <flux:avatar size="sm" name="Caleb Porzio" src="https://unavatar.io/x/calebporzio" />        <flux:heading>Caleb Porzio</flux:heading>    </button>    <flux:popover class="flex flex-col gap-3 rounded-xl shadow-xl">        <flux:avatar size="xl" name="Caleb Porzio" src="https://unavatar.io/x/calebporzio" />        <div>            <flux:heading size="lg">Caleb Porzio</flux:heading>            <div class="flex items-center gap-2">                <flux:text size="lg">@calebporzio</flux:text>                <flux:badge>Follows you</flux:badge>            </div>        </div>        <div class="flex items-center gap-4">            <flux:text class="flex gap-1"><flux:heading>775</flux:heading> following</flux:text>            <flux:text class="flex gap-1"><flux:heading>50.2k</flux:heading> followers</flux:text>        </div>        <div class="flex gap-2">            <flux:button variant="outline" size="sm" icon="check" icon:class="opacity-75" class="flex-1">Following</flux:button>            <flux:button variant="primary" size="sm" icon="chat-bubble-left-right" icon:class="opacity-75" class="flex-1">Message</flux:button>        </div>    </flux:popover></flux:dropdown>
```



[Log in to view](/login)



## [Position](#position)

Control the position of your popover using the position and align props on the dropdown component.





Top Start

Right Center

Left Center

Bottom End



```
<flux:dropdown position="top" align="start">    <flux:button>...</flux:button>    <flux:popover>...</flux:popover></flux:dropdown><flux:dropdown position="right" align="center">    <flux:button>...</flux:button>    <flux:popover>...</flux:popover></flux:dropdown><flux:dropdown position="left" align="center">    <flux:button>...</flux:button>    <flux:popover>...</flux:popover></flux:dropdown><flux:dropdown position="bottom" align="end">    <flux:button>...</flux:button>    <flux:popover>...</flux:popover></flux:dropdown>
```



[Log in to view](/login)



## [Gap & offset](#gap-offset)

The gap prop controls the distance between the trigger and popover, while offset shifts the popover along its alignment axis.





Gap: 16px

Offset: 32px



```
<!-- Gap --><flux:dropdown gap="16">    <flux:button>Gap: 16px</flux:button>    <flux:popover>...</flux:popover></flux:dropdown><!-- Offset --><flux:dropdown offset="32">    <flux:button>Offset: 32px</flux:button>    <flux:popover>...</flux:popover></flux:dropdown>
```



[Log in to view](/login)

## Examples



### [Category picker](#category-picker)

A list of selectable categories.





Categories

 



Fantasy Science fiction
Horror
Mystery
Romance
Autobiography
Thriller
Poetry
Children


Clear all





Copy to clipboard

```
<flux:dropdown>    <flux:button        icon="tag"        icon:variant="micro"        icon:class="text-zinc-400"    >        Categories        <x-slot name="iconTrailing">            <flux:badge size="sm" class="-mr-1">                <span x-text="$wire.categories.length" class="tabular-nums">&nbsp;</span>            </flux:badge>        </x-slot>    </flux:button>    <flux:popover class="max-w-[18rem] flex flex-col gap-4">        <flux:checkbox.group variant="pills" wire:model="categories">            <flux:checkbox value="fantasy" label="Fantasy" />            <flux:checkbox value="science-fiction" label="Science fiction" />            <flux:checkbox value="horror" label="Horror" />            <flux:checkbox value="mystery" label="Mystery" />            <flux:checkbox value="romance" label="Romance" />            <flux:checkbox value="autobiography" label="Autobiography" />            <flux:checkbox value="thriller" label="Thriller" />            <flux:checkbox value="poetry" label="Poetry" />            <flux:checkbox value="children" label="Children" />        </flux:checkbox.group>        <flux:separator variant="subtle" />        <flux:button            variant="subtle"            size="sm"            class="justify-start -m-2 !px-2"            wire:click="$set('categories', [])"        >            Clear all        </flux:button>    </flux:popover></flux:dropdown>
```



### [Feedback](#feedback)

A feedback form with radio options and a text input.





Feedback

 Bug report  Suggestion  Question

Cancel

esc



Submit

⏎







Copy to clipboard

```
<flux:dropdown>    <flux:button icon="chat-bubble-oval-left" icon:variant="micro" icon:class="text-zinc-300">        Feedback    </flux:button>    <flux:popover class="min-w-[30rem] flex flex-col gap-4">        <flux:radio.group variant="buttons" class="*:flex-1">            <flux:radio icon="bug-ant" checked>Bug report</flux:radio>            <flux:radio icon="light-bulb">Suggestion</flux:radio>            <flux:radio icon="question-mark-circle">Question</flux:radio>        </flux:radio.group>        <div class="relative">            <flux:textarea                rows="8"                class="dark:bg-transparent!"                placeholder="Please include reproduction steps. You may attach images or video files."            />            <div class="absolute bottom-3 left-3 flex items-center gap-2">                <flux:button variant="filled" size="xs" icon="face-smile" icon:variant="outline" icon:class="text-zinc-400 dark:text-zinc-300" />                <flux:button variant="filled" size="xs" icon="paper-clip" icon:class="text-zinc-400 dark:text-zinc-300" />            </div>        </div>        <div class="flex gap-2 justify-end">            <flux:button variant="filled" size="sm" kbd="esc" class="w-28">Cancel</flux:button>            <flux:button size="sm" kbd="⏎" class="w-28">Submit</flux:button>        </div>    </flux:popover></flux:dropdown>
```



### [Event details](#event-details)

Detailed information about an event.





Team sync

10:00 AM



Team sync

Let's review the progress made last week and define the priorities for the next

Going Not going Maybe

Guests

[Invite](#)

1 maybe, 1 awaiting

10:00 AM

11:00 AM

[Edit](#)

May 29 2025

·

Every weekday

Location

[Edit](#)

Paris HQ, 13 rue de la Prairie 75018





Copy to clipboard

```
<flux:dropdown position="bottom center">    <button type="button" class="w-54 rounded-lg p-2 flex items-center gap-2 bg-zinc-100 hover:bg-zinc-200">        <div class="self-stretch w-0.5 bg-zinc-800 rounded-full"></div>        <div>            <flux:heading>Team sync</flux:heading>            <flux:text class="mt-1">10:00 AM</flux:text>        </div>    </button>    <flux:popover class="w-80 p-0 data-open:flex flex-col">        <div class="p-4">            <flux:heading>Team sync</flux:heading>            <flux:text class="mt-2">Let's review the progress made last week and define the priorities for the next</flux:text>            <flux:radio.group variant="segmented" class="mt-3">                <flux:radio value="going" label="Going" checked />                <flux:radio value="not-going" label="Not going" />                <flux:radio value="maybe" label="Maybe" />            </flux:radio.group>        </div>        <flux:separator />        <div class="p-4 flex gap-2">            <flux:icon.users variant="micro" class="text-zinc-400" />            <div class="flex-1">                <div class="flex items-center justify-between">                    <div class="flex gap-2">                        <flux:heading>Guests</flux:heading>                    </div>                    <flux:text><flux:link href="#" variant="subtle">Invite</flux:link></flux:text>                </div>                <div class="flex items-center gap-3 mt-2">                    <flux:avatar.group>                        <flux:avatar size="xs" circle src="https://unavatar.io/x/calebporzio" />                        <flux:avatar size="xs" circle src="https://unavatar.io/github/hugosaintemarie" />                        <flux:avatar size="xs" circle src="https://unavatar.io/github/joshhanley" />                    </flux:avatar.group>                    <flux:text>1 maybe, 1 awaiting</flux:text>                </div>            </div>        </div>        <flux:separator />        <div class="p-4 flex gap-2">            <flux:icon.clock variant="micro" class="text-zinc-400" />            <div class="flex-1">                <div class="flex items-center justify-between">                    <div class="flex gap-2">                        <flux:heading>10:00 AM</flux:heading>                        <flux:icon.arrow-right variant="micro" class="text-zinc-400" />                        <flux:heading>11:00 AM</flux:heading>                    </div>                    <flux:text><flux:link href="#" variant="subtle">Edit</flux:link></flux:text>                </div>                <div class="flex gap-3 mt-2">                    <flux:text>May 29 2025</flux:text>                    <flux:text>·</flux:text>                    <flux:text class="flex items-center gap-1.5">                        <flux:icon.arrow-path-rounded-square variant="micro" class="text-zinc-400" />                        Every weekday                    </flux:text>                </div>            </div>        </div>        <flux:separator />        <div class="p-4 flex gap-2">            <flux:icon.map-pin variant="micro" class="text-zinc-400" />            <div class="flex-1">                <div class="flex items-center justify-between">                    <flux:heading>Location</flux:heading>                    <flux:text><flux:link href="#" variant="subtle">Edit</flux:link></flux:text>                </div>                <flux:text class="mt-2">Paris HQ, 13 rue de la Prairie 75018</flux:text>            </div>        </div>    </flux:popover></flux:dropdown>
```

## Related components

[Dropdown Create dropdown menus with buttons and menu items](/components/dropdown) [Tooltip Display informative tooltips when hovering over an element](/components/tooltip)

## Reference



### [flux:dropdown](#fluxdropdown)

The container component that manages popover positioning and interaction. Required wrapper for all popovers.

| Prop | Description |
| --- | --- |
| position | Position of the popover relative to the trigger element. Options: top, right, bottom (default), left. |
| align | Alignment of the popover relative to the trigger element. Options: start (default), center, end. |
| hover | If present, the popover opens on hover instead of click. Useful for tooltips and quick previews. |
| wire:model | Bind the open/closed state to a Livewire property for programmatic control. |

| Slot | Description |
| --- | --- |
| default | Must contain exactly one trigger element (button, link, etc.) followed by one flux:popover component. |

| Attribute | Description |
| --- | --- |
| data-flux-dropdown | Applied to the root element for styling and identification. |
| data-open | Applied when the popover is currently open. |



### [flux:popover](#fluxpopover)

A container component that displays content in a floating overlay. Must be used within a flux:dropdown component for positioning and interaction.

| Prop | Description |
| --- | --- |
| class | Additional CSS classes to apply to the popover container. Useful for setting width constraints like max-w-sm or w-80. |

| Slot | Description |
| --- | --- |
| default | The content to display inside the popover. Can include any HTML or Flux components. |

| Attribute | Description |
| --- | --- |
| data-flux-popover | Applied to the root element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0039_Profile

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




# 0040_Radio

# Radio

Select one option from a set of mutually exclusive choices. Perfect for single-choice questions and settings.





Select your payment method
Credit Card

Paypal

Bank transfer





Copy to clipboard

```
<flux:radio.group wire:model="payment" label="Select your payment method">    <flux:radio value="cc" label="Credit Card" checked />    <flux:radio value="paypal" label="Paypal" />    <flux:radio value="ach" label="Bank transfer" /></flux:radio.group>
```



## [With descriptions](#with-descriptions)

Align descriptions for each radio directly below its label.





Role
Administrator Administrator users can perform any action.


Editor Editor users have the ability to read, create, and update.


Viewer Viewer users only have the ability to read. Create, and update are restricted.






Copy to clipboard

```
<flux:radio.group label="Role">    <flux:radio        name="role"        value="administrator"        label="Administrator"        description="Administrator users can perform any action."        checked    />    <flux:radio        name="role"        value="editor"        label="Editor"        description="Editor users have the ability to read, create, and update."    />    <flux:radio        name="role"        value="viewer"        label="Viewer"        description="Viewer users only have the ability to read. Create, and update are restricted."    /></flux:radio.group>
```



## [Within fieldset](#within-fieldset)

Group radio inputs inside a fieldset and provide more context with descriptions for each radio option.





Role
Administrator Administrator users can perform any action.


Editor Editor users have the ability to read, create, and update.


Viewer Viewer users only have the ability to read. Create, and update are restricted.





Copy to clipboard

```
<flux:fieldset>    <flux:legend>Role</flux:legend>    <flux:radio.group>        <flux:radio            value="administrator"            label="Administrator"            description="Administrator users can perform any action."            checked        />        <flux:radio            value="editor"            label="Editor"            description="Editor users have the ability to read, create, and update."        />        <flux:radio            value="viewer"            label="Viewer"            description="Viewer users only have the ability to read. Create, and update are restricted."        />    </flux:radio.group></flux:fieldset>
```



## [Segmented](#segmented)

A more compact alternative to standard radio buttons.





Role Admin Editor Viewer





Copy to clipboard

```
<flux:radio.group wire:model="role" label="Role" variant="segmented">    <flux:radio label="Admin" />    <flux:radio label="Editor" />    <flux:radio label="Viewer" /></flux:radio.group>
```

You can also use the size="sm" prop to make the radios smaller.





Role Admin Editor Viewer





Copy to clipboard

```
<flux:radio.group wire:model="role" label="Role" variant="segmented" size="sm">    <flux:radio label="Admin" />    <flux:radio label="Editor" />    <flux:radio label="Viewer" /></flux:radio.group>
```



## [Segmented with icons](#segmented-with-icons)

Combine segmented radio buttons with icon prefixes.





Role Admin Editor Viewer





Copy to clipboard

```
<flux:radio.group wire:model="role" variant="segmented">    <flux:radio label="Admin" icon="wrench" />    <flux:radio label="Editor" icon="pencil-square" />    <flux:radio label="Viewer" icon="eye" /></flux:radio.group>
```



## [Radio cards](#radio-cards)

A bordered alternative to standard radio buttons.





Shipping

Standard

4-10 business days

Fast

2-5 business days

Next day

1 business day





Copy to clipboard

```
<flux:radio.group wire:model="shipping" label="Shipping" variant="cards" class="max-sm:flex-col">    <flux:radio value="standard" label="Standard" description="4-10 business days" checked />    <flux:radio value="fast" label="Fast" description="2-5 business days" />    <flux:radio value="next-day" label="Next day" description="1 business day" /></flux:radio.group>
```

You can swap between vertical and horizontal card layouts by conditionally applying flex-col based on the viewport.



Copy to clipboard

```
<flux:radio.group ... class="max-sm:flex-col">    <!-- ... --></flux:radio.group>
```



## [Vertical cards](#vertical-cards)

You can arrange a set of radio cards vertically by simply adding the flex-col class to the group container.





Shipping

Standard

4-10 business days

Fast

2-5 business days

Next day

1 business day





Copy to clipboard

```
<flux:radio.group label="Shipping" variant="cards" class="flex-col">    <flux:radio value="standard" label="Standard" description="4-10 business days" />    <flux:radio value="fast" label="Fast" description="2-5 business days" />    <flux:radio value="next-day" label="Next day" description="1 business day" /></flux:radio.group>
```



## [Cards with icons](#cards-with-icons)

You can arrange a set of radio cards vertically by simply adding the flex-col class to the group container.





Shipping

Standard

4-10 business days

Fast

2-5 business days

Next day

1 business day





Copy to clipboard

```
<flux:radio.group label="Shipping" variant="cards" class="max-sm:flex-col">    <flux:radio value="standard" icon="truck" label="Standard" description="4-10 business days" />    <flux:radio value="fast" icon="cube" label="Fast" description="2-5 business days" />    <flux:radio value="next-day" icon="clock" label="Next day" description="1 business day" /></flux:radio.group>
```



## [Cards without indicators](#cards-without-indicators)

For a cleaner look, you can remove the radio indicator using :indicator="false".





Shipping

Standard

4-10 business days

Fast

2-5 business days

Next day

1 business day





Copy to clipboard

```
<flux:radio.group label="Shipping" variant="cards" :indicator="false" class="max-sm:flex-col">    <flux:radio value="standard" icon="truck" label="Standard" description="4-10 business days" />    <flux:radio value="fast" icon="cube" label="Fast" description="2-5 business days" />    <flux:radio value="next-day" icon="clock" label="Next day" description="1 business day" /></flux:radio.group>
```



## [Custom card content](#custom-card-content)

You can compose your own custom cards through the flux:radio component slot.





Shipping

Standard

4-10 business days

Fast

2-5 business days

Next day

1 business day





Copy to clipboard

```
<flux:radio.group label="Shipping" variant="cards" class="max-sm:flex-col">    <flux:radio value="standard" checked>        <flux:radio.indicator />        <div class="flex-1">            <flux:heading class="leading-4">Standard</flux:heading>            <flux:text size="sm" class="mt-2">4-10 business days</flux:text>        </div>    </flux:radio>    <flux:radio value="fast">        <flux:radio.indicator />        <div class="flex-1">            <flux:heading class="leading-4">Fast</flux:heading>            <flux:text size="sm" class="mt-2">2-5 business days</flux:text>        </div>    </flux:radio>    <flux:radio value="next-day">        <flux:radio.indicator />        <div class="flex-1">            <flux:heading class="leading-4">Next day</flux:heading>            <flux:text size="sm" class="mt-2">1 business day</flux:text>        </div>    </flux:radio></flux:radio.group>
```



## [Pills](#pills)

Compact, rounded radio buttons that look like tags or badges. Perfect for filters, categories, and any time you want lightweight selectable options.





Priority Low
Medium
High
Critical






Copy to clipboard

```
<flux:radio.group wire:model="priority" label="Priority" variant="pills">    <flux:radio value="low" label="Low" />    <flux:radio value="medium" label="Medium" />    <flux:radio value="high" label="High" />    <flux:radio value="critical" label="Critical" /></flux:radio.group>
```



## [Buttons](#buttons)

Button-style radio options that look like a toolbar. Perfect for action selections and grouped controls where you want a more prominent visual style.





Feedback type  Bug report  Suggestion  Question





Copy to clipboard

```
<flux:radio.group variant="buttons" class="w-full *:flex-1" label="Feedback type">    <flux:radio icon="bug-ant" checked>Bug report</flux:radio>    <flux:radio icon="light-bulb">Suggestion</flux:radio>    <flux:radio icon="question-mark-circle">Question</flux:radio></flux:radio.group>
```

## Related components

[Field Structured form field with label and validation states](/components/field) [Checkbox Toggleable input control for making multiple selections](/components/checkbox) [Select Dropdown selection menus for choosing from options](/components/select)

## Reference



### [flux:radio.group](#fluxradiogroup)

| Prop | Description |
| --- | --- |
| wire:model | Binds the radio group selection to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| label | Label text displayed above the radio group. When provided, wraps the radio group in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the radio group. When provided alongside label, appears between the label and radio group within the flux:field wrapper. See the [field component](/components/field). |
| variant | Visual style of the group. Options: default, segmented, cards, pills, buttons. |
| invalid | Applies error styling to the radio group. |

| Slot | Description |
| --- | --- |
| default | The radio buttons to be grouped together. |

| Attribute | Description |
| --- | --- |
| data-flux-radio-group | Applied to the root element for styling and identification. |



### [flux:radio](#fluxradio)

| Prop | Description |
| --- | --- |
| label | Label text displayed above the radio button. When provided, wraps the radio button in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the radio button. When provided alongside label, appears between the label and radio button within the flux:field wrapper. See the [field component](/components/field). |
| value | Value associated with the radio button when used in a group. |
| checked | If true, the radio button is selected by default. |
| disabled | Prevents user interaction with the radio button. |
| icon | Name of the icon to display (for segmented variant). |

| Slot | Description |
| --- | --- |
| default | Custom content for card variant. |

| Attribute | Description |
| --- | --- |
| data-flux-radio | Applied to the root element for styling and identification. |
| data-checked | Applied when the radio button is selected. |



### [flux:radio.indicator](#fluxradioindicator)

Used for custom radio button layouts in card variant.

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0041_SelectNew

# Select

Choose a single option from a dropdown list.

For lists of up to 5 items, consider using [checkboxes](/components/checkbox) or [radio buttons](/components/radio) instead.





* Choose industry...
Photography
 Design services
 Web development
 Accounting
 Legal services
 Consulting
 Other





Copy to clipboard

```
<flux:select wire:model="industry" placeholder="Choose industry...">    <flux:select.option>Photography</flux:select.option>    <flux:select.option>Design services</flux:select.option>    <flux:select.option>Web development</flux:select.option>    <flux:select.option>Accounting</flux:select.option>    <flux:select.option>Legal services</flux:select.option>    <flux:select.option>Consulting</flux:select.option>    <flux:select.option>Other</flux:select.option></flux:select>
```



## [Small](#small)

A smaller select element for more compact layouts.





* Choose industry...
Photography
 Design services
 Web development
 Accounting
 Legal services
 Consulting
 Other





Copy to clipboard

```
<flux:select size="sm" placeholder="Choose industry...">    <flux:select.option>Photography</flux:select.option>    <flux:select.option>Design services</flux:select.option>    <flux:select.option>Web development</flux:select.option>    <flux:select.option>Accounting</flux:select.option>    <flux:select.option>Legal services</flux:select.option>    <flux:select.option>Consulting</flux:select.option>    <flux:select.option>Other</flux:select.option></flux:select>
```



## [Custom select](#custom-select)

An alternative to the browser's native select element. Typically used when you need custom option styling like icons, images, and other treatments.



This variant is only available in the Pro version of Flux.



[Upgrade to unlock ->](/pricing)





Photography

Design services

Web development

Accounting

Legal services

Consulting

Other





Copy to clipboard

```
<flux:select variant="listbox" placeholder="Choose industry...">    <flux:select.option>Photography</flux:select.option>    <flux:select.option>Design services</flux:select.option>    <flux:select.option>Web development</flux:select.option>    <flux:select.option>Accounting</flux:select.option>    <flux:select.option>Legal services</flux:select.option>    <flux:select.option>Consulting</flux:select.option>    <flux:select.option>Other</flux:select.option></flux:select>
```



## The button slot

If you need full control over the button used to trigger the custom select, you can use the button slot to render it yourself.

Copy to clipboard

```
<flux:select variant="listbox">    <x-slot name="button">        <flux:select.button class="rounded-full!" placeholder="Choose industry..." :invalid="$errors->has('...')" />    </x-slot>    <flux:select.option>Photography</flux:select.option>    ...</flux:select>
```



## Clearable

If you want to make the selected value clearable, you can use the clearable prop to add an "x" button to the right side of the input:

Copy to clipboard

```
<flux:select variant="listbox" clearable>    ...</flux:select>
```



## Options with images/icons

One distinct advantage of using a custom listbox select over the native <select> element is that you can now add icons and images to your options.





Owner

Administrator

Member

Viewer





Copy to clipboard

```
<flux:select variant="listbox" placeholder="Select role...">    <flux:select.option>        <div class="flex items-center gap-2">            <flux:icon.shield-check variant="mini" class="text-zinc-400" /> Owner        </div>    </flux:select.option>    <flux:select.option>        <div class="flex items-center gap-2">            <flux:icon.key variant="mini" class="text-zinc-400" /> Administrator        </div>    </flux:select.option>    <flux:select.option>        <div class="flex items-center gap-2">            <flux:icon.user variant="mini" class="text-zinc-400" /> Member        </div>    </flux:select.option>    <flux:select.option>        <div class="flex items-center gap-2">            <flux:icon.eye variant="mini" class="text-zinc-400" /> Viewer        </div>    </flux:select.option></flux:select>
```



## [Searchable select](#searchable-select)

The searchable select variant makes navigating large option lists easier for your users.



This variant is only available in the Pro version of Flux.



[Upgrade to unlock ->](/pricing)





No results found

Photography

Design services

Web development

Accounting

Legal services

Consulting

Other





Copy to clipboard

```
<flux:select variant="listbox" searchable placeholder="Choose industries...">    <flux:select.option>Photography</flux:select.option>    <flux:select.option>Design services</flux:select.option>    <flux:select.option>Web development</flux:select.option>    <flux:select.option>Accounting</flux:select.option>    <flux:select.option>Legal services</flux:select.option>    <flux:select.option>Consulting</flux:select.option>    <flux:select.option>Other</flux:select.option></flux:select>
```



## The search slot

If you need full control over the search field inside the listbox, you can use the search slot to render it yourself.

Copy to clipboard

```
<flux:select variant="listbox" searchable>    <x-slot name="search">        <flux:select.search class="px-4" placeholder="Search industries..." />    </x-slot>    ...</flux:select>
```



## [Multiple select](#multiple-select)

Allow your users to select multiple options from a list of options.



This variant is only available in the Pro version of Flux.



[Upgrade to unlock ->](/pricing)





Photography

Design services

Web development

Accounting

Legal services

Consulting

Other





Copy to clipboard

```
<flux:select variant="listbox" multiple placeholder="Choose industries...">    <flux:select.option>Photography</flux:select.option>    <flux:select.option>Design services</flux:select.option>    <flux:select.option>Web development</flux:select.option>    <flux:select.option>Accounting</flux:select.option>    <flux:select.option>Legal services</flux:select.option>    <flux:select.option>Consulting</flux:select.option>    <flux:select.option>Other</flux:select.option></flux:select>
```



## Selected suffix

By default, when more than one option is selected, the suffix " selected" will be appended to the number of selected options. You can customize this language by passing a selected-suffix prop to the select component.

Copy to clipboard

```
<flux:select variant="listbox" selected-suffix="industries selected" multiple>    ...</flux:select>
```

If you pass a custom suffix, and need localization, you can use the __() helper function to translate the suffix:

Copy to clipboard

```
<flux:select variant="listbox" selected-suffix="{{ __('industries selected') }}" multiple>    ...</flux:select>
```



## Checkbox indicator

If you prefer a checkbox indicator instead of the default checkmark icon, you can use the indicator="checkbox" prop.

Copy to clipboard

```
<flux:select variant="listbox" indicator="checkbox" multiple>    ...</flux:select>
```



## Clearing search

By default, a searchable select will clear the search input when the user selects an option. If you want to disable this behavior, you can use the clear="close" prop to only clear the search input when the user closes the select.

Copy to clipboard

```
<flux:select variant="listbox" searchable multiple clear="close">    ...</flux:select>
```



## [Combobox](#combobox)

A versatile combobox that can be used for anything from basic autocomplete to complex multi-selects.



This variant is only available in the Pro version of Flux.



[Upgrade to unlock ->](/pricing)





No results found

Photography

Design services

Web development

Accounting

Legal services

Consulting

Other





Copy to clipboard

```
<flux:select variant="combobox" placeholder="Choose industry...">    <flux:select.option>Photography</flux:select.option>    <flux:select.option>Design services</flux:select.option>    <flux:select.option>Web development</flux:select.option>    <flux:select.option>Accounting</flux:select.option>    <flux:select.option>Legal services</flux:select.option>    <flux:select.option>Consulting</flux:select.option>    <flux:select.option>Other</flux:select.option></flux:select>
```



## The input slot

If you need full control over the input element used to trigger the combobox, you can use the input slot to render it yourself.

Copy to clipboard

```
<flux:select variant="combobox">    <x-slot name="input">        <flux:select.input x-model="search" :invalid="$errors->has('...')" />    </x-slot>    ...</flux:select>
```



## [Backend search](#backend-search)

If you want to dynamically generate options on the server, you can use the :filter="false" prop to disable client-side filtering.



This variant is only available in the Pro version of Flux.



[Upgrade to unlock ->](/pricing)





Copy to clipboard

```
<flux:select wire:model="userId" variant="combobox" :filter="false">    <x-slot name="input">        <flux:select.input wire:model.live="search" />    </x-slot>    @foreach ($this->users as $user)        <flux:select.option value="{{ $user->id }}" wire:key="{{ $user->id }}">            {{ $user->name }}        </flux:select.option>    @endforeach</flux:select><!--public $search = '';public $userId = null;#[\Livewire\Attributes\Computed]public function users() {    return \App\Models\User::query()        ->when($this->search, fn($query) => $query->where('name', 'like', '%' . $this->search . '%'))        ->limit(20)        ->get();}-->
```



## [Create option](#create-option)

Allow users to the create new options using the <flux:select.option.create> component.

Flux will automatically hide the create option when the search input matches an existing item in the list. You can also specify the minimum number of characters required for the create option to appear using the min-length prop.



This variant is only available in the Pro version of Flux.



[Upgrade to unlock ->](/pricing)





No results found

Branding

Analytics

Infrastructure

Documentation

Security

Performance

Create ""





Copy to clipboard

```
<flux:select wire:model="projectId" variant="combobox">    <x-slot name="input">        <flux:select.input wire:model="search" placeholder="Start typing..." />    </x-slot>    @foreach ($this->projects as $project)        <flux:select.option :wire:key="$project->id">{{ $project->name }}</flux:select.option>    @endforeach    <flux:select.option.create wire:click="createProject" min-length="2">        Create "<span wire:text="search"></span>"    </flux:select.option.create></flux:select><!--public $search = '';public $projectId = null;public function createProject(){    $project = Project::create([        'name' => $this->search,    ]);    $this->projectId = $project->id;}-->
```



### [With backend search](#with-backend-search)

If you're using :filter="false", make sure to adjust your query to always include the newly created item when the search input is cleared.

Flux will automatically disable the create option during requests to prevent duplicate entries and when the list is updated, it performs a uniqueness check on the frontend.





No results found

Branding

Analytics

Infrastructure

Documentation

Security

Performance

Create ""





Copy to clipboard

```
<flux:select wire:model="projectId" variant="combobox" :filter="false">    <x-slot name="input">        <flux:select.input wire:model.live="search" placeholder="Start typing..." />    </x-slot>    @foreach($this->projects as $project)        <flux:select.option :value="$project->id">{{ $project->name }}</flux:select.option>    @endforeach    <flux:select.option.create wire:click="createProject" min-length="2">        Create "<span wire:text="search"></span>"    </flux:select.option.create></flux:select><!--#[\Livewire\Attributes\Computed]public function projects() {    return Project::query()        ->where('name', 'like', '%' . trim($this->search) . '%')        ->limit(20)->get()        ->when(blank($this->search) && $this->projectId, function ($results) {            return Project::query()                ->whereIn('id', [$this->projectId])                ->whereNotIn('id', $results->pluck('id'))                ->get()->merge($results);        });}-->
```



## With listbox variant

If you're using the listbox variant with backend search, make sure to clear the search input after creation to prevent an additional request from being sent when the search input is cleared by the frontend.

Copy to clipboard

```
public function createProject() {    // Create logic...    $this->search = '';}
```



## Loading message

When then create option is hidden by the frontend but new results aren't available yet, Flux displays a special "Loading..." message. To customize this message, use the when-loading prop on the <flux:select.option.empty> component.

Copy to clipboard

```
<flux:select wire:model="projectId" variant="combobox" :filter="false">    ...    <x-slot name="empty">        <flux:select.option.empty when-loading="Loading projects...">            No projects found.        </flux:select.option.empty>    </x-slot></flux:select>
```



### [With validation](#with-validation)

When you perform additional validation on the backend, the search input will indicate an invalid state when there are validation errors present. Make sure to reset the error bag when the user updates the input.





No results found

Branding

Analytics

Infrastructure

Documentation

Security

Performance

Create ""





Copy to clipboard

```
<flux:select wire:model="projectId" variant="combobox" :filter="false">    <x-slot name="input">        <flux:select.input wire:model.live="search" placeholder="Start typing..." />    </x-slot>    ...    <flux:select.option.create wire:click="createProject" min-length="2">        Create "<span wire:text="search"></span>"    </flux:select.option.create></flux:select><!--public function createProject() {    $this->validate(['search' => 'required|unique:projects,name']);    // Create logic...}public function updatedSearch() {    $this->resetErrorBag('search');}-->
```



### [With modal](#with-modal)

Use the modal prop to specify a name of a modal and handle more complex creation workflows inside a form.







Branding

Analytics

Infrastructure

Documentation

Security

Performance

Create new

Create new project

Enter the name of the new project.

Name

Create





Copy to clipboard

```
<flux:select wire:model="projectId" variant="listbox">    @foreach($this->projects as $project)        <flux:select.option :value="$project->id">{{ $project->name }}</flux:select.option>    @endforeach    <flux:select.option.create modal="create-project">Create new</flux:select.option></flux:select><flux:modal name="create-project" class="md:w-96">    <form wire:submit="createProject" class="space-y-6">        <div>            <flux:heading size="lg">Create new project</flux:heading>            <flux:text class="mt-2">Enter the name of the new project.</flux:text>        </div>        <flux:input wire:model="projectName" label="Name" placeholder="e.g. 'UX Research'" />        <div class="flex">            <flux:spacer />            <flux:button type="submit" variant="primary">Create</flux:button>        </div>    </form></flux:modal>
```

## Related components

[Field Structured form field with label and validation states](/components/field) [Pillbox Pill-based selection component](/components/pillbox) [Radio Control for selecting one option from many](/components/radio)

## Reference



### [flux:select](#fluxselect)

| Prop | Description |
| --- | --- |
| wire:model | Binds the select to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| placeholder | Text displayed when no option is selected. |
| label | Label text displayed above the select. When provided, wraps the select in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the select. When provided alongside label, appears between the label and select within the flux:field wrapper. See the [field component](/components/field). |
| description:trailing | The description provided will be displayed below the select instead of above it. |
| badge | Badge text displayed at the end of the flux:label component when the label prop is provided. |
| size | Size of the select. Options: sm, xs. |
| variant | Visual style of the select. Options: default (native select), listbox, combobox. |
| multiple | Allows selecting multiple options (listbox variant only). |
| filter | If false, disables client-side filtering. |
| searchable | Adds a search input to filter options (listbox and combobox variants only). |
| empty | Message shown when no search results are found for searchable selects. Default: No results found. |
| clearable | Displays a clear button when an option is selected (listbox and combobox variants only). |
| selected-suffix | Text appended to the number of selected options in multiple mode (listbox variant only). |
| clear | When to clear the search input. Options: select (default), close (listbox and combobox variants only). |
| disabled | Prevents user interaction with the select. |
| invalid | Applies error styling to the select. |

| Slot | Description |
| --- | --- |
| default | The select options. |
| trigger | Custom trigger content. Typically the select.button or select.input component (listbox and combobox variants only). |
| empty | Custom content shown when no options are found for searchable selects. Typically the select.option.empty component (listbox and combobox variants only). |

| Attribute | Description |
| --- | --- |
| data-flux-select | Applied to the root element for styling and identification. |



### [flux:select.option](#fluxselectoption)

| Prop | Description |
| --- | --- |
| value | Value associated with the option. |
| label | Text content displayed for the option. |
| selected-label | Text content displayed when the option is selected. |
| disabled | Prevents selecting the option. |

| Slot | Description |
| --- | --- |
| default | The option content (can include icons, images, etc. in listbox variant). |



### [flux:select.option.create](#fluxselectoptioncreate)

| Prop | Description |
| --- | --- |
| min-length | Minimum number of characters required in the search input before displaying the create option. |
| modal | Name of the modal to open when the option is selected. |
| wire:click | Livewire action to call when the option is selected. |



### [flux:select.option.empty](#fluxselectoptionempty)

| Prop | Description |
| --- | --- |
| when-loading | Message displayed when options are loading. |

| Slot | Description |
| --- | --- |
| default | Message displayed when no options are found. |



### [flux:select.button](#fluxselectbutton)

| Prop | Description |
| --- | --- |
| placeholder | Text displayed when no option is selected. |
| invalid | Applies error styling to the button. |
| size | Size of the button. Options: sm, xs. |
| disabled | Prevents selecting the option. |
| clearable | Displays a clear button when an option is selected. |



### [flux:select.input](#fluxselectinput)

| Prop | Description |
| --- | --- |
| placeholder | Text displayed when no option is selected. |
| invalid | Applies error styling to the input. |
| size | Size of the input. Options: sm, xs. |



### [flux:select.search](#fluxselectsearch)

| Prop | Description |
| --- | --- |
| placeholder | Placeholder text displayed when the input is empty. |
| icon | Name of the icon displayed at the start of the input. |
| clearable | Displays a clear button when the input has content. Default: true. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0042_Separator

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




# 0043_SkeletonNew

# Skeleton

Create placeholder content while loading data.











Copy to clipboard

```
<flux:skeleton.group animate="shimmer" class="flex items-center gap-4">    <flux:skeleton class="size-10 rounded-full" />    <div class="flex-1">        <flux:skeleton.line />        <flux:skeleton.line class="w-1/2" />    </div></flux:skeleton.group>
```



## [Line of text](#line-of-text)

Create a loading state for a single line of text. The flux:skeleton.line component occupies the full spatial line-height (e.g., ~20px) while rendering a slimmer bar, giving it the visual proportions of real text.















Copy to clipboard

```
<flux:skeleton.group animate="shimmer">    <flux:skeleton.line class="mb-2 w-1/4" />    <flux:skeleton.line />    <flux:skeleton.line />    <flux:skeleton.line class="w-3/4" /></flux:skeleton.group>
```



## [Animation](#animation)

Use the animate prop to add an animation to the skeleton.





None

Shimmer

Pulse





Copy to clipboard

```
<flux:skeleton /><flux:skeleton animate="shimmer" /><flux:skeleton animate="pulse" />
```



## [Examples](#examples)

Here are some examples of different ways you can use the skeleton component.



### [Table](#table)

Use the skeleton component to create a loading state for a table.





| Customer | Date | Status | Amount |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |





Copy to clipboard

```
<flux:skeleton.group animate="shimmer">    <flux:table>        <flux:table.columns>            <flux:table.column>Customer</flux:table.column>            <flux:table.column>Date</flux:table.column>            <flux:table.column>Status</flux:table.column>            <flux:table.column>Amount</flux:table.column>        </flux:table.columns>        <flux:table.rows>            @foreach (range(1, 5) as $order)                <flux:table.row>                    <flux:table.cell>                        <div class="flex items-center gap-2">                            <flux:skeleton class="rounded-full size-5" />                            <div class="flex-1">                                <flux:skeleton.line style="width: {{ rand(50, 100) }}%" />                            </div>                        </div>                    </flux:table.cell>                    <flux:table.cell>                        <flux:skeleton.line />                    </flux:table.cell>                    <flux:table.cell>                        <flux:skeleton.line />                    </flux:table.cell>                    <flux:table.cell>                        <flux:skeleton.line />                    </flux:table.cell>                </flux:table.row>            @endforeach        </flux:table.rows>    </flux:table></flux:skeleton.group>
```



### [Chart](#chart)

Use the skeleton component to create a loading state for a chart.





Today

$---

-:-- PM

Yesterday

$---





Copy to clipboard

```
<flux:card class="dark:bg-zinc-800">    <div class="flex flex-col gap-6">        <div class="flex gap-12">            <div>                <flux:text>Today</flux:text>                <flux:heading size="xl" class="mt-2 tabular-nums">$---</flux:heading>                <flux:text class="mt-2 tabular-nums">-:-- PM</flux:text>            </div>            <div>                <flux:text>Yesterday</flux:text>                <flux:heading size="lg" class="mt-2 tabular-nums">$---</flux:heading>            </div>        </div>        <flux:skeleton animate="shimmer" class="aspect-[4/1] size-full rounded-lg" />    </div></flux:card>
```

## Reference



### [flux:skeleton](#fluxskeleton)

| Prop | Description |
| --- | --- |
| animate | Animation style for the skeleton. Options: shimmer, pulse. Defaults to no animation. |

| Slot | Description |
| --- | --- |
| default | The skeleton elements (lines, boxes, circles). |

| CSS Variable | Description |
| --- | --- |
| --flux-shimmer-color | The background color used for the shimmer animation. Defaults to white in light mode and var(--color-zinc-900) in dark mode. Set this to match your page's background color to prevent the shimmer from showing through gaps between skeleton elements. |

| Attribute | Description |
| --- | --- |
| data-flux-skeleton | Applied to the root element for styling and identification. |



### [flux:skeleton.line](#fluxskeletonline)

| Prop | Description |
| --- | --- |
| size | Size of the line. Options: base, lg. Defaults to base. |
| animate | Animation style for the skeleton. Options: shimmer, pulse. Defaults to no animation. Can be inherited from parent flux:skeleton.group. |

| Attribute | Description |
| --- | --- |
| data-flux-skeleton-line | Applied to the root element for styling and identification. |



### [flux:skeleton.group](#fluxskeletongroup)

| Prop | Description |
| --- | --- |
| animate | Animation style for all skeleton elements within the group. Options: shimmer, pulse. Defaults to no animation. This value is inherited by child flux:skeleton and flux:skeleton.line components. |

| Attribute | Description |
| --- | --- |
| data-flux-skeleton-group | Applied to the root element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0044_SliderNew



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Slider

Select a value using a horizontal slider control.









Copy to clipboard

```
<flux:slider wire:model="amount" />
```



## [Min/max/step](#minmaxstep)

Use the min, max and step props to configure the slider.









Copy to clipboard

```
<flux:slider min="0" max="100" step="10" />
```



## [Displaying value](#displaying-value)

To display the current value, add an element with a wire:text directive.





Corner radius





Copy to clipboard

```
<flux:field>    <flux:label>        Corner radius        <x-slot name="trailing">            <span wire:text="amount" class="tabular-nums"></span>        </x-slot>    </flux:label>    <flux:slider wire:model="amount" /></flux:field>
```



## [With input](#with-input)

To display an input next to the slider and ensure accessibility, wrap both inside flux:field.





Corner radius





Copy to clipboard

```
<flux:field>    <flux:label>Corner radius</flux:label>    <div class="flex items-center gap-4 -mt-2">        <flux:slider wire:model="amount" />        <flux:input wire:model="amount" type="number" size="sm" class="max-w-18" />    </div></flux:field>
```



## [Big steps](#big-steps)

Use the big-step prop to define a step size that will be be used when pressing the arrow keys while holding the shift key.





Hold ⇧ and press arrow keys to adjust the value by 10.





Copy to clipboard

```
<flux:slider step="1" big-step="10" />
```



## [Step marks](#step-marks)

Display ticks below the slider to visualize the steps.









Copy to clipboard

```
<flux:slider min="1" max="5">    @foreach (range(1, 5) as $i)        <flux:slider.tick :value="$i" />    @endforeach</flux:slider>
```



## [Numbered steps](#numbered-steps)

Display numbers below the slider to visualize the steps.







1



2



3



4



5





Copy to clipboard

```
<flux:slider min="1" max="5">    @foreach (range(1, 5) as $i)        <flux:slider.tick :value="$i">{{ $i }}</flux:slider.tick>    @endforeach</flux:slider>
```



## [Custom steps](#custom-steps)

Display custom labels for specified steps.





Low



Mid



High





Copy to clipboard

```
<flux:slider min="1" max="5">    <flux:slider.tick value="1">Low</flux:slider.tick>    <flux:slider.tick value="3">Mid</flux:slider.tick>    <flux:slider.tick value="5">High</flux:slider.tick></flux:slider>
```



## [Range slider](#range-slider)

Select a range of values using two slider thumbs.









Copy to clipboard

```
<flux:slider range />
```



## Basic usage

Set the initial range using the value prop with comma separated values:

Copy to clipboard

```
<flux:slider range value="20,80" />
```

You can also bind the values to a Livewire property using wire:model:

Copy to clipboard

```
<flux:slider range wire:model="range" />
```

Now you can access the values from your Livewire component using an array of values:

Copy to clipboard

```
<?phpuse Livewire\Component;class Dashboard extends Component {    public array $range = [20, 80];}
```



### [Min steps between](#min-steps-between)

Use min-steps-between to set the minimum distance between thumbs. The value is defined in number of steps, where the size of each step is determined by the step attribute.









Copy to clipboard

```
<flux:slider range step="1" min-steps-between="10" />
```



### [Displaying values](#displaying-values)

To display the selected range, add two elements with a wire:text directive.





Price range

$ –
 $





Copy to clipboard

```
<div class="relative">    <flux:field>        <flux:label>            Price range            <x-slot name="trailing">                $<span wire:text="range[0]" class="tabular-nums"></span>                &ndash;                $<span wire:text="range[1]" class="tabular-nums"></span>            </x-slot>        </flux:label>        <flux:slider range wire:model="range" min="0" max="990" step="10" min-steps-between="10" big-step="100" />    </flux:field></div>
```



## [Custom styles](#custom-styles)

Customize the styles of the slider using the track:class and thumb:class props.









Copy to clipboard

```
<flux:slider track:class="h-5" thumb:class="size-5" />
```

## Related components

[Field Structured form field with label and validation](/components/field) [Input Text fields for collecting user input](/components/input)

## Reference



### [flux:slider](#fluxslider)

| Prop | Description |
| --- | --- |
| range | Enables range selection. |
| min | Minimum value of the slider. |
| max | Maximum value of the slider. |
| step | Step size of the slider. |
| big-step | Step size of the slider when holding shift. |
| min-steps-between | Minimum distance between thumbs in number of steps. |
| track:class | CSS classes applied to the track. |
| thumb:class | CSS classes applied to the thumb. |



### [flux:slider.tick](#fluxslidertick)

| Prop | Description |
| --- | --- |
| value | The value at which the tick should be displayed. |

| Slot | Description |
| --- | --- |
| default | The tick label. If left empty, displays a horizontal line. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0045_Switch

# Switch

Toggle a setting on or off. Suitable for binary options like enabling or disabling features.

Use switches as auto-saving controls outside forms; checkboxes otherwise.





Enable notifications





Copy to clipboard

```
<flux:field variant="inline">    <flux:label>Enable notifications</flux:label>    <flux:switch wire:model.live="notifications" />    <flux:error name="notifications" /></flux:field>
```



## [Fieldset](#fieldset)

Group related switches within a fieldset.





Email notifications


 Communication emails Receive emails about your account activity.



 Marketing emails Receive emails about new products, features, and more.



 Social emails Receive emails for friend requests, follows, and more.



 Security emails Receive emails about your account activity and security.





Copy to clipboard

```
<flux:fieldset>    <flux:legend>Email notifications</flux:legend>    <div class="space-y-4">        <flux:switch wire:model.live="communication" label="Communication emails" description="Receive emails about your account activity." />        <flux:separator variant="subtle" />        <flux:switch wire:model.live="marketing" label="Marketing emails" description="Receive emails about new products, features, and more." />        <flux:separator variant="subtle" />        <flux:switch wire:model.live="social" label="Social emails" description="Receive emails for friend requests, follows, and more." />        <flux:separator variant="subtle" />        <flux:switch wire:model.live="security" label="Security emails" description="Receive emails about your account activity and security." />    </div></flux:fieldset>
```



## [Left align](#left-align)

Left align switches for more compact layouts using the align prop.





Email notifications


 Communication emails

 Marketing emails

 Social emails

 Security emails





Copy to clipboard

```
<flux:fieldset>    <flux:legend>Email notifications</flux:legend>    <div class="space-y-3">        <flux:switch label="Communication emails" align="left" />        <flux:switch label="Marketing emails" align="left" />        <flux:switch label="Social emails" align="left" />        <flux:switch label="Security emails" align="left" />    </div></flux:fieldset>
```

## Related components

[Field Structured form field with label](/components/field) [Checkbox Toggleable control for multiple selections](/components/checkbox)

## Reference



### [flux:switch](#fluxswitch)

| Prop | Description |
| --- | --- |
| wire:model | Binds the switch to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| label | Label text displayed above the switch. When provided, wraps the switch in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the switch. When provided alongside label, appears between the label and switch within the flux:field wrapper. See the [field component](/components/field). |
| align | Alignment of the switch relative to its label. Options: right\|start (default), left\|end. |
| disabled | Prevents user interaction with the switch. |

| Attribute | Description |
| --- | --- |
| data-flux-switch | Applied to the root element for styling and identification. |
| data-checked | Applied when the switch is in the "on" state. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0046_Table

# Table

Display structured data in a condensed, searchable format.





| Customer | Date | Status | Amount |  |
| --- | --- | --- | --- | --- |
| Gustavo Mango | Jul 31, 9:50 AM | Paid | $162.00 | View invoice          Refund          Archive |
| Desirae George | Jul 31, 12:08 PM | Paid | $32.00 | View invoice          Refund          Archive |
| Emery Madsen | Jul 31, 11:50 AM | Paid | $163.00 | View invoice          Refund          Archive |
| Kaylynn Schleifer | Jul 31, 11:15 AM | Incomplete | $29.00 | View invoice          Refund          Archive |
| Kaiya Bator | Jul 31, 11:08 AM | Failed | $72.00 | View invoice          Refund          Archive |




Showing 1 to 5 of 24 results







1   2

  3

  4

  5





Copy to clipboard

```
<flux:table :paginate="$this->orders">    <flux:table.columns>        <flux:table.column>Customer</flux:table.column>        <flux:table.column sortable :sorted="$sortBy === 'date'" :direction="$sortDirection" wire:click="sort('date')">Date</flux:table.column>        <flux:table.column sortable :sorted="$sortBy === 'status'" :direction="$sortDirection" wire:click="sort('status')">Status</flux:table.column>        <flux:table.column sortable :sorted="$sortBy === 'amount'" :direction="$sortDirection" wire:click="sort('amount')">Amount</flux:table.column>    </flux:table.columns>    <flux:table.rows>        @foreach ($this->orders as $order)            <flux:table.row :key="$order->id">                <flux:table.cell class="flex items-center gap-3">                    <flux:avatar size="xs" src="{{ $order->customer_avatar }}" />                    {{ $order->customer }}                </flux:table.cell>                <flux:table.cell class="whitespace-nowrap">{{ $order->date }}</flux:table.cell>                <flux:table.cell>                    <flux:badge size="sm" :color="$order->status_color" inset="top bottom">{{ $order->status }}</flux:badge>                </flux:table.cell>                <flux:table.cell variant="strong">{{ $order->amount }}</flux:table.cell>                <flux:table.cell>                    <flux:button variant="ghost" size="sm" icon="ellipsis-horizontal" inset="top bottom"></flux:button>                </flux:table.cell>            </flux:table.row>        @endforeach    </flux:table.rows></flux:table><!-- Livewire component example code...    use \Livewire\WithPagination;    public $sortBy = 'date';    public $sortDirection = 'desc';    public function sort($column) {        if ($this->sortBy === $column) {            $this->sortDirection = $this->sortDirection === 'asc' ? 'desc' : 'asc';        } else {            $this->sortBy = $column;            $this->sortDirection = 'asc';        }    }    #[\Livewire\Attributes\Computed]    public function orders()    {        return \App\Models\Order::query()            ->tap(fn ($query) => $this->sortBy ? $query->orderBy($this->sortBy, $this->sortDirection) : $query)            ->paginate(5);    }-->
```



## [Simple](#simple)

The primary table example above is a full-featured table with sorting, pagination, etc. Here's a clean example of a simple data table that you can use as a simpler starting point.





| Customer | Date | Status | Amount |
| --- | --- | --- | --- |
| Lindsey Aminoff | Jul 29, 10:45 AM | Paid | $49.00 |
| Hanna Lubin | Jul 28, 2:15 PM | Paid | $312.00 |
| Kianna Bushevi | Jul 30, 4:05 PM | Refunded | $132.00 |
| Gustavo Geidt | Jul 27, 9:30 AM | Paid | $31.00 |





Copy to clipboard

```
<flux:table>    <flux:table.columns>        <flux:table.column>Customer</flux:table.column>        <flux:table.column>Date</flux:table.column>        <flux:table.column>Status</flux:table.column>        <flux:table.column>Amount</flux:table.column>    </flux:table.columns>    <flux:table.rows>        <flux:table.row>            <flux:table.cell>Lindsey Aminoff</flux:table.cell>            <flux:table.cell>Jul 29, 10:45 AM</flux:table.cell>            <flux:table.cell><flux:badge color="green" size="sm" inset="top bottom">Paid</flux:badge></flux:table.cell>            <flux:table.cell variant="strong">$49.00</flux:table.cell>        </flux:table.row>        <flux:table.row>            <flux:table.cell>Hanna Lubin</flux:table.cell>            <flux:table.cell>Jul 28, 2:15 PM</flux:table.cell>            <flux:table.cell><flux:badge color="green" size="sm" inset="top bottom">Paid</flux:badge></flux:table.cell>            <flux:table.cell variant="strong">$312.00</flux:table.cell>        </flux:table.row>        <flux:table.row>            <flux:table.cell>Kianna Bushevi</flux:table.cell>            <flux:table.cell>Jul 30, 4:05 PM</flux:table.cell>            <flux:table.cell><flux:badge color="zinc" size="sm" inset="top bottom">Refunded</flux:badge></flux:table.cell>            <flux:table.cell variant="strong">$132.00</flux:table.cell>        </flux:table.row>        <flux:table.row>            <flux:table.cell>Gustavo Geidt</flux:table.cell>            <flux:table.cell>Jul 27, 9:30 AM</flux:table.cell>            <flux:table.cell><flux:badge color="green" size="sm" inset="top bottom">Paid</flux:badge></flux:table.cell>            <flux:table.cell variant="strong">$31.00</flux:table.cell>        </flux:table.row>    </flux:table.rows></flux:table>
```



## [Pagination](#pagination)

Allow users to navigate through different pages of data by passing in any model paginator to the paginate prop.









Showing 1 to 5 of 24 results







1   2

  3

  4

  5





Copy to clipboard

```
<!-- $orders = \App\Models\Order::paginate(5) --><flux:table :paginate="$orders">    <!-- ... --></flux:table>
```



## [Sortable](#sortable)

Allow users to sort rows by specific columns using a combination of the sortable, sorted, and direction props.





| Customer | Date | Amount |
| --- | --- | --- |
| Gustavo Mango | Jul 31, 9:50 AM | $162.00 |
| Desirae George | Jul 31, 12:08 PM | $32.00 |
| Emery Madsen | Jul 31, 11:50 AM | $163.00 |
| Kaylynn Schleifer | Jul 31, 11:15 AM | $29.00 |





Copy to clipboard

```
<flux:table>    <flux:table.columns>        <flux:table.column>Customer</flux:table.column>        <flux:table.column sortable sorted direction="desc">Date</flux:table.column>        <flux:table.column sortable>Amount</flux:table.column>    </flux:table.columns>    <!-- ... --></flux:table>
```



## [Sticky header](#sticky-header)

Keep the header visible during vertical scrolling by adding the sticky prop to the table.columns component.



Make sure to set a background color on the header row to prevent content overlap.





| Customer | Date | Status | Amount |  |
| --- | --- | --- | --- | --- |
| Lindsey Aminoff | Jul 29, 10:45 AM | Paid | $49.00 | View invoice          Refund          Archive |
| Hanna Lubin | Jul 28, 2:15 PM | Paid | $312.00 | View invoice          Refund          Archive |
| Kianna Bushevi | Jul 30, 4:05 PM | Paid | $132.00 | View invoice          Refund          Archive |
| Gustavo Geidt | Jul 27, 9:30 AM | Paid | $31.00 | View invoice          Refund          Archive |
| Nolan George | Jul 26, 7:55 PM | Paid | $313.00 | View invoice          Refund          Archive |
| Desirae George | Jul 31, 12:08 PM | Paid | $32.00 | View invoice          Refund          Archive |
| Jackson Bothman | Jul 30, 3:45 PM | Refunded | $94.00 | View invoice          Refund          Archive |
| Hanna Lipshutz | Jul 29, 11:30 AM | Paid | $22.00 | View invoice          Refund          Archive |
| Alfredo Levin | Jul 25, 10:10 AM | Paid | $12.00 | View invoice          Refund          Archive |
| Zain Lubin | Jul 28, 9:20 AM | Paid | $91.00 | View invoice          Refund          Archive |





Copy to clipboard

```
<!-- Set the height of the table container... --><flux:table container:class="max-h-80">    <flux:table.columns sticky class="bg-white dark:bg-zinc-900">         <!-- ... -->    </flux:table.columns>    <!-- ... --></flux:table>
```



## [Sticky columns](#sticky-columns)

Keep important info visible during horizontal scrolling by adding the sticky prop to table.column and table.cell components.



Make sure to set a background color on columns and cells to prevent content overlap.





| ID | Customer | Email | Date | Status | Amount |  |
| --- | --- | --- | --- | --- | --- | --- |
| #428 | Lindsey Aminoff | [[email protected]](/cdn-cgi/l/email-protection) | Jul 29, 10:45 AM | Paid | $49.00 | View invoice          Refund          Archive |
| #427 | Hanna Lubin | [[email protected]](/cdn-cgi/l/email-protection) | Jul 28, 2:15 PM | Paid | $312.00 | View invoice          Refund          Archive |
| #426 | Kianna Bushevi | [[email protected]](/cdn-cgi/l/email-protection) | Jul 30, 4:05 PM | Paid | $132.00 | View invoice          Refund          Archive |
| #424 | Gustavo Geidt | [[email protected]](/cdn-cgi/l/email-protection) | Jul 27, 9:30 AM | Paid | $31.00 | View invoice          Refund          Archive |
| #423 | Nolan George | [[email protected]](/cdn-cgi/l/email-protection) | Jul 26, 7:55 PM | Paid | $313.00 | View invoice          Refund          Archive |
| #421 | Desirae George | [[email protected]](/cdn-cgi/l/email-protection) | Jul 31, 12:08 PM | Paid | $32.00 | View invoice          Refund          Archive |
| #420 | Jackson Bothman | [[email protected]](/cdn-cgi/l/email-protection) | Jul 30, 3:45 PM | Refunded | $94.00 | View invoice          Refund          Archive |
| #419 | Hanna Lipshutz | [[email protected]](/cdn-cgi/l/email-protection) | Jul 29, 11:30 AM | Paid | $22.00 | View invoice          Refund          Archive |
| #418 | Alfredo Levin | [[email protected]](/cdn-cgi/l/email-protection) | Jul 25, 10:10 AM | Paid | $12.00 | View invoice          Refund          Archive |
| #417 | Zain Lubin | [[email protected]](/cdn-cgi/l/email-protection) | Jul 28, 9:20 AM | Paid | $91.00 | View invoice          Refund          Archive |





Copy to clipboard

```
<flux:table container:class="max-h-80">    <flux:table.columns sticky class="bg-white dark:bg-zinc-900">        <flux:table.column sticky class="bg-white dark:bg-zinc-900">ID</flux:table.column>        <!-- ... -->    </flux:table.columns>    <flux:table.rows>        @foreach ($this->orders as $order)            <flux:table.row :key="$order->id">                <flux:table.cell sticky class="bg-white dark:bg-zinc-900">{{ $order->id }}</flux:table.cell>                <!-- ... -->            </flux:table.row>        @endforeach    </flux:table.rows></flux:table>
```

## Related components

[Avatar Display user profile images or fallback initials](/components/avatar) [Badge Display small counts, status indicators, or labels](/components/badge) [Dropdown Display expandable menus for row actions](/components/dropdown)

## Reference



### [flux:table](#fluxtable)

| Prop | Description |
| --- | --- |
| paginate | A Laravel paginator instance to enable pagination. |
| container:class | Additional CSS classes applied to the container. Useful for setting height constraints like max-h-80. |

| Attribute | Description |
| --- | --- |
| data-flux-table | Applied to the root element for styling and identification. |



### [flux:table.columns](#fluxtablecolumns)

| Prop | Description |
| --- | --- |
| sticky | When present, makes the header row sticky when scrolling. |

| Slot | Description |
| --- | --- |
| default | The table columns. |



### [flux:table.column](#fluxtablecolumn)

| Prop | Description |
| --- | --- |
| align | Alignment of the column content. Options: start, center, end. |
| sortable | Enables sorting functionality for the column. |
| sorted | Indicates this column is currently being sorted. |
| direction | Sort direction when column is sorted. Options: asc, desc. |
| sticky | When present, makes the column sticky when scrolling. |



### [flux:table.rows](#fluxtablerows)

| Slot | Description |
| --- | --- |
| default | The table rows. |



### [flux:table.row](#fluxtablerow)

| Slot | Description |
| --- | --- |
| default | The table cells for this row. |

| Prop | Description |
| --- | --- |
| key | An alias for wire:key: the unique identifier for the row. |
| sticky | When present, makes the row sticky when scrolling. |



### [flux:table.cell](#fluxtablecell)

| Prop | Description |
| --- | --- |
| align | Alignment of the cell content. Options: start, center, end. |
| variant | Visual style of the cell. Options: default, strong. |
| sticky | When present, makes the cell sticky when scrolling. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0047_Tabs



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Tabs

Organize content into separate panels within a single container. Easily switch between sections without leaving the page.

For full-page navigation, use the [navbar component ->](/components/navbar)





Profile

Account

Billing





Copy to clipboard

```
<flux:tab.group>    <flux:tabs wire:model="tab">        <flux:tab name="profile">Profile</flux:tab>        <flux:tab name="account">Account</flux:tab>        <flux:tab name="billing">Billing</flux:tab>    </flux:tabs>    <flux:tab.panel name="profile">...</flux:tab.panel>    <flux:tab.panel name="account">...</flux:tab.panel>    <flux:tab.panel name="billing">...</flux:tab.panel></flux:tab.group>
```



## [With icons](#with-icons)

Associate tab labels with icons to visually distinguish different sections.





Profile

Account

Billing





Copy to clipboard

```
<flux:tab.group>    <flux:tabs>        <flux:tab name="profile" icon="user">Profile</flux:tab>        <flux:tab name="account" icon="cog-6-tooth">Account</flux:tab>        <flux:tab name="billing" icon="banknotes">Billing</flux:tab>    </flux:tabs>    <flux:tab.panel name="profile">...</flux:tab.panel>    <flux:tab.panel name="account">...</flux:tab.panel>    <flux:tab.panel name="billing">...</flux:tab.panel></flux:tab.group>
```



## [Padded edges](#padded-edges)

By default, the tabs will have no horizontal padding around the edges. If you want to add padding you can do by adding Tailwind utilities to the tabs and/or tab.panel components.





Profile

Account

Billing





Copy to clipboard

```
<flux:tabs class="px-4">    <flux:tab name="profile">Profile</flux:tab>    <flux:tab name="account">Account</flux:tab>    <flux:tab name="billing">Billing</flux:tab></flux:tabs>
```



## [Scrollable tabs](#scrollable-tabs)

If your tabs extend beyond the viewport, especially on mobile devices, you should make them scrollable to prevent horizontal overflow.





Profile

Account

Billing

Security

Notifications

Integrations

API





Copy to clipboard

```
<flux:tab.group>    <flux:tabs scrollable>        <flux:tab name="profile">Profile</flux:tab>        <flux:tab name="account">Account</flux:tab>        <flux:tab name="billing">Billing</flux:tab>        <flux:tab name="security">Security</flux:tab>        <flux:tab name="notifications">Notifications</flux:tab>        <flux:tab name="integrations">Integrations</flux:tab>        <flux:tab name="api">API</flux:tab>    </flux:tabs>    <flux:tab.panel name="profile">...</flux:tab.panel>    <flux:tab.panel name="account">...</flux:tab.panel>    <flux:tab.panel name="billing">...</flux:tab.panel>    <flux:tab.panel name="security">...</flux:tab.panel>    <flux:tab.panel name="notifications">...</flux:tab.panel>    <flux:tab.panel name="integrations">...</flux:tab.panel>    <flux:tab.panel name="api">...</flux:tab.panel></flux:tab.group>
```

You can hide the scrollbar by addding scrollable:scrollbar="hide". Note that this will also hide it on desktop, where users may rely on it for horizontal scrolling.



### [Faded edge](#faded-edge)

Use scrollable:fade to add a fade effect to the trailing edge. This visual cue indicates that additional tabs are available beyond the visible area.





Profile

Account

Billing

Security

Notifications

Integrations

API





Copy to clipboard

```
<flux:tab.group>    <flux:tabs scrollable scrollable:fade>        <flux:tab name="profile">Profile</flux:tab>        <flux:tab name="account">Account</flux:tab>        <flux:tab name="billing">Billing</flux:tab>        <flux:tab name="security">Security</flux:tab>        <flux:tab name="notifications">Notifications</flux:tab>        <flux:tab name="integrations">Integrations</flux:tab>        <flux:tab name="api">API</flux:tab>    </flux:tabs>    <flux:tab.panel name="profile">...</flux:tab.panel>    <flux:tab.panel name="account">...</flux:tab.panel>    <flux:tab.panel name="billing">...</flux:tab.panel>    <flux:tab.panel name="security">...</flux:tab.panel>    <flux:tab.panel name="notifications">...</flux:tab.panel>    <flux:tab.panel name="integrations">...</flux:tab.panel>    <flux:tab.panel name="api">...</flux:tab.panel></flux:tab.group>
```



## [Segmented tabs](#segmented-tabs)

Tab through content with visually separated, button-like tabs. Ideal for toggling between views inside a container with a constrained width.





List

Board

Timeline





Copy to clipboard

```
<flux:tabs variant="segmented">    <flux:tab>List</flux:tab>    <flux:tab>Board</flux:tab>    <flux:tab>Timeline</flux:tab></flux:tabs>
```



## [Segmented with icons](#segmented-with-icons)

Combine segmented tabs with icon prefixes.





List

Board

Timeline





Copy to clipboard

```
<flux:tabs variant="segmented">    <flux:tab icon="list-bullet">List</flux:tab>    <flux:tab icon="squares-2x2">Board</flux:tab>    <flux:tab icon="calendar-days">Timeline</flux:tab></flux:tabs>
```



## [Small segmented tabs](#small-segmented-tabs)

For more compact layouts, you can use the size="sm" prop to make the tabs smaller.





Demo

Code





Copy to clipboard

```
<flux:tabs variant="segmented" size="sm">    <flux:tab>Demo</flux:tab>    <flux:tab>Code</flux:tab></flux:tabs>
```



## [Pill tabs](#pill-tabs)

Tab through content with visually separated, pill-like tabs.





List

Board

Timeline





Copy to clipboard

```
<flux:tabs variant="pills">    <flux:tab>List</flux:tab>    <flux:tab>Board</flux:tab>    <flux:tab>Timeline</flux:tab></flux:tabs>
```



## [Dynamic tabs](#dynamic-tabs)

If you need, you can dynamically generate additional tabs and panels in your Livewire component. Just make sure you use matching names for the new tabs and panels.





 Tab #1

Tab #2

Add tab







Copy to clipboard

```
<flux:tab.group>    <flux:tabs>        @foreach($tabs as $id => $tab)            <flux:tab :name="$id">{{ $tab }}</flux:tab>        @endforeach        <flux:tab icon="plus" wire:click="addTab" action>Add tab</flux:tab>    </flux:tabs>    @foreach($tabs as $id => $tab)        <flux:tab.panel :name="$id">            <!-- ... -->        </flux:tab.panel>    @endforeach</flux:tab.group><!-- Livewire component example code...    public array $tabs = [        'tab-1' => 'Tab #1',        'tab-2' => 'Tab #2',    ];    public function addTab(): void    {        $id = 'tab-' . str()->random();        $this->tabs[$id] = 'Tab #' . count($this->tabs) + 1;    }-->
```

## Related components

[Navbar Build responsive navigation bars](/components/navbar) [Radio Allow users to select a single option from a list](/components/radio)

## Reference



### [flux:tab.group](#fluxtabgroup)

Container for tabs and their associated panels.

| Slot | Description |
| --- | --- |
| default | The tabs and panels components. |



### [flux:tabs](#fluxtabs)

| Prop | Description |
| --- | --- |
| wire:model | Binds the active tab to a Livewire property. See [wire:model documentation](https://livewire.laravel.com/docs/wire-model) |
| variant | Visual style of the tabs. Options: default, segmented, pills. |
| size | Size of the tabs. Options: base (default), sm. |
| scrollable | Enables horizontal scrolling. |
| scrollable:scrollbar | Controls scrollbar visibility when tabs are scrollable. Options: hide. |
| scrollable:fade | Adds a fade effect to the trailing edge when tabs are scrollable. |

| Slot | Description |
| --- | --- |
| default | The individual tab components. |

| Attribute | Description |
| --- | --- |
| data-flux-tabs | Applied to the root element for styling and identification. |



### [flux:tab](#fluxtab)

| Prop | Description |
| --- | --- |
| name | Unique identifier for the tab, used to match with its panel. |
| icon | Name of the icon to display at the start of the tab. |
| icon:trailing | Name of the icon to display at the end of the tab. |
| icon:variant | Variant of the icon. Options: outline, solid, mini, micro. |
| selected | If true, the tab is selected by default. |
| action | Converts the tab to an action button (used for "Add tab" functionality). |
| accent | If true, applies accent color styling to the tab. |
| size | Size of the tab (only applies when variant="segmented"). Options: base (default), sm. |
| disabled | Disables the tab. |

| Slot | Description |
| --- | --- |
| default | The tab label content. |

| Attribute | Description |
| --- | --- |
| data-flux-tab | Applied to the tab element for styling and identification. |
| data-selected | Applied when the tab is selected/active. |



### [flux:tab.panel](#fluxtabpanel)

| Prop | Description |
| --- | --- |
| name | Unique identifier matching the associated tab. |
| selected | If true, the panel is selected by default. |

| Slot | Description |
| --- | --- |
| default | The panel content displayed when the associated tab is selected. |

| Attribute | Description |
| --- | --- |
| data-flux-tab-panel | Applied to the panel element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0048_Text

# Text

Consistent typographical components like text and link.





Text component

This is the standard text component for body copy and general content throughout your application.





Copy to clipboard

```
<flux:heading>Text component</flux:heading><flux:text class="mt-2">This is the standard text component for body copy and general content throughout your application.</flux:text>
```



## [Size](#size)

Use standard Tailwind to control the size of the text so that you can more easily adapt to different screen sizes.





Larger text size

Default text size

Smaller text





Copy to clipboard

```
<flux:text class="text-base">Base text size</flux:text><flux:text>Default text size</flux:text><flux:text class="text-xs">Smaller text</flux:text>
```



## [Color](#color)

Use the variant and color props to adjust the text color based on its importance and context.





Strong text color

Default text color

Subtle text color

Colored text





Copy to clipboard

```
<flux:text variant="strong">Strong text color</flux:text><flux:text>Default text color</flux:text><flux:text variant="subtle">Subtle text color</flux:text><flux:text color="blue">Colored text</flux:text>
```



## [Link](#link)

Use the link component to create clickable text that navigates to other pages or resources.





Visit our [documentation](#) for more information.





Copy to clipboard

```
<flux:text>Visit our <flux:link href="#">documentation</flux:link> for more information.</flux:text>
```



## [Link variants](#link-variants)

Links can be styled differently based on their context and importance.





[Default link](#)



[Ghost link](#)



[Subtle link](#)





Copy to clipboard

```
<flux:link href="#">Default link</flux:link><flux:link href="#" variant="ghost">Ghost link</flux:link><flux:link href="#" variant="subtle">Subtle link</flux:link>
```



## [Link as button](#link-as-button)

Use the as="button" prop to render the link as a button.





Create new account →





Copy to clipboard

```
<flux:link as="button" wire:click="...">Create new account →</flux:link>
```

## Related components

[Heading Create hierarchical section headings](/components/heading) [Card Containers for content with consistent styling](/components/card)

## Reference



### [flux:text](#fluxtext)

| Prop | Description |
| --- | --- |
| size | Size of the text. Options: sm, default, lg, xl. Default: default. |
| variant | Text variant. Options: strong, subtle. Default: default. |
| color | Color of the text. Options: default, red, orange, yellow, lime, green, emerald, teal, cyan, sky, blue, indigo, violet, purple, fuchsia, pink, rose. Default: default. |
| inline | If true, the text element will be a span instead of a p. |



### [flux:link](#fluxlink)

| Prop | Description |
| --- | --- |
| href | The URL that the link points to. Required. |
| variant | Link style variant. Options: default, ghost, subtle. Default: default. |
| external | If true, the link will open in a new tab. |
| as | The HTML tag to render the link as. Options: a (default), button. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0049_Textarea

# Textarea

Capture multi-line text input from users. Ideal for comments, descriptions, and feedback.





Description





Copy to clipboard

```
<flux:textarea />
```



## [With placeholder](#with-placeholder)

Display a hint inside the textarea to guide users on what to enter.





Order notes





Copy to clipboard

```
<flux:textarea    label="Order notes"    placeholder="No lettuce, tomato, or onion..."/>
```



## [Fixed row height](#fixed-row-height)

Customize the height of the textarea by passing a rows prop.





Note





Copy to clipboard

```
<flux:textarea rows="2" label="Note" />
```



## [Auto-sizing textarea](#auto-sizing-textarea)

Using CSS's new field-sizing property, the textarea will automatically adjust its height to fit the content by passing in the rows="auto" prop.

This feature is not available in all web browsers. Visit [caniuse.com](https://caniuse.com/?search=field-sizing) to see which browsers support this feature.









Copy to clipboard

```
<flux:textarea rows="auto" />
```



## [Configure resize](#configure-resize)

If you want to restrict the user from resizing the textarea, you can use the resize="none" prop.









Copy to clipboard

```
<flux:textarea resize="vertical" /><flux:textarea resize="none" /><flux:textarea resize="horizontal" /><flux:textarea resize="both" />
```

## Related components

[Field Structured form field with label](/components/field) [Input Text fields for collecting user input](/components/input)

## Reference



### [flux:textarea](#fluxtextarea)

| Prop | Description |
| --- | --- |
| wire:model | Binds the textarea to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| placeholder | Placeholder text displayed when the textarea is empty. |
| label | Label text displayed above the textarea. When provided, wraps the textarea in a flux:field component with an adjacent flux:label component. See the [field component](/components/field). |
| description | Help text displayed below the textarea. When provided alongside label, appears between the label and textarea within the flux:field wrapper. See the [field component](/components/field). |
| description:trailing | The description provided will be displayed below the textarea instead of above it. |
| badge | Badge text displayed at the end of the flux:label component when the label prop is provided. |
| rows | Number of visible text lines. Use "auto" for automatic height adjustment. Default: 4. |
| resize | Control how the textarea can be resized. Options: vertical (default), horizontal, both, none. |
| invalid | If true, applies error styling to the textarea. |

| Attribute | Description |
| --- | --- |
| data-flux-textarea | Applied to the textarea element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0050_Time picker



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Time picker

Allow users to select specific times for scheduling events or setting appointments. Perfect for time-based filtering and precise scheduling.









Copy to clipboard

```
<flux:time-picker />
```



## Basic usage

Set the initial selected time using the value prop with a H:i formatted time string:

Copy to clipboard

```
<flux:time-picker value="11:30" />
```

You can also bind the selection to a Livewire property using wire:model:

Copy to clipboard

```
<flux:time-picker wire:model="time" />
```



## [Input trigger](#input-trigger)

Attach the time picker to a time input for more precise time selection control.





:





Copy to clipboard

```
<flux:time-picker type="input" />
```



## Without dropdown

Remove the dropdown from the input trigger.





:





Copy to clipboard

```
<flux:time-picker type="input" :dropdown="false" />
```



## [Multiple times](#multiple-times)

Allow users to select multiple times.









Copy to clipboard

```
<flux:time-picker multiple />
```



## [Time format](#time-format)

By default, the time picker will use the browser's locale to determine the time format.

You can override this by setting the time-format attribute to 12-hour or 24-hour.





12-hour

24-hour





Copy to clipboard

```
<flux:time-picker time-format="12-hour" /><flux:time-picker time-format="24-hour" />
```



## [Interval](#interval)

You can set the interval between the displayed time options by setting the interval attribute to a number of minutes. The default is 30 minutes.









Copy to clipboard

```
<flux:time-picker interval="60" />
```



## [Min/max times](#minmax-times)

Restrict the selectable times by setting minimum and maximum boundaries.









Copy to clipboard

```
<flux:time-picker min="09:00" max="17:00" />
```

You can also use the convenient "now" shorthand:

Copy to clipboard

```
<!-- Prevent selection before now... --><flux:time-picker min="now" /><!-- Prevent selection after now... --><flux:time-picker max="now" />
```



## [Unavailable times](#unavailable-times)

Disable specific times from being selected. Useful for blocking out appointments, showing booked times, or indicating unavailable time slots.









Copy to clipboard

```
<flux:time-picker unavailable="03:00,04:00,05:30-07:29" />
```



## [Open to](#open-to)

Set the time that the time picker will open to. Otherwise, the time picker defaults to the selected time, or the current time.









Copy to clipboard

```
<flux:time-picker open-to="10:00" />
```



## [Localization](#localization)

By default, the time picker will use the browser's locale (e.g. navigator.language).

You can override this behavior by setting the locale attribute to any valid locale string (e.g. fr for French, en-US for English, etc.):









Copy to clipboard

```
<flux:time-picker locale="ja-JP" />
```

## Related components

[Date picker Displays a date picker interface for selecting dates](/components/date-picker) [Calendar Displays a calendar interface for selecting dates](/components/calendar) [Input Text fields for collecting user input](/components/input)

## Reference



### [flux:time-picker](#fluxtime-picker)

| Prop | Description |
| --- | --- |
| wire:model | Binds the time picker to a Livewire property. See the [wire:model documentation](https://livewire.laravel.com/docs/wire-model) for more information. |
| value | Selected time(s). Format depends on mode: single time (H:i) or multiple times (H:i,H:i). |
| type | Type of time picker. Options: input, button. Default: button. |
| multiple | Allow users to select multiple times. Default: false. |
| time-format | Time format. Options: auto (default), 12-hour, 24-hour. |
| interval | Interval in minutes between the displayed time options. Default: 30. |
| min | Earliest selectable time. Can be a time string or "now". |
| max | Latest selectable time. Can be a time string or "now". |
| unavailable | Unavailable times. Can be a time string or a comma-separated list of time strings. |
| open-to | Time to open the time picker to. Default: selected time, or now. |
| label | Label text displayed above the time picker. When provided, wraps the component in a flux:field with an adjacent flux:label. |
| description | Help text displayed above the time picker. When provided alongside label, appears between the label and time picker within the flux:field wrapper. |
| description:trailing | The description provided will be displayed below the time picker instead of above it. |
| badge | Badge text displayed at the end of the flux:label component when the label prop is provided. |
| placeholder | Placeholder text displayed when no time is selected. |
| size | Size of the time picker. Options: sm, xs. |
| clearable | Displays a clear button when a time is selected. |
| disabled | Prevents user interaction with the time picker. |
| invalid | Applies error styling to the time picker. |
| locale | Set the locale for the time picker. Examples: fr, en-US, ja-JP. |

| Attribute | Description |
| --- | --- |
| data-flux-time-picker | Applied to the root element for styling and identification. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0051_Toast



Flux Pro component

This component is only available in the Pro version of Flux.



[Upgrade to Pro ->](/pricing) [Upgrade to Pro ->](/pricing)

# Toast

A message that provides feedback to users about an action or event, often temporary and dismissible.

To use the Toast component from Livewire, you must include it somewhere on the page; often in your layout file:



Copy to clipboard

```
<body>    <!-- ... -->    <flux:toast /></body>
```

If you are using wire:navigate to navigate between pages, you may want to persist the toast component so that toast messages don't suddenly disappear when navigating away from the page.



Copy to clipboard

```
<body>    <!-- ... -->    @persist('toast')        <flux:toast />    @endpersist</body>
```

Once the toast component is present on the page, you can use the Flux::toast() method to trigger a toast message from your Livewire components:





Save changes





Copy to clipboard

```
<?phpnamespace App\Livewire;use Livewire\Component;use Flux\Flux;class EditPost extends Component{    public function save()    {        // ...        Flux::toast('Your changes have been saved.');    }}
```

You can also trigger a toast from Alpine directly using Flux's magic methods:



Copy to clipboard

```
<button x-on:click="$flux.toast('Your changes have been saved.')">    Save changes</button>
```

Or you can use the window.Flux global object to trigger a toast from any JavaScript in your application:



Copy to clipboard

Both $flux and window.Flux support the following method parameter signatures:



Copy to clipboard

```
Flux.toast('Your changes have been saved.')// Or...Flux.toast({    heading: 'Changes saved',    text: 'Your changes have been saved.',    variant: 'success',})
```



## [With heading](#with-heading)

Use a heading to provide additional context for the toast.





Save changes





Copy to clipboard

```
Flux::toast(    heading: 'Changes saved.',    text: 'You can always update this in your settings.',);
```



## [Variants](#variants)

Use the variant prop to change the visual style of the toast.





Success

Warning

Danger





Copy to clipboard

```
Flux::toast(variant: 'success', ...);Flux::toast(variant: 'warning', ...);Flux::toast(variant: 'danger', ...);
```



## [Positioning](#positioning)

By default, the toast will appear in the bottom right corner of the page. You can customize this position using the position prop.





Save changes





Copy to clipboard

```
<flux:toast position="top end" /><!-- Customize top padding for things like navbars... --><flux:toast position="top end" class="pt-24" />
```



## [Duration](#duration)

By default, the toast will automatically dismiss after 5 seconds. You can customize this duration by passing a number of milliseconds to the duration prop.





Save changes





Copy to clipboard

```
// 1 second...Flux::toast(duration: 1000, ...);
```



## [Permanent](#permanent)

Use a value of 0 as the duration prop to make the toast stay open indefinitely.





Save changes





Copy to clipboard

```
// Show indefinitely...Flux::toast(duration: 0, ...);
```



## [Stack](#stack)

To show a stack of toasts, you can wrap the flux:toast component in a flux:toast.group component. By default, toasts in a stack overlap and expand on hover to show each toast vertically.





Save changes





Copy to clipboard

```
<flux:toast.group>    <flux:toast /></flux:toast.group>
```

Use the expanded prop to always show the toast stack in an expanded state, making all toasts visible at once.



Copy to clipboard

```
<flux:toast.group expanded>    <flux:toast /></flux:toast.group>
```

The group component also accepts the position prop to control where the toast stack appears on the screen.



Copy to clipboard

```
<flux:toast.group position="top end">    <flux:toast /></flux:toast.group>
```

## Related components

[Callout A flexible content container for alerts, messages, and notifications](/components/callout) [Modal Display temporary content in a modal dialog](/components/modal)

## Reference



### [flux:toast](#fluxtoast)

| Prop | Description |
| --- | --- |
| position | Position of the toast on the screen. Options: bottom end (default), bottom center, bottom start, top end, top center, top start. |



### [flux:toast.group](#fluxtoastgroup)

| Prop | Description |
| --- | --- |
| position | Position of the toast group on the screen. Options: bottom end (default), bottom center, bottom start, top end, top center, top start. |
| expanded | If true, always shows the toast stack in an expanded state, making all toasts visible at once. Default: false. |



### [Flux::toast()](#fluxtoast)

The PHP method used to trigger toasts from Livewire components.

| Parameter | Description |
| --- | --- |
| heading | Optional heading text for the toast. |
| text | Main content text of the toast. |
| variant | Visual style. Options: success, warning, danger. |
| duration | Duration in milliseconds. Use 0 for permanent toasts. Default: 5000. |



### [$flux.toast()](#fluxtoast)

The Alpine.js magic method used to trigger toasts from Alpine components. It can be used in two ways:

```
// Simple usage with just a message...$flux.toast('Your changes have been saved')// Advanced usage with full configuration...$flux.toast({    heading: 'Success!',    text: 'Your changes have been saved',    variant: 'success',    duration: 3000})
```

| Parameter | Description |
| --- | --- |
| message | A string containing the toast message. When using this simple form, the message becomes the toast's text content. |
| options | Alternatively, an object containing: - heading: Optional title text - text: Main message text - variant: Visual style (success, warning, danger) - duration: Display time in milliseconds |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)




# 0052_Tooltip

# Tooltip

Provide additional information when users hover over or focus on an element.

Because tooltips rely on hover states, touch devices like mobile phones often don't show them. Therefore, it is recommended that you convey essential information via the UI rather than relying on a tooltip for mobile users.





Settings





Copy to clipboard

```
<flux:tooltip content="Settings">    <flux:button icon="cog-6-tooth" icon:variant="outline" /></flux:tooltip>
```

As a shorthand, you can pass a tooltip prop into a button component directly.



Copy to clipboard

```
<flux:button tooltip="Settings" ... />
```



## [Info tooltip](#info-tooltip)

In cases where a tooltip's content is essential, you should make it toggleable. This way, users on touch devices will be able to trigger it on click/press rather than hover.





Tax identification number

For US businesses, enter your 9-digit Employer Identification Number (EIN) without hyphens.

For European companies, enter your VAT number including the country prefix (e.g., DE123456789).





Copy to clipboard

```
<flux:heading class="flex items-center gap-2">    Tax identification number    <flux:tooltip toggleable>        <flux:button icon="information-circle" size="sm" variant="ghost" />        <flux:tooltip.content class="max-w-[20rem] space-y-2">            <p>For US businesses, enter your 9-digit Employer Identification Number (EIN) without hyphens.</p>            <p>For European companies, enter your VAT number including the country prefix (e.g., DE123456789).</p>        </flux:tooltip.content>    </flux:tooltip></flux:heading>
```



## [Position](#position)

Position tooltips around the element for optimal visibility. Choose from top, right, bottom, or left.





Settings

Settings

Settings

Settings





Copy to clipboard

```
<flux:tooltip content="Settings" position="top">    <flux:button icon="cog-6-tooth" icon:variant="outline" /></flux:tooltip><flux:tooltip content="Settings" position="right">    <flux:button icon="cog-6-tooth" icon:variant="outline" /></flux:tooltip><flux:tooltip content="Settings" position="bottom">    <flux:button icon="cog-6-tooth" icon:variant="outline" /></flux:tooltip><flux:tooltip content="Settings" position="left">    <flux:button icon="cog-6-tooth" icon:variant="outline" /></flux:tooltip>
```



## [Disabled buttons](#disabled-buttons)

By default, tooltips on disabled buttons won't be triggered because pointer events are disabled as well. However, as a workaround, you can target a wrapping element instead of the button directly.





Merge pull request

Cannot merge until reviewed by a team member





Copy to clipboard

```
<flux:tooltip content="Cannot merge until reviewed by a team member">    <div>        <flux:button disabled icon="arrow-turn-down-right">Merge pull request</flux:button>    </div></flux:tooltip>
```

## Related components

[Button Interactive elements for user actions](/components/button) [Icon Visual symbols and metaphors for UI elements](/components/icon)

## Reference



### [flux:tooltip](#fluxtooltip)

| Prop | Description |
| --- | --- |
| content | Text content to display in the tooltip. Alternative to using the flux:tooltip.content component. |
| position | Position of the tooltip relative to the trigger element. Options: top (default), right, bottom, left. |
| align | Alignment of the tooltip. Options: center (default), start, end. |
| disabled | Prevents user interaction with the tooltip. |
| gap | Spacing between the trigger element and the tooltip. Default: 5px. |
| offset | Offset of the tooltip from the trigger element. Default: 0px. |
| toggleable | Makes the tooltip clickable instead of hover-only. Useful for touch devices. |
| interactive | Uses the proper ARIA attributes (aria-expanded and aria-controls) to signal that the tooltip has interactive content. |
| kbd | Keyboard shortcut hint displayed at the end of the tooltip. |

| Attribute | Description |
| --- | --- |
| data-flux-tooltip | Applied to the root element for styling and identification. |



### [flux:tooltip.content](#fluxtooltipcontent)

| Prop | Description |
| --- | --- |
| kbd | Keyboard shortcut hint displayed at the end of the tooltip content. |

Copyright © 2026 Wireable LLC ·[Terms of Service](/terms)

Built with

 by  
 [Caleb Porzio](https://x.com/calebporzio) and [Hugo Sainte-Marie](https://x.com/hugosaintemarie)
