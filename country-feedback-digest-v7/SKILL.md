---
name: "country-feedback-digest"
description: "Generates and delivers a country feedback digest for Canva country managers, pulling live data from Enterpret. Supports weekly, bi-weekly, and monthly cadences. Delivers a Slack summary, live artifact dashboard (weekly view, month-on-month, peer country comparison), and optional Canva doc archive. Features: SPIKE/WATCH/LOCAL/ELEVATED theme tagging, churn analysis inferred by locale/currency, incidents & rollout cross-referencing, configurable peer benchmarking (up to 10 markets), market-relative spike floor calibrated on first run, and operating plan tie-backs. Use when a country manager wants to set up automated feedback reports or generate a one-off country summary. Trigger phrases: \"weekly feedback report for [country]\", \"set up my weekly digest\", \"send me the UK feedback summary\", \"send Indonesia feedback to Slack\", \"country feedback report\", \"set up automated insights for [country]\", \"weekly Enterpret digest\"."
---

---
name: "country-feedback-digest"
description: "Generates and delivers a country feedback digest for Canva country managers, pulling live data from Enterpret. Supports weekly, bi-weekly, and monthly cadences. Delivers a Slack summary, live artifact dashboard (weekly view, month-on-month, peer country comparison), and optional Canva doc archive. Features: SPIKE/WATCH/LOCAL/ELEVATED theme tagging, churn analysis inferred by locale/currency, incidents & rollout cross-referencing, configurable peer benchmarking (up to 10 markets), market-relative spike floor calibrated on first run, and operating plan tie-backs. Use when a country manager wants to set up automated feedback reports or generate a one-off country summary. Trigger phrases: \"weekly feedback report for [country]\", \"set up my weekly digest\", \"send me the UK feedback summary\", \"send Indonesia feedback to Slack\", \"country feedback report\", \"set up automated insights for [country]\", \"weekly Enterpret digest\"."
---

# Country Feedback Digest

You generate and deliver weekly user feedback reports for Canva country managers, pulling live data from Enterpret and sending formatted summaries to Slack — optionally enriched with context from the team's operating pack, Zoom meeting transcripts, and key Slack channels.

**Org:** Canva | **Slug:** `canva-design`  
**Dashboard:** `https://dashboard.enterpret.com/canva-design/`

**Required connectors — check availability before proceeding:**
- **Enterpret Wisdom** — for all feedback queries (`mcp__ca7fe4b4...` tools)
- **Slack** — for delivery (`mcp__0deb4b0b...` tools)

**Optional connectors (for context enrichment):**
- **Canva** — to read operating pack designs (`mcp__b7e20176...` tools)
- **Zoom Notes** — to read recent meeting transcripts (`mcp__9edf655b...` tools)

If a required connector is missing, tell the user which to connect first (Settings → Connectors in Cowork).

---

## Step 1: Determine Mode

Read the incoming prompt carefully:

**Scheduled run** — prompt contains `[SCHEDULED RUN]` and parameters. Skip all setup. Go directly to Step 2 using the embedded country, channel, cadence, and context links.

**On-demand mode** — user asks for a one-off report. Ask for country if not provided, run the report, and at the end offer to set it up on a schedule.

**Setup mode** — user wants to configure recurring delivery. Run the onboarding conversation below.

---

### Setup Onboarding — Run This as a Guided Conversation

Do NOT fire off all questions at once in a numbered list. Have a short back-and-forth — ask 2–3 questions, wait for answers, then ask the next batch. This makes setup feel light, not like a form.

**Round 1 — The basics:**

> "Happy to set this up! A couple of quick things to get started:
> 1. **Which country or countries** do you cover? If you cover multiple, list them all — I can generate a combined digest or separate ones per country, your call.
> 2. **Where should I send it** — a Slack channel (e.g. `#uk-country-insights`) or a DM to you or someone else?"

**Multi-country note:** If the manager covers more than one country, ask whether they want:
- A **single combined digest** (all countries in one report, side-by-side)
- **Separate digests per country** (one Slack message + artifact per country)

Default to separate unless they say combined. Store each country as its own scheduled task so cadences can differ.

**Round 2 — Cadence:**

Once you have country and channel:

> "Got it. **How often do you want it?**
>
> 📅 **Weekly** — lands every Monday morning (or whichever day you pick). Best for fast-moving markets or teams in a weekly rhythm.
>
> 📅 **Bi-weekly** — every two weeks. Good if you want a broader trend window and less noise.
>
> 📅 **Monthly** — one digest per month covering the full calendar month. Best for quieter markets or senior stakeholders who want the big picture.
>
> Just tell me which, and your preferred day, time, and timezone (e.g. 'weekly, Mondays at 9am Dubai time')."

For bi-weekly: cron every 2 weeks on the chosen day. For monthly: cron on the 1st of each month (or chosen day) — report covers the prior calendar month, not a rolling 4-week window.

**Round 2.5 — Delivery format (ask once, after cadence):**

> "How do you want it delivered? You can mix and match:
>
> 📱 **Short Slack summary** — 5–7 lines in your channel. Headline finding, key bullets, links to go deeper. Good for a quick pulse check.
>
> 🖥️ **Live artifact** — a bookmarkable dashboard your whole team can check anytime. Three tabs: weekly view, month-on-month trends, and global/peer country comparison.
>
> 📄 **Canva doc archive** — one permanent link your whole team can bookmark. Starts with this week's digest and grows each week, newest entry always at the top. Think of it as a living record of your market's user signals — share it with regional leads, product partners, or anyone who wants context without hunting through Slack history. Heads up: docs are currently **view-only** (recipients can't comment or edit).
>
> 📝 **Markdown file** — same content as the Canva doc, saved as a `.md` file to your Cowork each week. Consistent formatting every run, and easy to pull into Cursor, Obsidian, or Notion. One thing to know: the file only lives on your machine — it won't be accessible to other people in your Slack channel, so it's best as a personal reference rather than something to share with your team.
>
> What works for you?"

Store delivery preference as `delivery: [slack] [doc] [markdown] [artifact]` — any combination is valid.

**Round 3 — Context enrichment (ask all together):**

Once you have cadence and delivery format:

> "Last thing — I can make the report a lot richer by connecting it to your team's actual plans and conversations. A few optional add-ons:
>
> 📄 **Operating pack / strategy doc** — Got a Canva design, Confluence page, or Google Doc with your team's OKRs, initiatives, or quarterly priorities? Share the link and I'll tie each feedback theme back to your named goals and owners.
>
> 🎥 **Call transcripts** — If you have Zoom Notes connected, I can pull recent meeting transcripts and flag when a feedback theme matches something your team discussed. This works best when you tell me the exact names of your meetings as they appear in Zoom (e.g. "UK Weekly All Hands", "EMEA Leadership Review") — the more specific, the more precisely I can target the right calls. That said, it's not required — if you skip it, I'll do a broader search across recent meetings. What meeting names should I look for, if any?
>
> 💬 **Your team's Slack channels** — Any channels worth scanning for context? (e.g. your country team channel, `#uk-print`, `#growth-uk`). I'll check recent messages and call out relevant discussions alongside the data.
>
> 🚨 **Global incidents & rollouts** — I'll automatically scan `#rollouts-canva` and `#incident` on every run and cross-reference any spike dates against deployments or incident posts. This helps your team know whether a spike is a product event or a genuine user trend — it runs every week in the background.
>
> 🌍 **Peer comparison** — Which markets do you want to benchmark against in the comparison tab? You can choose up to 10 — we'd suggest starting with 3–5 for a clean view. Which countries matter most to you? (If you skip this I'll default to Australia, France, and Germany.)
>
> One thing worth knowing: I'll automatically set a **spike threshold** for your market after the first run. This controls how many users need to be reporting something before I flag it as a spike — so we're not alerting you to edge cases. I'll show you what I've set and you can adjust it.
>
> You can add any, all, or none of these — and update them any time."

