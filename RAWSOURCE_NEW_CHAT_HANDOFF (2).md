# RAWSOURCE PROJECT — NEW CHAT HANDOFF

## WHAT THIS PROJECT IS

RawSource (rawsource.com) is a specialty chemical distributor in Fort Lauderdale, FL. We're rebuilding their entire website from the data layer up. The site runs on WordPress + WooCommerce. We are building static HTML pages that deploy ON TOP of the existing WordPress infrastructure at the exact same URLs — preserving 100% of SEO progress. Zero broken links. Zero orphaned pages.

---

## GITHUB REPO — THE SINGLE SOURCE OF TRUTH

**Repo:** `jploo1234/rawsource-data` (private)
**Raw URL pattern:** `https://raw.githubusercontent.com/jploo1234/rawsource-data/main/{filename}`

### Files in the repo:

| File | What it is | Size |
|---|---|---|
| `rawsource_master_list_v8_2_patched.json` | THE master data — 1,095 chemicals with full PubChem/CosIng enrichment | ~4.8 MB |
| `RAWSOURCE_BUILD_RULES.json` | Complete rules: brand, taxonomy, SEO, hierarchy, field maps, mistakes to avoid | ~30 KB |
| `calcium-carbonate-FINAL.html` | ✅ APPROVED product page template (the gold standard) | Reference |
| `rawsource-homepage-final.html` | ✅ APPROVED homepage | Reference |

### How to use the repo:

1. **ALWAYS fetch `RAWSOURCE_BUILD_RULES.json` first** — it has everything: brand colors, fonts, logo rules, taxonomy, SEO preservation rules, page hierarchy, field mapping, and previous mistakes to avoid
2. **Fetch the master JSON only when you need chemical data** — it's 4.8MB, so fetch it selectively (or fetch and parse in code)
3. **Fetch approved templates when building new pages** — to match exact patterns

### Fetch commands:
```
web_fetch: https://raw.githubusercontent.com/jploo1234/rawsource-data/main/RAWSOURCE_BUILD_RULES.json
web_fetch: https://raw.githubusercontent.com/jploo1234/rawsource-data/main/rawsource_master_list_v8_2_patched.json
web_fetch: https://raw.githubusercontent.com/jploo1234/rawsource-data/main/calcium-carbonate-FINAL.html
web_fetch: https://raw.githubusercontent.com/jploo1234/rawsource-data/main/rawsource-homepage-final.html
```

---

## WHAT'S DONE vs WHAT'S PENDING

### ✅ DONE
- **1,095 product pages** at `/product/{slug}/` — fully built, approved template
- **Homepage** — approved
- **Master JSON** — 1,095 chemicals, PubChem + CosIng enriched, classified into locked taxonomy
- **Build rules file** — 30KB compact reference with everything needed
- **3 industry landing pages** (templates exist, need branding fixes): Agriculture, Oil & Gas, Beauty & Personal Care
- **Industry inner pages** (solution detail + family detail templates exist for Agriculture and Oil & Gas)

### 🔨 IN PROGRESS / NEXT
- **Catalog page (`/shop/`)** — must use the v5 catalog template (`product-catalog-v5__2_.html`) with correct branding. All 1,095 chemicals must be perfectly categorized, filterable, and every card must link to its inner product page with zero empty values
- **Remaining 10 industry pages** — follow the Door A/B/C pattern documented in build rules
- **Subsystem gap closure** — most industries have <50% subsystem coverage

---

## CRITICAL SEO PRESERVATION RULES

This is the most important section. The live site has DIFFERENT URL slugs than what we used in development templates. These mismatches would destroy SEO if deployed.

### Live URLs vs Wrong Dev Slugs:

| What's LIVE on rawsource.com | WRONG dev slug (NEVER USE) |
|---|---|
| `/industries/oil-and-gas/` | ~~oil-gas-mining~~ |
| `/industries/beauty-and-personal-care/` | ~~beauty-personal-care~~ |
| `/industries/coatings-and-construction/` | ~~coatings-construction~~ |
| `/home-care-institutional-industrial-cleaning/` | ~~hii-cleaning~~ |

