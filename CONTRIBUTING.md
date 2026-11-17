# Contributing

Open an issue describing the behavior, expected outcome and reproducible steps. Include platform and firmware versions when relevant; use synthetic payloads instead of household captures.

Run the Python and Node checks in the root README. For cloud/UI changes also run `npm ci --ignore-scripts`, `npm run build` and `npm run check` in `tools/deco_cloud`.

Keep measured, modeled, synthetic, stale and unknown states distinct. Do not broaden router endpoints, retry budgets, exported fields or network authority without documenting and testing the change. Hardware measurements need their own evidence; fixture tests cannot establish them.

Never attach credentials, session URLs, raw MAC/IP identifiers, private room maps or packet captures to public contributions. Report security issues privately as described in SECURITY.md.
