<div align="center">

# 0xda-market

**Provider-agnostic market infrastructure for digital products and assets.**

[Platform](https://0xda-market.nilx.one) · [Core](https://github.com/0xda-market/core) · [WebApp Core](https://github.com/0xda-market/webapp-core) · [Telegram Bot](https://github.com/0xda-market/telegram-bot)

</div>

---

## Overview

0xda-market is an engineering-first marketplace that separates the buyer-facing commercial price from broker supply economics.

The administrator owns the market price. Brokers publish finite inventory and their own supply asks. Core decides whether that supply is executable under FX freshness, margin, cost, buffer, and reservation constraints, then routes eligible order flow privately without exposing competitor asks.

## Current market contract

- **One client price.** Broker asks do not raise the price shown to the buyer.
- **Executable supply only.** Unprofitable or stale-FX supply can remain visible to broker/admin surfaces but cannot back a client quote.
- **Broker competition through routing.** Eligible supply is ranked privately; the current deterministic tiers are 100%, 80/20, or 70/20/10.
- **Server-owned FX.** Core persists provider-backed exchange-rate snapshots, enforces freshness, converts the USDT market price exactly, then applies currency-aware upward presentation.
- **Finite inventory.** Broker listings track total, available, reserved, and sold quantities under optimistic concurrency.
- **Explicit lifecycle.** Quotes, acceptance, payment-pending state, fulfillment, and order refresh remain durable core contracts rather than browser state.

## Engineering principles

- **Contracts over assumptions.** Public behavior is explicit, stable, and testable.
- **Predictability over cleverness.** Operational clarity matters more than abstraction for its own sake.
- **Architecture before implementation.** Dependencies point toward a provider-agnostic core.
- **Root cause over workarounds.** Fixes remove the actual failure mode.
- **Documentation is part of the change.** Architecture and public contracts stay synchronized with code.
- **Smallest correct change.** Every pull request should be scoped, reviewable, and complete.

## Architecture

```text
Telegram / future hosts
        │
        ▼
 channel adapter + webapp-core
        │
        ▼
       core
   ┌────┼─────┐
   ▼    ▼     ▼
  FX  stores  fulfillment/payment adapters
```

`core` owns market truth: products, users, roles, pricing, FX, listings, reservations, routing, quotes, orders, and payment state. `webapp-core` owns reusable browser interaction and presentation state. Channel adapters own authentication, signed transport, messenger SDK integration, shell presentation, and deployment entry points.

## Repositories

| Repository | Purpose |
| --- | --- |
| [`core`](https://github.com/0xda-market/core) | Provider-agnostic market kernel, APIs, pricing, FX, inventory, routing, and order lifecycle. |
| [`webapp-core`](https://github.com/0xda-market/webapp-core) | Host-agnostic marketplace UI, role workspaces, localization, and browser interaction contracts. |
| [`telegram-bot`](https://github.com/0xda-market/telegram-bot) | Telegram identity/transport adapter and Mini App host. |
| `docs` *(private)* | Cross-repository product, domain, and architecture documentation. |
| [`mind`](https://github.com/0xda-market/mind) | Versioned vendor-independent context baseline used for structured organization/project context. |
| [`.github`](https://github.com/0xda-market/.github) | Organization profile and shared GitHub configuration. |

The legacy `telegram-broker-bot` repository is archived; broker and administrator flows live inside the single Telegram bot and shared WebApp workspaces.

## Localization

The reusable WebApp currently has full UI bundles for English, Ukrainian, Russian, Spanish, and Brazilian Portuguese. Recognized European regional locales preserve region identity while falling back to English UI copy where a full bundle is not yet shipped. Product names remain core-owned localizations, and language does not hard-code buyer currency.

## Technology

The core and Telegram adapter are built primarily with **Ruby 3.3**, **Rack**, **Puma**, **Minitest**, and **PostgreSQL**. Shared browser behavior is maintained in `webapp-core`. Interfaces and infrastructure adapters remain replaceable around the domain core.

## Status

0xda-market is under active development. The implemented foundation already includes catalog/localization, administrator pricing, broker inventory, reservation-aware checkout, profitability gates, broker routing incentives, automated FX acquisition, localized price presentation, and role-aware Telegram Mini App surfaces.

Payment-provider settlement, broker payout accounting, refunds/disputes, and provider-specific automated fulfillment remain explicit next-layer contracts rather than assumptions hidden in the UI.

## License

Repository-specific licensing is defined in each repository. The [`core`](https://github.com/0xda-market/core) repository is available under the MIT License.
