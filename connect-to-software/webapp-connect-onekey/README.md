# JavaScript + OneKey Provider (纯 JS)

Use OneKey’s injected provider in the browser (EIP‑1193). This is the most direct way to integrate OneKey into a web dApp, with multi‑chain capabilities and dedicated guides per chain.

- Ethereum / EVM → see `ETH` docs below
- Bitcoin → see `BTC` docs below
- NEAR → see `NEAR` docs below
- Solana → see `SOLANA` docs below
- Nostr → see `Nostr` docs below
- WebLN → see `WebLN` docs below

Typical detection pattern:

```js
const provider = (window.$onekey && window.$onekey.ethereum) || window.ethereum;
// Request accounts / permissions
await provider.request({ method: 'eth_requestAccounts' });
```

Refer to chain‑specific sections for signing, transactions, events, and RPC details.
