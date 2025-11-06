---
description: Open OneKey with deeplinks across platforms using a WalletConnect URI (MetaMask-style, simplified)
---

# Use deeplinks

This guide shows how to open the OneKey app from mobile web/WebViews using deeplinks that carry a WalletConnect URI. It mirrors the minimal pattern from MetaMask’s docs.

- Where: mobile browsers, WebViews, React Native/Expo, Telegram Mini Apps, etc.
- Always keep a fallback (Universal Link or QR)

## Link types and priority

1) Custom scheme (preferred)
- `onekey-wallet://wc?uri={encodeURIComponent(wcUri)}`

2) Raw WalletConnect URI (optional)
- `wc:xxxxx@2?relay-protocol=irn&symKey=...`

3) Universal Link (fallback)
- `https://app.onekey.so/wc/connect/wc?uri={encodeURIComponent(wcUri)}`

Note: Always `encodeURIComponent` when putting the URI in a query string.

## Quick example (EVM)

```ts
import { SignClient } from '@walletconnect/sign-client';

const client = await SignClient.init({
  projectId: 'YOUR_PROJECT_ID',
  metadata: { name: 'My DApp', description: 'WalletConnect', url: 'https://example.com', icons: ['https://example.com/icon.png'] },
});

const { uri, approval } = await client.connect({
  requiredNamespaces: { eip155: { methods: ['eth_sendTransaction', 'personal_sign'], chains: ['eip155:1'], events: ['chainChanged', 'accountsChanged'] } },
});

if (uri) {
  const deepLink = `onekey-wallet://wc?uri=${encodeURIComponent(uri)}`;
  const universal = `https://app.onekey.so/wc/connect/wc?uri=${encodeURIComponent(uri)}`;
  const isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
  if (isMobile) {
    window.location.href = deepLink;
    setTimeout(() => { window.location.href = universal; }, 1500);
  } else {
    // Desktop: prefer QR; if linking, open Universal Link
    window.open(universal, '_blank');
  }
}

const session = await approval();
```

## Platform notes

- iOS Safari: prefer `location.href = deepLink`; short timeout to Universal Link fallback
- Android: custom scheme usually works well
- WebViews: often require a user gesture to open external links
- Desktop: prefer QR; provide a “Continue on mobile” Universal Link

## Fallback strategy

- Not installed: show QR or direct to download OneKey
- No response: fallback to Universal Link
- Long URI: reduce methods/events/chains to shorten

## Related

- OneKey Provider (EIP‑1193): connect-to-software/webapp-connect-onekey/README.md
- Web app integration (deeplinks): guides/web-app-integration-developer.md
