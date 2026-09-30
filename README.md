# Hyatt Place Daytona Beach Oceanfront — Investment Offering Microsite

Hodges Ward Elliott offering microsite for the fee-simple sale of the 143-key
Hyatt Place Daytona Beach Oceanfront, Daytona Beach Shores, Florida.

**Source site:** https://hyattplacedaytonabeachoceanfront.hodgeswardelliott.com/ (Squarespace)

## Stack

Static single page. No build step, no dependencies; one small inline script for the hero parallax. `index.html`
carries its own inline `<style>`; everything else is in `assets/`. Intended for
GitHub Pages from `main`.

```
index.html          single page, all sections
CNAME               custom domain
.nojekyll           bypass Jekyll processing
assets/
  *.webp            photography, event logos, Hyatt Place colour mark
  *.svg             HWE mark, Hyatt Place white mark, favicon
  og-image.jpg      social card, cropped from the hero
  *.docx            confidentiality agreement
```

Section anchors: `#hero #overview #property #highlights #hl-location #hl-events #hl-upside #confidentiality #contact`

### Live

**https://hyattplacedaytonabeachoceanfront.hodgeswardelliott.com/**: GitHub
Pages from `main` at root. DNS moved from Squarespace (`ext-cust.squarespace.com`)
to a CNAME for `fsmarketing123.github.io` at Hover on 30 Sep 2026, and `CNAME`
committed the same day.

It was staged first at `fsmarketing123.github.io/hyatt-place-daytona-beach-oceanfront-microsite/`
with the CNAME held back as `CNAME.pending`. A committed CNAME makes Pages
redirect the github.io address to the domain, which would have shown the old
Squarespace site. Every asset path is relative, so the page serves the same
from the subpath or the domain root.

### Local preview

`.claude/hpdb-sync.sh` mirrors this folder to `/tmp/hpdb-preview` and writes a
no-store server; the `hyatt-place-daytona-beach-oceanfront` launch entry serves
it on 8947. Re-run the sync after every edit and after a reboot.

## Provenance

Rebuilt from `../xx Working Files xx/Squarespace-Wordpress-Export-09-29-2026.xml`
and checked against `Hyatt Place Daytona Beach Oceanfront.jpeg` and the live site.

The export is one `page` item with seven sections. It carries every block's
fluid-engine `grid-area` and `z-index` at both breakpoints, and those are the
`--m` / `--d` / `--z` values in the markup. What it does not carry, taken from
the live page instead:

- **Code blocks**: the property table and the footer contacts export empty.
- **The footer** as a whole (site-level in Squarespace) and the HWE masthead.
- Button labels and links, the hero card's tint and radius, text-block insets.

All copy is verbatim.

### Images

All photography is from `../xx Images xx/`, resized to WebP (2400px for
full-bleed grounds, 900–1600px for blocks). Two files were not in the folder:

- **`events-arch.webp`**, the "World's Most Famous Beach" arch behind the
  events section (`daytona beach_2559789247.jpg` on the source), downloaded
  from the site's own Squarespace CDN at 2500w.
- **The Jeep Beach logo** is `xx Logos xx/Copy-of-Celebrating-Americas250th.png`
  — same 2021×748 artwork as the source's `jeep Beach logo.png`.

## Fidelity

Section heights against the live build at 1440×900:

| section | live | rebuild |
|---|---|---|
| `#hero` | 900 | 900 |
| `#overview` | 519 | 519 |
| `#property` | 1880 | 1880 |
| `#highlights` | 396 | 396 |
| `#hl-location` | 1199 | 1191 |
| `#hl-events` | 1408 | 1408 |
| `#hl-upside` | 933 | 933 |
| `#contact` | 739 | 523 — see below |

Grid metrics match exactly: row 29.09px, gutter column 32.19px, cell 45.23px.
All thirteen property-table rows match to the pixel.

At 375×812, five sections are within 8px of the source. The other three
differ on purpose, all covered under departures: `#hero` 812 against 856
(the re-spanned card), `#property` 2386 against 2311 (the address wraps
rather than scrolling sideways), and `#contact` 879 against 907.

### Sizing

Squarespace sizes sections off the viewport, and these reproduce it:

| setting | padding | min-height |
|---|---|---|
| large (hero) | `10vmax` | `100vh` |
| medium | `6.6vmax` | `66vh` |
| custom 44 (highlights band) | `4.4vmax` | `44vh` |
| small (overview, footer) | `3.3vmax` | `33vh` |

The grid is then centred vertically in the section.

**Image blocks are taken out of flow** (`position:absolute; inset:0`) so they
fill their grid area without adding their own height. Left in flow, the
photographs grew the auto rows under them and stretched `#property` by 285px.

### Type

