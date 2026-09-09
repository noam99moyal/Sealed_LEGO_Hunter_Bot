# Sealed LEGO Hunter

A **Grok Bot** that hunts **factory-sealed LEGO** deals for *your* country.

You configure it once (ship-to, marketplaces, cadence, discount bands, watchlist, benchmarks). Then **this same bot** scans on a schedule and pings you in chat when something hits your bands. It **never auto-buys** and **never messages sellers**.

---

## Download / install

Add the bot from this public template link:

**➡️ [Add Sealed LEGO Hunter](https://x.ai/bot/OBVjf4fwaUTIZT3th9QKp)**

1. Open the link while signed into [x.ai](https://x.ai) / Grok Bot.
2. Add the template to your assistants.
3. Open the new chat — the first-run wizard starts there.

No code to clone for day-to-day use. This repo is documentation + the public template pointer.

---

## How it works

### 1. First-run wizard
On first open the bot asks (one topic at a time):

| Step | What you set |
|------|----------------|
| **Ship-to** | Country, city/region for shipping quotes, currency |
| **Marketplaces** | Which sites to scan (classifieds, peer-to-peer, auction, retail, price comparators). For rate-limited sites, optional watchlist **priority YES/NO** columns |
| **Cadence** | How often (e.g. 1–3× daily), weekdays vs every day, your timezone |
| **Discount bands** | Ignore below X% · negotiate-notify X→under Y% · buy-notify at Y%+ (all vs **landed** price) |
| **Watchlist** | Google Drive sheet (preferred) or paste/CSV in chat |
| **Benchmarks** | Official **LEGO.com** RRP for your country (current sets) · **BrickEconomy** new/sealed for retired (US skew noted) |
| **Defaults** | Sealed-only **on** · failure pings **on** |

After you confirm, the bot writes landed-price formulas for *your* ship-to and creates scan routines **on itself** — no second bot to spin up.

### 2. What each scan does
- Reads your watchlist (`Number`, `Name`, `Watch`; optional priority + Best deal columns).
- On classifieds / P2P / auction sites: searches **three ways** per set — **number-only**, **name-only**, and **combined** (plus local-language name when known) — then merges unique listings. Never only one of number or name. Retail catalogs may use set number alone.
- Matches listings to watchlist rows carefully (set number preferred; reject polybags/lots/wrong numbers/vague theme-only ads).
- Scores **landed price** = item + buyer fees + shipping to your ship-to (per-marketplace; not copied from another country).
- Compares to the right benchmark and acts by band:
  - Below ignore → quiet on that listing
  - Negotiate / buy bands → included in the chat digest (re-reported each scan if still qualifying)
- **Sealed-only**: factory-sealed / MISB; neutralize “never used” style phrases before open/used checks; uncertain listings skipped.
- Updates Drive `Best deal` / `Best link` each scan when a sheet is connected.

### 3. Chat digest & alerts
Qualifying hits use a fixed digest layout (Buy / Negotiate sections, % off + landed vs bench, listing links, 🆕🔁⬆️📉 tags). Failures sit **above** the digest. Full spec: [docs/deal-digest-and-watchlist.md](docs/deal-digest-and-watchlist.md).

### 4. Failure reporting
If a required step fails — anti-bot / captcha / splash wall, HTTP 403/5xx, site down, login needed, sheet unreadable, missing benchmarks — the bot **pings you that run**.

Also fail-loud: if a site returns many ads but almost none pass the sealed filter (`sealed_pass ≈ 0`), that run **pings you**.

Quiet only when every required site completed cleanly and there was nothing new to report (no qualifying deals and no failures).

See [docs/sealed-filter-hygiene.md](docs/sealed-filter-hygiene.md) for sealed-filter rules and regression checklist.

---

## Watchlist shape (Drive default)

| Column | Purpose |
|--------|---------|
| `Number` | Set number |
| `Name` | English set name |
| `Year` | Optional (user context) |
| `Watch` | `YES` / `NO` |
| Market priority (e.g. `eBay`) | `YES` / `NO` for rate-limited sites |
| `Benchmark` | Reference price for % off |
| `Best deal` | Cheapest sealed landed meeting threshold (blank if none) |
| `Best link` | URL for that listing only |

Do **not** add Best % off, Best site, Pricing updated, or official shop URL by default.

Connect **Google Drive** in Grok Bot for the preferred Sheet workflow, or paste a CSV if you prefer.

---

## What this is / isn’t

| Is | Isn’t |
|----|--------|
| A configurable sealed-LEGO deal **hunter** | An auto-buyer |
| Notify-only in chat | Seller DM automation |
| Geography-agnostic until **you** configure it | Locked to one country’s marketplaces |
| Failure-aware (bot walls, sheet errors, zero-pass health checks) | Silent when a required search or filter dies |

---

## Privacy

The public template does **not** ship anyone else’s sheet IDs, logins, or region-specific fee tables. You bring your own ship-to, sites, and watchlist.

---

## Links

- **Install bot:** https://x.ai/bot/OBVjf4fwaUTIZT3th9QKp
- **Digest & watchlist UX:** [docs/deal-digest-and-watchlist.md](docs/deal-digest-and-watchlist.md)
- **Sealed-filter hygiene:** [docs/sealed-filter-hygiene.md](docs/sealed-filter-hygiene.md)
- **Benchmarks:** [LEGO.com](https://www.lego.com) (your local RRP) · [BrickEconomy](https://www.brickeconomy.com) (retired / market reference)
- **This repo:** https://github.com/noam99moyal-sudo/lego-deal-template

---

## License

Docs in this repository are provided as-is for sharing the Grok Bot template. The bot runs on x.ai / Grok Bot; use of the product follows x.ai’s terms.