### Locked Industry Slugs (must match live site EXACTLY):
```
/industries/oil-and-gas/
/industries/agriculture/
/industries/beauty-and-personal-care/
/industries/coatings-and-construction/
/industries/textiles/
/industries/lubricants/
/industries/water-treatment/
/home-care-institutional-industrial-cleaning/     ← NOTE: root-level, NOT under /industries/
```

### New industries (no existing URL — create fresh):
```
/industries/plastics-polymers/
/industries/food-beverage/
/industries/pharmaceuticals/
/industries/industrial-manufacturing/
/industries/mining/
```

### Product page slugs: 885 chemicals have existing WooCommerce URLs — those slugs are LOCKED FOREVER. Never change them. 209 newer chemicals use generated slugs.

### Existing sub-pages that are LIVE and INDEXED (must keep or 301 redirect):
- Oil & Gas: `/antifoam/`, `/gas-sweetening/`
- Agriculture: `/the-right-ingredients-for-your-agricultural-needs/`, `/biotechnology-and-genetic-engineering/`, `/nutrition-products-for-crops/`
- Beauty: `/skin-care/`, `/color-and-makeup/`, `/hair-care/`
- Coatings: `/paints-and-graphic-ink/`, `/construction/`, `/roof-coatings/`
- Textiles: `/textile-finishing/`, `/textile-softening/`, `/textile-waterproofing/`
- Lubricants: `/industrial-machinery-ensuring-reliability/`, `/marine-protecting-against-corrosion/`, `/energy-optimizing-performance/`
- Water: `/coagulation-and-flocculation-in-water-treatment/`, `/water-disinfection-ensuring-safe-and-clean-water/`, `/ph-adjustment-in-water-treatment-balancing-act-for-quality-water/`
- HI&I: `/automotive/`, `/bathroom/`, `/hard-surface/`

### WooCommerce category pages (keep or redirect):
```
/product-category/amines/
/product-category/acids/
/product-category/sodium-salts/
/product-category/Alcohol/
/product-category/Esters/
/product-category/Solvents/
/product-category/Surfactants/
/product-category/silicones/silanes/
```

### DO NOT TOUCH (service pages stay as-is):
```
/services/
/services/supply-chain/
/services/blending/
/technical-support-for-chemical-products/
/order-now/
/contact-us/
```

---

## BRAND SYSTEM — QUICK REFERENCE

(Full details in `RAWSOURCE_BUILD_RULES.json`)

### Colors:
- **Navy Dark:** `#0C1E3D` (header, footer, hero backgrounds)
- **Navy:** `#1F4788` (borders, secondary backgrounds)
- **Gold:** `#E9A72D` (CTAs, accents, highlights) — **NOT #E8A838**
- **Gold Hover:** `#D49530`

### Fonts:
- **Primary:** `Plus Jakarta Sans` — **NOT DM Sans** (all industry templates currently have the wrong font)
- **Mono:** `IBM Plex Mono` — CAS numbers, chemical formulas, code-like content

### Logo:
- Format: Base64-encoded transparent PNG (320×58px)
- Header: `<img>` tag, height 24px, `display:block`
- Footer: `<img>` tag, height 20px
- NEVER use the "RS" square placeholder found in industry templates
- NEVER place on gold background (invisible)
- Extract exact base64 string from `calcium-carbonate-FINAL.html`

### Voice:
- Confident, technical, zero fluff
- Use precise chemistry language
- Banned words: "innovative," "world-class," "cutting-edge," "synergy," "leverage," "solutions" (as noun)

---

## LOCKED TAXONOMY

