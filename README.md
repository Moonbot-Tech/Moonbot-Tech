<p align="center">
  <a href="https://moonbot.pro">
    <img src="https://raw.githubusercontent.com/Moonbot-Tech/Moonbot-Tech/main/assets/moonbot-logo-full.svg" alt="Moonbot" width="199">
  </a>
</p>

<h1 align="center">Moonbot</h1>

<p align="center">
  <b>Professional desktop terminal for cryptocurrency scalping</b><br>
  Manual and algorithmic trading in one workstation — built and refined since 2017
</p>

<p align="center">
  <a href="https://moonbot.pro"><img src="https://img.shields.io/badge/website-moonbot.pro-4C6EF5" alt="Website"></a>
  <img src="https://img.shields.io/badge/since-2017-6B7280" alt="Since 2017">
  <a href="https://t.me/MoonbotNews"><img src="https://img.shields.io/badge/Telegram-MoonbotNews-26A5E4?logo=telegram&logoColor=white" alt="Telegram"></a>
</p>

<p align="center">
  <a href="#what-moonbot-is">What Moonbot is</a> ·
  <a href="#repositories">Repositories</a> ·
  <a href="#architecture">Architecture</a> ·
  <a href="#supported-exchanges">Exchanges</a> ·
  <a href="#links">Links</a>
</p>

---

## What Moonbot Is

Moonbot is a professional trading terminal for cryptocurrency scalping, in continuous development since 2017. It is a desktop workstation for traders who work with market microstructure: tick-by-tick price data, graphical order book depth, liquidation levels, and sub-second order execution.

The terminal combines **manual and algorithmic trading** in a single application — over 20 built-in strategies with 300+ configurable parameters, a trigger system where one strategy can activate another, a backtesting module, and an emulator for risk-free strategy development.

Moonbot is architecturally split: an execution **core** can run on a VPS close to the exchange, while the control interface stays on the trader's machine. The two communicate over a custom UDP protocol — **MoonProto** — which is what most of the code in this organization implements.

**What this is not:** Moonbot is not a cloud service, not a mobile app, and not a signal bot. It does not hold funds and does not store API keys on any third-party infrastructure — the terminal connects to exchanges through the trader's own API keys, and all data and settings stay on the trader's machine or server.

## Repositories

| Repository | What it is | Language |
|---|---|---|
| [**MoonTerminal**](https://github.com/Moonbot-Tech/MoonTerminal) | Development repository for the Moonbot cross-platform terminal | Rust |
| [**MoonProto**](https://github.com/Moonbot-Tech/MoonProto) | Client-side runtime SDK for building MoonBot-compatible terminals, dashboards, and control tools over a running MoonBot core | Rust |
| [**MoonUI**](https://github.com/Moonbot-Tech/MoonUI) | User interface layer for MoonTerminal | Rust |
| [**TradesLag**](https://github.com/Moonbot-Tech/TradesLag) | Measurement tool for trade stream latency across exchanges | Rust |

## Architecture

```
   Exchange APIs                MoonBot Core                Client
  ─────────────────           ────────────────           ────────────
  Binance · Bybit             orders, strategies         MoonTerminal
  HTX · Gate · Bitget   <──>  risk logic, balances  <──> or any tool
  Hyperliquid                 authoritative state         built on
  spot · futures              (runs on VPS or local)      MoonProto
                                                    │
                                              MoonProto
                                            UDP transport
```

The core is the execution engine — it owns exchange connections, orders, strategies, risk logic, and authoritative trading state. **MoonProto** is the client-side bridge to that core: transport, authorization, reconnect, subscriptions, retained state, events, and typed user intents. Applications built on MoonProto handle UI and product logic; they never talk to exchanges directly.

This separation is what allows the execution engine to sit in a datacenter next to the exchange while the trader works from anywhere — and to keep managing an open position if the client connection drops.

## Supported Exchanges

**Centralized:** Binance · Bybit · HTX · Gate · Bitget — spot and futures
**Decentralized:** Hyperliquid — including tokenized assets via HIP-3

New exchanges and markets are added regularly.

## Links

- **Website** — [moonbot.pro](https://moonbot.pro)
- **Documentation** — [moonbot.pro/documentation](https://moonbot.pro/documentation)
- **Trading statistics** — [stat.moonbot.pro](https://stat.moonbot.pro)
- **Telegram** — [@MoonbotNews](https://t.me/MoonbotNews)

---

<p align="center">
  <strong>Moonbot</strong> · Advanced terminal for cryptocurrency trading · <a href="https://moonbot.pro">moonbot.pro</a>
</p>