**Poppins throughout**, at the client's request (300–700 from Google Fonts). It
replaced Instrument Sans (body, a width match for the source's Aktiv Grotesk),
Roboto Condensed (headings) and Cormorant Garamond (the glass-band label).

Poppins is considerably wider than all three, so text blocks wrap more and
several sections are taller than the Fidelity table above. Two things were
re-fitted for it (the hero name has since moved into the logo):

- **The glass-band label** is Poppins Light at the template's size.


## Colour scheme

The Squarespace scheme (periwinkle, black, olive-gold buttons, green footer) has
been replaced with hyatt.com's scheme for this hotel. The live hyatt.com page
blocks automated browsers, so the colours were read off the Wayback Machine
snapshot of 3 Dec 2025.

| token | value | used for |
|---|---|---|
| `--cream` | `#f6edd8` | page ground, `#overview` |
| `--navy` | `#283e53` | `#property`, footer, headings on light grounds, buttons, band overlays |
| `--teal` | `#4a6b74` | `#hl-location`, button hover |
| `--sand` | `#d3b782` | property-table rules, contact-group rules |
| `--charcoal` | `#282828` | body copy |

Every CA button is the CTA section's pair (see below): a sand **Sign CA
Online** and an outline **Download CA (DOCX)**, 11px uppercase at .18em, 240px
minimum. In `#overview` the pair is one centred row in a grid block spanning
both of the source's button cells. `#hl-upside` has none: the CTA section
follows it directly. On those light grounds
(`.cta-btns.on-light`) the outline is navy over a 70% cream fill, which keeps it
legible over the pool water, and fills navy on hover. The photo overlays are
tinted navy (`#hl-events` .45; `#highlights` has none) and cream on
`#hl-upside`. Fonts are unchanged; hyatt.com's Trend Sans One and Memphis are
proprietary.

## CTA section

`#confidentiality`, between `#hl-upside` and the footer, is the **HWE CTA
Section** template (`../../xx Templates xx/cta-section`, from the Hyatt House
Lincoln Park build): "Access the / *Offering Memorandum*", the template's
paragraph, and Sign CA Online / Download CA (DOCX). The spacing, headline scale, `.75` dimming of the italic line and the phone stacking
are the template's. Adapted to this site:

- The headline keeps the template's Cormorant Garamond Light (roman, and
  italic for the second line), the one non-Poppins type on the page. The
  paragraph and buttons are Poppins instead of the template's Jost.
- The paragraph is capped at 60ch rather than 50ch, with balanced wrapping, so
  it sets on two lines at desktop widths.
- The hyatt.com palette: a teal band, so it separates from the navy footer,
  with a sand primary button and a cream outline secondary.
- This deal's RightSignature link and bundled CA; the download saves as
  "Hyatt Place Daytona Beach Oceanfront - Confidentiality Agreement.docx".
- The template's `cta-section.js` scroll reveal is folded into the page's own
  script. The hidden state is applied only by script and skipped under
  reduced motion.

## Hero glass

The hero card is liquid frosted glass: a 22px backdrop blur that also lifts
saturation (180%) and brightness (108%); a white fill that runs from 55% at the
top-left to 30% at the bottom-right; a 1px white rim with inset highlights top
and bottom and a soft inner glow; a curved specular sheen across the top third
(`::before`, screen-blended); and a soft navy-tinted drop shadow. Radius stays
45px (32px on phones). Where `backdrop-filter` is unsupported the fill falls
back to solid white at 82%, so the logo stays legible.

## Hero bubbles

The hero card is a button. A transparent `<button class="hero-hit">` covers the
card's grid area above the logo, so the whole card is one target; the card lifts
on hover and presses in on click through `:has()`. Each press releases 48 glass
bubbles, 8–34px, in the colours of the logo's nine circles: `#fed208`,
`#231f20` (×2), `#f58023`, `#7582bf`, `#b2aa7e`, `#d6e03e`, `#51b3cf` and
`#74c168`, read from the SVG.

Bubbles start at random points inside the card, on a layer (`.bubbles`) between
the photograph and the card. Each first shows blurred through the glass, then
rises, spreads out at its own angle and fades over 1.6–2.8s. They run on the Web
Animations API and are removed when they finish; at most 200 are in flight, so
repeated clicks cannot pile up. Under `prefers-reduced-motion` a press gives a
brief glow on the card instead.

## Textured ground

`#overview` carries a tiled concrete grain: `assets/texture-concrete-wall.png`,
byte-identical to `xx Patterns xx/concrete-wall-1.png` (520×520, transparent
with dark speckle). It is pinned (`background-attachment: fixed`), repeats at
its native 520px, and sits on its own `::before` layer at 80% opacity with
`mix-blend-mode: multiply` against the cream. A separate layer keeps the
opacity off the copy; the section's `isolation: isolate` limits the blend to
the cream. Under `@media (hover:none)` it scrolls instead, since iOS Safari
ignores `fixed` and repaints badly under it.

`#property`, `#hl-location` and `#confidentiality` take the white version, `assets/texture-concrete-wall-white.png`
(from `xx Patterns xx/concrete-wall-white.png`, the same 520px speckle in
near-white), with the same pinning and tiling, at 70% opacity, and
`mix-blend-mode: screen` rather than multiply. Multiply can only darken, so
near-white speckle multiplied into the navy or teal would vanish; screen is its
light-on-dark counterpart.

## Deliberate departures from the source

