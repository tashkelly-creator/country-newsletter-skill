# Country Feedback Digest

A Cowork skill for Canva country managers. Pulls weekly user feedback from Enterpret and delivers it as a Slack summary, live artifact dashboard, Canva doc, and/or markdown file.

## Features
- SPIKE/WATCH/LOCAL/ELEVATED theme tagging
- Churn analysis via unified locale field discovery (with currency as fallback)
- Incidents & rollout cross-referencing (auto-scans #rollouts-canva and #incident)
- Configurable peer country benchmarking (up to 10 markets)
- Market-relative spike floor calibrated on first run
- Operating plan tie-backs
- Per-record country attribution verification for quotes (prevents misattributed verbatims)
- Stable Canva doc archive links (uses permanent design ID, not expiring session URLs)

## Installation

1. Download `country-feedback-digest-v7.skill`
2. Open Cowork
3. Double-click the `.skill` file → click **Save skill**
4. Connect **Enterpret Wisdom** and **Slack** in Settings → Connectors
5. Type: `Set up my weekly feedback digest for [your country]`

## Trigger phrases
- "Set up my weekly feedback digest for [country]"
- "Send me the UK feedback summary"
- "Weekly Enterpret digest"

## Connectors required
- **Enterpret Wisdom** (required)
- **Slack** (required)
- **Canva** (optional — for Canva doc delivery)
- **Zoom Notes** (optional — for meeting transcript context)

## Version history
- **v7** (current) — Fixes a quote misattribution bug by requiring per-record country verification before any verbatim is labelled with a country; switches churn analysis to unified locale field discovery instead of the old per-source probe; fixes Canva doc archive links to use the stable `canva.com/design/[ID]` permalink instead of expiring session URLs; drops the redundant Enterpret dashboard link from the Slack summary (still available via the artifact/doc).
- **v6** — see `country-feedback-digest-v6/`

## Support
Questions? Ask in #international-x-uv
