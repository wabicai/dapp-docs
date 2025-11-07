---
description: Solana integration via OneKey provider — detect, connect, send transactions, and sign messages
---

# Solana

Use OneKey’s Solana provider in web apps.

## Quick links

- [Detecting the Provider](detecting-the-provider.md)
- [Establishing a Connection](establishing-a-connection.md)
- [Sending a Transaction](sending-a-transaction.md)
- [Signing a Message](signing-a-message.md)

## Minimal pattern

```js
// Detect
const provider = window?.$onekey?.solana || window?.solana
if (!provider?.isOneKey) throw new Error('OneKey Solana provider not detected')

// Connect
const { publicKey } = await provider.connect()
console.log(publicKey.toString())
```

## Events

- `connect`, `disconnect`, `accountChanged`

## Common errors

- 4001: user rejected the request

## Mobile & deeplinks

- Use OneKey deeplinks with a WalletConnect URI for mobile handoff
- See [Use deeplinks](../../../guides/use-deeplinks.md)