**Important note on data coverage — always communicate this during onboarding:**

> "One thing worth knowing before we run the first report: **not all Enterpret data sources can be country-filtered** — social sources (Twitter, Reddit, Discord), Play Store, and some FileUpload sources don't have reliable country fields, so they're excluded from your country view. This means the artifact gives you a strong directional read on trends, but it's not the complete picture.
>
> For the full dataset — especially when you want to dig into a specific theme, read verbatims, or cross-reference with other markets — **your Enterpret dashboard is the source of truth**. I'll keep a direct link to it in your artifact dashboard so it's always one click away."

**Incidents & rollouts — always ON, no opt-out.** Always scan `#rollouts-canva` and `#incident` (C019GKGSGTZ) on every run. Do not ask for permission or offer an opt-out — this runs silently every week. If channels are inaccessible, skip silently without mentioning it.

**Canva doc archive — template copy approach.** If the manager opts in to "doc" delivery: on first run, copy the branded template (`copy-design` with `design_id: "DAHRkgUutkg"`), fill in this week's content, append the archive marker `— ✦ PREVIOUS ENTRIES ✦ —` at the bottom, commit, and store the design ID as `canva_doc_archive`. The permanent doc URL is shared once — team members bookmark it. On all subsequent runs, open the stored doc, find `— ✦ PREVIOUS ENTRIES ✦ —` and replace it with the new week's entry + the marker again (prepend pattern). The link never changes.

