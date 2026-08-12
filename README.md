# Country Feedback Digest

A Cowork skill for Canva country managers. Pulls weekly user feedback from Enterpret and delivers it as a Slack summary, live artifact dashboard, Canva doc, and/or markdown file.

## Features
- SPIKE/WATCH/LOCAL/ELEVATED theme tagging
- Churn analysis inferred by locale/currency
- Incidents & rollout cross-referencing (auto-scans #rollouts-canva and #incident)
- Configurable peer country benchmarking (up to 10 markets)
- Market-relative spike floor calibrated on first run
- Operating plan tie-backs

## Installation

1. Download `country-feedback-digest-v6.skill`
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

## Support
Questions? Ask in #international-x-uv
