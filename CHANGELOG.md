# Changelog

All notable changes to Nexus Trade monitoring tools are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).  
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [1.0.3] — 2026-03-17

### NexusMonitor MT5 — Initial public release

First publicly distributed build of the MT5 monitoring Expert Advisor.

#### Features
- Real-time account monitoring — equity, balance, drawdown, open positions
- Push-only HTTPS communication to the Nexus Trade Sync Service
- Account snapshots every 30 seconds (delta-only — only changes are sent)
- Immediate push on trade open / close / modify events
- Daily performance report (once per trading day)
- Visual status dashboard overlay on the chart (INITIALIZING → CONNECTING → ACTIVE)
- Alert threshold state machine (WARNING state when limits are approached)
- Automatic account identification — login and broker server read directly from MT5
- Error state with detailed error codes (1–9) displayed on the dashboard
- Full chart restoration on EA removal
- No trading logic — read-only monitoring only

#### Technical
- Platform: MetaTrader 5 (build 2755+)
- Authentication: `X-API-Key` header
- Default endpoint: `https://api.nexustradestudio.com`
- Snapshot interval: 30 seconds