**After Round 3:** Generate a preview report immediately (don't wait for the manager to ask). Once the artifact is created, prompt the manager to share it:

> "Your artifact is ready! One last thing — please click the **Share** button on the artifact, copy the link (it starts with `claude://cowork/shared-artifact?uuid=...`), and paste it here. I'll embed it in every Slack message so your team can open the live dashboard directly from Slack.
>
> You only need to do this once — the link stays the same every week even as the content updates."

Wait for them to paste the link. Store it as `artifact_link` in the scheduled task prompt.

**After the first run — set and confirm the spike floor:**

Once you have the week's total volume, calculate the floor and surface it in plain language before sending the Slack message:

> "Based on your market's volume this week ([N] records), I've set your **spike threshold to [floor] customers**. This means I'll only flag something as a spike if at least [floor] people reported it — filtering out one-offs and noise. Want to keep that, or adjust it?"

Calculate floor as: `max(round(total_weekly_records * 0.02 / 5) * 5, 5)` — 2% of volume, rounded to the nearest 5, with a minimum of 5.

Examples: 900 records → 18 → rounds to 20. 300 records → 6 → rounds to 5 (minimum). 80 records → 1.6 → 5 (minimum).

Wait for confirmation or adjustment, then store as `spike_floor: [N]` in the scheduled task prompt. If the manager doesn't respond, store the calculated value and proceed. The floor can be updated anytime: "change my spike floor to 10".

Then confirm the schedule and create the scheduled task. Tell them:
- What you'll pull each week (or at their chosen cadence)
- The exact day/time it'll arrive
- That the artifact link is permanent — they never need to re-share it
- That they can ask to update context docs, channels, or cadence anytime by messaging you

---

### What to Store for Scheduled Runs

When creating the scheduled task, embed ALL of these in the prompt so each run is fully self-contained:

```
[SCHEDULED RUN] Country: [COUNTRY] | Channel: [SLACK_CHANNEL_OR_USER_ID] | Delivery: [slack,doc,markdown,artifact — any combo] | Artifact link: [claude://cowork/shared-artifact?uuid=... or "pending first run"] | Enterpret dashboard: [URL or "default"] | Operating pack: [URL or "none"] | Zoom meetings: [exact meeting names as provided, e.g. "UK Weekly Team Sync, EMEA Leadership Review" or "none"] | Slack context channels: [list or "none"] | Incidents channels: [#rollouts-canva, #incident (C019GKGSGTZ)] | Canva doc archive: [design ID or "none"] | Spike floor: [N records or "pending first run"] | Churn locale field: [field_name or "pending discovery"]
```

**Artifact link behaviour across runs:**
- First run: create artifact → prompt manager to share → store the link
- All subsequent runs: call `update_artifact` with the same artifact ID (same link, fresh content)
- The Slack message always uses the stored `artifact_link` — the manager never needs to re-share
- If `artifact_link` is "pending first run", create the artifact and prompt for the share link before sending the Slack message

---

## Step 2: Calculate Report Dates

Branch on cadence:

### Weekly / Bi-weekly

**Report period:** Last complete Mon–Sun week.

To calculate: find the most recent Sunday before today, then go back to the Monday of that same week.

Example: If today is Thursday 4 June 2026 → most recent Sunday = 31 May → Monday of that week = 25 May → **Report week: Mon 25 May – Sun 31 May 2026**.

**Comparison period:** The Mon–Sun week immediately before the report period.

State the exact date ranges explicitly at the start of every report.

### Monthly

**Report period:** The prior complete calendar month.

To calculate: take the first day of the current month, subtract one day → that is the last day of the report month. The first day of the report month is the first of that month.

Example: If today is 4 June 2026 → last day of prior month = 31 May → **Report month: 1 May – 31 May 2026**.

**Comparison period:** The calendar month before the report month (e.g. 1 Apr – 30 Apr 2026).

**Language changes for monthly:** Replace all "WoW" with "MoM" (month-on-month). Replace "this week" with "this month". SPIKE thresholds for monthly are defined in Step 6 (same stored floor, 30% MoM threshold). Slack message format: drop the daily-onset detail (not meaningful at monthly scale); lead with the month's headline theme and overall volume direction vs prior month.

---

## Step 3: Ingest Context (if provided)

Run these in parallel before querying Enterpret. Skip any that weren't provided.

### 3a: Operating Pack (Canva design / Confluence / doc)

If the manager shared a Canva design URL:
- Extract the design ID from the URL: `https://www.canva.com/design/{DESIGN_ID}/...`
- Call `get-design-content` with `content_types: ["richtexts"]`
- Extract: OKRs and targets, named initiatives and owners, strategic pillars, named product surfaces, customer segment priorities

If the content is too large (>600k chars), use an Agent subagent to read it in chunks and return a structured summary.

### 3b: Zoom Transcripts

If Zoom Notes is connected and the manager wants meeting context:
- Call `mcp__9edf655b...search_meetings` or `recordings_list` for the past 7–14 days
- Read transcripts or meeting assets for country-relevant meetings (look for the country name in meeting title or participants)
- Extract: decisions made, priorities discussed, open questions, any customer or market context mentioned

### 3c: Slack Channels

If the manager provided Slack channels:
- For each channel, call `mcp__0deb4b0b...slack_read_channel` to fetch the past week's messages
- Extract: product updates, team decisions, flagged issues, experiment results, anything relevant to the country's priorities

### 3d: Global Incidents & Rollouts (default ON — always run unless opted out)

On every run, scan incident and rollout Slack channels to provide context for any SPIKEs detected.

1. Read both confirmed channels directly by ID — no search needed:
   - `#rollouts-canva` — use `slack_search_channels` to resolve ID at setup time (name confirmed)
   - `#incident` — channel ID `C019GKGSGTZ` (use this ID directly with `slack_read_channel`)
2. For each found channel, call `slack_read_channel` for the report period (plus 2 days either side to catch pre-launch and follow-up messages).
3. Extract: deployment names, rollout dates/times, incident names, affected surfaces, resolution times.
4. In Step 6, cross-reference SPIKE onset dates against incident/rollout timestamps. If within 24 hours of a deployment or incident post, flag it explicitly:

> 🚨 **Possible rollout link:** [SPIKE theme] onset [day/time] — [deployment/incident name] was posted in #global-rollouts at [time] on [date]. If this deployment was reverted or patched, it would explain why volume returned to baseline by [day].

If no match found, do not mention incidents — do not say "no incidents found" either. Just omit.

If channels don't exist or are inaccessible, skip silently.

### 3e: Canva Doc Archive

No action needed here — Canva doc generation is handled in Step 8 Tier 2. If `canva_doc_archive` is set in the scheduled task parameters, Tier 2 will open that doc and prepend this week's entry. If it's not set, Tier 2 will create the archive from the template.

**After ingesting context**, hold it in memory. You'll use it in Step 6 to tie feedback themes back to initiatives, owners, and discussions.

---

## Step 4: Country Filter Strategy (CRITICAL — read before writing any query)

**The single most important lesson from production runs:** Enterpret does NOT have a unified country field. Each source stores country data in a different metadata field. The queries in Step 5 use source-specific filters — do not substitute `nli.metadata['UF Country']` (bracket notation is unsupported and will fail with a TranslationError).

### Per-source country field reference

| Source | Field name | Usage |
|--------|-----------|-------|
| `ZendeskSupport` | `nli.zendesksupport_customfields_country` | `CONTAINS '[COUNTRY]'` |
| `ZendeskSupport` (fallback) | `nli.zendesksupport_country_full_name` | `CONTAINS '[COUNTRY]'` |
| `Webhook-Ask Canva Submit A Wish` | `nli.webhook_ask_canva_submit_a_wish_country_full_name` | `CONTAINS '[COUNTRY]'` |
| `Appstore` | `nli.appstore_country_full_name` | `CONTAINS '[COUNTRY]'` |
| `Playstore` | No reliable country field | Flag as coverage gap |
| `FileUpload-Canva Pro/Teams Churn Survey` | No source-specific country field — use the unified locale field (see Query G) | — |
| `FileUpload-Canva AI (PFP)` | No reliable country field | Flag as coverage gap |
| `FileUpload-Product Feedback Platform` | No reliable country field | Flag as coverage gap |
| `Twitter`, `Reddit`, `Discord` | No country metadata | Flag as coverage gap |

**Run separate queries per source** — do not try to combine sources in a single country-filtered query. A ZendeskSupport query with `nli.zendesksupport_customfields_country` will not filter records from other sources.

**If ZendeskSupport returns 0:** Try the fallback field `nli.zendesksupport_country_full_name`. If still 0, try `nli.zendesksupport_user_country`. If all return 0, investigate before concluding no data exists.

**Coverage gap note for every report:** FileUpload sources (AI PFP, Product Feedback Platform) and social sources (Twitter, Reddit, Discord, Playstore) likely contain country signal but cannot currently be isolated. This means AI-related feedback themes — which often dominate global rankings — will be systematically undercounted in country reports. Always flag this explicitly.

**This applies to every use of these sources, not just volume/theme counts** — including quote-sourcing in Query F. A source having no country field means any single record from it cannot be attributed to a specific country, full stop. Never infer country from the report's context (i.e. "we're running the UK digest, so this quote must be from the UK") — that assumption is exactly what caused a real misattribution in production (see Query F below).

### Country name reference

| Country | ZendeskSupport value | Submit A Wish value | App Store value |
|---------|---------------------|--------------------|-----------------| 
| United Kingdom | `United Kingdom` | `United Kingdom` | `GBR` or `United Kingdom` |
| France | `France` | `France` | `FRA` or `France` |
| Australia | `Australia` | `Australia` | `AUS` or `Australia` |
| Germany | `Germany` | `Germany` | `DEU` or `Germany` |
| Indonesia | `Indonesia` | `Indonesia` | `IDN` or `Indonesia` |
| Japan | `Japan` | `Japan` | `JPN` or `Japan` |
| Brazil | `Brazil` | `Brazil` | `BRA` or `Brazil` |
| India | `India` | `India` | `IND` or `India` |
| Canada | `Canada` | `Canada` | `CAN` or `Canada` |
| Singapore | `Singapore` | `Singapore` | `SGP` or `Singapore` |

---

## Step 5: Run the Queries

Run these queries using `mcp__ca7fe4b4...run_graph_query`. Exclude staff sources in all queries:
```
AND nli.source NOT IN ['FileUpload-Always On Product Feedback (Staff)', 'FileUpload-Bug Reporting (Staff)']
```

Always use `COUNT(DISTINCT nli.record_id)` — never `COUNT(*)`.  
Always wrap dates with `toDateTime(...)` — e.g. `toDateTime('2026-05-25')`.

---

### Query A — ZendeskSupport Volume + Sentiment (this week)

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_SENTIMENT]->(sp:SentimentPrediction)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.source = 'ZendeskSupport'
AND nli.zendesksupport_customfields_country CONTAINS '[COUNTRY]'
RETURN sp.label AS sentiment_label, COUNT(DISTINCT nli.record_id) AS total
ORDER BY total DESC
```

Run again for the comparison week (change date range only).

---

### Query B — ZendeskSupport Top Themes (this week)

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.source = 'ZendeskSupport'
AND nli.zendesksupport_customfields_country CONTAINS '[COUNTRY]'
AND t.type != 'MISC'
RETURN t.name AS theme_name, COUNT(DISTINCT nli.record_id) AS total
ORDER BY total DESC
LIMIT 20
```

Run again for comparison week to compute WoW % change per theme.

---

### Query C — Submit A Wish Volume + Top Themes (this week)

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.source = 'Webhook-Ask Canva Submit A Wish'
AND nli.webhook_ask_canva_submit_a_wish_country_full_name CONTAINS '[COUNTRY]'
AND t.type != 'MISC'
RETURN t.name AS theme_name, COUNT(DISTINCT nli.record_id) AS total
ORDER BY total DESC
LIMIT 10
```

---

### Query D — App Store Volume (this week)

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.source = 'Appstore'
AND nli.appstore_country_full_name CONTAINS '[COUNTRY]'
RETURN COUNT(DISTINCT nli.record_id) AS total
```

---

