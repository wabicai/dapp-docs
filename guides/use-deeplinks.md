---
description: Use deeplinks to connect users to OneKey across platforms with WalletConnect
---

# Use deeplinks

This guide shows how to open the OneKey app from web (mobile/desktop) and cross‑platform containers using deeplinks that carry a WalletConnect URI.

- Works in mobile browsers, WebViews, React Native/Expo, Telegram Mini Apps, etc.
- Keep a fallback (Universal Link or QR) for reliable UX.

## When to use deeplinks

- You need to jump from a mobile web page or in‑app WebView to OneKey
- You want a single flow that works across iOS and Android
- You use an aggregator or WalletConnect already and want consistent UX

## Link types and priority

1) Custom scheme (recommended)
- `onekey-wallet://wc?uri={encoded_wc_uri}`
- Best on mobile to directly open the OneKey app

2) Raw WalletConnect URI (recommended)
- `wc:xxxxx@2?relay-protocol=irn&symKey=...`
- Some runtimes open raw WC URIs directly

3) Universal link (fallback)
- `https://app.onekey.so/wc/connect/wc?uri={encoded_wc_uri}`
- Use when custom schemes are blocked by the environment

Always wrap the URI in `encodeURIComponent(wcUri)` when placing into a query string.

## Quick start (EVM example)

```ts
import { SignClient } from '@walletconnect/sign-client';

const client = await SignClient.init({
  projectId: 'YOUR_PROJECT_ID',
  metadata: {
    name: 'My DApp',
    description: 'WalletConnect integration',
    url: 'https://example.com',
    icons: ['https://example.com/icon.png'],
  },
});

const { uri, approval } = await client.connect({
  requiredNamespaces: {
    eip155: {
      methods: ['eth_sendTransaction', 'personal_sign'],
      chains: ['eip155:1'],
      events: ['chainChanged', 'accountsChanged'],
    },
  },
});

if (uri) {
  const deepLink = `onekey-wallet://wc?uri=${encodeURIComponent(uri)}`;      // preferred
  const raw = uri;                                                           // alternative
  const universal = `https://app.onekey.so/wc/connect/wc?uri=${encodeURIComponent(uri)}`; // fallback
  window.open(deepLink, '_blank');
}

const session = await approval();
console.log('Connected:', session);
```

## Platform guidance

- iOS Safari: prefer `location.href = deepLink`; use a short timeout to fallback to the Universal Link
- Android browsers: custom schemes usually work well
- WebViews / app containers: require a user gesture to open external links
- Desktop: prefer QR; offer a "Continue on mobile" button with the Universal Link

## Fallback strategy

- Not installed: show a QR option or direct users to download OneKey
- No response: fallback to the Universal Link
- Long URIs: reduce methods/events/chains to shorten the payload

## Related docs

- WalletConnect: connect-to-software/using-walletconnect/README.md
- Web app integration (deeplinks): guides/web-app-integration-developer.md
- OneKey Provider (EIP‑1193): connect-to-software/webapp-connect-onekey/README.md
- Wallet Kit aggregators: connect-to-software/wallet-kit/README.md
