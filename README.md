# Eastwood Global × GOSU Academy — partnership landing page

Static single-page site for **gosu.eastwood.global**. No build step, no dependencies, no framework. Push the contents of this folder to a repository and serve it.

## Contents

```
index.html            the whole page: markup, inline layout styles, motion script
css/styles.css        Eastwood Global design system entry point
css/tokens/*.css      colour, type, spacing and font tokens
css/interactions.css  hover states and corner-tick pseudo-elements
assets/*.png          photography, co-brand lockup, patterns, favicon, OG image
CNAME                 gosu.eastwood.global (GitHub Pages custom domain)
.nojekyll             tells GitHub Pages to serve files as-is
```

## Deploying

**GitHub Pages.** Push to a repository, then Settings → Pages → deploy from branch, root. The `CNAME` file claims the subdomain; point a DNS CNAME record for `gosu` at `<org>.github.io`. Delete `CNAME` if you are hosting elsewhere.

**Any other static host.** Upload the folder. Netlify, Vercel, Cloudflare Pages and S3 all serve it without configuration.

## Before going live

1. **Compress the images.** This is the one outstanding item. The folder ships about 17MB of PNGs, including a 4.5MB hero. Convert every photo to WebP at roughly 1600px wide and update the six `assets/*.png` references in `index.html`. Expect the set to land under 1.5MB with no visible quality loss. Until then mobile Largest Contentful Paint will score poorly.
2. **Confirm the OG image URL.** `og:image` and `twitter:image` are absolute and point at `https://gosu.eastwood.global/assets/og-eg-gosu.png`. If the domain changes, update both.
3. **Check the CTA links.** All four Discovery Call buttons point at `https://www.eastwood.global/enquire-now-form` with `utm_source=gosu&utm_medium=landing` and `utm_content` set to `hero`, `mid` or `footer`. Change the base URL in one place per button if the form moves.

## How the page is built

**Layout** is inline styles on the elements themselves, sized with `clamp()` so type and spacing scale fluidly rather than snapping at breakpoints. The two grids that carry four items use `[data-quadgrid]` rules in the `<style>` block: one column below 560px, two up to 1199px, four at 1200px and above.

**Two heroes exist in the markup.** A wide 16:9 crop (`[data-hero="wide"]`) and a tall portrait crop (`[data-hero="tall"]`). A media query at 768px shows exactly one; the other is `display: none`. Edit copy in both if you change the headline.

**Motion** is a single script at the bottom of `index.html`, about 120 lines. It sets `data-motion="on"` on `<html>`, then an IntersectionObserver at a 0.15 threshold adds `data-revealed` to each `[data-reveal]` element as it enters view. Every transition lives in CSS keyed on `[data-reveal]:not([data-revealed])`, so with JavaScript disabled the page renders in its final state rather than blank. The script also runs the stat count-up, draws the programme icons, and drives the scroll progress bar and sticky nav.

`prefers-reduced-motion: reduce` collapses all durations to 1ms and stops the hero zoom, the scroll cue and the drifting pattern.

**Design system.** Colours, type and spacing come from the Eastwood Global tokens in `css/`. Apple Green `#BDD100` is the lead accent, Deep Blue `#000077` the field. Inter throughout, with a single Bodoni Moda Italic line in the footer. Do not add a second editorial face or a second accent colour.

## Content notes

Figures used in the proof band: 100% IB pass rate, 36.9 average group score, 42/45 highest in group, 1 of 7 schools authorised to deliver the IB Diploma fully online. Coach credentials and the 35,000 GOSU student figure came from the partnership brief. Verify all of these against the current source before launch.
