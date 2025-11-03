---
description: Quickly choose the right OneKey dApp integration path and jump to the relevant guides
---

# Developer Guide

> Start with Quick Start (../quick-start.md) for runnable snippets. This page helps you choose the right route and jump to deep‑dive guides.

## Who Should Read This

| Role | Focus |
|---|---|
| Web dApp Developers | Inject a provider and use chain APIs in the browser |
| Wallet Aggregator Integrators | Bring OneKey into RainbowKit, Web3Modal, Web3 Onboard, etc. |

> Need hardware SDK or Air‑Gap? See https://github.com/OneKeyHQ/hardware-sdk-docs

## Decision Paths

### 1) Native Provider Integration

| Option | When to choose | Link |
|---|---|---|
| OneKey Provider (EIP‑1193) | Direct provider injection; replace or extend MetaMask | ../connect-to-software/webapp-connect-onekey/README.md |
| MetaMask Compatibility | App relies on `window.ethereum` and needs OneKey | ../connect-to-software/compatible-with-metamask/README.md |

### 2) Wallet Aggregators

| Option | When to choose | Link |
|---|---|---|
| Web3 Onboard / RainbowKit / Web3Modal | Consolidate OneKey with other wallets via mainstream kits | ../connect-to-software/support-wallet-kit/README.md |

### 3) Cross‑Platform Connectivity

| Option | When to choose | Link |
|---|---|---|
| WalletConnect | Reach mobile/desktop apps via QR / deep link | ../connect-to-software/using-walletconnect/README.md |
| Mobile Deep Link | Jump between mobile browsers and OneKey app | ../connect-to-software/using-walletconnect/mobile-deep-link.md |

## Quick Navigation

- Web App Integration Guide: web-app-integration-developer.md (end‑to‑end tutorial)
- ETH Provider: ../connect-to-software/webapp-connect-onekey/eth/README.md
- BTC Provider: ../connect-to-software/webapp-connect-onekey/btc/README.md
- Solana Provider: ../connect-to-software/webapp-connect-onekey/solana/README.md
- NEAR Provider: ../connect-to-software/webapp-connect-onekey/near/README.md

## API Reference Index

- EVM Provider API: ../connect-to-software/webapp-connect-onekey/eth/provider-api.md
- BTC Provider API: ../connect-to-software/webapp-connect-onekey/btc/api-reference/README.md
- Nostr Provider API: ../connect-to-software/webapp-connect-onekey/nostr/api-reference/README.md
- WebLN API: ../connect-to-software/webapp-connect-onekey/webln/api-reference/README.md
- WalletConnect (Aptos): ../connect-to-software/using-walletconnect/aptos/wallet-connect-api.md

## FAQ

- Need hardware signing or BLE transport? Use the Hardware SDK docs.
- Provider not detected (`window.$onekey` or `window.ethereum`)? See MetaMask compatibility detection.
- Mobile deep links failing? See WalletConnect deep‑link integration.
