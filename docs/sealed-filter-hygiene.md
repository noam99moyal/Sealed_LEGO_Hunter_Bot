# Sealed-filter hygiene (marketplace-agnostic)

Defaults for **Sealed LEGO Hunter**. Apply to whatever marketplaces the user configured (eBay, Vinted, local classifieds, retail, price comparators, etc.). **No site-specific integrations** — these rules are language- and marketplace-agnostic.

## 1. Never-used false positives

Open/used hard-skips must **not** fire on “never used” style wording.

**Before** checking for used/opened/incomplete tokens:

1. Neutralize (strip or mask) phrases that mean *new / unused*, in each language you support for that marketplace — e.g. `never used`, `unused`, `never worn`, `brand new unused`, and local equivalents that embed a “used” stem inside a negation.
2. Only then apply real used/opened hard-skips on the remaining text.

Naive substring matches on a bare “used” stem (any language) will false-positive NEW-in-box ads and official NEW/unused condition chips.

Still hard-skip after neutralization when the text clearly means opened, incomplete, built, or used-as-opened.

## 2. Listing → watchlist matching

Do **not** score wrong products onto a watchlist row (polybag, different set number, bare theme name).

Prefer:

- **Require the target set number**, **or**
- Distinctive name tokens **and** no *foreign* set number present.

Reject:

- Lots / multipacks without the target number
- Polybags / foil packs / GWP when the watchlist row is a boxed set (unless that row *is* the polybag)
- Vague theme-only ads (franchise name only) with no number and no unique set name

## 3. Fail-loud health check

If a marketplace returns **many** candidate ads but `sealed_pass ≈ 0` for that site/run → **ping the user that run**. Never stay quiet as if the market is empty. Treat it as a likely filter bug or site change.

This sits alongside existing failure pings (bot walls, 403s, sheet/login/benchmark failures).

---

## Regression checklist

Use these as “must pass / must fail” cases when changing sealed or match logic.

### New / sealed chips that must PASS (after neutralization)

| Case | Why |
|------|-----|
| Title/body: “never used”, “unused”, “never worn” | Negation must not count as used |
| Local “never used” that contains a used-stem (any language you support) | Same class of bug |
| Official condition chip: unused / never worn / new-in-box style | Chip means NEW |
| “Factory sealed” / “MISB” / local sealed synonym + no opened language | True sealed |
| Stock photos + sealed claim in description, no opened language | Description wins |

### Open / used that must FAIL (skip)

| Case | Why |
|------|-----|
| “Opened”, “built”, “incomplete”, “no box”, “minifigs only” | Clearly not MISB boxed set |
| “New without tags” style chips that mean opened apparel/toys | Not factory-sealed box |
| Real used/opened after never-used phrases are neutralized | Residual used signal |
| Contradicting text: sealed claim + “opened once” | Hard-skip |

### Wrong-set match that must FAIL

| Case | Why |
|------|-----|
| Different set number in title vs watchlist row | Wrong product |
| Polybag / foil pack for a boxed-set watchlist row | Wrong format |
| Lot / GWP / “with free …” without target number | Not the set |
| Bare theme/franchise name only | Too vague |
| Distinctive name tokens **plus** a foreign set number | Prefer reject |

### Health check that must PING

| Case | Why |
|------|-----|
| Marketplace: 20+ candidates, `sealed_pass = 0` | Likely filter bug |
| Site blocked / 403 / captcha | Existing fail-loud |
