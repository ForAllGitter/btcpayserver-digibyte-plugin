# BTCPay Server DigiByte Plugin

**Accept DigiByte (DGB) payments with BTCPay Server** — self-hosted, non-custodial, and fully open-source.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Architecture

```
┌─────────────────┐      ┌─────────────────┐      ┌──────────────────────┐
│  DigiByte Core  │─────▶│    NBXplorer     │─────▶│   BTCPay Server      │
│     Node        │      │    (Indexer)     │      │  + DigiByte Plugin   │
└─────────────────┘      └─────────────────┘      └──────────────────────┘
```

- **DigiByte Core** provides the blockchain and RPC interface  
- **NBXplorer** indexes addresses and detects payments  
- **This Plugin** turns it into invoices, checkout pages, and store integration

---

## Prerequisites

- [ ] DigiByte Core node (fully synced) with `txindex=1`
- [ ] NBXplorer that can communicate with the DigiByte node
- [ ] BTCPay Server ≥ 2.3.7
- [ ] .NET 8.0 SDK (only needed for development)

---

## Quick Start

```bash
git clone https://github.com/ForAllGitter/btcpayserver-digibyte-plugin.git
cd btcpayserver-digibyte-plugin
dotnet build
```

Full operator instructions → **[docs/RUNBOOK.md](docs/RUNBOOK.md)**  
Architecture & design decisions → **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)**

---

## Documentation Map

| Document | Audience | Purpose |
|----------|----------|---------|
| [README.md](README.md) | Everyone | 60-second overview |
| [docs/RUNBOOK.md](docs/RUNBOOK.md) | Operators | How to run & troubleshoot |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | Contributors | Why the code is structured this way |
| [docs/SNAPSHOT.md](docs/SNAPSHOT.md) | Operators | How to create & verify chain snapshots |
| [CHANGELOG.md](CHANGELOG.md) | Everyone | What changed and why |

---

## License

MIT — free for any merchant, integrator, or fork. No gatekeepers.
