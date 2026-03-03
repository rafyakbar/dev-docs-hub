## [​](#introduction)Introduction

Clusters are a hierarchical structure in panels that allow you to group [resources](../resources) and [custom pages](./custom-pages) together. They are useful for organizing your panel into logical sections, and can help reduce the size of your panel’s sidebar. When using a cluster, a few things happen:

- A new navigation item is added to the navigation, which is a link to the first resource or page in the cluster.
- The individual navigation items for the resources or pages are no longer visible in the main navigation.
- A new sub-navigation UI is added to each resource or page in the cluster, which contains the navigation items for the resources or pages in the cluster.
- Resources and pages in the cluster get a new URL, prefixed with the name of the cluster. If you are generating URLs to [resources](../resources#generating-urls-to-resource-pages) and [pages](./custom-pages#generating-urls-to-pages) correctly, then this change should be handled for you automatically.
- The cluster’s name is in the breadcrumbs of all resources and pages in the cluster. When clicking it, you are taken to the first resource or page in the cluster.


## [​](#creating-a-cluster)Creating a cluster

Before creating your first cluster, you must tell the panel where cluster classes should be located. Alongside methods like `discoverResources()` and `discoverPages()` in the [configuration](../panel-configuration), you can use `discoverClusters()`:

Copy

```
public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->discoverResources(in: app_path('Filament/Resources'), for: 'App\\Filament\\Resources')
        ->discoverPages(in: app_path('Filament/Pages'), for: 'App\\Filament\\Pages')
        ->discoverClusters(in: app_path('Filament/Clusters'), for: 'App\\Filament\\Clusters');
}

```

Now, you can create a cluster with the `php artisan make:filament-cluster` command:

Copy

```
php artisan make:filament-cluster Settings

```

This will create a new cluster class in the `app/Filament/Clusters` directory:

Copy

```
<?php

namespace App\Filament\Clusters\Settings;

use BackedEnum;
use Filament\Clusters\Cluster;
use Filament\Support\Icons\Heroicon;

class SettingsCluster extends Cluster
{
    protected static string | BackedEnum | null $navigationIcon = Heroicon::OutlinedSquares2x2;
}

```

The [`$navigationIcon`](../navigation#customizing-a-navigation-items-icon) property is defined by default since you will most likely want to customize this immediately. All other [navigation properties and methods](../navigation) are also available to use, including [`$navigationLabel`](../navigation#customizing-a-navigation-items-label), [`$navigationSort`](../navigation#sorting-navigation-items) and [`$navigationGroup`](../navigation#grouping-navigation-items). These are used to customize the cluster’s main navigation item, in the same way you would customize the item for a resource or page.

## [​](#adding-resources-and-pages-to-a-cluster)Adding resources and pages to a cluster

To add resources and pages to a cluster, you just need to define the `$cluster` property on the resource or page class, and set it to the cluster class [you created](#creating-a-cluster):

Copy

```
use App\Filament\Clusters\SettingsCluster;

protected static ?string $cluster = SettingsCluster::class;

```

## [​](#code-structure-recommendations-for-panels-using-clusters)Code structure recommendations for panels using clusters

When using clusters, it is recommended that you move all of your resources and pages into a directory with the same name as the cluster. For example, here is a directory structure for a panel that uses a cluster called `Settings`, containing a `ColorResource` and two custom pages:

Copy

```
.
+-- Clusters
|   +-- Settings
|   |   +-- SettingsCluster.php
|   |   +-- Pages
|   |   |   +-- ManageBranding.php
|   |   |   +-- ManageNotifications.php
|   |   +-- Resources
|   |   |   +-- Colors
|   |   |   |   +-- ColorResource.php
|   |   |   |   +-- Pages
|   |   |   |   |   +-- CreateColor.php
|   |   |   |   |   +-- EditColor.php
|   |   |   |   |   +-- ListColors.php

```

This is a recommendation, not a requirement. You can structure your panel however you like, as long as the resources and pages in your cluster use the [`$cluster`](#adding-resources-and-pages-to-a-cluster) property. This is just a suggestion to help you keep your panel organized. When a cluster exists in your panel, and you generate new resources or pages with the `make:filament-resource` or `make:filament-page` commands, you will be asked if you want to create them inside a cluster directory, according to these guidelines. If you choose to, then Filament will also assign the correct `$cluster` property to the resource or page class for you. If you do not, you will need to [define the `$cluster` property](#adding-resources-and-pages-to-a-cluster) yourself.

## [​](#setting-the-sub-navigation-position-for-all-pages-in-a-cluster)Setting the sub-navigation position for all pages in a cluster

The sub-navigation is rendered at the start of each page by default. It can be customized per-page, but you can also customize it for the entire cluster at once by setting the `$subNavigationPosition` property. The value may be `SubNavigationPosition::Start`, `SubNavigationPosition::End`, or `SubNavigationPosition::Top` to render the sub-navigation as tabs:

Copy

```
use Filament\Pages\Enums\SubNavigationPosition;

protected static ?SubNavigationPosition $subNavigationPosition = SubNavigationPosition::End;

```

## [​](#customizing-the-cluster-breadcrumb)Customizing the cluster breadcrumb

The cluster’s name is in the breadcrumbs of all resources and pages in the cluster. You may customize the breadcrumb name using the `$clusterBreadcrumb` property in the cluster class:

Copy

```
protected static ?string $clusterBreadcrumb = 'cluster';

```

Alternatively, you may use the `getClusterBreadcrumb()` to define a dynamic breadcrumb name:

Copy

```
public static function getClusterBreadcrumb(): string
{
    return __('filament/clusters/cluster.name');
}

```

## [​](#removing-the-sub-navigation-from-a-cluster)Removing the sub navigation from a cluster

By default, all resources and pages in a cluster will show the sub-navigation. If you want to remove the sub-navigation from all resources and pages in a cluster, you can set the `$shouldRegisterSubNavigation` property to `false` in the cluster class:

Copy

```
protected static bool $shouldRegisterSubNavigation = false;

```

Alternatively, you may override the `shouldRegisterSubNavigation()` method to define dynamic behavior:

Copy

```
public static function shouldRegisterSubNavigation(): bool
{
    return FeatureFlag::active();
}

```

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/06-navigation/04-clusters.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[Your logo here](https://github.com/sponsors/danharrin)

[User menu](/docs/5.x/navigation/user-menu)[Overview](/docs/5.x/users/overview)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
