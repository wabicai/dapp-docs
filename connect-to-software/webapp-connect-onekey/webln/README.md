---
description: WebLN integration via OneKey — enable, getInfo, makeInvoice, sendPayment, sign/verify message
---

# WebLN

Use OneKey’s WebLN provider to interact with Lightning-enabled apps.

## Quick links

- [Guide](guide.md)
- [API Reference](api-reference/README.md)
- [Events](event.md)

## Minimal pattern

```js
const provider = window?.$onekey?.webln || window?.webln
if (!provider) throw new Error('OneKey WebLN provider not detected')

await provider.enable()
const info = await provider.getInfo()
```

## Events

- See [Events](event.md) for account/network updates

## Common errors

- 4001: user rejected
- Invalid params/data: ensure proper invoice/message formats

## Mobile & deeplinks

- Use OneKey deeplinks to bridge from mobile H5/WebViews
- See [Use deeplinks](../../../guides/use-deeplinks.md)
