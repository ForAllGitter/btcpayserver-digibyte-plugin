# DigiDollar ($DD) Support – Roadmap Stub

**Status:** Future consideration  
**Priority:** High novelty / high value

---

## Why this matters

DigiDollar ($DD) is now live on DigiByte mainnet.  
It is an over-collateralized, on-chain stablecoin minted by time-locking DGB.

A BTCPay Server plugin that can accept **both DGB and $DD** natively would be genuinely novel in the current ecosystem.

Most merchants want price stability. Offering $DD as a payment option alongside (or instead of) volatile DGB would significantly increase real-world usefulness.

---

## Possible Approaches

1. **Treat $DD as a separate payment method**  
   Similar to how some plugins handle tokens on other chains.

2. **Unified DigiByte payment method** that can detect both DGB and $DD outputs.

3. **Invoice denomination in $DD** with automatic conversion / display.

---

## Open Questions

- How are $DD outputs currently identified on-chain?
- Is there a standard way to query $DD balances / transactions via RPC or NBXplorer?
- Do we need wallet-side support for minting/redeeming, or only for receiving?

---

## Current Decision

This is intentionally left as a **roadmap stub**.  
The first priority is a solid, reliable DGB payment plugin.  
Native $DD support will be evaluated once the core DGB path is production-ready.

Contributions and research on the points above are very welcome.