### Query E — Global Top Themes (this week, no country filter)

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND t.type != 'MISC'
AND nli.source NOT IN ['FileUpload-Always On Product Feedback (Staff)', 'FileUpload-Bug Reporting (Staff)']
RETURN t.name AS theme_name, COUNT(DISTINCT nli.record_id) AS total
ORDER BY total DESC
LIMIT 20
```

Use this to determine **truly local** issues: in country top 10 but NOT in global top 10.

---

### Query F — Verbatim Quotes (top 3 issues)

**CRITICAL — country attribution must be verified per-record, never assumed.** A quote can only be labelled "[COUNTRY] customer" if the specific record it came from has a country-filterable field that actually matches. Candidate-gathering and country-verification are the same step, not sequential — the candidate query itself must include the country filter. (This bug shipped once in production: a quote from an Appstore record with `appstore_country_full_name = 'Italy'` was labelled "UK customer" because the candidate query filtered by theme only, with no country filter at all. Caught by the country manager reading the linked record, not by this process — the fix below closes that gap.)

**Important:** Zendesk tickets are multi-message support threads — they rarely yield clean short verbatims. Prefer short-form sources for quotes, but only the ones that actually carry a country field for this record.

Step 1: Get record IDs filtered to short-form sources **AND filtered to this country**. Run one query per source (not a combined `IN [...]` list) since the country field name differs by source:

```cypher
// Appstore
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND t.name CONTAINS '[THEME_NAME]'
AND nli.source = 'Appstore'
AND nli.appstore_country_full_name CONTAINS '[COUNTRY]'
RETURN DISTINCT nli.record_id AS record_id, nli.source AS data_source, nli.record_timestamp AS ts
ORDER BY ts DESC
LIMIT 15
```

```cypher
// Submit A Wish
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND t.name CONTAINS '[THEME_NAME]'
AND nli.source = 'Webhook-Ask Canva Submit A Wish'
AND nli.webhook_ask_canva_submit_a_wish_country_full_name CONTAINS '[COUNTRY]'
RETURN DISTINCT nli.record_id AS record_id, nli.source AS data_source, nli.record_timestamp AS ts
ORDER BY ts DESC
LIMIT 15
```

**Sources with NO country field at all — Trustpilot, Reddit, Twitter, `FileUpload-Always On Product Feedback`, `FileUpload-Bug Reporting (Non-Staff)`, `FileUpload-Product Feedback Platform`.** Do not query these for quotes that will be labelled with a specific country — there is no field to verify against. If used at all (only after both country-verified sources below return nothing), the quote **must** be labelled generically — `"[verbatim]" — Global customer (no country data available for this source)` — never `"[COUNTRY] customer"`. Say this explicitly in the report rather than silently defaulting to the report's country.

Step 2: If both country-verified queries above (Appstore, Submit A Wish) return 0 candidates for a theme, fall back to ZendeskSupport **with the same country filter already used in Query B** (`nli.zendesksupport_customfields_country CONTAINS '[COUNTRY]'`) — this is still country-verified, just longer-form and less quotable. Only fall back to an unverified source (labelled "Global customer", per above) if country-verified ZendeskSupport also returns nothing.

Step 3: Pass the resulting record IDs to `find_user_quote`.

Format for Priority Findings quotes and the Canva doc/markdown narrative: `"[verbatim]" — [COUNTRY] customer ([data_source]) ↗` with link `https://dashboard.enterpret.com/canva-design/record/[record_id]`. Including the source name keeps the country-verification path auditable at a glance in those single-quote contexts. The "What customers are saying" artifact card (Tier 3, Weekly tab item 5) is the exception — it holds multiple quotes per theme, so a repeated per-quote source tag becomes clutter; follow that section's own formatting guidance instead (one note at the bottom of the card if sources didn't end up mixed, no tag on individual quotes).

**Record ID format:** Enterpret record IDs are full UUIDs, e.g. `a9091f90-40f5-5f48-9b46-c26ab6d3cea1`. Always use the full UUID returned by the query — never truncate or shorten it. The record link format is: `https://dashboard.enterpret.com/canva-design/record/[full-uuid]`

---

### Query F2 — Empty Results Fallback (run if Query A returns 0)

If Query A returns 0 records, do not proceed with the report. Instead try these fallback fields in order:

1. `nli.zendesksupport_country_full_name CONTAINS '[COUNTRY]'`
2. `nli.zendesksupport_user_country CONTAINS '[COUNTRY]'`

If all three field variants return 0, stop and message the manager:

> "I couldn't find any [COUNTRY] feedback records for [WEEK_START]–[WEEK_END]. I tried three country filter fields and all returned 0. This usually means a field name change or the country value doesn't match exactly. Here's what I tried: `zendesksupport_customfields_country`, `zendesksupport_country_full_name`, `zendesksupport_user_country`. Want me to investigate, or try a different spelling?"

Do NOT deliver an empty or fabricated report. Do NOT substitute global data.

---

### Query H — Peer Country Comparison (run in parallel with other queries)

Runs the same ZendeskSupport volume + top themes query for each peer country. Use the stored `peer_countries` list; default to Australia, France, Germany if not set.

For each peer country, run Query A (volume) and Query B (top 10 themes) with the appropriate country field and value from the reference table in Step 4. These can run in parallel.

Results feed directly into the compare tab peer table and LOCAL/ELEVATED analysis. If a peer country query returns 0 or times out, omit that country from the table silently — do not show a row of zeros.

**Peer countries are configurable.** Ask during Round 3 of onboarding:

> "For the peer comparison tab, which markets do you want to benchmark against? You can choose up to 10 — we'd suggest starting with 3–5 for a clean view. Which countries matter most to you?"

Store as `peer_countries: [list]` in the scheduled task prompt. If the manager doesn't specify, default to Australia, France, Germany and tell them they can update anytime.

**Normalise before claiming a market "stands out."** Raw counts are dominated by market size (the US will always look big). When comparing a specific theme or bucket across peers — not just total volume — divide by each market's own weekly total to get a % share, and compare shares, not raw counts. Only call a market a genuine outlier if its share is clearly separated from its peers' shares, not just its raw count. If an operating-pack or other qualitative claim (e.g. "GB has the highest EMEA volume of X") doesn't hold up against the peer markets actually configured for this run, say so plainly rather than presenting the qualitative claim as this week's confirmed finding — note it as directional/from a different time window instead.

---

### Query G — Churn Themes (country-inferred via locale)

The churn source (`FileUpload-Canva Pro/Teams Churn Survey`) has no source-specific country field. Infer country from locale instead. Follow this sequence:

**Step G1 — Discover the locale field (first run only, then store result)**

`keys(nli)` and similar reflection functions are **not supported** by this graph engine (only registered UDFs are allowed) — a schema probe using `keys()` will fail with a TranslationError. Instead, discover the field name by deliberately querying a plausible-but-wrong property name and reading the engine's suggestion:

```cypher
MATCH (nli:NaturalLanguageInteraction)
WHERE nli.source = 'FileUpload-Canva Pro/Teams Churn Survey'
RETURN nli.locale AS x
LIMIT 1
```

This fails, but the error includes a "Did you mean one of these?" list with the real field names available on that node — that's the actual schema discovery mechanism this engine supports. For this org, that lookup surfaces `uf_locale_GOexjw__list`: a **unified locale field shared across multiple sources** (not a churn-specific field, and not the same as any `zendesksupport_*` field) — this is what's actually populated on the churn survey rows. Confirm it's populated for the churn source specifically before relying on it:

