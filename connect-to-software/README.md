# Connect to OneKey

This section mirrors the MetaMask Connect/JavaScript category and keeps a single entry: connect to OneKey using the injected EIP‑1193 provider. No extra SDK is required for the web — detect and call the provider directly.

## Recommended

- JavaScript (EIP‑1193, pure web):
  - Prefer `window.$onekey.ethereum`; fall back to `window.ethereum` as needed
  - Multi‑chain; see per‑chain sections for signing/transactions/events (ETH, BTC, Solana, NEAR, Nostr, WebLN)

> Note: To stay focused, we do not include separate navigation entries for WalletKit/WalletConnect or “MetaMask compatibility”. If your app already uses them, you can keep using them. This documentation centers on the native provider flow, aligned with MetaMask’s Connect/JavaScript.

## Minimal example (EVM)

```js
const provider = window?.$onekey?.ethereum
  || window?.ethereum?.providers?.find(p => p?.isOneKey || p?.onekey)
  || window?.ethereum;
if (!provider) throw new Error('OneKey not detected');
const [account] = await provider.request({ method: 'eth_requestAccounts' });
console.log('Account:', account);
```

See “JavaScript (EIP‑1193)” for details.
