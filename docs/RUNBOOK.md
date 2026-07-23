# DigiByte Plugin – Operator Runbook

This document contains the hard-won operational knowledge needed to run the plugin reliably.

---

## Critical Requirements

### 1. `txindex=1` is non-negotiable

NBXplorer **will fail** on arbitrary transaction lookups if the DigiByte node does not have `txindex=1`.

```ini
# digibyte.conf
server=1
txindex=1
rpcuser=your_rpc_user
rpcpassword=your_rpc_password
rpcallowip=127.0.0.1
rpcport=14022
port=12024
```

### 2. Port Reference

| Service              | Port   | Purpose                        |
|----------------------|--------|--------------------------------|
| DigiByte P2P         | 12024  | Peer connections               |
| DigiByte RPC         | 14022  | JSON-RPC interface             |
| NBXplorer            | 24444  | Default API port               |

### 3. NBXplorer Configuration (`digibyte.config`)

```ini
chains=dgb
dgb.rpc.url=http://127.0.0.1:14022
dgb.rpc.user=your_rpc_user
dgb.rpc.password=your_rpc_password
dgb.node.endpoint=127.0.0.1:12024
```

### 4. Handshake Verification (Do this first)

Before writing any payment code or enabling the plugin, verify the connection:

```bash
curl http://localhost:24444/v1/cryptos/DGB/status
```

You must receive a valid JSON response. If this fails, **stop** and fix the node / NBXplorer configuration.

---

## Confirmation Targets

DigiByte produces a block roughly every **15 seconds**.

Recommended confirmation targets for invoices:

| Risk Level     | Confirmations | Approx. Time |
|----------------|---------------|--------------|
| Low risk       | 6             | ~1.5 min     |
| Medium risk    | 12            | ~3 min       |
| High value     | 20+           | ~5 min       |

This is very different from Bitcoin’s 10-minute blocks. Do **not** copy Bitcoin confirmation assumptions.

---

## Address Types

The plugin supports all current DigiByte address formats:

| Type     | Prefix   | Notes                          |
|----------|----------|--------------------------------|
| P2PKH    | `D...`   | Legacy                         |
| P2SH     | `S...`   | Version byte `0x3F` (important)|
| P2WPKH   | `dgb1q...` | Native SegWit                |
| Taproot  | `dgb1p...` | Bech32m                      |

**Never** use Bitcoin’s default P2SH encoder — it will silently accept invalid addresses.

---

## Common Failure Modes

| Symptom                              | Most likely cause                     |
|--------------------------------------|---------------------------------------|
| `/v1/cryptos/DGB/status` returns 404 | NBXplorer not registered for DGB     |
| Transactions not detected            | Missing `txindex=1`                  |
| Invalid address errors               | Wrong version bytes / Bech32 config  |
| Peer connection refused              | Wrong magic bytes or port            |