### Material Families (18 in build rules, 26 in full list):
Silicone Fluids & Oils, Silicone Emulsions, Silicone Surfactants, Silicone Gum Blends, Silanes & Organosilanes, Amines & Amine Derivatives, Polyetheramines, Glycols & Glycol Ethers, Surfactants — Anionic, Surfactants — Nonionic, Surfactants — Cationic, Surfactants — Amphoteric, Acids & Salts, Esters & Emollients, Resins & Polymers, Isocyanates, Polyols & Polyol Intermediates, Monomers & Reactive Diluents, Solvents, Pigments & Colorants, Fillers & Extenders, Natural Extracts & Botanicals, Preservatives & Biocides, Phosphonates & Scale Inhibitors, Rheology Modifiers, Specialty Additives

### Industries (13):
Agriculture, Oil & Gas, Mining, Coatings & Construction, Textiles, HI&I Cleaning, Water Treatment, Beauty & Personal Care, Food & Beverage, Pharmaceuticals, Lubricants, Plastics & Polymers, Industrial Manufacturing

### Functional Roles (25+ in build rules):
See `RAWSOURCE_BUILD_RULES.json` for the complete locked list.

**These enums are FINAL. No new values without explicit approval. No variations, synonyms, or free text.**

---

## CRITICAL BRANDING FIXES NEEDED

ALL uploaded industry template HTML files contain these 4 WRONG values that must be fixed in every build:

1. **Wrong font:** `DM Sans` → must be `Plus Jakarta Sans`
2. **Wrong gold:** `#E8A838` → must be `#E9A72D`
3. **Wrong logo:** `<div class="logo-mark">RS</div>` → must be `<img>` with base64 PNG from approved template
4. **Encoding artifacts:** `Â°F` → must sanitize to `°F` (UTF-8 mojibake from WooCommerce)

---

## PAGE HIERARCHY — 4 LEVELS

Every industry follows the same structure:

**Level 1: Industry Landing** → `/industries/{slug}/`
- Tab bar: Overview, Door A (Process Problems), Door B (Product Families), Door C (Procurement)
- Segment toggles filter both Door A tiles and Door B cards

**Level 2: Solution Detail** → `/industries/{slug}/problems/{problem-id}/`
- 300px sidebar with all problems grouped by segment
- Chemical recommendations with drawer that opens product details
- Links down to Level 4 product pages

**Level 3: Family Detail** → `/industries/{slug}/products/{family-slug}/`
- 300px sidebar with all families grouped by segment
- Grid of chemical cards for that family, filtered to industry
- Links down to Level 4 product pages

**Level 4: Product Page** → `/product/{slug}/` ← DONE (1,095 pages)

---

## CATALOG PAGE REQUIREMENTS

The catalog page at `/shop/` must:
- Use the `product-catalog-v5__2_.html` template layout (card grid, NOT table)
- Contain ALL 1,095 chemicals from the master JSON
- Every product perfectly categorized by material family, industry, and functional role
- Every card links to its Level 4 product page (`/product/{slug}/`)
- ZERO empty values — every visible field must be populated or the field hidden
- Left sidebar with collapsible filter sections (material family, industry, functional role) with accurate counts
- Product cards show: name, CAS (mono font), material family, industry tags, description snippet, RFQ + SDS buttons
- Slide-out drawer on card click with full product preview
- Synonym search index embedded for fuzzy matching
- Grid/list view toggle, sort options (A→Z, Z→A, Family, Relevance), pagination
- Correct branding (Plus Jakarta Sans, #E9A72D gold, base64 logo)

---

## WORKING STYLE NOTES

- JP (the owner) is not a programmer — needs step-by-step instructions for anything technical
- Zero tolerance for hallucinated chemical data — if it's not in the JSON, don't invent it
- Zero tolerance for wrong branding — every hex value, font name, and logo must be exact
- Prefers systematic approaches with clear checkpoints
- Will reject work that doesn't match approved designs exactly

---

## STARTING A NEW TASK

1. Fetch `RAWSOURCE_BUILD_RULES.json` from GitHub first
2. Check what's needed (reference the DONE/PENDING list above)
3. Fetch the approved template closest to what you're building
4. Fetch the master JSON if you need chemical data
5. Build with correct branding from the start — don't use placeholder values
6. Match live site URLs exactly — check the SEO section above before creating any links
