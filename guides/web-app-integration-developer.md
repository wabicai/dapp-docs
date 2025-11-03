---
description: Integrate web dApps with OneKey using the Provider API, wallet aggregators, or WalletConnect
---

# Web App Integration Developer Guide

> Start with the minimal runnable snippet in Quick Start (detect → connect). This page focuses on options and references for production integration.

## Started

To develop for OneKey Browser Extension or Mobile Apps, install OneKey on your development machine.
- Download: https://onekey.so/download?client=browserExtension

This guide assumes intermediate knowledge of HTML, CSS, and JavaScript.

Once OneKey is installed and running, new browser tabs expose a `window.$onekey` object. Your website will interact with OneKey through this provider.

## Intro

As a dApp developer, you have the following options to connect to OneKey:

- OneKey Provider API (multi‑chain)
- Wallet aggregator GUIs/SDKs (RainbowKit, Web3Modal, Web3 Onboard, etc.)
- WalletConnect (QR / deep link, cross‑platform)

## OneKey Provider API

OneKey injects a provider into websites, allowing them to request blockchain operations via OneKey. For example, the Ethereum Provider API follows EIP‑1193.

- Entry: connect-to-software/webapp-connect-onekey/
- Examples: ETH (accounts, transactions, signing), SOL, NEAR, BTC, Nostr, WebLN

## Supported Clients

| Platform | Client | dApp Support |
|---|---|---|
| Browser | OneKey Chrome extension | Connect via injected Provider |
| Browser | OneKey Edge extension | Connect via injected Provider |
| Desktop | OneKey App (Windows/macOS/Linux) | Built‑in Browser integration |
| Mobile  | OneKey App (iOS/Android) | Built‑in Browser + WalletConnect |

## Use Wallet Aggregator GUIs and SDKs

Aggregators that support OneKey. If you already use an aggregator, see the docs for best practices.

- MetaMask compatibility: connect-to-software/compatible-with-metamask/
- Web3 Onboard: connect-to-software/support-wallet-kit/web3-onboard.md
- RainbowKit: connect-to-software/support-wallet-kit/rainbowkit.md
- Web3Modal: connect-to-software/support-wallet-kit/web3modal.md
- Aptos Wallet Adapter: connect-to-software/support-wallet-kit/aptos-wallet-adapter.md

## WalletConnect Integration

For cross‑platform connections, use WalletConnect. Users connect the OneKey app by scanning a QR code or using a mobile deep link.

- Entry: connect-to-software/using-walletconnect/README.md
- Mobile deep link: connect-to-software/using-walletconnect/mobile-deep-link.md
- EVM example: connect-to-software/using-walletconnect/eth.md
- Aptos example: connect-to-software/using-walletconnect/aptos/README.md

## Next Steps

- Minimal runnable example: quick-start.md
- Per‑chain APIs: see connect-to-software/webapp-connect-onekey/*
- Troubleshooting: provider detection, user rejection, hex encoding — see quick-start.md