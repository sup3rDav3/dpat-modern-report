# DPAT Modern Report

A single-script patcher that modernizes the HTML report output of the
[DPAT module](https://github.com/knavesec/Max) in knavesec/Max.


## What it changes

| Feature | Detail |
|---|---|
| **Dark theme** | GitHub-inspired palette, Space Grotesk + IBM Plex Mono fonts |
| **Stat cards** | Total Cracked, Domain Admins, Kerberoastable, High Value — populated at runtime from the summary table |
| **Sidebar navigation** | All 14 sections linked to their detail pages |
| **Severity pills** | Critical / High / Medium / Low / None labels on every summary row |
| **Section cards** | Each detail table wrapped in a card with a title and row count |
| **Self-contained** | CSS is embedded — no separate `report.css` needed |
| **Print friendly** | Clean black-on-white stylesheet for `Ctrl+P` / PDF export |

## Install

```bash
# 1. Clone Max as normal
git clone https://github.com/knavesec/Max.git
cd Max

# 2. Drop the patcher in
cp /path/to/patch_max.py .

# 3. Run it once
python3 patch_max.py
```

Expected output:
```
[+] Backed up max.py → max.py.bak
[+] Patch 1: modern HTML shell with embedded CSS + JS
[+] Patch 2: flag summary page for stat cards
[+] Patch 3: wrap tables in section cards with row counts
[✓] Done — 3 applied, 0 skipped.
```

## Usage

Run `max.py dpat` exactly as you normally would — no flags change:

```bash
python3 max.py dpat \
  -n ntds.dit \
  -c hashcat.potfile \
  -o outputdir \
  --html \
  --sanitize
```

Open `outputdir/Report.html` in any browser.

## Uninstall

```bash
cp max.py.bak max.py
```

## Notes

- Running the patcher twice on an already-patched file does nothing
- If a patch step shows `SKIPPED`, the upstream source has changed slightly in that area; the rest of the patches still apply and the report will still look modern
- The sidebar links point to the filenames the tool generates — if a category has zero results the detail page will exist but show an empty table
