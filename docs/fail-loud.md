# Universal fail-loud (every marketplace)

Locked default for **Sealed LEGO Hunter**. Applies to **every** configured marketplace and price comparator — including ones added later. Notify-only (no seller DMs); this is about failure reporting.

## Rule

If **any** marketplace or comparator fails to fetch, parse, login, or return usable data during a deal scan → **ping the user in chat that same run** with:

- what failed
- what they can do (retry login, approve a captcha, check the sheet, etc.)

**Never** stay quiet and treat a blocked/broken site as an empty market.

## Soft vs hard

| Kind | Meaning | Chat |
|------|---------|------|
| **Soft** | Site blocked/broken, but a **documented** fallback or mirror still covered the same offers | List the soft failure **above** the deal digest |
| **Hard** | Site dead with **no** usable fallback | **Always** ping (even if other sites found deals) |

## When quiet is allowed

Quiet **only** when:

1. Every **required** configured site actually **succeeded**, and
2. There are genuinely **no** qualifying sealed hits at/above the user’s discount bands.

If any required site failed (hard) or soft-failed, that run is **not** quiet.

## Also ping

- Many candidates but `sealed_pass ≈ 0` on a site (filter/health bug) — see [sealed-filter-hygiene.md](sealed-filter-hygiene.md)
- Sheet unreadable, missing benchmarks, connector errors

## Scope

Whatever the user configured in the wizard (classifieds, P2P, auction, retail, official LEGO.com locale, comparators, mirrors). **Do not** hard-code a country-specific site list into this rule — it travels with every new marketplace they add.
