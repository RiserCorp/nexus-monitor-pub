<div align="center">

<img src="https://nexustradestudio.com/logo.png" alt="Nexus Trade" width="80" />

# Nexus Trade — Monitoring Tools

**Open-source MT5/MT4 Expert Advisors for the [Nexus Trade](https://nexustradestudio.com) platform.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-MetaTrader%205-blueviolet)](https://www.metatrader5.com)
[![Latest release](https://img.shields.io/github/v/release/RiserCorp/nexus-monitor-pub)](https://github.com/RiserCorp/nexus-monitor-pub/releases/latest)

</div>

---

## What is Nexus Trade?

[Nexus Trade](https://nexustradestudio.com) is a real-time monitoring platform for algorithmic traders running prop firm accounts. Connect your MT5 terminal, set your drawdown rules, and receive alerts before limits are hit — all from a single dashboard.

These monitoring tools are the bridge between your trading terminal and the platform. They collect account data and push it to Nexus Trade. **They never take any trading decisions.**

---

## Available tools

| Tool | Platform | Version | Description |
|------|----------|---------|-------------|
| [NexusMonitorMT5](mt5/NexusMonitorMT5.ex5) | MetaTrader 5 | v1.0.3 | Account monitoring EA for MT5 |
| NexusMonitorMT4 | MetaTrader 4 | coming soon | — |

---

## NexusMonitor MT5

### Requirements

- MetaTrader 5 (build 2755+)
- An active [Nexus Trade](https://nexustradestudio.com) account
- Your API key (generated from the dashboard)

---

### Installation

**1. Download the EA**

Download `NexusMonitorMT5.ex5` from the [latest release](https://github.com/RiserCorp/nexus-monitor-pub/releases/latest) or directly from the `mt5/` folder above.

**2. Place it in your MT5 Experts folder**

Copy the file to:
```
<MT5 data folder>\MQL5\Experts\Nexus\
```
You can find your MT5 data folder via **File → Open Data Folder** in MetaTrader 5.

**3. Refresh the Navigator**

In MetaTrader 5, right-click the **Expert Advisors** section in the Navigator panel and select **Refresh**. The EA will appear under `Nexus`.

**4. Whitelist the Nexus Trade URL**

Before the EA can make HTTP requests, the Sync Service URL must be allowed:

1. Go to **Tools → Options → Expert Advisors**
2. Check **"Allow WebRequest for listed URL"**
3. Add: `https://api.nexustradestudio.com`

**5. Attach the EA to a dedicated chart**

Drag the EA onto a **dedicated chart** (any symbol / any timeframe).  
Do not use a chart you actively trade on — a separate EURUSD M1 chart works perfectly.

**6. Enter your parameters**

| Parameter | Description |
|-----------|-------------|
| `InpApiKey` | Your API key — copy it from your [Nexus Trade dashboard](https://nexustradestudio.com/home/api-keys) |
| `InpServiceUrl` | Leave empty — defaults to `https://api.nexustradestudio.com` |

Enable **"Allow live trading"** and **"Allow DLL imports"** if prompted.

---

### Dashboard

Once connected, a status overlay appears on the chart:

| State | Meaning |
|-------|---------|
| `INITIALIZING` | EA is starting up and connecting |
| `CONNECTING` | Fetching config from Nexus Trade |
| `ACTIVE` | Monitoring is running normally |
| `WARNING` | An alert threshold has been crossed |
| `ERROR` | Initialization failed — see error code below |

---

### Error codes

| Code | Cause | Fix |
|------|-------|-----|
| 1 | API key not set | Enter your API key in the EA parameters |
| 2 | Network timeout / service unreachable | Check the URL whitelist and your internet connection |
| 3 | API key rejected (HTTP 401) | Regenerate your API key on nexustradestudio.com |
| 4 | Account not found (HTTP 404) | Create the account on nexustradestudio.com first |
| 5 | Monitoring disabled for this account | Enable monitoring in your dashboard |
| 6 | Platform mismatch | Verify the platform is set to MT5 on the account |
| 7 | Unexpected server response | Contact support |
| 8 | URL blocked by MT5 (error 4014) | Add the URL to MT5 allowed URLs (see step 4) |
| 9 | MT5 not connected to a broker | Log into a trading account in MT5 first |

---

### How it works

- The EA reads your account login and broker server **directly from the MT5 terminal** — you don't enter them manually.
- Account data is pushed to Nexus Trade every **30 seconds** (delta-only — only changes are sent).
- Trade events (open / close / modify) are pushed **immediately**.
- A **daily performance report** is sent once per day.
- On removal, the chart is fully restored to its original appearance.

---

## Frequently asked questions

**Do I need to leave MT5 running?**  
Yes. The EA pushes data while MT5 is running and connected. Monitoring pauses when MT5 is closed or disconnected.

**Can I attach it to a VPS?**  
Yes — this is the recommended setup for 24/7 monitoring.

**Does it affect my trading?**  
No. The EA is read-only. It never places, modifies, or closes any orders.

**Can I use it on multiple accounts?**  
Attach one instance of the EA per account, each on its own chart.

**Is the source code available?**  
The source code is maintained privately. The compiled `.ex5` binary is freely available here under the MIT license.

---

## Support

- Platform: [nexustradestudio.com](https://nexustradestudio.com)
- Documentation: [docs.nexustradestudio.com](https://nexustradestudio.com)
- Issues with this EA: [open an issue](https://github.com/RiserCorp/nexus-monitor-pub/issues)

---

## License

[MIT](LICENSE) — © 2026 [RiserCorp](https://github.com/RiserCorp)
