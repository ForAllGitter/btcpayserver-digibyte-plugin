# Architecture – DigiByte BTCPay Plugin

This document explains *why* the code is structured the way it is.

---

## High-Level Flow

```
Invoice Created
      │
      ▼
PaymentMethodHandler.ConfigurePrompt()
      │  (generates address via NBXplorer / RPC)
      ▼
Address tracked by NBXplorer
      │
      ▼
DigiByteListener receives events
      │
      ▼
Payment detected → Invoice status updated
```

---

## Key Interfaces (BTCPay Server)

| Interface                    | Our Implementation                  | Purpose                              |
|-----------------------------|-------------------------------------|--------------------------------------|
| `IPaymentMethodHandler`     | `DigiBytePaymentMethodHandler`      | Creates payment prompts & addresses  |
| `IHostedService`            | `DigiByteListener`                  | Watches for new payments             |
| `IPaymentLinkExtension`     | `DigiBytePaymentLinkExtension`      | Adds payment links to invoices       |
| `ICheckoutModelExtension`   | `DigiByteCheckoutModelExtension`    | Checkout UI integration              |
| `ISyncSummaryProvider`      | `DigiByteSyncSummaryProvider`       | Shows sync status in BTCPay UI       |

---

## Where DigiByte Diverges from Bitcoin

| Area                    | Bitcoin Assumption          | DigiByte Reality                     |
|-------------------------|-----------------------------|--------------------------------------|
| Block time              | ~10 minutes                 | ~15 seconds                          |
| P2SH version byte       | `0x05`                      | `0x3F`                               |
| Address prefixes        | `1...` / `3...` / `bc1...`  | `D...` / `S...` / `dgb1...`          |
| Confirmation targets    | 1–6 blocks common           | Much higher numbers needed           |
| Network magic           | `f9beb4d9`                  | `fac3b6da` (`0xDAB6C3FA`)            |

These differences are the reason we maintain our own `DigiByteSpecificBtcPayNetwork` instead of reusing Bitcoin’s network object.

---

## Important Classes

- `DigiByteSpecificBtcPayNetwork` – Network definition + address encoding
- `DigiByteAddressHelper` – Safe parsing of all address types
- `DigiByteRpcProvider` – Thin wrapper around DigiByte Core RPC
- `DigiByteListener` – Event-driven payment detection
- `DigiBytePaymentMethodHandler` – Core payment logic

---

## Design Principles

1. Prefer NBXplorer over raw RPC for payment detection (more reliable).
2. Fail fast on configuration errors (partial configs are rejected).
3. Keep DGB-specific logic isolated so future contributors can find it quickly.
4. Document every non-obvious decision in this file or the Runbook.
