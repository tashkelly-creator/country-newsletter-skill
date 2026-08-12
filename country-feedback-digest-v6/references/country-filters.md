# Country Filter Reference

## CRITICAL: Never use bracket notation

Do NOT use `nli.metadata['UF Country']` — bracket notation causes a TranslationError. Always use dot notation with source-specific field names from the table below.

---

## Per-Source Country Field Reference

| Source | Field name | Usage |
|--------|-----------|-------|
| `ZendeskSupport` | `nli.zendesksupport_customfields_country` | `CONTAINS '[COUNTRY]'` |
| `ZendeskSupport` (fallback 1) | `nli.zendesksupport_country_full_name` | `CONTAINS '[COUNTRY]'` |
| `ZendeskSupport` (fallback 2) | `nli.zendesksupport_user_country` | `CONTAINS '[COUNTRY]'` |
| `Webhook-Ask Canva Submit A Wish` | `nli.webhook_ask_canva_submit_a_wish_country_full_name` | `CONTAINS '[COUNTRY]'` |
| `Appstore` | `nli.appstore_country_full_name` | `CONTAINS '[COUNTRY]'` |
| `FileUpload-Canva Pro/Teams Churn Survey` | No direct country field — infer via locale/currency (see below) | — |
| `FileUpload-Product Feedback Platform` | No reliable country field — returns 0 for most countries | Flag as coverage gap |
| `FileUpload-Always On Product Feedback` | No reliable country field | Flag as coverage gap |
| `FileUpload-Canva AI (PFP)` | No reliable country field | Flag as coverage gap |
| `Playstore` | No reliable country field | Flag as coverage gap |
| `Twitter` | No country metadata | Flag as coverage gap |
| `Reddit` | No country metadata | Flag as coverage gap |
| `Discord` | No country metadata | Flag as coverage gap |
| `Trustpilot` | No country field — but record locale often infers country | Use for quotes, not volume counts |

**Run one source per query.** A ZendeskSupport query with `zendesksupport_customfields_country` will not filter records from other sources.

---

## Country Name & Locale Reference

| Country | ZendeskSupport value | Submit A Wish value | App Store value | Locale | Currency |
|---------|---------------------|--------------------|-----------------|----|-----|
| United Kingdom | `United Kingdom` | `United Kingdom` | `GBR` or `United Kingdom` | `en-GB` | `GBP` |
| Australia | `Australia` | `Australia` | `AUS` or `Australia` | `en-AU` | `AUD` |
| United States | `United States` | `United States` | `USA` or `United States` | `en-US` | `USD` |
| Indonesia | `Indonesia` | `Indonesia` | `IDN` or `Indonesia` | `id-ID` | `IDR` |
| Japan | `Japan` | `Japan` | `JPN` or `Japan` | `ja-JP` | `JPY` |
| Germany | `Germany` | `Germany` | `DEU` or `Germany` | `de-DE` | `EUR`* |
| France | `France` | `France` | `FRA` or `France` | `fr-FR` | `EUR`* |
| Brazil | `Brazil` | `Brazil` | `BRA` or `Brazil` | `pt-BR` | `BRL` |
| India | `India` | `India` | `IND` or `India` | `en-IN` | `INR` |
| Canada | `Canada` | `Canada` | `CAN` or `Canada` | `en-CA`, `fr-CA` | `CAD` |
| Mexico | `Mexico` | `Mexico` | `MEX` or `Mexico` | `es-MX` | `MXN` |
| Spain | `Spain` | `Spain` | `ESP` or `Spain` | `es-ES` | `EUR`* |
| Singapore | `Singapore` | `Singapore` | `SGP` or `Singapore` | `en-SG` | `SGD` |
| Philippines | `Philippines` | `Philippines` | `PHL` or `Philippines` | `fil-PH` | `PHP` |
| South Korea | `South Korea` | `South Korea` | `KOR` or `South Korea` | `ko-KR` | `KRW` |
| Netherlands | `Netherlands` | `Netherlands` | `NLD` or `Netherlands` | `nl-NL` | `EUR`* |

*EUR is shared across all EU countries — do not use currency alone as a churn filter for these markets. Use locale only.

---

## Churn Survey — Country Inference

The churn source has no direct country field. Infer from locale or currency:

1. Run a schema probe on first use to find available fields:
```cypher
MATCH (nli:NaturalLanguageInteraction)
WHERE nli.source = 'FileUpload-Canva Pro/Teams Churn Survey'
RETURN keys(nli) AS available_fields LIMIT 1
```
2. Look for fields containing: `locale`, `currency`, `billing_country`, `language`, `region`
3. Filter using locale first (more precise), then currency as fallback
4. For EU markets (FR, DE, ES, NL) — locale only, never EUR as sole filter
5. If both return 0, omit churn section entirely — do not substitute global data

---

## ZendeskSupport: If All Fields Return 0

Try in order:
1. `nli.zendesksupport_customfields_country CONTAINS '[COUNTRY]'`
2. `nli.zendesksupport_country_full_name CONTAINS '[COUNTRY]'`
3. `nli.zendesksupport_user_country CONTAINS '[COUNTRY]'`

If all three return 0, stop and notify the manager — do not deliver a report with no data.
