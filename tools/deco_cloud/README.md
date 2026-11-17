# Optional authenticated cloud companion

An outbound publisher reads the local bridge, rebuilds an export allowlist and posts over HTTPS. A Cloudflare Worker authenticates ingest; a SQLite Durable Object stores bounded telemetry. Authenticated viewers receive snapshots and WebSocket updates. No router-control API or inbound tunnel exists.

## Build locally

From this directory:

```sh
npm ci --ignore-scripts
npm test
npm run build
npm run check
```

The build includes selected RuView components retained in this repository and Three.js. Notices are served at /ruview/notices. Generated assets, types and build output are ignored.

## Configuration boundary

No deployed endpoint, credentials or household feed is published here. Deployment uses your own Cloudflare account and may incur provider charges. The retained Worker name is ruview-deco because the publisher allows only https://ruview-deco.<your-subdomain>.workers.dev. Renaming it requires a deliberate code/config review.

Provide secret bindings privately:

- PUBLISHER_HASH: SHA256 of a random 32-byte publisher token represented as 64 lowercase hex characters.
- VIEWERS: JSON array of {hash,role,expires}; hashes identify independently generated invitation tokens, roles are owner/viewer, and expiry is epoch milliseconds.

env.d.ts declares names only. Raw tokens stay outside Git. Missing bindings deny authenticated actions. Invitations are capabilities, not verified email identities. Login uses a Secure, HttpOnly, SameSite=Strict cookie capped by invitation expiry. Never put tokens in query strings.

Use an ignored .dev.vars with synthetic test credentials for local development. npm run dev binds loopback; the publisher needs explicit --local-test for local HTTP. No public live demo is provided.

## Publisher and data lifecycle

../deco_bridge/research_feed.py reads the local snapshot. install_publisher.py manages a separate owner-scoped LaunchAgent; inspect it before choosing to install/start. It requires private native config.json and cloud.private.json in the app's Application Support directory. The cloud file contains origin and publisher_token; optional ICMP probes need a privately verified gateway_mac. The deployment checker additionally uses a private owner_invitation.

The Mac must be awake, on the authorized network and running the native app. The publisher does not recover owner logins. Stop/uninstall it separately and revoke hashes when retiring cloud access.

The cloud retains latest telemetry and at most 180 RF samples in a 15-minute window. This is an application bound, not a guarantee about platform backups. Owner-authored floor plans persist separately; do not commit actual maps or name bindings.

The RF view uses owner-placed anchors and adjustable propagation assumptions. Coverage spheres are an uncalibrated schematic. Radio readings and reported attachment changes stay separate. Still/walking labels record actions; they do not validate a movement detector.

Source research records successful authenticated delivery. Extraction validation is offline only: no deployment, source installation access or new hardware trial is performed.