**Hero lockup.** The stacked colour mark plus the two text lines ("Daytona
Beach Oceanfront", "Daytona Beach Shores, FL") are replaced by one horizontal
lockup, `assets/logo-hyatt-place-daytona-horz.svg`, from
`xx Logos xx/Hyatt-Place-Daytona-Beach-Oceanfront-Horz-logo.svg`. The export
was stripped of its Illustrator metadata (547KB → 38KB, artwork unchanged) and
its viewBox trimmed to the artwork. It is the page's `h1`. The card behind it is
landscape now — ten columns by eight rows, in liquid frosted glass — with the logo
centred: 439×214 in a 551×310 card at 1440, 245×119 in 330×234 on a phone.

**Mobile hero card spans its content.** Under 768px the source's white card
collapses to a bare bar across two rows, and the Hyatt Place mark, the property
name and the location reflow below it onto the open photograph. Here the card
spans the mark and both lines, as it does on desktop, on a 14-row mobile grid
rather than the source's 18.

**Footer contacts are two-up.** On the live site at 1440 the contacts stack
one per row, because the 320px contact plus its 20px margin does not fit twice
in the 664px block. The supplied screenshot, taken wider, shows them two-up,
and that is what this matches — hence the shorter footer. They drop to one
column under 900px.

**Address wraps below 1300px.** The two unbreakable address lines make the
table 389px wide. On the source it scrolls sideways in a 309px column at 1024
and a 330px one on a phone; here the value wraps instead.

**Email fix.** The source's link for Rudy Reudelhuber is
`mailto:rreudelhuber @hodgeswardelliott.com`, with a space; it is corrected here.

**HWE marks are `assets/hwe-white.svg`** (the stripped copy from the Venezia
build), replacing the two PNGs, one hotlinked from a Squarespace CDN path.
**The property-section mark** is `Hyatt Place Logo - white.svg` rather than the
204px `Hyatt-Place-KOfull.png`.

**The CA is bundled** at `assets/Hyatt-Place-Daytona-Beach-Oceanfront-CA.docx`
instead of the Squarespace `/s/` path, which will not exist after cutover.

**Images carry alt text.** Every `alt` in the source is empty.

## Kept as-is

- Four image blocks are "fit" (`object-fit: contain`): the property mark and
  the three event logos. `hl-room-view.webp` keeps its focal point,
  `object-position: 33.9% 49.6%`.
- On mobile, the oceanfront copy comes after its three photographs and the
  events copy after the speedway, bike-week photo and logo — the source's own
  mobile order.
- No scroll animation or lightbox; the source has none.

## Hero parallax

Added at the client's request; the source has none. Two sections carry
`data-px`: the hero and the Investment Highlights band. The hero zooms from
1.00 to 1.15 and the band from 1.00 to 1.25 (`data-px="0.25"`); each and drifts slower than the page (up to 16% of the section height). The hero starts at
rest and reaches full zoom once its own height has scrolled past; the band
zooms while it crosses the viewport, from its top meeting the bottom of the
screen to its bottom leaving the top.

The Investment Highlights heading uses the **HWE Glass Image Band** template
(`../../xx Templates xx/HWE Glass Image Band/`, from the Hyatt House Shenandoah
build): a square plate of warm charcoal glass at 34% over a 4px blur, hairline
white rules top and bottom, and the label in white Poppins Light (the template
uses Cormorant Garamond),
58px at desktop, on one line. The plate is centred on the band; under 560px it
caps at the viewport width and the label may wrap, as in the template. The band
is 900px tall on desktop.

The template's `glass-image-band.js` hover zoom is not used: the band has the
scroll zoom instead, at the client's request.


`#hl-upside` runs the other way (`data-px-dir="out"`): its pool photograph
starts at 1.25 and settles to 1.00. Because it is second-last on the page, the
usual mapping would run out of page at 82% and leave the photo at 1.045, so a
zoom-out section finishes as its bottom meets the viewport bottom instead. The
photo also sits 4% of its layer lower (`--py0:4%`, ~66px at 1440, and up to
166px lower once the drift is added), so the copy lies over open sky and the
pool-deck umbrellas stay below it. Coverage was checked at every stage: at least
34px of photo past each edge at 1440, and 28px on a phone.


**On phones only**, `#hl-upside`'s own photograph fades to 10% over a white ground
(and a white wash in place of the cream one), so the copy sits on a near-plain
ground rather than over the pool deck, and the same
photograph appears at full strength in its own frame below the copy
(`.upside-photo`, 330×186 at 375), easing in with the CTA section's reveal. The
frame is decorative, since the section photo already stands for it, so it is
`aria-hidden`. It is `display:none` from 768px up, and desktop is unchanged.

The photograph is on `#hero::before`, which script cannot address, so the
handler writes `--pz` and `--py` on the section and the layer inherits them —
one compositor-friendly `transform`. The layer is inset `-16%` top and bottom
and the section clips it, so the drift never uncovers an edge. The handler is
rAF-throttled, does nothing once the hero is off screen, and is not installed
under `prefers-reduced-motion`.
