# Provenance and extraction boundary

Extracted on 2026-11-17 from:

- Repository: https://github.com/dayumheroic/RuView_DayumHeroic
- Branch: `codex/deco-stock-telemetry-research`
- Commit: `4f412518d3bbf478b76aa4c2661d4a19db423dde`
- Upstream RuView: https://github.com/ruvnet/RuView

The extraction includes `tools/deco_bridge`, `tools/deco_cloud`, the local mesh page, the bridge sensing mapper and the transitive RuView UI dependencies needed to build the optional cloud view. The original directory layout and internal schema names are retained to avoid an unrelated behavior rewrite. Existing `ruview.*` names indicate compatibility/provenance, not ownership of upstream RuView.

The full Rust sensing server, firmware, pretrained models and unrelated upstream project are excluded. Internal playbooks, handoffs, PR transcripts, private floor-plan data, deployment configuration and hardware captures are excluded. Public documentation here is rewritten around the extracted scope.

## Ownership boundaries

- Sean Steinhoff: research direction and AI-assisted development of the stock Deco integration, local bridge, companion workflows and verification criteria. See the source branch history for the development record.
- RuView / rUv and upstream contributors: retained UI shell, styles, sensing renderer, supporting services and pose renderer. Those components are reused under the source MIT license. This project does not claim upstream sensing capabilities.
- Rodrigo Roque: protocol implementation reference `roquerodrigo/tplink-deco-api`, pinned in the collector notice. Retain its copyright and license.
- Three.js: installed through npm, with its notice included by the cloud UI build.

New public packaging, README artwork and extraction documentation were prepared with AI assistance under Sean's direction. This repository starts with an extraction commit; it does not import upstream commit history as Sean's work.

## Hardware evidence

The source branch records measured hardware and delivery results in its research playbooks. Those are historical source records, not fresh measurements made by this extraction. Private raw evidence is intentionally not republished. Firmware-specific semantics and inference limits remain explicit in the root README.
