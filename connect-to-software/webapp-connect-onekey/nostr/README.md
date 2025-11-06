---
description: Nostr integration via OneKey provider — getPublicKey, signEvent, signSchnorr, and more
---

# Nostr

Integrate Nostr capabilities using OneKey’s provider.

## Quick links

- Guide → guide.md
- API Reference → api-reference/README.md
- Events → event.md

## Minimal pattern

```js
const provider = window?.$onekey?.nostr || window?.nostr
if (!provider) throw new Error('OneKey Nostr provider not detected')

const pubkey = await provider.getPublicKey()
// Example: sign an event (fill your own event fields)
// const signed = await provider.signEvent(event)
```

## Events

- See Events page for account/network related updates

## Common errors

- 4001: user rejected
- Invalid params: match NIP‑07 expectations

## Mobile & deeplinks

- Use OneKey deeplinks when bridging from mobile web/WebViews
- See Guides → Use deeplinks
