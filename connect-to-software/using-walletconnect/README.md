# JavaScript + WalletConnect

WalletConnect enables cross‑platform connections between your DApp and the OneKey app on mobile and desktop. This page gives you a minimal, production‑oriented entry and links to deeper platform guides.

## When to Use WalletConnect

- You need to reach native OneKey apps from mobile web, Telegram Mini Apps, or another native app.
- You want a single connection flow that works across devices and OSes.
- You already use an aggregator (Web3Modal/RainbowKit/Web3 Onboard) and prefer WalletConnect under the hood.

## Recommended Link Order

1) Deep Link (recommended): `onekey-wallet://wc?uri={encoded_wc_uri}`
2) Raw WalletConnect URI (recommended): `wc:xxxxx@2?relay-protocol=irn&symKey=...`
3) Universal Link (fallback): `https://app.onekey.so/wc/connect/wc?uri={encoded_wc_uri}`

Always wrap with `encodeURIComponent(wcUri)` when injecting into URLs.

## Quick Start (EVM via SignClient)

```ts
import { SignClient } from '@walletconnect/sign-client';

// 1) Init WC client
const client = await SignClient.init({
  projectId: 'YOUR_PROJECT_ID',
  metadata: {
    name: 'My DApp',
    description: 'WalletConnect integration',
    url: 'https://example.com',
    icons: ['https://example.com/icon.png'],
  },
});

// 2) Request connection (EVM example)
const { uri, approval } = await client.connect({
  requiredNamespaces: {
    eip155: {
      methods: ['eth_sendTransaction', 'personal_sign'],
      chains: ['eip155:1'],
      events: ['chainChanged', 'accountsChanged'],
    },
  },
});

// 3) Open OneKey with preferred links
if (uri) {
  // Method 1: Deep Link (recommended)
  const deepLink = `onekey-wallet://wc?uri=${encodeURIComponent(uri)}`;

  // Method 2: Raw WalletConnect (recommended)
  const raw = uri; // e.g., open via window.open(raw) on mobile

  // Method 3: Universal Link (fallback)
  const universal = `https://app.onekey.so/wc/connect/wc?uri=${encodeURIComponent(uri)}`;

  // Choose based on your runtime (browser/native/TMA)
  window.open(deepLink, '_blank');
}

// 4) Wait for approval → session
const session = await approval();
console.log('Connected:', session);
```

> Mobile/TMA specific opening (Telegram Mini Apps / React Native) requires different link openers. See Mobile Deep Link Guide below.

## Deeplinks guide

For a complete, production‑oriented deeplink guide (mobile web, RN/Expo, TMA), see:

- Use deeplinks: guides/use-deeplinks.md
- Link types: custom scheme `onekey-wallet://`, raw WC `wc:...`, Universal Link fallback `https://app.onekey.so/...`

## Chain‑Specific Examples

- EVM (ETH): `using-walletconnect/eth.md`

## Best Practices

- Always encode WC URIs when used inside query strings: `encodeURIComponent(wcUri)`.
- Prefer Deep Link or raw WC, and keep Universal Link as a fallback.
- Keep URIs short; very long payloads can hit OS URL limits.
- Test on real devices. Simulators and dev mode can behave differently.

## Troubleshooting

- Deep link does not open OneKey:
  - Verify OneKey app is installed.
  - iOS: check Associated Domains; Android: check intent‑filters.
- Universal link stays in browser:
  - Associated domain or digital asset links may be misconfigured.
- WalletConnect handshake fails:
  - Verify `projectId`, network connectivity, and required namespaces.
