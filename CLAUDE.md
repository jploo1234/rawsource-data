# RAWSOURCE.COM — COMPLETE AUTONOMOUS BUILD

## COST CONTROLS
- ONE PASS per page. No loops. No rewrites.
- Read ALL templates ONCE at startup. Cache in memory.
- Extract logo base64 ONCE from calcium-carbonate-FINAL.html. Reuse everywhere.
- Parse rawsource_master_list_v8_2_patched.json ONCE. It is the SINGLE SOURCE OF TRUTH for all chemical data.
- Each task: build, verify, commit, next. Never revisit a completed page.

## AUTO-RESTART PROTOCOL
If context fills or session times out, the wrapper script will relaunch with:
"Read CLAUDE.md. Run: ls *.html | sort to see existing files. Run: git log --oneline -20 to see completed tasks. Then build the NEXT uncompleted task from the task list. Continue until all tasks are done."

## STARTUP SEQUENCE (run ONCE)

1. Read: RAWSOURCE_BUILD_RULES_LATEST.json, PROJECT_INSTRUCTIONS_FINAL.md, INDUSTRY_TAXONOMY_MAPPING.md
2. Extract logo: grep -oP 'data:image/png;base64,[A-Za-z0-9+/=]+' calcium-carbonate-FINAL.html | head -1 > /tmp/logo_uri.txt
3. Study beauty-personal-care-v3.html — this is the GOLD STANDARD for all styling
4. Parse rawsource_master_list_v8_2_patched.json — 1,095 chemicals, 'industries' field is a LIST not a string

## BRAND RULES — ABSOLUTE UNIFORMITY

### CSS Tokens (EXACT :root block for every page):
```css
:root {
  --navy:#0f2035;--navy-deep:#0a1628;--navy-dark:#0a1628;--navy-light:#162a45;--navy-wash:#F0F4FA;
  --accent:#E9A72D;--accent-hover:#D49530;--accent-soft:#FEF6E8;
  --white:#FFFFFF;--off-white:#FAFBFD;--surface:#F4F6F9;--surface-alt:#EDF0F5;
  --text-primary:#1A1F2E;--text-secondary:#4A5568;--text-muted:#7B8599;--text-on-dark:rgba(255,255,255,0.85);
  --border:#D6DCE6;--border-light:#E8ECF2;
  --radius-sm:4px;--radius-md:6px;--radius-lg:10px;--radius-xl:14px;
  --shadow-xs:0 1px 2px rgba(15,42,82,0.04);--shadow-sm:0 1px 4px rgba(15,42,82,0.06);--shadow-md:0 4px 16px rgba(15,42,82,0.08);--shadow-lg:0 8px 32px rgba(15,42,82,0.10);--shadow-xl:0 16px 48px rgba(15,42,82,0.14);
  --font:'Plus Jakarta Sans',-apple-system,sans-serif;--mono:'IBM Plex Mono',monospace;--ease:cubic-bezier(0.22,0.61,0.36,1);
  --badge-available:#2D8A4E;--badge-available-bg:#E8F5ED;--badge-sourcing:#B8860B;--badge-sourcing-bg:#FEF6E8;
}
```

### NEVER USE: DM Sans, JetBrains Mono, #E8A838, #0F2440, radius-lg 8px