```cypher
MATCH (nli:NaturalLanguageInteraction)
WHERE nli.source = 'FileUpload-Canva Pro/Teams Churn Survey'
AND nli.uf_locale_GOexjw__list IS NOT NULL
RETURN nli.uf_locale_GOexjw__list AS locale, COUNT(DISTINCT nli.record_id) AS cnt
ORDER BY cnt DESC
LIMIT 15
```

Store the discovered field name in the scheduled task prompt as `churn_locale_field: [field_name]`. **This field name is org-specific** (Enterpret appears to auto-generate a suffix per unified field) — don't assume `uf_locale_GOexjw__list` is portable to a different Enterpret org; re-run the discovery probe once per org and cache the result.

**Step G2 — Query using the discovered locale field**

Use the locale codes from the reference table below with the stored `churn_locale_field`.

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.source = 'FileUpload-Canva Pro/Teams Churn Survey'
AND nli.[CHURN_LOCALE_FIELD] CONTAINS '[LOCALE_CODE]'
AND t.type != 'MISC'
RETURN t.name AS theme_name, COUNT(DISTINCT nli.record_id) AS total
ORDER BY total DESC
LIMIT 10
```

Also run the same filter without the theme join to get total churn volume for the week (for the WoW headline number). Run both queries again for the comparison period to compute WoW % change.

**Step G3 — No match = skip churn section entirely**

If the locale query returns 0 records for both the report and comparison week, do not include a churn section in the output. Do not substitute global churn data. Do not say "no churn data available" — just omit the section silently. The source coverage note in the artifact should flag churn as unavailable for this market.

**Locale reference table:**

| Country | Locale codes |
|---------|-------------|
| United Kingdom | `en-GB` |
| Australia | `en-AU` |
| Indonesia | `id-ID` |
| Japan | `ja-JP` |
| Brazil | `pt-BR` |
| Canada | `en-CA`, `fr-CA` |
| Singapore | `en-SG` |
| France | `fr-FR` |
| Germany | `de-DE` |
| India | `en-IN` |
| Spain | `es-ES` |
| Netherlands | `nl-NL` |
| United States | `en-US` |

**Inference callout — always include when churn data is shown:**

When churn data is successfully inferred, add a brief methodology note in the artifact's churn card and Canva doc:

> ⓘ *Churn data inferred from locale [locale code] — the churn survey source has no direct country field, so this uses a unified locale field shared across sources rather than a source-specific one. Coverage may be incomplete if a respondent's locale setting doesn't match their actual market.*

This callout keeps the data honest and helps country managers understand why their churn numbers may differ from what they see in other tools.

---

### Query I — Subscription Plan Breakdown per Priority Theme

Run this for each priority theme (top 3–4 by volume) to power the segment pills in the artifact. Use `zendesksupport_subscriptions_clean` — the cleaned, deduplicated subscription field confirmed in production. **If this field is not found, the engine's error will suggest the actual field names available (e.g. `zendesksupport_subscriptions__sl`) — check those suggestions before concluding the breakdown is unavailable, since the exact field name may vary by org.**

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.zendesksupport_customfields_country CONTAINS '[COUNTRY]'
AND t.name CONTAINS '[THEME_NAME]'
AND t.type != 'MISC'
AND nli.zendesksupport_subscriptions_clean IS NOT NULL
RETURN nli.zendesksupport_subscriptions_clean AS plan, COUNT(DISTINCT nli.record_id) AS cnt
ORDER BY cnt DESC
```

Run in parallel with Query F (verbatim quotes) — both are per-theme lookups that can execute simultaneously.

**Consolidate raw plan values into display labels before computing %:**

| Raw value(s) | Display label |
|---|---|
| `Canva Free` | Free |
| `Canva Pro` | Pro |
| `Canva for Business`, `ENTC` | Business |
| `Canva for Teams`, `Canva for Teams 26+` | Teams |
| `C4Edu Managed`, `C4Edu School`, `C4Edu District` | Edu |
| `Canva for Non-Profit` | Non-Profit |

**Computing %:** Sum counts within each consolidated label, divide by the total of all labelled records. Only show pills for plans with **≥5% share**. Order by % descending.

**If the field exists but every sampled record has an empty string:** this is a genuine data-population gap for that theme this week, not a query error — do not fabricate a plan breakdown. Don't repeat a "plan: not populated" caption on every individual quote or finding card — that's noise once it's said once. Instead, mention the gap a single time, in the source coverage & methodology card (see Tier 3 spec), so the manager knows it's a data-side gap without it cluttering every quote.

**Note:** `zendesksupport_subscriptions_clean` (or its org-specific equivalent) only covers ZendeskSupport records. Records from other sources are excluded automatically by the `IS NOT NULL` filter — this is expected.


## Step 6: Identify Key Narratives + Tie to Context

Before writing the output, synthesise:

1. **Headline story** — One declarative sentence naming the biggest development this week. Include dates and outcome where known (e.g. "Billing Confusion Spiked +67% — Possible Klarna BNPL Correlation").

2. **Spike flag** — tag **SPIKE** if: ≥25% WoW increase AND volume ≥ stored `spike_floor`. If `spike_floor` is "pending first run", calculate dynamically: `max(round(total_weekly_records * 0.02 / 5) * 5, 5)`. Tag **WATCH** if: 15–24% WoW AND volume ≥ half the spike floor (round up). WATCH themes are surfaced briefly but not treated as priority findings. For SPIKEs: note onset day, platform split, affected segments, whether volume returned to baseline.

   Monthly cadence uses the same stored floor. SPIKE threshold for monthly: ≥30% MoM AND volume ≥ spike floor.

3. **Truly local** (country top 10, NOT global top 10) → tag **LOCAL**.

4. **Over-indexed locally** (in both country top 10 AND global top 10, but country rank is 5+ positions higher than global rank) → tag **ELEVATED**. Example: UK #3 vs global #14. These are shared global issues the country experiences disproportionately — different signal from LOCAL, worth calling out separately in the compare tab. Note the rank gap: "UK ranks this 11 positions higher than globally."

5. **Operating pack connections** — For each top issue, check if it maps to a named initiative, owner, pillar, or metric in the operating pack. Cite directly: _"🔗 Op Pack: [relevant quote or goal] — owner: [name]."_ Only make connections that are genuinely relevant; don't force-fit. If the operating pack makes a comparative or superlative claim (e.g. "highest in EMEA"), treat it as the pack's claim, not a verified finding of this run, unless this run's own peer data actually reproduces it (see Query H normalisation note) — if it doesn't reproduce, say so rather than repeating the claim as confirmed.

6. **Incidents / rollout cross-reference** — If Step 3d found a deployment or incident within 24h of a SPIKE onset, include the cross-reference callout. This is often the single most useful thing a country manager learns from the digest — whether they need to chase a product team or whether it already resolved.

7. **Zoom / Slack context** — If a Zoom transcript or Slack message mentioned this theme, call it out: _"Also surfaced in [meeting name / channel] on [date]."_

8. **Churn pattern** — Plan type concentration, WoW direction, is volume rising from a new driver or intensification of existing ones.

---

