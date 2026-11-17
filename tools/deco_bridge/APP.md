# Native Mac application: research preview

Requires macOS, Swift and Python 3.11+. Follow [collector setup and certificate trust](README.md) first. From the repository root:

```sh
.venv/bin/python tools/deco_bridge/install_macos.py --host "$DECO_LAN_IP" --pin "$PIN"
open "$HOME/Applications/RuView Deco Bridge.app"
```

The installer builds an unsigned app for the current architecture and creates a private isolated runtime under ~/Library/Application Support/RuViewDecoBridge. It refuses to overwrite an existing app or silently change trust configuration. It is not signed/notarized or a portable distribution.

Existing RuView names are retained for compatibility. The native window uses the included mesh page through 127.0.0.1:8766 and supplies its random private bridge key in a header. Credentials stay in process memory; Python/JavaScript cannot guarantee secure memory erasure. No owner password is saved.

Compare the pin with the trusted router certificate before signing in. The dashboard reads device/client forms; Reconnect is explicit and cooldown-limited. Pause stops future reads, although an in-flight request may finish.

## API

| Route | Purpose |
|---|---|
| GET /v1/snapshot | Separate source-timestamped radio and mesh data. Unknown lists remain null. |
| POST /v1/deco/connect | Explicit password and pin-confirmation action. |
| POST /v1/deco/pause | Stop subsequent collection and clear active mesh data. |
| POST /v1/deco/reset | Bounded local recovery, without automatic owner login. |

All routes require the private bridge key. Host/Origin validation, fixed static assets and loopback binding constrain the service. An optional explicit --ruview-origin grants another local UI origin access; the native app does not need it.

RF and mesh have different polling/freshness rules. Stale records stay labeled; missing values never become fabricated zeros. See [implementation](bridge_service.py) and [boundary tests](test_bridge_service.py).

## Lifecycle and limits

Quit the native app to stop its service. The cloud publisher has a separate lifecycle. To uninstall, quit, remove the app and optionally its private Application Support folder. Historical captures elsewhere are separate.

Sleep/wake, Apple Silicon hardware acceptance, signing, full resource budgets and clean-profile uninstall remain open. Historical source research records Intel Mac radio and protected mesh collection; this extraction does not remeasure hardware.
