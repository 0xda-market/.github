# Repository Roles

This document defines how repositories in the `0xda-market` organization are classified.

Repository role and GitHub visibility are independent properties. A public repository is not necessarily a final product, and a private repository is not an architectural layer by itself.

## Foundations

### `core`

**Role:** foundation  
**Visibility:** public

`core` is the provider-agnostic backend and domain foundation of `0xda-market`.

It owns reusable market rules and infrastructure that client-facing products can build on: products, users, roles, pricing, FX, broker inventory, reservations, routing, quotes, orders, and payment state.

`core` is not a final product.

### `webapp-core`

**Role:** foundation  
**Visibility:** public

`webapp-core` is the reusable web application foundation.

It owns host-agnostic browser interaction, presentation state, role workspaces, and reusable WebApp behavior from which concrete client products can be built.

`webapp-core` is not a final product.

A concrete client may inherit from both public foundations while remaining private:

```text
core ──────────┐
               ├──→ client product 🔐
webapp-core ───┘
```

## Products

### `telegram-bot` 🔐

**Role:** product  
**Visibility:** private

`telegram-bot` is currently the first concrete client-facing `0xda-market` product.

Its Telegram Web App is a component of that product rather than the shared `webapp-core` itself.

```text
0xda-market
│
├─ core                         public foundation
├─ webapp-core                  public foundation
└─ telegram-bot 🔐              private product
   └─ web-app 🔐                private product component
```

A future standalone website should be treated as another client product. It may inherit reusable behavior from `core` and `webapp-core` while keeping its product-specific implementation private.

```text
core ──────────┐
               ├──→ website 🔐
webapp-core ───┘

core ──────────┐
               ├──→ telegram-bot 🔐
webapp-core ───┘       └─ web-app 🔐
```

## Organization context

### `mind`

**Role:** mind  
**Visibility:** public

The organization `mind` repository is a fork of the canonical mind protocol and describes structured organization/project context. It is knowledge infrastructure, not a market product.

In interfaces that distinguish provenance, it should be presented as `fork/mind`.

### `.github`

**Role:** profile  
**Visibility:** public

The `.github` repository owns the public organization profile and shared GitHub configuration. Its `profile/README.md` is the canonical human-readable organization introduction.

## Classification model

Every repository should be understood along at least two independent axes:

| Axis | Values |
| --- | --- |
| Role | `foundation`, `product`, `mind`, `profile` |
| Visibility | `public`, `private` |

Current classification:

| Repository | Role | Visibility |
| --- | --- | --- |
| `core` | foundation | public |
| `webapp-core` | foundation | public |
| `telegram-bot` | product | private 🔐 |
| `telegram-bot/web-app` | product component | private 🔐 |
| `fork/mind` | mind | public |
| `.github` | profile | public |

## Interpretation rule

Consumers such as `mind-web` must not infer repository role from GitHub visibility.

Visibility answers **who may read the repository**. Role answers **what the repository is in the system**.

These concepts must remain separate so that, for example, a public open-source product can still be classified as a product and a private implementation can inherit public foundations without changing their architectural meaning.