## Step 7: Product Area Bucketing

Assign every theme to exactly one bucket (mutually exclusive, priority order):

| Bucket | Includes |
|--------|---------|
| **Billing** | Subscriptions, cancellation, payments, invoicing, refunds, renewal, unknown charges |
| **Account** | Login, SSO, email lock-out, ownership verification, authentication, OTP |
| **AI** | AI prompt quality, AI output quality, AI feature requests, AI reliability, AI ethics concerns, AI pricing |
| **Print** | Print orders, fulfillment, delivery, print quality, post-order support |
| **Editor** | Design tools, templates, assets, canvas performance, export |
| **Other** | Education eligibility, Creator Program, Legal, Help experience, anything not above |

Calculate % for country and global. When **Other > 15%** of country total, list the top 3 sub-categories within Other.

**Note on AI undercounting:** AI feedback from FileUpload sources (Always On PFP, Always On Product Feedback) cannot be country-filtered. Country AI % will be structurally lower than global AI % — this is a coverage gap, not a real market difference. Always flag it in the product area comparison note.

---

## Step 8: Generate Deliverables

Generate only the formats the manager requested during onboarding. Run them in the order below. Each is independent — don't skip one because another is taking long.

---

### Tier 1: Short Slack Message (always include if delivery includes "slack")

Send **one concise message** — not a data dump. This is the at-a-glance pulse check.

```
[FLAG EMOJI for country] *[COUNTRY] Feedback Digest · [WEEK_START] – [WEEK_END]*

*[HEADLINE — single most important thing this week. Factual, no editorialising.]*

• Volume: [N] items ([WoW%] WoW · [N] prior week)
• [SPIKE theme if present]: [theme name] — [N] records, [WoW%] WoW · [global rank if applicable]
• [LOCAL theme if present]: [theme name] — [N] records · UK-specific (not in global top 10)
• Churn: [N] responses ([WoW%] WoW) · [dominant plan type]%

🖥️ Full artifact dashboard → [artifact link or "open in Cowork"]

📄 Canva doc → [doc link if generated]

📝 Markdown file → [attached/available in Cowork]
```

**Do NOT include an Enterpret dashboard link in this Slack message.** It used to be a fourth link line here, but it made the message noisier without adding much a country manager needs in a quick pulse check — the artifact's header and source-coverage note already link to the Enterpret dashboard, so it's still one click away for anyone who opens the dashboard. Keep the Slack message limited to the three link types above (whichever the manager opted into).

**Formatting — put a blank line between every link line.** Stacking `emoji → link` lines back-to-back with no blank line between them can cause Slack's auto-linkifier to swallow the trailing newline and the next line's leading emoji into the URL itself, breaking every link in the block. Always separate consecutive link lines with a blank line, as shown above — this holds regardless of how many link types are included.

Keep to 5–7 content lines (not counting the blank spacer lines between links). No tables, no methodology notes. If someone wants more, it's in the artifact or doc.

**Rules for the headline:**
- Describe only what the data shows — no inferences about root cause unless directly evidenced
- Include dates and direction: "AI Prompt Non-Adherence spiked Mon 26 May (+45% WoW)"
- If volume peaked then returned: "...Volume returned to prior-week levels by [day]" — NOT "self-resolved"

---

### Tier 2: Canva Doc Archive (include if delivery includes "doc")

The Canva doc is a **running archive** — one permanent link that grows each week, newest entry at the top. The manager shares it once; the link never changes. Their team can bookmark it and always see the latest digest plus full history.

**Template design ID:** `DAHRkgUutkg`
**Placeholder fields:** `{{Date}}` and `{{Summary}}` (element ID `PBHwrtX0FYYbpb4Z`)
**Archive marker:** `— ✦ PREVIOUS ENTRIES ✦ —` (marks where new entries get inserted each run)

---

#### First run (no `canva_doc_archive` ID stored):

1. Call `mcp__b7e20176...copy-design` with `design_id: "DAHRkgUutkg"` — creates a fresh copy of the branded template.
2. Note the new copy's `design.id`.
3. Call `mcp__b7e20176...read-design` on the copy with `open_transaction: true` — note the `transaction_id`.
4. Call `mcp__b7e20176...edit-design` with the transaction, `page_index: 1`, `is_responsive: true`:
   - Replace `{{Date}}` → `Week of [WEEK_START] – [WEEK_END]`
   - Replace `{{Summary}}` → `[FULL_NARRATIVE]\n\n— ✦ PREVIOUS ENTRIES ✦ —`

   Run as **two separate `edit-design` calls** — one operation per call on responsive pages.
5. Call `edit-design` with `finalize: "commit"` to save.
6. Store the design ID as `canva_doc_archive` in the scheduled task prompt.
7. Construct the archive URL using the stable design ID format: `https://www.canva.com/design/[design.id]`
   **IMPORTANT:** Do NOT use `view_url` or `edit_url` from the API response — these are signed short URLs (`canva.com/d/...`) that expire after the session. The stable permalink is always `https://www.canva.com/design/[DESIGN_ID]`.
8. Present the stable link with context:

   > "Your digest archive is live 📄 — https://www.canva.com/design/[DESIGN_ID]. Share this link with your regional leads, product partners, or anyone who wants to stay close to your market's user signals. Each week's digest gets added at the top automatically."

---

#### Subsequent runs (`canva_doc_archive` ID is stored):

1. Call `mcp__b7e20176...read-design` on the stored `canva_doc_archive` ID with `open_transaction: true`.
2. Call `mcp__b7e20176...edit-design` with `page_index: 1`, `is_responsive: true`:
   - Find `— ✦ PREVIOUS ENTRIES ✦ —` → replace with `**Week of [WEEK_START] – [WEEK_END]**\n\n[FULL_NARRATIVE]\n\n— ✦ PREVIOUS ENTRIES ✦ —`
3. Call `edit-design` with `finalize: "commit"` to save.
4. Present the same stable archive URL (link never changes — always `https://www.canva.com/design/[canva_doc_archive_id]`):

   > "This week's digest has been added to your archive 📄 — https://www.canva.com/design/[canva_doc_archive_id]"

   **Reminder:** Never use the `view_url` / `edit_url` from `read-design` or `copy-design` responses here — those are ephemeral signed URLs. Construct the link from the stored design ID.

**If `find_and_replace_text` fails or edits don't persist:** Tell the user what happened, link the archive directly, and note it's a known Canva MCP limitation. Do not create a new doc.

---

**`[FULL_NARRATIVE]` content spec — compose as flowing prose:**

1. **Week's lead finding** — 2–3 sentences. Factual: dates, volume, onset, direction.
2. **KPI snapshot** — Volume / Top SPIKE / Biggest Win / Churn (inline, not a table)
3. **Priority findings** — For each top 3–4 themes:
   - SPIKE or LOCAL badge
   - Record count + WoW change + global rank (if applicable)
   - 2–3 sentence description (onset, platform split, affected segments)
   - 1–2 verbatim quotes (per Query F — country-verified, source cited in the attribution)
