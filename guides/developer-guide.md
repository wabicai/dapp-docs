---
description: Quickly choose the right OneKey dApp integration path and jump to the relevant guides
---

# 🚀 Developer Guide

> Use this quick navigator to map your dApp to the right OneKey integration path in minutes.

## 👨‍💻 Who Should Read This

<table>
<tr>
<td>🌐 <strong>Web dApp Developers</strong></td>
<td>🧰 <strong>Wallet Aggregator Integrators</strong></td>
</tr>
<tr>
<td>Inject providers to unlock on-chain capabilities in the browser</td>
<td>Bring OneKey into RainbowKit, Web3Modal, Web3 Onboard, and similar toolchains</td>
</tr>
</table>

{% hint style="warning" %}
Need hardware SDK or Air Gap capabilities? Switch to the [OneKey Hardware SDK documentation](https://github.com/OneKeyHQ/hardware-js-sdk/tree/main/hardware-sdk-docs).
{% endhint %}

## 🎯 Decision Paths

### 1️⃣ Native Provider Integration

| Option | When to Choose It | Quick Link |
|--------|-------------------|------------|
| **OneKey Provider (EIP-1193)** | Direct provider injection to replace or extend MetaMask | [→ OneKey Provider](../connect-to-software/webapp-connect-onekey/README.md) |
| **MetaMask Compatibility Mode** | Existing apps rely on `window.ethereum` and need OneKey support | [→ MetaMask Compatibility](../connect-to-software/compatible-with-metamask/README.md) |

### 2️⃣ Wallet Aggregators

| Option | When to Choose It | Quick Link |
|--------|-------------------|------------|
| **Web3 Onboard / RainbowKit / Web3Modal** | Consolidate OneKey alongside other wallets through mainstream aggregators | [→ Aggregator Support Matrix](../connect-to-software/support-wallet-kit/README.md) |

### 3️⃣ Cross-Platform Connectivity

| Option | When to Choose It | Quick Link |
|--------|-------------------|------------|
| **WalletConnect** | Extend to mobile apps, desktop clients, or deep-link experiences | [→ WalletConnect Guide](../connect-to-software/using-walletconnect/README.md) |
| **Mobile Deep Link** | Jump between mobile browsers and the OneKey app | [→ Deep Link Guide](../connect-to-software/using-walletconnect/mobile-deep-link.md) |

---

## 📚 Quick Navigation

- [Web App Integration Guide](web-app-integration-developer.md) – complete browser integration playbook
- [Ethereum & EVM Provider API](../connect-to-software/webapp-connect-onekey/eth/README.md)
- [Bitcoin Provider API](../connect-to-software/webapp-connect-onekey/btc/README.md)
- [Solana Provider API](../connect-to-software/webapp-connect-onekey/solana/README.md)
- [NEAR Provider API](../connect-to-software/webapp-connect-onekey/near/README.md)

## 🧪 Demos & Tools

| Tool | Purpose | Entry Point |
|------|---------|-------------|
| **OneKey Provider Demo** | Validate EIP-1193 integration and multi-chain signing | [→ Provider Demo](../connect-to-software/webapp-connect-onekey/README.md#example) |
| **WalletConnect Demo** | Explore QR flows and event handling | [→ WalletConnect Demo](../connect-to-software/using-walletconnect/README.md#demo) |

## 🔍 API Reference Index

- [EVM Provider API](../connect-to-software/webapp-connect-onekey/eth/provider-api.md)
- [BTC Provider API](../connect-to-software/webapp-connect-onekey/btc/api-reference/README.md)
- [Nostr Provider API](../connect-to-software/webapp-connect-onekey/nostr/api-reference/README.md)
- [LN WebLN API](../connect-to-software/webapp-connect-onekey/webln/api-reference/README.md)
- [WalletConnect API (Aptos)](../connect-to-software/using-walletconnect/aptos/wallet-connect-api.md)

## ❓ FAQ

- Need hardware signing or BLE transport? Use the [Hardware SDK docs](https://github.com/OneKeyHQ/hardware-js-sdk/tree/main/hardware-sdk-docs).
- Provider not detected (`window.$onekey` or `window.ethereum`)? Start with the [MetaMask compatibility guide](../connect-to-software/compatible-with-metamask/detectethereumprovider.md).
- Deep links failing on mobile? Review the [WalletConnect deep-link integration](../connect-to-software/using-walletconnect/mobile-deep-link.md).

## 📚 Glossary

- **Provider**: EIP-1193/EIP-6963 compliant browser interface exposing blockchain RPC methods.
- **Wallet Aggregator**: Third-party component that standardizes multi-wallet connectivity, e.g., Web3Modal or RainbowKit.
- **Deep Link**: URL scheme that launches the OneKey app from another application.
- **Session**: A WalletConnect term for the long-lived channel used to deliver subsequent signing requests.
