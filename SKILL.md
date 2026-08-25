---
name: country-feedback-digest
description: >
  Generates and delivers a country feedback digest for Canva country managers, pulling live
  data from Enterpret. Supports weekly, bi-weekly, and monthly cadences. Delivers a Slack
  summary, live artifact dashboard (weekly view, month-on-month, peer country comparison),
  and optional Canva doc archive. Features: SPIKE/WATCH/LOCAL/ELEVATED theme tagging, churn analysis
  inferred by locale/currency, incidents & rollout cross-referencing, configurable peer
  benchmarking (up to 10 markets), market-relative spike floor calibrated on first run, and
  operating plan tie-backs. Use when a country manager wants to set up automated feedback
  reports or generate a one-off country summary.
  Trigger phrases: "weekly feedback report for [country]", "set up my weekly digest",
  "send me the UK feedback summary", "send Indonesia feedback to Slack", "country feedback
  report", "set up automated insights for [country]", "weekly Enterpret digest".
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
> For the full dataset — especially when you want to dig into a specific theme, read verbatims, or cross-reference with other markets — **your Enterpret dashboard is the source of truth**. I'll include a direct link to it in every digest so it's always one click away."

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
[SCHEDULED RUN] Country: [COUNTRY] | Channel: [SLACK_CHANNEL_OR_USER_ID] | Delivery: [slack,doc,markdown,artifact — any combo] | Artifact link: [claude://cowork/shared-artifact?uuid=... or "pending first run"] | Enterpret dashboard: [URL or "default"] | Operating pack: [URL or "none"] | Zoom meetings: [exact meeting names as provided, e.g. "UK Weekly Team Sync, EMEA Leadership Review" or "none"] | Slack context channels: [list or "none"] | Incidents channels: [#rollouts-canva, #incident (C019GKGSGTZ)] | Canva doc archive: [design ID or "none"] | Spike floor: [N records or "pending first run"]
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
| `FileUpload-Canva Pro/Teams Churn Survey` | No reliable country field (tested, returns 0 for France/UK) | Flag as coverage gap |
| `FileUpload-Canva AI (PFP)` | No reliable country field | Flag as coverage gap |
| `FileUpload-Product Feedback Platform` | No reliable country field | Flag as coverage gap |
| `Twitter`, `Reddit`, `Discord` | No country metadata | Flag as coverage gap |

**Run separate queries per source** — do not try to combine sources in a single country-filtered query. A ZendeskSupport query with `nli.zendesksupport_customfields_country` will not filter records from other sources.

**If ZendeskSupport returns 0:** Try the fallback field `nli.zendesksupport_country_full_name`. If still 0, try `nli.zendesksupport_user_country`. If all return 0, investigate before concluding no data exists.

**Coverage gap note for every report:** FileUpload sources (AI PFP, Churn Survey, Product Feedback Platform) and social sources (Twitter, Reddit, Discord, Playstore) likely contain country signal but cannot currently be isolated. This means AI-related feedback themes — which often dominate global rankings — will be systematically undercounted in country reports. Always flag this explicitly.

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

**Important:** Zendesk tickets are multi-message support threads — they rarely yield clean short verbatims. Prefer short-form sources for quotes.

Step 1: Get record IDs filtered to short-form sources:
```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND t.name CONTAINS '[THEME_NAME]'
AND nli.source IN [
  'Webhook-Ask Canva Submit A Wish',
  'FileUpload-Always On Product Feedback',
  'FileUpload-Bug Reporting (Non-Staff)',
  'FileUpload-Product Feedback Platform',
  'Appstore', 'Trustpilot', 'Reddit', 'Twitter'
]
RETURN DISTINCT nli.record_id AS record_id, nli.source AS data_source, nli.record_timestamp AS ts
ORDER BY ts DESC
LIMIT 15
```

Step 2: Pass those record IDs to `find_user_quote`. If no quotes found from short-form sources, broaden to ZendeskSupport as fallback.

Format: `"[verbatim]" — [COUNTRY] customer` with link `https://dashboard.enterpret.com/canva-design/record/[record_id]`

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

---

### Query G — Churn Themes (country-inferred via locale or billing)

The churn source (`FileUpload-Canva Pro/Teams Churn Survey`) has no direct country field. Infer country from locale or billing/currency metadata instead. Follow this sequence:

**Step G1 — Discover available fields (first run only, then store result)**

Run a schema probe to find which locale/billing fields exist on the churn source:

```cypher
MATCH (nli:NaturalLanguageInteraction)
WHERE nli.source = 'FileUpload-Canva Pro/Teams Churn Survey'
RETURN keys(nli) AS available_fields
LIMIT 1
```

Look for fields containing: `locale`, `currency`, `billing_country`, `language`, `region`, `plan_country`. Store the discovered field names in the scheduled task prompt as `churn_locale_field: [field_name]` and `churn_currency_field: [field_name]`.

**Step G2 — Query using inferred country filter**

Try locale first (more precise), then currency as fallback. Use the locale codes and currencies from the reference table below.

```cypher
MATCH (nli:NaturalLanguageInteraction)-[:SUMMARIZED_BY]->(fi:FeedbackInsight)
-[:HAS_TAGS]->(cft:CustomerFeedbackTags)-[:HAS_THEME]->(t:Theme)
WHERE nli.record_timestamp >= toDateTime('[WEEK_START]') AND nli.record_timestamp < toDateTime('[WEEK_END_EXCLUSIVE]')
AND nli.source = 'FileUpload-Canva Pro/Teams Churn Survey'
AND nli.[LOCALE_FIELD] CONTAINS '[LOCALE_CODE]'
AND t.type != 'MISC'
RETURN t.name AS theme_name, COUNT(DISTINCT nli.record_id) AS total
ORDER BY total DESC
LIMIT 10
```

If locale query returns 0, retry with the currency field:

```cypher
... AND nli.[CURRENCY_FIELD] = '[CURRENCY_CODE]'
```

Run the same query for the comparison period to compute WoW % change.

**Step G3 — No match = skip churn section entirely**

If both locale and currency queries return 0 records, do not include a churn section in the output. Do not substitute global churn data. Do not say "no churn data available" — just omit the section silently. The source coverage note in the artifact should flag churn as unavailable for this market.

**Locale and currency reference table:**

| Country | Locale codes | Currency | Notes |
|---------|-------------|----------|-------|
| United Kingdom | `en-GB` | `GBP` | Currency is unique to UK — reliable fallback |
| Australia | `en-AU` | `AUD` | Currency is unique to AU — reliable fallback |
| Indonesia | `id-ID` | `IDR` | Currency is unique — reliable fallback |
| Japan | `ja-JP` | `JPY` | Currency is unique — reliable fallback |
| Brazil | `pt-BR` | `BRL` | Currency is unique — reliable fallback |
| Canada | `en-CA`, `fr-CA` | `CAD` | Currency is unique — reliable fallback |
| Singapore | `en-SG` | `SGD` | Currency is unique — reliable fallback |
| France | `fr-FR` | `EUR` | EUR is shared across EU — locale only, do not use currency as sole filter |
| Germany | `de-DE` | `EUR` | EUR is shared across EU — locale only |
| India | `en-IN` | `INR` | Currency is unique — reliable fallback |

**Inference callout — always include when churn data is shown:**

When churn data is successfully inferred, add a brief methodology note in the artifact's churn card and Canva doc:

> ⓘ *Churn data inferred from [locale: en-GB / billing currency: GBP] — the churn survey source has no direct country field. Records where [field] matched [value] were included. Coverage may be incomplete if users have mismatched locale settings.*

This callout keeps the data honest and helps country managers understand why their churn numbers may differ from what they see in other tools.

---

---

### Query I — Subscription Plan Breakdown per Priority Theme

Run this for each priority theme (top 3–4 by volume) to power the segment pills in the artifact. Use `zendesksupport_subscriptions_clean` — the cleaned, deduplicated subscription field confirmed in production.

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

**Note:** `zendesksupport_subscriptions_clean` only covers ZendeskSupport records. Records from other sources are excluded automatically by the `IS NOT NULL` filter — this is expected.


## Step 6: Identify Key Narratives + Tie to Context

Before writing the output, synthesise:

1. **Headline story** — One declarative sentence naming the biggest development this week. Include dates and outcome where known (e.g. "Billing Confusion Spiked +67% — Possible Klarna BNPL Correlation").

2. **Spike flag** — tag **SPIKE** if: ≥25% WoW increase AND volume ≥ stored `spike_floor`. If `spike_floor` is "pending first run", calculate dynamically: `max(round(total_weekly_records * 0.02 / 5) * 5, 5)`. Tag **WATCH** if: 15–24% WoW AND volume ≥ half the spike floor (round up). WATCH themes are surfaced briefly but not treated as priority findings. For SPIKEs: note onset day, platform split, affected segments, whether volume returned to baseline.

   Monthly cadence uses the same stored floor. SPIKE threshold for monthly: ≥30% MoM AND volume ≥ spike floor.

3. **Truly local** (country top 10, NOT global top 10) → tag **LOCAL**.

4. **Over-indexed locally** (in both country top 10 AND global top 10, but country rank is 5+ positions higher than global rank) → tag **ELEVATED**. Example: UK #3 vs global #14. These are shared global issues the country experiences disproportionately — different signal from LOCAL, worth calling out separately in the compare tab. Note the rank gap: "UK ranks this 11 positions higher than globally."

5. **Operating pack connections** — For each top issue, check if it maps to a named initiative, owner, pillar, or metric in the operating pack. Cite directly: _"🔗 Op Pack: [relevant quote or goal] — owner: [name]."_ Only make connections that are genuinely relevant; don't force-fit.

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
🔍 Enterpret dashboard → [ENTERPRET_DASHBOARD_URL]
```

Keep to 5–7 lines. No tables, no methodology notes. If someone wants more, it's in the artifact or doc.

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
   - 1–2 verbatim quotes
4. **Operating plan tie-back** — Each theme → named initiative → signal status (🔴/🟡/🟢)
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

**The artifact is a self-contained HTML page with:**

- Header with country flag, week dates, total volume, WoW change, links to Enterpret dashboard, operating pack, and Talk to Users deck
- Headline finding block (orange left-border callout)
- 3 KPI tiles (total volume, top priority theme, biggest win)
- Tab navigation: **Weekly view** | **Month-on-month** | **Global & peer comparison**

**Weekly tab (in this order):**
1. **Wins this week** — themes with the largest WoW/MoM improvement, with a positive user quote from Trustpilot or App Store, and brief context on whether a fix likely caused it. Show this first — it sets a positive tone before moving to issues.
2. **Priority findings card** — top 3–4 themes by volume, with verbatim quotes linked to individual Enterpret records (`↗ view record`), and **subscription plan breakdown pills** (from Query I). Do NOT show SPIKE/WATCH/LOCAL/ELEVATED badge labels — these add visual clutter. Instead, describe what makes each theme notable in plain language (e.g. "up 45% this week", "unique to this market", "affecting Pro users most"). Add pills at the bottom of each finding card:

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
3. **Product area comparison bars** (right) — country % vs global %
4. **Incidents/rollout callout** (if a match was found in Step 3d) — shown inline with the relevant finding
5. **Theme ranking table** (country rank vs global rank, record counts, WoW) — no badge labels
6. Operating plan tie-back card (initiatives → owners → signal status)
7. Churn drivers card with quotes (quote links go to individual Enterpret records: `/record/[record_id]`)
8. Source coverage & methodology card
9. **SSOT note** — include at the bottom of the weekly tab:

  > ⓘ *This artifact shows trends from Enterpret sources that can be country-filtered. Not all sources are included — social (Twitter, Reddit, Discord), Play Store, and some FileUpload sources are excluded due to missing country metadata. Use this digest as a directional read. For the full dataset and deeper analysis, your [Enterpret dashboard]([ENTERPRET_DASHBOARD_URL]) is the source of truth.*

**Month-on-month tab:**
- Monthly volume bar chart (Jan–current)
- Top 5 themes grouped bar chart (Jan–current)
- Monthly KPI tiles (volume only — no sentiment)

**Global & peer comparison tab:**
- Country vs global KPI tiles (share of volume, billing over-index)
- Peer country table (comparable markets + global row)
- Local vs shared-global theme split (described in plain language, no badge labels)

**Styling rules:**
- Brand colour: `#006B6B` (teal) for headers, KPI tiles, chart primary series
- No SPIKE/WATCH/LOCAL/ELEVATED badge colours — removed. Use plain descriptive text instead.
- All Enterpret links → the country-specific dashboard URL from `references/country-dashboards.md` (fall back to `https://dashboard.enterpret.com/canva-design/` if not listed)
- Chart.js only (from CDN). No `localStorage`. No `position: fixed`.

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
4. **ZendeskSupport ≠ good verbatims** — tickets are multi-message threads. Always try short-form sources first for quotes (Submit A Wish, App Store, Product Feedback, Reddit, Trustpilot).
5. **AI themes will be missing** — FileUpload sources (AI PFP, Always On Product Feedback) have no reliable country filter. AI feedback is systematically undercounted. Flag this clearly.
6. **Don't skip truly-local vs global** — this is the highest-value insight for country managers.
7. **Operating pack connections must be genuine** — don't force-fit every theme to a pillar. Only call out real, specific connections with named owners or goals.
8. **Zoom/Slack context is additive, not mandatory** — if no relevant context found, skip those sections silently.
9. **Always show WoW change** — raw counts without trends are not actionable.
10. **Temporal onset matters for spikes** — name the specific day if identifiable, and whether it self-resolved.
11. **Churn data is inferred, not filtered** — the churn survey source has no direct country field. Use locale then currency to infer. If both return 0, omit the churn section entirely — never substitute global data. For EU markets (FR, DE), do not use EUR as a filter since it is shared across countries; locale only.
12. **Churn inference callout is mandatory** — whenever churn data is shown, include the methodology note so managers understand how it was derived. Do not present inferred churn data as if it were directly filtered.
13. **Plan breakdown pills require Query I** — always run Query I for each priority theme before building the artifact. Only omit if the query returns 0 results for all themes.
14. **Canva doc archive: never create a new doc on subsequent runs** — always open the stored `canva_doc_archive` ID and prepend. Creating a new doc every week defeats the purpose of the archive and breaks the shared bookmark.
15. **Canva doc URL: never use `view_url` or `edit_url` from the API** — these are signed short URLs (`canva.com/d/...`) that expire after the session. Always construct the stable permalink as `https://www.canva.com/design/[DESIGN_ID]` using the stored design ID.

---

## References

- `references/slack-example.md` — Annotated example of the target Slack output (UK, May 25–31 2026)
- `references/country-filters.md` — Per-source country field names and known country values
- `references/country-dashboards.md` — Country-specific Enterpret dashboard URLs. **Look up this file at the start of every run** to resolve `[ENTERPRET_DASHBOARD_URL]` for the current country. If the country is not listed, fall back to the default: `https://dashboard.enterpret.com/canva-design/`
