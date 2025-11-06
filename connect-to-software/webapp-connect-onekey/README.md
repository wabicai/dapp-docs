# JavaScript (EIP‑1193)

Connect to OneKey via the injected EIP‑1193 provider. This mirrors MetaMask’s JavaScript flow and requires no extra SDK in the browser.

## Detect provider

```js
// Prefer OneKey’s dedicated injection (avoid multi‑wallet conflicts)
const provider = window?.$onekey?.ethereum
  || window?.ethereum?.providers?.find(p => p?.isOneKey || p?.onekey)
  || window?.ethereum;
if (!provider) throw new Error('OneKey provider not detected');
```

## Request accounts

```js
const accounts = await provider.request({ method: 'eth_requestAccounts' });
const account = accounts?.[0];
```

## Events

```js
provider.on?.('accountsChanged', (accounts) => {
  // Handle account change
});
provider.on?.('chainChanged', (chainId) => {
  // Handle network change (recreate clients if needed)
});
```

## Send a transaction (EIP‑1559)

```js
const txHash = await provider.request({
  method: 'eth_sendTransaction',
  params: [{ from: account, to: '0x...', value: '0x...', /* optional: maxFeePerGas / maxPriorityFeePerGas */ }]
});
```

## Sign data

```js
// Personal sign (text)
await provider.request({ method: 'personal_sign', params: ['0x68656c6c6f', account] });

// EIP‑712 (Typed Data v4)
await provider.request({ method: 'eth_signTypedData_v4', params: [account, JSON.stringify(typedData)] });
```

## Errors and compatibility

- 4001: user rejected
- 4902: chain not added → use `wallet_addEthereumChain`
- Data formats: hex strings with 0x prefix; avoid raw BigInt in params

## Mobile deeplinks (brief)

- Custom scheme: `onekey-wallet://wc?uri={encodeURIComponent(wcUri)}`
- Universal link (fallback): `https://app.onekey.so/wc/connect/wc?uri={encodeURIComponent(wcUri)}`
- See Guides → Use deeplinks

## Per‑chain docs

- Ethereum / EVM → see `ETH` below
- Bitcoin → see `BTC` below
- NEAR → see `NEAR` below
- Solana → see `SOLANA` below
- Nostr → see `Nostr` below
- WebLN → see `WebLN` below
