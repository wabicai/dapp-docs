---
description: Ethereum & EVM integration with OneKey’s injected EIP‑1193 provider
---

# ETH / EVM

Use the injected EIP‑1193 provider to build EVM dApps with OneKey. Behavior mirrors MetaMask. Start by detecting the provider and requesting accounts, then use the methods below for transactions and signing.

## Quick links

- Provider API: provider lifecycle, detection, events → provider-api.md
- RPC API: common JSON‑RPC calls → rpc-api.md
- Accessing Accounts: request/connect flow → accessing-accounts.md
- Sending Transactions: EIP‑1559 transaction flow → sending-transactions.md
- Signing Data: personal_sign, EIP‑712 → signing-data.md

## Minimal pattern

```js
const provider = window?.$onekey?.ethereum
  || window?.ethereum?.providers?.find(p => p?.isOneKey || p?.onekey)
  || window?.ethereum
if (!provider) throw new Error('OneKey not detected')
const [account] = await provider.request({ method: 'eth_requestAccounts' })
```

## Events & network

- Listen to `accountsChanged` and `chainChanged`
- For switching/adding chains: `wallet_switchEthereumChain`, `wallet_addEthereumChain`

## Common errors

- 4001: user rejected
- 4902: unknown chain (add the chain first)
- Invalid params: use 0x‑prefixed hex strings; avoid raw BigInt in RPC params

## Mobile & deeplinks

- Use OneKey deeplinks that carry a WalletConnect URI
- See Guides → Use deeplinks

See also Connect → JavaScript (EIP‑1193) for an extended introduction.
