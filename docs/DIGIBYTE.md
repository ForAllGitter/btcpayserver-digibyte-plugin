# DigiByte Realities

This document captures DigiByte-specific facts that frequently surprise people coming from Bitcoin.

---

## Block Time & Confirmations (MultiShield)

DigiByte targets a **15-second block time**.

| Confirmations | Approximate Time |
|---------------|------------------|
| 1             | ~15 seconds      |
| 6             | ~90 seconds      |
| 12            | ~3 minutes       |
| 20            | ~5 minutes       |

**Important:**  
BTCPay Server’s default invoice expiration and confirmation targets are tuned for Bitcoin (~10-minute blocks).  
If you leave those defaults, merchants accepting DigiByte will experience unnecessarily long waits and frustrated customers.

This plugin will ship with DigiByte-aware defaults.

---

## Odocrypt

Odocrypt is one of DigiByte’s five mining algorithms. It **mutates every 10 days**.

This is completely irrelevant to payment processing and merchant operations.  
It only affects miners and mining software.

If you are implementing or debugging the payment plugin and see “Odocrypt” mentioned, you can safely ignore it.

---

## Multi-Algorithm Mining

DigiByte uses five independent Proof-of-Work algorithms:

- SHA256d
- Scrypt
- Qubit
- Skein
- Odocrypt

This design improves decentralization of hashrate.  
For a BTCPay plugin it has no direct impact — we only care about the resulting UTXO set and transaction confirmations.

---

## Address Formats

| Type     | Prefix     | Notes                          |
|----------|------------|--------------------------------|
| P2PKH    | `D...`     | Legacy                         |
| P2SH     | `S...`     | Version byte `0x3F`            |
| Native SegWit | `dgb1q...` | Bech32                    |
| Taproot  | `dgb1p...` | Bech32m                        |

Never reuse Bitcoin’s default P2SH encoder.
