# Chat digest & watchlist UX defaults

Reusable defaults for **Sealed LEGO Hunter**. Geography-agnostic. No seller DMs (notify-only in chat).

---

## Chat deal digest

When reporting qualifying sealed deals:

**Title**
```text
## LEGO deals — <local time> (<session>)
```

**One-line counts**
```text
**N buy** (≥ buy threshold) · **M negotiate** (negotiate band) · sealed only
```

**Sections (in order)**
1. Failures / health warnings **above** the digest (short) — blocked marketplace, sealed-funnel health, etc. Never bury them under deals.
2. `### Buy — act if you want it`
3. `### Negotiate (…) `

**Each hit**
- Set number + English name
- `**X% off** · landed **CURRENCY Y** vs bench CURRENCY Z · site · [listing](url)`
- Short listing title
- Tags: `🆕` first · `🔁` still live · `⬆️` band upgrade · `📉` price drop

**Caps**
- ~12 hits per section
- Overflow → update the Drive sheet `Best deal` / `Best link` columns (do not dump endless lists in chat)

**Skip from the digest**
- Junk / false matches: non-LEGO titles, light kits, OEM part-number collisions, wrong-set / polybag / vague theme-only (see sealed-filter hygiene)

---

## Alert policy

- **Re-report** every qualifying sealed deal in chat **each scan**, even if it was shown on previous days (use `🔁` / `🆕` / `⬆️` / `📉` so the user can skim).
- **No seller DMs** in this template (chat notify only; never auto-buy).

---

## Drive watchlist columns (slim)

When using Google Drive for the watchlist, default columns:

| Column | Purpose |
|--------|---------|
| `Number` | Set number |
| `Name` | English set name |
| `Year` | Optional context for the user (scanners may ignore) |
| `Watch` | `YES` / `NO` |
| Market priority (e.g. `eBay`) | `YES` / `NO` for rate-limited marketplaces |
| `Benchmark` | RRP / BrickEconomy reference used for % off |
| `Best deal` | Cheapest **sealed** landed price that meets the user’s discount threshold; **blank if none** |
| `Best link` | URL for that best listing only |

**Do not add by default:** Best % off, Best site, Pricing updated, official shop URL.

**Each scan:** auto-refresh `Best deal` and `Best link` when a Drive sheet is connected.

Optional extra (not required): local-language name column for search.
