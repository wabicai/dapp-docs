---
description: NEAR integration via OneKey provider — detect, connect, send transactions, and sign
---

# NEAR

Build NEAR dApps with OneKey’s provider. Start with detection and connection, then follow the sending/signing guides.

## Quick links

- [Introduction](introduction.md)
- [Integrating](integrating/README.md)
  - [Detecting the Provider](integrating/detecting-the-provider.md)
  - [Establishing a Connection](integrating/establishing-a-connection.md)
  - [Accessing Accounts](integrating/accessing-accounts.md)
  - [Detecting Provider Network](integrating/detecting-provider-network.md)
  - [Watch Accounts & Network Status](integrating/watch-accounts-and-network-status.md)
  - [Sending Transactions](integrating/sending-transactions/README.md)
  - [Signing Messages](integrating/signing-messages.md)
  - [RPC API Calling](integrating/rpc-api-calling.md)
  - [Debug Logging](integrating/debug-logging.md)
  - [Migrate from Near Web Wallet](integrating/migrate-from-near-web-wallet.md)
- [Reference](reference/README.md)
- [Resources](resources/README.md)

## Minimal pattern

Use the Provider SDK to create a NEAR provider instance.

```ts
import { OneKeyNearProvider } from '@onekeyfe/onekey-near-provider'

const provider = new OneKeyNearProvider()
// Request accounts (example)
await provider.request({ method: 'near_accounts' })
```

## Events & network

- Watch account/network status via the Integrating section

## Common errors

- 4001: user rejected
- Invalid params: ensure method names and arguments follow the NEAR provider spec

## Mobile & deeplinks

- Use OneKey deeplinks to bridge from mobile H5/WebViews
- See [Use deeplinks](../../../guides/use-deeplinks.md)
