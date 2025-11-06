---
description: Web/H5 deeplinks — open OneKey with a WalletConnect URI and provide robust fallbacks
---

# Web app integration (deeplinks)

This guide targets web/H5 dApps. It shows how to open OneKey from the browser using a deeplink that carries a WalletConnect URI, and how to design robust fallbacks across platforms.

- Overview: guides/developer-guide.md

## Flow

1) Create a WalletConnect `uri`
2) Choose an opener based on the runtime (deeplink/raw URI/Universal Link)
3) User approves in OneKey → receive a session
4) Use per‑chain provider/RPC to interact with accounts

## Code template (EVM)

```ts
import { SignClient } from '@walletconnect/sign-client';

export async function connectWithOneKey() {
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
    const deepLink = `onekey-wallet://wc?uri=${encodeURIComponent(uri)}`;
    const universal = `https://app.onekey.so/wc/connect/wc?uri=${encodeURIComponent(uri)}`;
    const isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
    if (isMobile) {
      window.location.href = deepLink;
      setTimeout(() => { window.location.href = universal; }, 1500);
    } else {
      window.open(universal, '_blank');
    }
  }

  const session = await approval();
  return session;
}
```

## Platform notes

- iOS Safari: stricter popup rules — prefer `location.href = deepLink` with a short timeout fallback
- Android browsers: custom schemes generally work well
- Embedded WebViews: open external links on user gesture
- Telegram Mini Apps: use the platform’s external opener on user interaction

## Fallback UX (recommended)

- Deeplink button (mobile‑first): “Open in OneKey”
- QR (desktop‑first): scan with the OneKey mobile app
- Universal Link button: when custom schemes are blocked
- Store link: offer to download OneKey if not installed

## About aggregators

To keep this doc lean, we don’t provide a dedicated aggregator section. If your project already integrates RainbowKit/Web3Modal/Web3 Onboard, prioritize OneKey in their mobile‑open logic.

## After session established

- EVM: use the EIP‑1193 provider (`eth_requestAccounts`, `eth_sendTransaction`, `personal_sign`, ...)
- Other chains: use each chain’s provider/RPC

Entry: connect-to-software/webapp-connect-onekey/README.md

## Troubleshooting

- Deeplink doesn’t open: ensure OneKey is installed; try Universal Link; ensure user‑initiated action
- Universal Link stays in browser: use QR fallback; associated domain config is app‑side
- WalletConnect handshake fails: verify `projectId` and connectivity; simplify `requiredNamespaces`
- URI too long: reduce methods/events/chains; avoid extra payload in query strings