### Google Fonts (every page):
```html
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### Logo (from /tmp/logo_uri.txt):
- Header: `<a href="https://rawsource.com" class="logo"><img src="{LOGO_URI}" alt="RawSource" style="height:24px;display:block"></a>`
- Footer: `<img src="{LOGO_URI}" alt="RawSource" style="height:20px">`
- NEVER use text like `<div class="logo-mark">RS</div>` or `<span class="logo-word">`

### Header (every page — match BPC exactly):
```css
.site-header{position:sticky;top:0;z-index:1000;background:var(--navy-dark);padding:0 48px;height:56px;display:flex;align-items:center;justify-content:space-between;gap:32px}
```

### Typography (uniform):
- Hero H1: 36px, weight 800, -0.8px spacing
- Section H2: 24px, weight 700
- Body: 14px, line-height 1.55
- Eyebrow: IBM Plex Mono, 11px, uppercase, 1.2px spacing
- CAS: always var(--mono)

## FOOTER — EVERY PAGE

Must include: base64 logo, address, phone, social icons (YouTube, LinkedIn, Facebook, WhatsApp as gold circles on navy), industry links, product family links, services links, legal links.

```html
<footer class="footer">
<div class="footer-inner">
<div class="footer-grid">
<div class="footer-brand">
  <div class="logo"><img src="{LOGO_URI}" alt="RawSource" style="height:20px"></div>
  <p>Bulk chemicals and ingredients — stocked and globally sourced for manufacturers, formulators, and distributors.</p>
  <div class="footer-addr">515 E Las Olas Blvd, Suite 1301<br>Fort Lauderdale, FL 33301<br>+1 (305) 307-6515</div>
  <div class="footer-social">
    <a href="https://www.youtube.com/@RawSource" aria-label="YouTube"><svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M23.5 6.2a3 3 0 00-2.1-2.1C19.5 3.5 12 3.5 12 3.5s-7.5 0-9.4.6A3 3 0 00.5 6.2 31.3 31.3 0 000 12a31.3 31.3 0 00.5 5.8 3 3 0 002.1 2.1c1.9.6 9.4.6 9.4.6s7.5 0 9.4-.6a3 3 0 002.1-2.1A31.3 31.3 0 0024 12a31.3 31.3 0 00-.5-5.8zM9.6 15.6V8.4l6.3 3.6-6.3 3.6z"/></svg></a>
    <a href="https://www.linkedin.com/company/rawsource" aria-label="LinkedIn"><svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M20.4 20.5h-3.6v-5.6c0-1.3 0-3-1.9-3s-2.1 1.4-2.1 2.9v5.7H9.2V9h3.4v1.6h.1a3.8 3.8 0 013.4-1.9c3.6 0 4.3 2.4 4.3 5.5v6.3zM5.3 7.4a2.1 2.1 0 110-4.2 2.1 2.1 0 010 4.2zM7.1 20.5H3.5V9h3.6v11.5zM22.2 0H1.8C.8 0 0 .8 0 1.7v20.6c0 .9.8 1.7 1.8 1.7h20.4c1 0 1.8-.8 1.8-1.7V1.7c0-.9-.8-1.7-1.8-1.7z"/></svg></a>
    <a href="https://www.facebook.com/RawSourceChemicals" aria-label="Facebook"><svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M24 12a12 12 0 10-13.9 11.9v-8.4H7.1V12h3V9.4c0-3 1.8-4.7 4.5-4.7 1.3 0 2.7.2 2.7.2v3h-1.5c-1.5 0-2 .9-2 1.9V12h3.3l-.5 3.5h-2.8v8.4A12 12 0 0024 12z"/></svg></a>
    <a href="https://wa.me/13053076515" aria-label="WhatsApp"><svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M17.5 14.4l-2-1c-.3-.1-.5-.2-.7.2l-1 1.2c-.2.2-.3.3-.6.1s-1.2-.4-2.3-1.4a8.6 8.6 0 01-1.6-2c-.2-.3 0-.4.1-.6l.4-.4.3-.4v-.5l-1-2.2c-.2-.6-.5-.5-.7-.5h-.6a1.1 1.1 0 00-.8.4 3.5 3.5 0 00-1.1 2.6c0 1.5 1.1 3 1.3 3.2s2.2 3.3 5.3 4.7a17.8 17.8 0 001.8.7 4.3 4.3 0 002 .1c.6-.1 2-.8 2.2-1.6s.3-1.5.2-1.6-.3-.2-.6-.4zM12 21.8a9.9 9.9 0 01-5-1.4l-.4-.2-3.7 1 1-3.6-.3-.4a9.9 9.9 0 1115.3-8.5 9.9 9.9 0 01-6.9 13.1zM12 0a12 12 0 00-10.4 18L0 24l6.2-1.6A12 12 0 1012 0z"/></svg></a>
  </div>
</div>
<div class="footer-col"><h5>Industries</h5>
  <a href="/industries/water-treatment/">Water Treatment</a>
  <a href="/industries/oil-and-gas/">Oil, Gas &amp; Mining</a>
  <a href="/industries/coatings-and-construction/">Coatings &amp; Construction</a>
  <a href="/industries/beauty-and-personal-care/">Personal Care &amp; Cosmetics</a>
  <a href="/industries/industrial-manufacturing/">Industrial Manufacturing</a>
  <a href="/industries/agriculture/">Agriculture</a>
  <a href="/industries/textiles/">Textiles</a>
  <a href="/home-care-institutional-industrial-cleaning/">Home &amp; Industrial Care</a>
</div>
<div class="footer-col"><h5>Product Families</h5>
  <a href="/silicones/">Silicones &amp; Silanes</a><a href="#">Surfactants &amp; Emulsifiers</a><a href="#">Solvents &amp; Glycols</a><a href="#">Amines &amp; Intermediates</a><a href="#">Polymers &amp; Resins</a><a href="#">Additives &amp; Modifiers</a><a href="#">Acids &amp; Inorganics</a><a href="#">Polyols &amp; Isocyanates</a>
