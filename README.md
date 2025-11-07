# Introduction

This repository contains the official docs for integrating the OneKey software wallet into your dApp. The structure centers on the EIP‑1193 provider model: a single “Connect to OneKey” entry focused on the injected provider, plus per‑chain API references (ETH/EVM, BTC, Solana, NEAR, Nostr, WebLN).

> For hardware/Air‑Gap SDKs, see: https://github.com/OneKeyHQ/hardware-sdk-docs

## Quick start (browser/JavaScript)

1) Install the OneKey browser extension or mobile app. In your dApp page, open DevTools and confirm `window.$onekey` exists.

2) Detect the provider and request accounts (EVM example):

```html
<script>
(async () => {
  const provider = window?.$onekey?.ethereum
    || window?.ethereum?.providers?.find(p => p?.isOneKey || p?.onekey)
    || window?.ethereum;
  if (!provider) {
    console.warn('OneKey not detected. Install the extension and retry.');
    return;
  }
  // Request accounts
  const [account] = await provider.request({ method: 'eth_requestAccounts' });
  console.log('Account:', account);
  // Optional: send a sample tx
  // const txHash = await provider.request({
  //   method: 'eth_sendTransaction',
  //   params: [{ from: account, to: '0x0000000000000000000000000000000000000001', value: '0x38d7ea4c68000' }]
  // });
  // console.log('Tx:', txHash);
})();
</script>
```

3) Continue per‑chain:

- EVM: Provider API / RPC / accounts / transactions / signing → see “Connect to OneKey → ETH”
- Others: see the chain sections (BTC/NEAR/Solana/Nostr/WebLN)

## Integration entry points

- [Connect to OneKey (overview)](connect-to-software/README.md)
- [JavaScript (EIP‑1193)](connect-to-software/webapp-connect-onekey/README.md)

## API references

- [ETH/EVM](connect-to-software/webapp-connect-onekey/eth/README.md)
- [Bitcoin](connect-to-software/webapp-connect-onekey/btc/README.md)
- [NEAR](connect-to-software/webapp-connect-onekey/near/README.md)
- [Solana](connect-to-software/webapp-connect-onekey/solana/README.md)
- [Nostr](connect-to-software/webapp-connect-onekey/nostr/README.md)
- [WebLN](connect-to-software/webapp-connect-onekey/webln/README.md)

## Support

- Issues & discussions: https://github.com/OneKeyHQ/hardware-js-sdk
- Product site: https://onekey.so/
- Help Center: https://help.onekey.so/hc
