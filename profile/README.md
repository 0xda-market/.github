<div align="center">

# 0xda-market

**Provider-agnostic market infrastructure for digital products and assets.**

[Platform](https://0xda-market.nilx.one) · [Core](https://github.com/0xda-market/core) · [WebApp Core](https://github.com/0xda-market/webapp-core) · Telegram Bot 🔐

</div>

---

## Organization

`0xda-market` is a child organization in the **aiaiaiai tech. / 4xAI tech.** ecosystem.

- **Parent organization:** [aiaiaiai tech.](https://github.com/aiaiaiaitech)
- **Owner:** [0x0sky](https://github.com/0x0sky)
- **Role:** digital commerce organization

This relationship is part of the ecosystem's organizational and ownership model. GitHub itself represents `0xda-market` and `aiaiaiaitech` as peer organization namespaces and does not encode this parent-child relationship natively.

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

### Repository model

`0xda-market` separates reusable foundations from concrete client-facing products. Repository role and GitHub visibility are independent: `core` and `webapp-core` are public foundations, while products built on top of them may remain private.

See [Repository Roles](../docs/repository-roles.md) for the canonical classification model.

## Repositories

| Repository | Role | Visibility | Purpose |
| --- | --- | --- | --- |
| [`core`](https://github.com/0xda-market/core) | foundation | public | Provider-agnostic market kernel, APIs, pricing, FX, inventory, routing, and order lifecycle. |
| [`webapp-core`](https://github.com/0xda-market/webapp-core) | foundation | public | Host-agnostic marketplace UI, role workspaces, localization, and browser interaction contracts. |
| `telegram-bot` | product | private 🔐 | Telegram identity/transport adapter, Mini App host, and current client-facing product. |
| `docs` | documentation | private 🔐 | Cross-repository product, domain, and architecture documentation. |
| [`mind`](https://github.com/0xda-market/mind) | mind | public | Versioned organization/project context baseline, represented as `fork/mind` where provenance is shown. |
| [`.github`](https://github.com/0xda-market/.github) | profile | public | Organization profile and shared GitHub configuration. |

The legacy `telegram-broker-bot` repository is archived; broker and administrator flows live inside the single Telegram bot and shared WebApp workspaces.

## Status

0xda-market is under active development. The implemented foundation already includes catalog/localization, administrator pricing, broker inventory, reservation-aware checkout, profitability gates, broker routing incentives, automated FX acquisition, localized price presentation, and role-aware Telegram Mini App surfaces.

Payment-provider settlement, broker payout accounting, refunds/disputes, and provider-specific automated fulfillment remain explicit next-layer contracts rather than assumptions hidden in the UI.

## License

Repository-specific licensing is defined in each repository. The [`core`](https://github.com/0xda-market/core) repository is available under the MIT License.