</div>
<div class="footer-col"><h5>Services</h5>
  <a href="/services/supply-chain/">Supply Chain Solutions</a><a href="/services/blending/">Chemical Customization</a><a href="/technical-support-for-chemical-products/">Quality &amp; Documentation</a><a href="/contact-us/">Request Bulk Quote</a>
</div>
</div>
<div class="footer-bottom">
  <div class="footer-copy">&copy; 2026 RawSource&reg;. All rights reserved.</div>
  <div class="footer-legal"><a href="/privacy-policy/">Privacy Policy</a><a href="/terms-and-conditions/">Terms of Use</a></div>
</div>
</div>
</footer>
```

Footer CSS:
```css
.footer{background:var(--navy-dark);border-top:1px solid rgba(255,255,255,0.04)}
.footer-inner{max-width:1400px;margin:0 auto;padding:52px 40px 40px}
.footer-grid{display:grid;grid-template-columns:1.4fr repeat(3,1fr);gap:40px;margin-bottom:40px}
.footer-brand{max-width:260px}
.footer-brand .logo{margin-bottom:12px}
.footer-brand .logo img{height:20px}
.footer-brand>p{font-size:12px;color:rgba(255,255,255,0.3);line-height:1.6}
.footer-addr{margin-top:12px;font-family:var(--mono);font-size:10px;color:rgba(255,255,255,0.2);line-height:1.6}
.footer-social{display:flex;gap:10px;margin-top:16px}
.footer-social a{display:flex;align-items:center;justify-content:center;width:32px;height:32px;border-radius:50%;background:var(--accent);color:var(--navy-dark);transition:all .2s}
.footer-social a:hover{background:var(--accent-hover);transform:translateY(-1px)}
.footer-col h5{font-size:10px;font-weight:700;color:rgba(255,255,255,0.25);text-transform:uppercase;letter-spacing:1px;margin-bottom:14px}
.footer-col a{display:block;font-size:12px;color:rgba(255,255,255,0.4);padding:3px 0;text-decoration:none;transition:color .12s}
.footer-col a:hover{color:rgba(255,255,255,0.7)}
.footer-bottom{padding-top:20px;border-top:1px solid rgba(255,255,255,0.04);display:flex;justify-content:space-between;align-items:center}
.footer-copy{font-size:11px;color:rgba(255,255,255,0.2)}
.footer-legal{display:flex;gap:16px}
.footer-legal a{font-size:11px;color:rgba(255,255,255,0.2);text-decoration:none}
```

## TASK LIST

### TASK 0: Fix product-catalog-v5__22.html
12 brand violations to fix in single pass:
1. Replace 'DM Sans',system-ui,sans-serif with 'Plus Jakarta Sans',-apple-system,sans-serif
2. Replace 'JetBrains Mono',monospace with 'IBM Plex Mono',monospace
3. Replace Google Fonts import DM+Sans/JetBrains+Mono with Plus+Jakarta+Sans/IBM+Plex+Mono
4. Replace ALL #E8A838 with #E9A72D
5. Replace #D4952E with #D49530
6. Replace #0F2440 with #0a1628
7. Replace --navy:#1F4788 with --navy:#0f2035
8. Replace --navy-light:#2B5BA0 with --navy-light:#162a45
9. Fix radius vars to match BPC (--radius-sm:4px;--radius-md:6px;--radius-lg:10px;--radius-xl:14px)
10. Remove .logo-mark and .logo-word HTML/CSS, replace header with BPC pattern using base64 logo img
11. Add full footer with address/phone/social icons before closing body tag
12. Add all missing BPC CSS vars (shadows, badge colors, surfaces)

ALSO: Rebuild the product data array from rawsource_master_list_v8_2_patched.json. Write a Python script to parse the master JSON and regenerate the const D=[...] array so every chemical matches the master exactly. The master JSON is truth.

Commit: "fix product catalog — brand alignment + master JSON sync"

### TASKS 1-6: Level 1 Landing Pages
Template: beauty-personal-care-v3.html structure exactly.
Each page: header, breadcrumbs, hero (with Nano Banana image), tabs, Door A/B/C, RFQ sidebar, bottom CTA, full footer.
Chemical data from rawsource_master_list_v8_2_patched.json filtered by industry.

Task 1: water-treatment-v1.html — /industries/water-treatment/ — "Water Treatment" — 213 chems
Task 2: coatings-construction-v1.html — /industries/coatings-and-construction/ — "Coatings & Construction" — 261
Task 3: textiles-v1.html — /industries/textiles/ — "Textiles" — 163
Task 4: home-industrial-care-v1.html — /home-care-institutional-industrial-cleaning/ — "HI&I Cleaning" — 382
Task 5: industrial-manufacturing-v1.html — /industries/industrial-manufacturing/ — "Industrial Manufacturing" — 328
Task 6: plastics-polymers-v1.html — /industries/plastics-polymers/ — "Plastics & Polymers" — 284

Product links: /shop/{slug}/ with trailing slash. Extract slug from source_url field.

Nano Banana prompts (env: NANO_BANANA_API_KEY):
- Water Treatment: "Cinematic industrial water treatment plant at twilight, crystal water through steel membrane filters, blue-teal palette, shallow DOF, editorial, no text no people"
- Coatings: "Macro of industrial coating applied to brushed aluminum, amber and navy tones, liquid texture, dramatic sidelight, editorial, no text no people"
- Textiles: "Close-up premium woven textile under finishing treatment, chemical sheen on threads, soft-focus loom background, neutral gold tones, editorial, no text no people"
- HI&I: "Overhead formulation lab bench, glass flasks with clear surfactant solutions, stainless steel, clinical blue-white, editorial, no text no people"
- Industrial Mfg: "Low-angle CNC metalworking with coolant mist and sparks, navy ambient gold accent, industrial editorial, no text no people"
- Plastics: "Macro translucent polymer pellets from stainless hopper, warm amber light, shallow DOF, manufacturing editorial, no text no people"

If Nano Banana unavailable, use CSS gradient fallback matching BPC hero-visual-inner.

### TASKS 7-13: Level 2 Solution Detail Pages
Template: solution-detail-agriculture-FIXED.html depth + solution-detail-ogm.html structure.
Same header/footer as L1 pages.

Task 7: solution-detail-water-treatment.html
Task 8: solution-detail-coatings-construction.html
Task 9: solution-detail-textiles.html
Task 10: solution-detail-home-industrial-care.html
Task 11: solution-detail-industrial-manufacturing.html
Task 12: solution-detail-plastics-polymers.html
Task 13: solution-detail-beauty-personal-care.html (L1 exists, L2 missing. 835 chemicals.)

### TASK 14: Final Verification + Security Audit

Run these checks:
```bash
# Brand violations (must all return 0):
grep -rl "DM Sans" *.html | grep -v node_modules | wc -l
grep -rl "DM+Sans" *.html | wc -l
grep -rl "JetBrains" *.html | wc -l
grep -rl "#E8A838" *.html | wc -l
grep -rl "logo-mark" water-treatment* coatings* textiles* home-industrial* industrial-manufacturing* plastics* solution-detail-water* solution-detail-coatings* solution-detail-textiles* solution-detail-home-industrial* solution-detail-industrial* solution-detail-plastics* solution-detail-beauty-personal-care* product-catalog* | wc -l
grep -rl "Â°" *.html | wc -l

