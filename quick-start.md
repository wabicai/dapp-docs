# Quick Start

This page gives you a minimal, production‑friendly path to get OneKey working in your web dApp. Keep it simple: install → detect → connect → first call, then follow the per‑chain guides.

## 1) Prerequisites

- Install OneKey Browser Extension or Mobile App.
- Open DevTools and confirm `window.$onekey` exists on your site.
- This guide assumes basic HTML/CSS/JS knowledge.

## 2) Pick your route

- OneKey Provider (EIP‑1193): multi‑chain provider for web dApps — see [OneKey Provider](connect-to-software/webapp-connect-onekey/README.md)
- Wallet Kit: RainbowKit / Web3Modal / Web3 Onboard — see [Wallet Kit](connect-to-software/wallet-kit/README.md)
- WalletConnect: cross‑platform deep link / QR — see [WalletConnect](connect-to-software/using-walletconnect/README.md)
- MetaMask Compatibility: rely on `window.ethereum` — see [MetaMask Compatibility](connect-to-software/compatible-with-metamask/README.md)

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

- EVM: [Ethereum & EVM](connect-to-software/webapp-connect-onekey/eth/README.md)
  - [Provider API](connect-to-software/webapp-connect-onekey/eth/provider-api.md), [RPC API](connect-to-software/webapp-connect-onekey/eth/rpc-api.md), [Accessing Accounts](connect-to-software/webapp-connect-onekey/eth/accessing-accounts.md), [Sending Transactions](connect-to-software/webapp-connect-onekey/eth/sending-transactions.md), [Signing Data](connect-to-software/webapp-connect-onekey/eth/signing-data.md)
- Bitcoin: [Bitcoin](connect-to-software/webapp-connect-onekey/btc/README.md)
- NEAR: [NEAR](connect-to-software/webapp-connect-onekey/near/README.md)
- Solana: [Solana](connect-to-software/webapp-connect-onekey/solana/README.md)
- Nostr: [Nostr](connect-to-software/webapp-connect-onekey/nostr/README.md)
- WebLN: [WebLN](connect-to-software/webapp-connect-onekey/webln/README.md)

## 5) Troubleshooting (quick)

- Not detected: ensure OneKey installed; retry after `DOMContentLoaded`.
- Rejected: user canceled; catch error and prompt retry.
- Hex errors: numeric fields must be 0x‑prefixed hex strings.

That’s it. Reach the full “Web App Integration” tutorial when you need end‑to‑end best practices.
