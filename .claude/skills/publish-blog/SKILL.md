---
name: publish-blog
description: Proofread the blog's pages, comment out anything not implemented yet (template placeholders, unwritten countries, the contact form), check the build, and push to GitHub when asked. Use when the user says "proofread", "clean up before publishing", "publish", or "push the blog".
---

# Proofread, hide unfinished bits, and publish

Run the steps in order. Steps 1–3 are always safe. Step 4 (commit + push) runs
**only if the user asked to push/publish in this request** — otherwise stop after
step 3 and ask.

## 1. Proofread

Read every content page in full (don't skim): `index.html`, `countries/*.html`
(skip `countries/template_country.html` text, which is placeholder by design), and
`_includes/*.html`.

Fix:
- Spelling (recurring offenders in this repo: "availabel", "accomodate", "restuarant",
  "deers", "Morover", doubled words like "which which").
- Grammar: plural/singular agreement ("This restaurants"), "recommend to X" →
  "recommend X-ing", "than"/"then", "it was close" → "closed", "quite many" → "a lot of".
- Capitalisation of nationalities/cuisines (Japanese, Indian, Thai, Vietnamese) and
  proper names (FindMe GF, Häagen-Dazs, Pokémon, Kobo Daishi, Shingon, Alfama).
- Facts that contradict each other on the same page (e.g. number of nights in a
  place) — **don't silently change these; list them for the user.**
- Broken markup: `<p>` wrapping block elements (`<h3>`, `<ul>`), stray `</p>`
  without an opening `<p>`, a ratings `<ul>` missing its `<li>`, `//` in paths.
- Inconsistent restaurant entries: every one should end with `<br/>` + blank `<br/>`
  + `Ratings:` + the two badges (`gf_logo.png`, `veg_logo.png`) with `X/5: ...`.

Keep the authors' voice: they write casually, with jokes and asides ("if you know,
you know", "get your ass bitten"). Fix errors; don't rewrite style, tone, or ratings.
Don't touch restaurant names as they appear on Google Maps (e.g. "UNO RAMEN",
"curry & tempura koisus", Japanese-script names).

## 2. Comment out what isn't implemented

"Not implemented" = still template content: Lorem Ipsum, `images/pic*.jpg`,
`template_country.html` / `generic.html` / `landing.html` link targets, placeholder
contact details, or a form with no backend.

- **Unwritten countries**: a country is written once `countries/<name>.html` exists
  with real content. For every country without one, comment out both its tile in
  `index.html` (`<article id="<name>">`) and its `<li>` in `_includes/menu.html`.
  When a country page *does* exist, make sure its tile and menu entry are
  uncommented and point at `countries/<name>.html` (menu: `{{ page.root }}countries/<name>.html`).
- **Links to template pages**: spotlight images use `<a class="image">` with no
  `href`; remove any `href="generic.html"` / `landing.html` / `template_country.html`.
- **Contact section** in `index.html`: stays wrapped in `{% comment %}…{% endcomment %}`
  until a real form backend exists. Use the Liquid comment (not `<!-- -->`) for any
  block that already contains an HTML comment, since HTML comments can't nest.
- Comment marker for HTML: `<!-- Not written up yet: uncomment once the country page exists.` … `-->`.

## 3. Check the build

```bash
export GEM_HOME=$(readlink -f ~/snap/code/current)/.local/share/gem/ruby/3.2.0
export PATH="$GEM_HOME/bin:$PATH"
jekyll build
```

Then check that every local `src`/`href` in `_site/**/*.html` (outside HTML
comments) resolves to a file. Ignore `landing.html` / `generic.html` (template
pages with known-missing `pic*.jpg`) as long as nothing links to them.

Path rule: pages in `countries/` set `root: ../` in their front matter and use
`../images/…`, `../assets/…`; the shared includes prefix paths with `{{ page.root }}`.
A new country page must do the same or its CSS and images break.

## 4. Commit and push (only on request)

1. `git status` and `git diff --stat` — show the user what's included. Don't commit
   unrelated files (`_site/`, `.jekyll-cache/` are gitignored anyway).
2. Commit on `master` with a short message in the repo's style (e.g. "Proofread
   Japan, hide unwritten countries"), ending with the Co-Authored-By trailer.
3. `git push origin master`.
4. Report the commit hash and the list of fixes, plus any contradictions from
   step 1 that you left for the user to resolve.
