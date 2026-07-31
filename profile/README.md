<div align="center">

# 0xda-market

**Provider-agnostic market infrastructure for digital assets and products.**

[Platform](https://0xda-market.nilx.one) · [Core](https://github.com/0xda-market/core) · [Telegram Bot](https://github.com/0xda-market/telegram-bot) · [Organization Mind](https://github.com/0xda-market/mind)

</div>

---

## Overview

0xda-market is an engineering-first market system for quoting, ordering, and executing transactions across interchangeable providers and venues.

The project keeps product-specific and provider-specific behavior outside the core. The core works with explicit contracts for intents, quotes, orders, execution, failures, idempotency, expiry, and concurrency.

## Engineering principles

- **Contracts over assumptions.** Public behavior is explicit, stable, and testable.
- **Predictability over cleverness.** Operational clarity matters more than abstraction for its own sake.
- **Architecture before implementation.** Dependencies point toward a provider-agnostic core.
- **Root cause over workarounds.** Fixes remove the actual failure mode.
- **Documentation is part of the change.** Architecture and public contracts stay synchronized with code.
- **Smallest correct change.** Every pull request should be scoped, reviewable, and complete.

## Architecture

```text
Telegram / REST / CLI
        │
        ▼
    transport
        │
        ▼
       core ◀──── adapters
        ▲
        │
    providers
        │
        ▼
 venues and external systems
```

The core remains independent of Telegram, databases, blockchains, exchanges, marketplaces, currencies, and product catalogs. Providers own their schemas, validation, upstream integrations, and operational policy.

## Repositories

| Repository | Purpose |
| --- | --- |
| [`core`](https://github.com/0xda-market/core) | Provider-agnostic server kernel and market API. |
| [`telegram-bot`](https://github.com/0xda-market/telegram-bot) | Telegram product catalog and client interaction adapter. |
| [`mind`](https://github.com/0xda-market/mind) | Versioned organizational identity, architecture, standards, and decisions. |
| [`.github`](https://github.com/0xda-market/.github) | Organization profile and shared GitHub configuration. |

## Current scope

The system is being built around:

- immutable intents, quotes, and orders;
- provider-owned quote and execution contracts;
- stable idempotency keys and retry semantics;
- explicit expiry and cancellation behavior;
- optimistic concurrency and conflict handling;
- strict separation of public terms and provider-private state;
- Telegram-facing product catalog and broker/client workflows;
- test and production environments with repeatable deployment contracts.

## Technology

The core service is built primarily with **Ruby 3.3**, **Rack**, **Puma**, **Minitest**, and **PostgreSQL**. Interfaces and integrations are intentionally replaceable around the domain core.

## Status

0xda-market is under active development. Interfaces, deployment workflows, product storage, localization, and provider integrations are evolving through reviewed pull requests and required CI.

## License

Repository-specific licensing is defined in each repository. The [`core`](https://github.com/0xda-market/core) repository is available under the MIT License.
