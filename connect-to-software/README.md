# Connect to OneKey

This section focuses on connecting to OneKey using the injected EIP‑1193 provider. No extra SDK is required for the web — detect and call the provider directly.

## Recommended

- JavaScript (EIP‑1193, pure web):
  - Prefer `window.$onekey.ethereum`; fall back to `window.ethereum` as needed
  - Multi‑chain; see per‑chain sections for signing/transactions/events (ETH, BTC, Solana, NEAR, Nostr, WebLN)

> Note: This section centers on the native provider flow based on EIP‑1193. If your app already uses Wallet Kits or needs compatibility guidance, see [Support Wallet Kits](support-wallet-kit/README.md) and [Compatible with MetaMask](compatible-with-metamask.md).

## Minimal example (EVM)

```js
const provider = window?.$onekey?.ethereum
  || window?.ethereum?.providers?.find(p => p?.isOneKey || p?.onekey)
  || window?.ethereum;
if (!provider) throw new Error('OneKey not detected');
const [account] = await provider.request({ method: 'eth_requestAccounts' });
console.log('Account:', account);
```

See [JavaScript (EIP‑1193)](webapp-connect-onekey/README.md) for details.
