# 0xda-market GitHub configuration

This repository owns the public GitHub organization profile and shared community configuration for [`0xda-market`](https://github.com/0xda-market).

## Organization repositories

- [`core`](https://github.com/0xda-market/core) is the public provider-agnostic market foundation.
- [`webapp-core`](https://github.com/0xda-market/webapp-core) is the public reusable WebApp foundation.
- `telegram-bot` 🔐 is the private Telegram client product and Mini App host.
- [`mind`](https://github.com/0xda-market/mind) contains versioned organizational context and engineering contracts.
- `docs` 🔐 contains private cross-repository product, domain, and architecture documentation.

See [Repository Roles](docs/repository-roles.md) for the canonical distinction between repository role and visibility.

Repository-specific implementation and deployment documentation remains in each repository.

## Shared GitHub configuration

- [`profile/README.md`](profile/README.md) is rendered on the organization page.
- [`ISSUE_TEMPLATE/`](ISSUE_TEMPLATE/) contains organization-wide issue forms and configuration.
- [`PULL_REQUEST_TEMPLATE.md`](PULL_REQUEST_TEMPLATE.md) defines the default pull request template.
- [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md), [`SECURITY.md`](SECURITY.md), and [`SUPPORT.md`](SUPPORT.md) provide shared community health guidance.

```text
.github/
├── README.md
├── docs/
│   └── repository-roles.md
├── profile/
│   └── README.md
├── ISSUE_TEMPLATE/
│   ├── bug.yml
│   ├── feature.yml
│   └── config.yml
├── PULL_REQUEST_TEMPLATE.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
└── SUPPORT.md
```

GitHub applies supported files from this repository as defaults to organization repositories that do not define their own equivalents.
