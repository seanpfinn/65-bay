# 65 Bay Street — redesign proposal

[![65 Bay Street social preview: the elevator rides from the lobby to floor 44 while the window view rises over Jersey City to the Hudson and the Manhattan skyline](og/og-preview.gif)](og/og-video.mp4)

<sub>Social preview video, 1200×630 at 60 fps. Click for the full-quality mp4.</sub>

A single-file concept homepage for **65bay.com**, the leasing site for 65 Bay Street, a rental high-rise at 65 Bay Street, Jersey City, NJ 07302, managed by Westminster Management. Replaces the current RentCafe (Yardi) template.

## Concept

**Pick your floor. The skyline comes with it.** In a high-rise, the floor is the product: it decides the view, the layouts on offer and the rent. So the hero is the tower drawn in the brand's bronze line beside a floor-to-ceiling window. On load the elevator rides from the lobby to floor 44, and the view rises with it: the Jersey City rooftops sink out of the frame, the waterfront walkway passes, and the Hudson and the Manhattan skyline open up. Drag the car, use the arrow keys or the ▲▼ call buttons, and a readout lists the real floor plans on that floor with sizes and starting rents. L is the lobby, R is the roof lounge.

The site's own plan names already encode the building ("1 BR 1 BA w/ Office Res 03 & 07: FL 3 - 48"). The redesign decodes them into a **stacking plan**: floors 3–51 by residence line 01–10, colored by plan type, synced with the elevator, with each plan card able to light up its homes in the tower. The amenities are a bronze elevator panel whose buttons light up, and the neighborhood is a mile ruler from the front door.

