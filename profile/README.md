<div align="center">

<img src="./assets/emblem.svg" width="144" alt="0xda-market emblem">

# 0xda-market

**Provider-agnostic market infrastructure for digital products and assets.**

A child organization of [aiaiaiai](https://github.com/aiaiaiai-org), separating reusable market contracts from provider-, channel-, and product-specific implementations.

[Platform](https://0xda-market.nilx.one) · [Core](https://github.com/0xda-market/core) · [WebApp Core](https://github.com/0xda-market/webapp-core)

</div>

---

## System

`core` owns market truth: products, users, roles, pricing, FX, inventory, reservations, routing, quotes, orders, and payment state. `webapp-core` owns reusable browser interaction and presentation state. Concrete products own authentication, transport, host integration, and deployment.

```text
channel / product
       ↓
  webapp-core
       ↓
      core
```

## Repositories

| Repository | Role | Visibility |
| --- | --- | --- |
| [`core`](https://github.com/0xda-market/core) | Provider-agnostic market kernel and contracts | public |
| [`webapp-core`](https://github.com/0xda-market/webapp-core) | Host-agnostic marketplace UI and localization | public |
| `telegram-bot` | Telegram transport and current product surface | private |
| [`mind`](https://github.com/0xda-market/mind) | Versioned organization context | public |
| [`.github`](https://github.com/0xda-market/.github) | Organization profile and shared GitHub configuration | public |

## Operating principles

- One client price; broker asks do not rewrite buyer-facing truth.
- Executable supply must satisfy freshness, cost, margin, and reservation constraints.
- Provider boundaries remain explicit.
- Documentation and contracts evolve with implementation.
- Repository-specific licensing is declared inside each repository.

<div align="center">

[Parent: aiaiaiai](https://github.com/aiaiaiai-org) · [Owner: 0x0sky](https://github.com/0x0sky)

</div>