4. **Operating plan tie-back** — Weave each theme's tie-back into that theme's own finding (as a 🔗 Op Pack note), rather than repeating the same initiatives again in a separate summary section — that duplicates content the reader already saw and displaces space that's better used for another real chart or data point.
5. **Churn drivers** — Top 3 by count, WoW change, plan type concentration, 1 quote
6. **Month-on-month context** — Volume trend narrative (Jan–current)
7. **Source coverage note** — Which sources contributed; flag coverage gaps (AI PFP, social)

---

### Tier 2b: Markdown File (include if delivery includes "markdown")

Save a `.md` file to the outputs folder and present it to the user via `mcp__cowork__present_files`.

**File naming:** `[country-slug]-feedback-[WEEK_START].md` (e.g. `uk-feedback-2026-06-09.md`)

**Content structure — same as the Canva doc, rendered as markdown:**

```markdown
# 🇬🇧 [COUNTRY] Weekly Feedback Digest
**Week of [WEEK_START] – [WEEK_END]**

---

## Summary
**[N] records** · vs [N] prior week · **[WoW%] WoW** · [source filter]
[2–3 sentence narrative: headline finding, what drove volume, key direction]

---

## 🚨 Priority Themes

### [SPIKE/WATCH] · [Theme name]([Enterpret citation URL])
**[N] records · [WoW%] WoW** (was [N])
[2–3 sentence description]

> "[verbatim quote]"
> — [UK/country customer]([record URL])

---

## 📊 Full Theme Breakdown
| Theme | This Week | Prior Week | WoW |
|---|---|---|---|
| [Theme]([citation URL]) | N | N | **+X% 🚨** |

---

## 🗂️ Theme Clusters
[Grouped by product area with totals]

---

## 🚨 Incidents & Rollouts
[Cross-reference findings or "No incidents flagged this week"]

---

## 📌 Watch for Next Week
- [theme] — [why]

---

## Source Coverage
[Filter used] · [N] records · [date range]

---
*Generated by Country Feedback Digest skill · Powered by Enterpret*
```

**Why markdown:** Unlike the Canva doc archive (which accumulates history in place), markdown gives a clean per-week snapshot that pastes cleanly into other tools, opens in Cursor, Obsidian, Notion, or any markdown editor, and works well for people who want to version-control their digests.

---

### Tier 3: Live Artifact (include if delivery includes "artifact")

Create or update a Cowork artifact using `mcp__cowork__create_artifact` (or `update_artifact` if one exists for this country).

**Artifact ID convention:** `[country-slug]-weekly-feedback` (e.g. `united-kingdom-weekly-feedback`)

**Design bar:** this is a dashboard a country manager will screenshot and share with their team — build it to that standard, not as a text report with a header. Concretely: bold, large KPI numbers (not just bold labels); every ranked or comparative dataset gets an actual bar/stacked-bar visual, not a plain HTML table; every visual gets one factual, non-editorialising insight callout near it (colored left-border box) stating the single most useful takeaway in plain language. Prefer one good chart over two paragraphs of prose describing the same numbers.

**The artifact is a self-contained HTML page with:**

- Header with country flag, week dates, total volume, WoW change, links to Enterpret dashboard, operating pack, and Talk to Users deck
- Headline finding block (orange left-border callout)
- 3–4 KPI tiles (total volume, top priority theme, biggest win, one more if useful — e.g. theme to watch)
- Tab navigation: **Weekly view** | **Month-on-month** | **Global & peer comparison**

