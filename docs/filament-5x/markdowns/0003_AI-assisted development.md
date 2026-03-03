## [​](#introduction)Introduction

This page is inspired by Laravel’s [AI Assisted Development documentation](https://laravel.com/docs/ai). Laravel Boost is developed by the Laravel team, and you can find out more about it in their official docs, alongside other information about building Laravel projects with AI assistance.

AI coding agents like [Claude Code](https://www.claude.com/product/claude-code), [Cursor](https://cursor.com), and [GitHub Copilot](https://github.com/features/copilot) can significantly accelerate your Filament development. Filament includes guidelines for [Laravel Boost](https://laravel.com/ai/boost) that teach AI agents how to write idiomatic Filament code and follow framework conventions. Laravel Boost even allows your agent to search the Filament documentation for answers when it encounters unfamiliar requirements.

## [​](#installing-laravel-boost)Installing Laravel Boost

Install Boost as a development dependency:

Copy

```
composer require laravel/boost --dev

```

Then run the interactive installer and select **Filament** when prompted:

Copy

```
php artisan boost:install

```

The installer will detect your IDE and AI agents, generating the necessary configuration files. To verify installation, check your `AGENTS.md`, `CLAUDE.md`, or similar file for a new **Filament** section. For more information about Laravel Boost, including available tools, documentation search, and IDE integration, see the [Laravel AI documentation](https://laravel.com/docs/ai).

## [​](#filament-blueprint)Filament Blueprint

The guidelines included with Boost are designed primarily for **implementing agents**: they help agents write correct Filament code once they know what to build. However, the quality of AI-generated code depends heavily on the quality of the plan. When an implementing agent has a clear, detailed specification, it can focus entirely on writing correct code rather than guessing at requirements or making assumptions about your intent. For complex features, you may find that agents struggle with the planning phase: choosing the right components, structuring relationships, and anticipating edge cases. A vague plan leads to vague code, and you end up spending more time correcting the agent than you saved by using it. **Filament Blueprint is a premium extension that helps AI agents produce accurate, detailed implementation plans for Filament.** It’s compatible with Filament v4 and above. Blueprint bridges the gap between what you want and what AI agents build. Instead of hoping an agent understands Filament’s conventions, Blueprint provides structured planning guidelines that produce unambiguous specification documents. A blueprint specifies everything an implementing agent needs:

- **Models**: Attributes, casts, relationships, and enums with exact syntax
- **Resources**: Full namespaces, scaffold commands, and configuration
- **Forms**: Field components, validation rules, and layout structure
- **Tables**: Columns, filters, actions, and sorting behavior
- **Authorization**: Plain-English policy rules that translate directly to code
- **Testing**: What to test and how to verify it works
- **More**: Reactive fields, wizards, imports/exports, bulk actions, widgets, multi-tenancy, and moreThe guidelines cover details that agents commonly get wrong, like namespaces, method names, component selection, and nested layout calculations, so the implementing agent can write correct code on the first try. The planning guidelines are designed for planning agents only, they shouldn’t consume the implementing agent’s context window. The planning agent copies all necessary details (namespaces, documentation URLs to fetch, exact method syntax) into the blueprint itself, so the implementing agent has everything it needs without loading the guidelines. If you’re interested in an example of a plan that Claude Opus 4.5 can write with and without Blueprint, visit the [Blueprint Plan Example](#blueprint-plan-example) section.

### [​](#installing-blueprint)Installing Blueprint

Blueprint is compatible with Filament v4 and above. Once you have [purchased a license for Blueprint](https://packages.filamentphp.com/portal/blueprint/checkout), install it via Composer:

Copy

```
composer config repositories.filament composer https://packages.filamentphp.com/composer
composer config --auth http-basic.packages.filamentphp.com "YOUR_EMAIL_ADDRESS" "YOUR_LICENSE_KEY"
composer require filament/blueprint --dev

```

Then run the Boost installer and select **Filament Blueprint** when prompted:

Copy

```
php artisan boost:install

```

To verify installation, check your `AGENTS.md`, `CLAUDE.md`, or similar file for a new **Filament Blueprint** section.

To access your purchased license, sign in to [Filament Packages](https://packages.filamentphp.com) with the email address used to purchase your Blueprint license.

### [​](#using-blueprint)Using Blueprint

To create a blueprint, enable **planning mode** in your AI agent and ask it to create a Filament Blueprint for your feature:

Copy

```
Create a Filament Blueprint for an order management system.

Orders belong to customers and have many order items. Each order has a status
(pending, confirmed, shipped, delivered, cancelled), shipping address, and
optional notes. Order items reference products with quantity and unit price.

I need to search orders by customer name and filter by status and date range.
The order form should calculate line totals automatically as items are added.
Only admins can delete orders, and orders can only be cancelled if not yet shipped.

```

The agent will produce a detailed specification document ready for direct implementation.

### [​](#blueprint-plan-example)Blueprint Plan Example

The following prompt was used with Claude Opus 4.5 in planning mode using Claude Code CLI:

Copy

```
Produce an implementation plan for a Filament v4 application. The application is
a SaaS invoicing system with the following capabilities:

- Manage customers
- Manage products
- Create and edit invoices
- Add line items to invoices
- Send invoices to customers
- Record and track payments
  
The plan should:
- Describe the primary user flows end to end (for example: creating an invoice,
  sending it, recording a payment).
- Map each domain concept and flow to concrete Filament primitives (Resources,
  Relation Managers, Pages, Actions).
- Identify state transitions (such as draft → sent → paid) and the Actions that
  trigger them.

```

You can read a plan written for this prompt [**without Blueprint**](https://filamentphp.com/blueprint/examples/invoicing/before.md) vs. [**with Blueprint**](https://filamentphp.com/blueprint/examples/invoicing/after.md), and compare the level of detail and thoughtfulness. You could have a go at passing these plans to your AI agent of choice in implementation mode to see how they perform!

When using Blueprint, `Using Filament Blueprint` was added at the start of the prompt.

### [​](#reporting-issues-with-blueprint)Reporting issues with Blueprint

If you encounter any issues or have suggestions for improving Filament Blueprint, please open an issue or discussion on the [Filament Blueprint Issues GitHub repository](https://github.com/filamentphp/blueprint-issues). If you have account or purchase-related questions, please email <support@filamentphp.com>.

[Edit this page on GitHub](https://github.com/filamentphp/filament/edit/5.x/docs/01-introduction/03-ai.md)

## Sponsored by

[https://kirschbaumdevelopment.com/solutions/filament-development](https://kirschbaumdevelopment.com/solutions/filament-development "Kirschbaum")[https://baiz.ai](https://baiz.ai "Baiz.ai")[https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament](https://mailtrap.io/email-sending?utm_source=community&utm_medium=referral&utm_campaign=filament "Mailtrap")[https://www.agiledrop.com/laravel?utm_source=filament](https://www.agiledrop.com/laravel?utm_source=filament "Agiledrop")[https://serpapi.com/?utm_source=filamentphp](https://serpapi.com/?utm_source=filamentphp "SerpApi")[https://cmsmax.com?ref=filamentphp.com](https://cmsmax.com?ref=filamentphp.com "CMS Max")[Your logo here](https://github.com/sponsors/danharrin)

[Installation](/docs/5.x/introduction/installation)[Optimizing local development](/docs/5.x/introduction/optimizing-local-development)

⌘I

[github](https://github.com/filamentphp/filament)[bluesky](https://bsky.app/profile/filamentphp.com)[x](https://twitter.com/filamentphp)[discord](https://filamentphp.com/discord)[linkedin](https://linkedin.com/company/filamentphp)

[Powered by](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=filament-34a8cf01)
