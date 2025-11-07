---
description: Make dApps compatible with MetaMask while prioritizing OneKey (EIP‑1193/EIP‑6963)
---

# Compatible with MetaMask

## Introduction

For EVM dApps, wallets like OneKey and MetaMask implement the Provider API following [EIP‑1193]. In most cases, a DApp that works with MetaMask also works with OneKey without code changes. When multiple wallets are installed, injected providers can conflict (e.g., `window.ethereum` ambiguity). This page shows how to prefer OneKey while staying compatible with MetaMask.

## Prefer OneKey provider

OneKey injects its provider at `window.$onekey.ethereum` in addition to the generic `window.ethereum`. Prefer the OneKey‑specific provider when available.

```javascript
const provider = (window.$onekey && window.$onekey.ethereum) || window.ethereum;
// Connect to wallet (legacy MetaMask API)
await provider.enable();
```

> Tip: Modern apps typically use `provider.request({ method: 'eth_requestAccounts' })` per EIP‑1193.

## Detect Ethereum provider (demo)

- Complete demo: https://codesandbox.io/embed/detect-ethereum-provider-q8chv5?autoresize=1&expanddevtools=1&fontsize=14&hidenavigation=1&module=%2Fsrc%2FEthereumProvider%2Findex.ts&theme=dark

## Avoiding conflicts (Wallet Switch)

When multiple extensions are installed, `window.ethereum` may be owned by different wallets at different times. OneKey provides a “Wallet Switch” feature to disable MetaMask‑compat injection when desired, ensuring only `window.$onekey.ethereum` is exposed to the page. This reduces ambiguity in multi‑wallet environments.

## Using wallet kits

If your app integrates a wallet kit, configure it to include/prioritize OneKey:

- Web3 Onboard — connect-to-software/support-wallet-kit/web3-onboard.md
- RainbowKit — connect-to-software/support-wallet-kit/rainbowkit.md
- Web3Modal — connect-to-software/support-wallet-kit/web3modal.md
- Aptos Wallet Adapter — connect-to-software/support-wallet-kit/aptos-wallet-adapter.md

## Identify OneKey provider

OneKey exposes a helper to identify itself in some environments.

```javascript
if ((provider.isOneKey && provider.isOneKey()) || provider.isOneKey) {
  console.log('The current provider comes from OneKey');
}
```

[EIP‑1193]: https://eips.ethereum.org/EIPS/eip-1193

## Further reading

- MetaMask Connect (JavaScript): https://docs.metamask.io/sdk/connect/javascript
