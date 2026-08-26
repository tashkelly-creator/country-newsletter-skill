# Slack Output Example — UK, May 25–31 2026

This is the target format for the single Slack message. Use it as a reference for tone, structure, and density.

---

## Single Slack Message

> **UK Weekly Feedback · May 25 – 31, 2026**
> 3,901 items · vs 4,360 prior (−10.5%) · 14 sources
>
> **AI Prompt Quality Drove a Mon 26 May Spike — Volume Returned to Prior-Week Levels by Sat 30 May**
> Two AI themes (prompt non-adherence +45%, output quality +47%) drove the spike — desktop-dominated (85%), cross-tier. Volume returned to baseline by Saturday.
>
> ---
> **Priority UK Findings**
>
> **SPIKE [216 records](https://enterpret.com/record/abc123) · +45% WoW · Global Rank #2**
> **[AI Prompt Non-Adherence](https://enterpret.com/record/abc124)**
> Sharp onset Mon 26 May (57 complaints vs 26–36 baseline), elevated 27–29 May, back to baseline by 30 May. 85% desktop/web. Affects Free, Pro Solo, Business, Teams proportionally. Profile consistent with a backend deployment corrected or partially rolled back.
> > "this ai never listens to what you actually putting in a prompt!" — UK customer [link](https://enterpret.com/record/abc125)
>
> **SPIKE [162 records](https://enterpret.com/record/abc126) · +47% WoW · Global Rank #4**
> **[AI Output Quality (Brand/Prompt Adherence)](https://enterpret.com/record/abc127)**
> Same temporal profile and segment mix as the prompt-non-adherence theme — different taxonomic angle, same underlying event. Wrong text, unrelated images, brand guidance ignored.
> > "it got all the text wrong, used a completely different cover from my upload and didn't follow instructions" — UK customer [link](https://enterpret.com/record/abc128)
>
> **ELEVATED [89 records](https://enterpret.com/record/abc129) · +8% WoW · UK Rank #5 · Global Rank #18**
> **[Print Delivery Delays](https://enterpret.com/record/abc130)**
> Disproportionately high in UK vs global. Order tracking complaints and missed delivery windows. No spike — steady elevated presence over 3+ weeks.
> > "ordered 10 days ago and still nothing, tracking hasn't updated since Wednesday" — UK customer [link](https://enterpret.com/record/abc131)
>
> **LOCAL [56 records](https://enterpret.com/record/abc132) · −14% WoW · NOT in Global top 10**
> **[Ownership Verification](https://enterpret.com/record/abc133)**
> Account-recovery friction. Declining WoW. UK-specific edge case; volume still meaningful.
>
> **WATCH [41 records](https://enterpret.com/record/abc134) · +19% WoW**
> **[Export Quality — PDF](https://enterpret.com/record/abc135)**
> Below spike threshold but trending up. Worth monitoring next week.
>
> ---
> **UK vs Global Product Area Share**
> After mutually exclusive priority-bucket assignment across 1,548 UK records vs 60,616 global records this week:
> [Billing](https://enterpret.com/record/abc136) UK 36.7% · Global 21.6% (+15.1 pp)
> [Account](https://enterpret.com/record/abc137) UK 22.1% · Global 7.3% (+14.8 pp)
> [AI](https://enterpret.com/record/abc138) UK 10.2% · Global 8.8% (+1.4 pp)
> [Print](https://enterpret.com/record/abc139) UK 21.0% · Global 11.7% (+9.3 pp)
> [Editor](https://enterpret.com/record/abc140) UK 12.8% · Global 10.0% (+2.8 pp)
> [Other](https://enterpret.com/record/abc141) UK 7.4% · Global 50.4% (−43.0 pp)
>
> ---
> **Churn · 102 responses (+34% WoW)**
> ⓘ *Churn data inferred from locale: en-GB. Counts are directional — see artifact for full breakdown.*
> [Pricing Too High for Value](https://enterpret.com/record/abc142): 8 this week · 9 prior · −1 · UK pounds and cost-of-living language recurs
> [General Complaint About Canva](https://enterpret.com/record/abc143): 12 this week · 13 prior · −1
> [Pushback Against AI Emphasis](https://enterpret.com/record/abc144): 2 this week · new theme · NEW
> > "Can you kindly make it cheaper. I would have love to keep a Pro if it was 7, 8 pound per month or have unlimited AI usage." — UK churner, Pro Solo [link](https://enterpret.com/record/abc145)
>
> ---
> **🚨 Incidents & rollouts**
> No incidents or rollout posts in `#rollouts-canva` or `#incident` overlapping this week's spike window.
>
> ---
> **Source coverage**
> 14 of 16 sources returned UK data, filtered on `zendesksupport_customfields_country CONTAINS 'United Kingdom'`. Top sources: ZendeskSupport 1,383 · Canva AI (PFP) 696 · Submit A Wish 640 · Product Feedback 390 · Churn Survey 329.
> Coverage gaps: Twitter, Reddit, Discord, Playstore lack country metadata — coverage gap, not absence of UK signal.

---

## Key Formatting Notes

- **One message only** — everything above is a single Slack message, not split across two
- Record links point to **individual Enterpret records** (e.g. `/record/[uuid]`) — not citations pages
- Theme names are linked to a representative record, not a citations page
- **SPIKE**, **ELEVATED**, **LOCAL**, **WATCH** tags appear in bold before the record count — they are visual anchors
- "Self-resolved" is prohibited — use "Volume returned to prior-week levels by [date]"
- Verbatim quotes are indented as block quotes with the customer's plan type where known
- WoW deltas use `+X%` / `−X%` for % changes and `+X pp` / `−X pp` for percentage point changes
- Confidence level is implicit in phrasing — "consistent with", "likely same underlying event", "implies" = Medium/Low; "driven by" = High
- **AI is its own product area** — never grouped into Other
- Churn section always includes the inference callout (locale or currency) when shown
- Incidents & rollouts section always appears — "no overlap found" if nothing flagged
- Source methodology references the actual field used (`zendesksupport_customfields_country`), not "UF Country"