**Weekly tab (in this order) — this tab is UK-only data; cross-market comparisons belong in the Global & peer comparison tab, not here:**
1. **Wins this week** — themes with the largest WoW/MoM improvement, with a positive user quote from Trustpilot or App Store, and brief context on whether a fix likely caused it. Show this before the issues list — it sets a positive tone.
2. **Priority findings card** — top 3–4 themes by volume, with verbatim quotes linked to individual Enterpret records (`↗ view record`), **subscription plan breakdown pills** (from Query I) where available, and inline 🔗 Op Pack tie-backs (see note in `[FULL_NARRATIVE]` spec — don't duplicate these in a separate tie-back section). Do NOT show SPIKE/WATCH/LOCAL/ELEVATED badge labels — these add visual clutter. Instead, describe what makes each theme notable in plain language (e.g. "up 45% this week", "unique to this market", "affecting Pro users most"). Add pills at the bottom of each finding card:

  ```html
  <div class="segment-pills">
    <span class="seg-pill">Free <strong>58%</strong></span>
    <span class="seg-pill">Pro <strong>42%</strong></span>
    <span class="seg-pill">Business <strong>17%</strong></span>
    <span class="seg-pill">Teams <strong>8%</strong></span>
  </div>
  ```

  CSS (include in artifact `<style>` block):
  ```css
  .segment-pills { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 6px; }
  .seg-pill { font-size: 10px; padding: 2px 8px; border-radius: 10px; background: #f0f0f0; color: #555; }
  .seg-pill strong { color: #006B6B; }
  ```

  If Query I shows the field exists but is unpopulated (empty string) for this theme, don't show pills at all for it, and don't add a per-finding caption saying so either — one mention of the gap in the source coverage & methodology card (item 8 below) is enough; repeating "not populated" on every finding is noise.
3. **Product area mix** — a stacked bar (or grouped bars) comparing country % vs global % per bucket, not a plain list of percentages. (This one stays in the weekly tab despite being a country-vs-global comparison, since it's the direct evidence behind the headline billing/AI-coverage callouts made earlier on the same tab — moving it away from those callouts would separate a claim from its chart.)
4. **Incidents/rollout callout** (if a match was found in Step 3d) — shown inline with the relevant finding
5. **What customers are saying** — a dedicated card gathering country-verified verbatims from Query F across the priority themes. Aim for **two quotes per theme** (more if genuinely distinct) rather than one — it reads as a much richer section and is worth the extra `find_user_quote` calls. Never include a quote here that hasn't passed Query F's country-verification step. Don't put a per-quote source tag (e.g. "ZendeskSupport") on every entry — if every quote in the card ends up from the same source (common, since Appstore/Submit A Wish often return 0 or off-topic candidates for a given theme+week even after trying), say so once in a single note at the bottom of the card instead of repeating a tag under each quote. If sources genuinely do vary across quotes, that variety is usually obvious from context and still doesn't need a tag on each one. Don't append a per-quote plan-availability note either — if plan data wasn't populated, that belongs once in the source coverage card.
6. **Sentiment mix** — stacked bar of Negative/Neutral/Positive share, this week vs prior week, if sentiment data was pulled (Query A) — this is real data that's easy to compute and easy to skip building; don't skip it, unless the manager has asked for a leaner artifact.
7. **Churn drivers card** — more than a single quote. Include: the bar chart of top churn themes with WoW change; one insight callout naming what's actually driving churn this week (e.g. which themes dominate, whether it's easing or worsening, and by how much) — factual, not editorialised; and 2–3 quotes grouped under their specific churn theme (not just one generic quote for the whole card). Only include this card if Query G produced data.
8. Source coverage & methodology card
9. **SSOT note** — include at the bottom of the weekly tab:

  > ⓘ *This artifact shows trends from Enterpret sources that can be country-filtered. Not all sources are included — social (Twitter, Reddit, Discord), Play Store, and some FileUpload sources are excluded due to missing country metadata. Use this digest as a directional read. For the full dataset and deeper analysis, your [Enterpret dashboard]([ENTERPRET_DASHBOARD_URL]) is the source of truth.*

**Month-on-month tab:**
- Monthly volume bar chart (Jan–current)
- Top 5 themes grouped bar chart (Jan–current)
- Monthly KPI tiles (volume only — no sentiment)

**Global & peer comparison tab:**
- **Theme ranking chart** — a real bar chart (country vs global, two colors) rather than a plain table, ranked by country volume. If global counts are much larger, scale the global series down by a fixed factor and say so in a caption, or use two separate scales — don't just print a wide-ranging table of raw numbers. Lives here, not the weekly tab — it's a country-vs-global comparison, and this tab is where all cross-market comparisons belong.
- Country vs global KPI tiles (share of volume, billing over-index)
- Peer country table or chart (comparable markets + global row)
- The peer-normalised comparison (per theme/bucket, normalised by market size — see Query H) belongs here too — it's the compare tab's core job, alongside the theme ranking chart above.

**Styling rules:**
- Brand colour: `#006B6B` (teal) for headers, KPI tiles, chart primary series
- No SPIKE/WATCH/LOCAL/ELEVATED badge colours — removed. Use plain descriptive text instead.
- All Enterpret links → the country-specific dashboard URL from `references/country-dashboards.md` (fall back to `https://dashboard.enterpret.com/canva-design/` if not listed)
- Charts: prefer native inline SVG/CSS bar charts built from the actual numbers over a charting library — this keeps the artifact fully self-contained and avoids any external-request restrictions in the hosting environment. No `localStorage`. No `position: fixed`.

**Deliver order:** Present Canva doc and/or markdown file → then send Slack message → then confirm artifact is updated.

---

## Step 9: Schedule (Setup Mode Only)

After delivering the preview, confirm cadence and create a scheduled task.

**Timezone handling — always confirm before scheduling:**

Cron expressions run in UTC. When the manager says "Monday 9am", convert their local time to UTC and confirm it back before creating the task:

> "Monday 9am AEST = Sunday 11pm UTC. I'll schedule it as `0 23 * * 0`. Does that look right?"

If the manager doesn't provide a timezone, ask for it — don't assume. Common offsets: GMT/BST (UK, ±0/+1), AEST/AEDT (AU, +10/+11), WIB (Indonesia, +7), JST (Japan, +9), CET/CEST (Europe, +1/+2), IST (India, +5:30).

Note daylight saving: UK, AU, and EU change clocks seasonally. Mention this if relevant: "This will shift by an hour when daylight saving changes in [month] — let me know if you want to adjust it then."

- **Prompt**: The full `[SCHEDULED RUN]` string with all stored parameters (see What to Store section above)
- **Cron**: Converted to UTC using the manager's confirmed timezone
- Confirm task ID and tell the manager they can ask to update or cancel anytime

---

## Common Pitfalls

1. **Never use `nli.metadata['UF Country']`** — bracket notation causes a TranslationError. Use source-specific fields from the table in Step 4.
2. **Run one source per query** — don't try to combine ZendeskSupport + Submit A Wish in one country-filtered query.
3. **Week dates matter** — last complete Mon–Sun week ends on Sunday. June 1 being a Monday means it's the START of the new week, not the end of the old one.
4. **ZendeskSupport ≠ good verbatims** — tickets are multi-message threads. Always try short-form sources first for quotes (Submit A Wish, App Store, Product Feedback, Reddit, Trustpilot) — but only the ones with a country field for this record (see Pitfall #19).
5. **AI themes will be missing** — FileUpload sources (AI PFP, Always On Product Feedback) have no reliable country filter. AI feedback is systematically undercounted. Flag this clearly.
6. **Don't skip truly-local vs global** — this is the highest-value insight for country managers.
7. **Operating pack connections must be genuine** — don't force-fit every theme to a pillar. Only call out real, specific connections with named owners or goals. If a qualitative claim from the pack doesn't hold up against this run's own peer data, say so (see Step 6.5).
8. **Zoom/Slack context is additive, not mandatory** — if no relevant context found, skip those sections silently.
9. **Always show WoW change** — raw counts without trends are not actionable.
10. **Temporal onset matters for spikes** — name the specific day if identifiable, and whether it self-resolved.
11. **Churn data uses a unified locale field, not a source-specific one** — `keys(nli)` doesn't work in this graph engine; discover the real field name via the deliberate-wrong-property-name trick in Query G1, and confirm it's populated on the churn source before trusting it. If discovery fails for both locale attempts, omit the churn section entirely — never substitute global data.
12. **Churn inference callout is mandatory** — whenever churn data is shown, include the methodology note so managers understand how it was derived. Do not present inferred churn data as if it were directly filtered.
13. **Plan breakdown pills require Query I** — always run Query I for each priority theme before building the artifact. If the expected field name errors, check the engine's suggested alternatives before concluding the breakdown is unavailable. If the field exists but is empty for every sampled record, mention the gap once in the source coverage card — don't fabricate a breakdown, and don't repeat a "not populated" caption on every individual finding or quote; that's noise once it's already been said.
14. **Canva doc archive: never create a new doc on subsequent runs** — always open the stored `canva_doc_archive` ID and prepend. Creating a new doc every week defeats the purpose of the archive and breaks the shared bookmark.
15. **Canva doc URL: never use `view_url` or `edit_url` from the API** — these are signed short URLs (`canva.com/d/...`) that expire after the session. Always construct the stable permalink as `https://www.canva.com/design/[DESIGN_ID]` using the stored design ID.
16. **Slack link lines need blank-line spacing** — stacking `emoji → link` lines with no blank line between them can cause Slack's auto-linkifier to swallow the newline and next line's emoji into the URL, breaking every link in the block. Always separate consecutive link lines with a blank line.
17. **Don't duplicate the operating-pack tie-back in its own section** — weave it into each priority finding inline instead. A separate summary section just repeats what the reader already saw and crowds out a genuine data visual that could go there instead.
18. **Raw peer counts mislead — normalise by market size before calling anything an outlier**, and don't repeat an operating-pack superlative claim as this run's confirmed finding unless the actual peer data reproduces it.
19. **Never attribute a quote to a country without verifying that specific record's country field.** Query F's candidate query must include the country filter, not just the theme filter — filtering by theme/date alone and then labelling every result with the report's country is how a misattribution reaches a customer-facing deliverable (this happened once in production with an Italian Appstore review labelled "UK customer"). Sources with no country field (Trustpilot, Reddit, Twitter, most FileUpload-*) can supply a quote only if explicitly labelled "Global customer (no country data available for this source)" — never the report's country. When in doubt, prefer a country-verified ZendeskSupport quote over an unverifiable short-form one.

---

## References

- `references/slack-example.md` — Annotated example of the target Slack output (UK, May 25–31 2026)
- `references/country-filters.md` — Per-source country field names and known country values. Note: its churn section describes the old `keys(nli)` schema-probe approach, which this SKILL.md's Query G now supersedes (that function isn't supported by the graph engine) — follow Query G here, not the reference file, for churn.
- `references/country-dashboards.md` — Country-specific Enterpret dashboard URLs. **Look up this file at the start of every run** to resolve `[ENTERPRET_DASHBOARD_URL]` for the current country. If the country is not listed, fall back to the default: `https://dashboard.enterpret.com/canva-design/`

