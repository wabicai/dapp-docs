# Quick Start

This page gives you a minimal, production‑friendly path to get OneKey working in your web dApp. Keep it simple: install → detect → connect → first call, then follow the per‑chain guides.

## 1) Prerequisites

- Install OneKey Browser Extension or Mobile App.
- Open DevTools and confirm `window.$onekey` exists on your site.
- This guide assumes basic HTML/CSS/JS knowledge.

## 2) Pick your route

- OneKey Provider (EIP‑1193): multi‑chain provider for web dApps — see `connect-to-software/webapp-connect-onekey/`
- Wallet Aggregators: RainbowKit / Web3Modal / Web3 Onboard — see `connect-to-software/support-wallet-kit/`
- WalletConnect: cross‑platform deep link / QR — see `connect-to-software/using-walletconnect/`
- MetaMask Compatibility: rely on `window.ethereum` — see `connect-to-software/compatible-with-metamask/`

## 3) Minimal example (EVM)

```html
<script>
(async () => {
  const provider = window?.$onekey?.ethereum
    || window?.ethereum?.providers?.find(p => p?.isOneKey || p?.onekey)
    || window?.ethereum;
  if (!provider) {
    console.warn('OneKey not detected. Install the extension and reload.');
    return;
  }
  const [account] = await provider.request({ method: 'eth_requestAccounts' });
  console.log('Account:', account);
  // Optional first tx (0.001 ETH). Use your own recipient and value.
  // const txHash = await provider.request({
  //   method: 'eth_sendTransaction',
  //   params: [{ from: account, to: '0x0000000000000000000000000000000000000001', value: '0x38d7ea4c68000' }]
  // });
  // console.log('Tx:', txHash);
})();
</script>
```

## 4) Go deeper (per‑chain)

- EVM: `connect-to-software/webapp-connect-onekey/eth/`
  - Provider API, RPC API, Accounts, Send Tx, Sign Data
- Bitcoin: `connect-to-software/webapp-connect-onekey/btc/`
- NEAR: `connect-to-software/webapp-connect-onekey/near/`
- Solana: `connect-to-software/webapp-connect-onekey/solana/`
- Nostr: `connect-to-software/webapp-connect-onekey/nostr/`
- WebLN: `connect-to-software/webapp-connect-onekey/webln/`

## 5) Troubleshooting (quick)

- Not detected: ensure OneKey installed; retry after `DOMContentLoaded`.
- Rejected: user canceled; catch error and prompt retry.
- Hex errors: numeric fields must be 0x‑prefixed hex strings.

That’s it. Reach the full “Web App Integration” tutorial when you need end‑to‑end best practices.