# Required elements in new pages:
for f in water-treatment-v1.html coatings-construction-v1.html textiles-v1.html home-industrial-care-v1.html industrial-manufacturing-v1.html plastics-polymers-v1.html product-catalog-v5__22.html; do
  echo "=== $f ==="
  grep -c "Plus Jakarta Sans" "$f"
  grep -c "#E9A72D" "$f"
  grep -c "515 E Las Olas" "$f"
  grep -c "307-6515" "$f"
  grep -c "footer-social" "$f"
  grep -c "data:image/png;base64," "$f"
done

# Dead link check:
grep -ohP 'href="[^"]*"' *.html | sort -u | grep -v "^href=\"#\"$" | grep -v "javascript:" | grep -v "mailto:" > /tmp/all_links.txt
echo "Total unique links: $(wc -l < /tmp/all_links.txt)"
# Check internal links have trailing slashes:
grep -P 'href="/[^"]*[^/]"' *.html | grep -v "\.css\|\.js\|\.png\|\.jpg" && echo "WARNING: links without trailing slash found" || echo "OK: all internal links have trailing slashes"

# Security check:
grep -rl "eval(" *.html | wc -l  # should be 0
grep -rl "document.write" *.html | wc -l  # should be 0
grep -rl "innerHTML.*<script" *.html | wc -l  # should be 0
# Check no hardcoded API keys:
grep -rl "sk-ant-\|BANANA.*=" *.html | wc -l  # should be 0
```

Fix any failures. Commit: "final verification — all pages pass brand + security audit"

## DO NOT STOP UNTIL ALL 15 TASKS (0-14) ARE COMPLETE.
