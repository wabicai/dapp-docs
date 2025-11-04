# Connect to OneKey

Choose how your dApp connects to OneKey, following a simple, MetaMask‑SDK–style flow. Start with pure JavaScript provider integration, or pick an aggregator (Wallet Kit) when you need a plug‑and‑play UX across wallets.

## Options at a glance

- JavaScript + MetaMask (Recommended)
  - EIP‑1193 compatible; works with existing MetaMask‑based dApps
  - Prefer `window.$onekey.ethereum` when available to target OneKey explicitly
- JavaScript + OneKey Provider (EIP‑1193, pure JS)
  - Use OneKey’s injected provider for web dApps
  - Multi‑chain with per‑chain guides (ETH, BTC, Solana, NEAR, Nostr, WebLN)
- Wallet Kit (Aggregators)
  - Web3 Onboard (EVM), RainbowKit (EVM), Web3Modal (EVM)
  - Aptos Wallet Adapter (Aptos)
  - WalletConnect (cross‑platform linking)

## Recommended path

1) Building a web dApp and want direct control? Start with “JavaScript + OneKey Provider”.
2) Already using `window.ethereum` logic? See “JavaScript + MetaMask (compatible)”.
3) Need a polished multi‑wallet UX? Use “Wallet Kit” with your preferred aggregator.

