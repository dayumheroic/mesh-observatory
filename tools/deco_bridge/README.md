# Stock Deco collector

Owner-authorized stock-firmware telemetry research. See the root [README](../../README.md) for evidence limits and [THIRD-PARTY-NOTICES](THIRD-PARTY-NOTICES) for protocol attribution.

## Offline setup

From the repository root:

```sh
python3 -m venv .venv
.venv/bin/python -m pip install --only-binary=:all: -r tools/deco_bridge/requirements.txt
.venv/bin/python -m unittest discover -s tools/deco_bridge -v
.venv/bin/python tools/deco_bridge/deco_bridge.py replay --input tools/deco_bridge/synthetic.json
```

Replay is synthetic. For native installation see [APP.md](APP.md).

## Live collection

Use the main Deco's LAN address from its device-information screen. Only an explicit RFC1918 IPv4 target is accepted. Independently verify the router's leaf-certificate SHA256 fingerprint through an already trusted local connection. An unauthenticated initial fetch does not establish trust; do not silently change pins after a mismatch.

```sh
.venv/bin/python tools/deco_bridge/deco_bridge.py probe --host "$DECO_LAN_IP" --pin "$PIN"
.venv/bin/python tools/deco_bridge/deco_bridge.py capture --host "$DECO_LAN_IP" --pin "$PIN" --output "$HOME/Deco-private-capture"
```

The owner password is entered locally with getpass. One login attempt is allowed per process; no browser credentials are read. The CLI reads devices, clients, performance and mode. Optional extended forms have uncertain exact-firmware support; an error can stop a batch with partial evidence.

Private captures must remain outside Git with owner-only permissions. Raw files can contain identifiers even after key-name redaction. Aliased exports still reveal timing/activity. Do not attach either to public issues.

Legacy AES-CBC/MD5/RSA compatibility sits inside same-socket certificate-pinned HTTPS. No arbitrary endpoint proxy, sweep, router write or firmware upload is exposed.

## Mac current-link radio

```sh
swiftc tools/deco_bridge/mac_radio.swift -o /private/tmp/mesh-mac-radio
/private/tmp/mesh-mac-radio --samples 10 --interval 1
```

Public CoreWLAN APIs provide RSSI/noise/channel/rate for one associated Mac link. No SSID/BSSID, raw CSI or room localization is produced. This is live hardware collection; offline tests do not invoke it.
