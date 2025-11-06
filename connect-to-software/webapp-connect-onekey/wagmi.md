---
description: Connect to OneKey from React apps using wagmi and the injected EIP‑1193 provider (MetaMask‑style)
---

# React + wagmi

This guide follows MetaMask’s `connect/javascript-wagmi` style while reflecting OneKey’s reality: OneKey injects an EIP‑1193 provider. We’ll configure wagmi to prefer OneKey’s provider (`window.$onekey.ethereum`) and gracefully fall back to other injected providers when needed.

## Install

```bash
npm i wagmi viem
```

wagmi v2 uses viem under the hood. We’ll use the Injected connector.

## Create a OneKey‑first injected connector

Prefer OneKey’s dedicated injection to avoid ambiguity when multiple wallets are installed.

```ts
// onekeyConnector.ts
import { createConfig, http } from 'wagmi'
import { mainnet, polygon, arbitrum, base, optimism } from 'wagmi/chains'
import { injected } from 'wagmi/connectors'

function getOneKeyFirstProvider(): any {
  // Prefer OneKey’s dedicated injection
  const onekey = (window as any)?.$onekey?.ethereum
  if (onekey) return onekey

  // Fallback: try multi-provider list
  const list = (window as any)?.ethereum?.providers
  const okFromList = list?.find((p: any) => p?.isOneKey || p?.onekey)
  if (okFromList) return okFromList

  // Final fallback: single injected provider
  return (window as any)?.ethereum
}

export const config = createConfig({
  chains: [mainnet, polygon, arbitrum, base, optimism],
  connectors: [
    injected({
      target() {
        return {
          id: 'onekey',
          name: 'OneKey',
          provider: getOneKeyFirstProvider,
        }
      },
      shimDisconnect: true,
    }),
  ],
  transports: {
    [mainnet.id]: http(),
    [polygon.id]: http(),
    [arbitrum.id]: http(),
    [base.id]: http(),
    [optimism.id]: http(),
  },
})
```

Notes
- We intentionally prefer `window.$onekey.ethereum` so the dApp connects to OneKey even when multiple wallets are installed.
- If OneKey is not installed, the connector falls back to other injected providers.

## App setup

```tsx
// main.tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { WagmiProvider } from 'wagmi'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
import { config } from './onekeyConnector'
import App from './App'

const queryClient = new QueryClient()

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <WagmiProvider config={config}>
      <QueryClientProvider client={queryClient}>
        <App />
      </QueryClientProvider>
    </WagmiProvider>
  </React.StrictMode>,
)
```

## Connect and read account

```tsx
// App.tsx
import { useAccount, useConnect, useDisconnect } from 'wagmi'

export default function App() {
  const { address, isConnected } = useAccount()
  const { connect, connectors, isPending } = useConnect()
  const { disconnect } = useDisconnect()

  if (isConnected) {
    return (
      <div>
        <p>Connected: {address}</p>
        <button onClick={() => disconnect()}>Disconnect</button>
      </div>
    )
  }

  return (
    <div>
      {connectors.map((c) => (
        <button key={c.uid} disabled={isPending} onClick={() => connect({ connector: c })}>
          Connect with {c.name}
        </button>
      ))}
    </div>
  )
}
```

## Sign and send (examples)

```ts
import { createWalletClient, custom } from 'viem'

const provider = (window as any)?.$onekey?.ethereum
  || (window as any)?.ethereum?.providers?.find((p: any) => p?.isOneKey || p?.onekey)
  || (window as any)?.ethereum

const client = createWalletClient({ transport: custom(provider) })
const [account] = await provider.request({ method: 'eth_requestAccounts' })

// Personal sign
await provider.request({ method: 'personal_sign', params: ['0x68656c6c6f', account] })

// EIP-1559 tx
const txHash = await provider.request({
  method: 'eth_sendTransaction',
  params: [{ from: account, to: '0x...', value: '0x...' }],
})
```

## Events and network

- Listen to `accountsChanged` and `chainChanged`
- For network switching and adding chains, use `wallet_switchEthereumChain` and `wallet_addEthereumChain` (same as MetaMask)

## Mobile and deeplinks

- To bridge from mobile web or WebViews, use deeplinks carrying a WalletConnect URI
- Prefer `onekey-wallet://wc?uri={encodeURIComponent(wcUri)}`; fallback to the Universal Link
- See: Guides → Use deeplinks

## Troubleshooting

- 4001: user rejected
- 4902: chain not added (switch to `wallet_addEthereumChain`)
- Ensure hex strings are 0x‑prefixed; avoid passing raw BigInt in RPC params
