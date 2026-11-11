# মকবুল কমপ্লেক্স ওয়েবসাইট

Self contained Bengali one page site. No build step, no frameworks, no internet needed to view.
(Fonts come from the visitor's device, so nothing is downloaded.)

## Files
```
mokbul-complex/
├── index.html              ← the whole website (HTML + CSS + a little JS)
├── README.md
├── GITHUB.md               ← GitHub এ আপলোড ও Pages চালু করার ধাপ
├── .gitignore
└── assets/
    ├── building-corner.jpg  ← ভবনের পাশের দিক, hero + gallery   1400×1867
    ├── building-front.jpg   ← ভবনের সামনের দিক                  1000×1333
    ├── building-shopfront.jpg ← নিচতলার দোকান ও ভাড়া ব্যানার      1000×688
    ├── office-room-1.jpg    ← অফিস কক্ষ, টেবিল/পার্টিশন         1200×900
    ├── office-room-2.jpg    ← অফিস কক্ষ, চেয়ার/ব্যানার          1200×900
    ├── logo.png             ← পুরো ভবনসহ স্কয়ার লোগো (180×180)
    └── logo-large.jpg       ← একই লোগো বড় সাইজে (512×512)
```
The logo icon is a square crop of the building photo so the full building stays visible.
It is used in the header, the footer and as the browser tab icon.

## Look and feel
White page with light blue accents: `--blue:#1173b5`, `--blue-soft:#eef7fd`,
`--blue-line:#d8e9f6`. Only the WhatsApp buttons keep the official WhatsApp green.
All colours sit in the `:root` block at the top of the CSS, so changing the brand blue
means editing one line.

### Light / dark mode
The round button in the header switches theme. It saves the choice in `localStorage`
(key `mc-theme`), and on a first visit it follows the phone or laptop system setting.
All dark colours are in the `html[data-theme="dark"]` block right under `:root`, so you
can tune the dark palette without touching the rest of the CSS. The theme is applied by
a tiny inline script in `<head>` before paint, so there is no white flash on reload.

### Motion
Kept light on purpose:
- scroll reveal via one `IntersectionObserver` (no scroll listeners per element),
- header shadow on scroll via a single passive scroll listener,
- CSS only hovers and a 0.3s colour transition when the theme changes,
- the map pin bob and everything else stop when the visitor has
  `prefers-reduced-motion` turned on.

If JavaScript is blocked, all content stays visible (`html.js-reveal` guard), so the page
never shows blank sections.

## Hero
The hero uses the building photo as a large image on the right side of a white page,
with a soft white fade so the text stays readable. On mobile the photo moves below
the text and full width.

## How to open it
- Double-click `index.html`, or
- From inside the folder: `python3 -m http.server 8000` then open http://localhost:8000

## Business details baked in
| Field | Value |
|---|---|
| Name | মকবুল কমপ্লেক্স / Mokbul Complex |
| Address | মকবুল কমপ্লেক্স, ডিমলা বাজার, ডিমলা, নীলফামারী ৫৩৫০ |
| Coordinates | 26.1499115, 88.9202475 |
| Google Maps place | https://maps.app.goo.gl/8JRTs1y2gCRQ3Yxg9 |
| Phone (call) | 01319-998569 |
| WhatsApp | 01981-340287 (= wa.me/8801981340287) |

## How to edit
Everything is in the `SITE` block at the bottom of `index.html`:

```js
const SITE = {
  phoneDisplay: "01319-998569",
  phoneDial:    "+8801319998569",
  waNumber:     "8801981340287",
  address:      "মকবুল কমপ্লেক্স, ডিমলা বাজার, ডিমলা, নীলফামারী ৫৩৫০",
  shortAddress: "ডিমলা বাজার, ডিমলা, নীলফামারী ৫৩৫০",
  mapCoords:    "26.1499115,88.9202475",
  mapsPlace:    "https://maps.app.goo.gl/8JRTs1y2gCRQ3Yxg9",
  hours:        "প্রতিদিন সকাল ৯টা থেকে রাত ৮টা"
};
```

Changing these updates the phone links, WhatsApp links, address, map and directions
button everywhere on the page.

Map: it loads after the visitor taps the card, so the page stays fast and the rest of
the site works with no internet. The embed URL is built from `mapCoords`, and the
"গুগল ম্যাপে ভবন দেখুন" button opens `mapsPlace`.

## Small fixes already included
- Anchor links no longer hide section headings under the sticky header (`scroll-margin-top`).
- Images carry `width`/`height` and `loading="lazy"` (hero uses `fetchpriority="high"`),
  so the layout does not jump while loading. Because those attributes also set a height,
  every cropped image box (`.space img`, `.overview-media img`) now declares `height:auto`
  so the CSS `aspect-ratio` wins and all cards line up at exactly 16:11.
- The icon only call button appears on very small phones to stop the header overflowing.
- Map is still tap to load, so Google Maps never blocks the first paint.

## Content that is intentionally not claimed
The facilities section lists only things visible in the photos: road side location,
windows, electrical points and fans, signboard, shutters, street parking, stairs,
room or full floor rental. Lift, generator backup, CCTV and fire safety are not
mentioned because they could not be verified from the photos. Tell me if the building
has them and the cards get added.

Rent, floor area and availability are never printed. Every call to action goes to
phone or WhatsApp.

## Writing style
No em dashes anywhere in index.html (checked with a grep). Bengali copy stays short and
concrete, without filler lines.

## How to replace or add photos
Overwrite files in `assets/` keeping the same names, or add new `<figure>` blocks inside
`<div class="gal-grid">`. The gallery uses CSS columns, so photos keep their real
proportions and any number of images works.

## Publishing (optional)
Upload the whole `mokbul-complex` folder to any static host: Netlify Drop, GitHub Pages,
Cloudflare Pages or a cPanel `public_html`. No server side code is needed.