**Carried over from the live brand:** the real "65 BAY STREET / JERSEY CITY" wordmark (traced from the live logo file), its bronze `#ac8152` and the site's navy `#1c3251`, the bronze band at the top of the page, and the site's type system: Adamina headings with italic Playfair Display lead-ins (the live site's "*Experience* Jersey City Living" pattern) and Roboto Condensed for everything else. Section lead-ins reuse the site's own phrases ("Welcome to," "Where every detail matters," "Signature amenities," "Steps from downtown," "Visit us today"). The "65" from the wordmark doubles as the monogram in the mobile tab bar and the app icons, and the window view is graded in the same navy and bronze.

## Audit summary (live site, November 2026)

1. **The old building name is still live in the leasing flow.** Resident and applicant portal URLs use `/trump-bay-street-0/`, the pet policy contains an empty link to `trumpbaystreet.com/.../contact-us`, and photo filenames start with `tbs_`. → Ask Yardi to rename the property slug and redirect the old one, remove the old-domain link, and rename the files.
2. **The best offer is buried.** "NO SECURITY DEPOSIT REQUIRED" appears only on the Availability page, in caps, linking to `http://go.jetty.com/move`. The homepage shows no rents at all. → No-deposit in the header strip, proof band and FAQ; starting rents in the hero readout and the stacking plan.
3. **Size claims contradict the plan list.** The homepage says 546 to "over 1,300" sq ft; the Availability page says one-bedrooms run 552–1,092 and two-bedrooms reach 1,308. The listed plans run 546 (studio), 685–1,092 (one-bed) and 1,133–1,181 (two-bed). → Use the plan list's figures everywhere; confirm whether larger homes exist.
4. **Plan names are internal codes.** "0 BR 1 BA Res 10: FL 8 - 44, 50 - 51" is the studio. Residence 07 on floors 3–6 is listed under two plans (797–801 and 1,092 sq ft), and residence line 05 never appears. → Human names ("Studio · 546 sq ft"), codes kept as small print; confirm the Res 07 overlap.
5. **Availability doesn't render without JavaScript** ("Loading units…"), and the unit list loads from a third-party embed. → Server-render starting rents (the RentCafe API can feed the static readout and cards).
6. **Location claims disagree between pages.** The homepage leads with Exchange Place (0.5 mi), the Neighborhood page title says "near Grove Street Path Station" and its intro links "apartments near Newport Mall" back to the homepage, and the FAQ lists NYU and Columbia under "nearby employers & institutions." → One honest framing: between Exchange Place and Grove Street, 0.5 mi to the PATH.
7. **SEO basics.** The same generic `meta keywords` list on every page; `theme-color` `#999`; the FAQ's description is RentCafe boilerplate ("submit your lease application today!"); no Open Graph image or structured data found; the FAQ has no FAQPage markup; a heading renders as "Refined&Location-Forward." → Rewritten title and description, 1200×630 OG image + video, `ApartmentComplex` + `LocalBusiness` + `FAQPage` JSON-LD.
8. **Two Google Tag Manager containers** (`GTM-KW343BQ2`, `GTM-TNGCMSXR`) load on every page, which risks double-counted leads. → Consolidate to one.
9. **Navigation dead ends.** "Gallery," "Contact Us" and "Login" are `href="#"` parents, and the full nav and login menu are duplicated in the markup. → Five anchors plus one Book a tour button; portals in the header strip and Visit card.
10. **Alt text describes the wrong thing.** A common room is "A modern building with a glass facade and a brick exterior," the walk-in closet photo is titled "Bathroom," the dog spa is "a bathroom with a pink cabinet," the Exchange Place PATH card shows "two women holding shopping bags," and the fitness tile is an iStock photo (`istock-894242814.jpg`). → Descriptive labels; real photos only.
11. **Hygiene.** Hours print as "9 AM to - 6 PM"; the "Get Connected" block repeats on every page; the pet policy says "Breeds: Restrictions" with no list; the contact form asks for a message but not bedrooms, move-in date or tour type. → Cleaned up; the tour form asks for plan, move-in month and in-person or virtual.

## What's in the redesign

- Hero elevator (`<figure>`): generated SVG tower and window view in four parallax layers (Manhattan skyline, waterfront walkway, low rooftops, Jersey City towers). The tower is a `role=slider` (1–52, arrow/PageUp/PageDown/Home/End keys and pointer drag) with ▲▼ buttons and an `aria-live` readout of the plans on that floor.
- Proof band: $0 security deposit, 0.5 mi to Exchange Place PATH, Walk Score 95, 24-hour attended lobby.
- Stacking plan: 49 floors × 10 residence lines built from the plan list, synced with the elevator's floor, plus eight plan cards (size, floors, rent range, units available, link to the existing floor plan page) that light up their homes in the tower.
- "Who's moving in?" tabs (`role=tablist`, arrow/Home/End keys, `aria-selected`, `hidden` panels): Just me · I work from home · Room for two · My dog's coming. Hero chips open the matching tab.
- Amenities as a bronze elevator panel (a second tablist), "Inside every home," neighborhood mile ruler, transit and places, six FAQs, hours with today highlighted (New York time), and a tour request form.
- Mobile tab bar (≤980px): "65" monogram · Floors · Amenities · Call · **Book a tour** pill ("Tour" under 430px), with scroll-spy on Floors and Amenities. It rises after the elevator reaches floor 44, stays visible through the footer, and the footer is padded so it's never covered.

## Spacing & performance

- Spacing tokens 8/12/16/24/32/48/64px, fluid section padding `clamp(64px,9vw,112px)`.
- One `backdrop-filter` layer (sticky header), one rAF-throttled scroll handler using `getBoundingClientRect()` for scroll-spy, a pre-tinted SVG grain, no blend modes, and only the weights used (Adamina 400, Playfair Display italic 400, Roboto Condensed 400–600). The elevator animates SVG transforms on four groups only. `content-visibility` isn't used.
- Load sequence: header slides down → headline lines rise from masks → lede, CTAs, chips and trust row → the card springs in → the tower's linework draws → the elevator rides L → 44 as the view rises → tab bar rises last. Gated on `load` + `document.fonts.ready` + 250ms with a 4s fallback; reduced motion shows floor 44 at once; without JS everything is visible (the view sits at street level and the readout shows floor 44).
- Plan cards and the tabs become snap-scrolling swipe rows on phones; the mile ruler scrolls sideways.
- Verified at 1440, 390 and 360px: no page overflow, no layout shift while changing floors (the readout reserves its tallest state), no console errors, tab bar visible at hero/mid-page/footer with and without reduced motion and hidden on desktop, exactly one selected tab-bar item in Floors and Amenities and none elsewhere, slider and tab keys working.

## Notes before launch

- **Logo:** the wordmark is traced from the live site's `65baystreet_logo_copper.png` (one `<symbol id="brand-logo">`, plus a `brand-mark` "65" monogram cut from it for the tab bar and icons). Replace both with the master vector if management has one, and regenerate the icons.
- **No photos are used.** Amenity panels have labeled placeholder tiles. The building's own photo set (pool, sauna, lobby, roof lounge, game room) should go in once alt text is fixed; the stock gym photo should be replaced.
- **The window view is an illustration**, not a rendering of the view from any specific home. Consider a real photo per floor band (low, mid, high) shot from the building.
- **Rents are a snapshot** of the Availability page on Nov 22, 2026 and are labeled with that date. Wire the readout and cards to the RentCafe/Yardi feed before launch, or drop the figures.
- **No invented claims.** Everything comes from the live site: plans, floors, sizes, rents, availability, amenities, on-site retail, pet policy, hours, distances, the 7-minute PATH ride, Walk Score, the nearby places and the FAQ answers.
- **Confirm before launch:** the floor count (plans list floors up to 51; floor 49 and residence line 05 have no listed plans), the Res 07 floors 3–6 overlap, whether any home exceeds 1,181 sq ft, that the CVS at 88 Morgan Street and the other "on-site retail" are in the building, the breed restrictions, the Jetty program terms, and Equal Housing Opportunity/fair-housing wording with management.
- **Form:** the tour form has a demo submit handler. Wire it to the RentCafe lead API or the leasing inbox before launch. The SMS opt-in is unchecked by default.

## Files

- `index.html` — the page (inline CSS and JS; Google Fonts is the only external request)
- `logo.svg`, `favicon.svg`, `apple-touch-icon.png`, `icon-192.png`, `icon-512.png`, `site.webmanifest`
- `og/og-video.html` — 1200×630 composition driven by a deterministic `render(t)`
- `og/og-video.mp4` — 8 s, 60 fps H.264; `og/og-image.jpg` — final held frame; `og/og-preview.gif` — 720px preview

## Social preview & metadata

Beats: the card springs in and the tower draws in bronze → the wordmark, "Welcome to 65 Bay Street" and "Pick your floor. / The skyline / comes with it." rise → the elevator rides L → 44 as the rooftops sink and the skyline opens up → studio, one-bedroom and two-bedroom starting rents land → the mobile tab bar rises last, then holds. An address, no-deposit, PATH and phone ticker moves exactly 1px per frame (verified on the encoded file).

`og:url`, the canonical, OG/Twitter images, the video and JSON-LD all use the deploy URL, **https://65-bay-tan.vercel.app/**. At launch, find-and-replace that URL with `https://www.65bay.com/`.
