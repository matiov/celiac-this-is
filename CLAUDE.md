# Celiac This Is

A Jekyll static site: a personal travel blog listing gluten-free/vegetarian-friendly
restaurants by city, for people with Celiac disease. Built on the "Forty" template by
HTML5 UP (see [LICENSE.txt](LICENSE.txt)).

## Running locally

See [README.txt](README.txt) for the exact `jekyll serve` invocation and the
non-standard `GEM_HOME` this machine needs.

## Structure

- **Content pages**: [index.html](index.html) is the home page with one tile per
  country. Country pages live in [countries/](countries/) — [japan.html](countries/japan.html),
  [usa.html](countries/usa.html), [portugal.html](countries/portugal.html) are real,
  filled-in pages — one `<section class="spotlights">` block per city, each followed
  by a `#<city>-food` section listing restaurants with gluten-free (🌾) and vegetarian
  ratings out of 5. [template_country.html](countries/template_country.html) is the
  skeleton to copy for a new country; it has `published: false` so it isn't built
  (remove that line in the copy, or preview with `jekyll serve --unpublished`).
- **Unwritten countries** (Peru, Ecuador, Italy, Germany, Switzerland, Belgium,
  France): their tiles in `index.html` and entries in `_includes/menu.html` are
  commented out until `countries/<name>.html` exists. The home page ends with a
  "Rate Us!" section (`#rate`) embedding a Tally form (`tally.so/r/yPWPEx`); responses
  are collected on tally.so, not in this repo.
- **Paths**: pages in `countries/` set `root: ../` in front matter and reference
  `../images/…` / `../assets/…`; the includes prefix paths with `{{ page.root }}`
  (empty for root-level pages). Keep this when adding a country page.
- **`_includes/`**: [head.html](_includes/head.html) (`<head>` boilerplate + CSS
  links) and [header.html](_includes/header.html) (site header/logo) are pulled into
  every page via `{% include %}`, as is [menu.html](_includes/menu.html) (the
  slide-out country menu).
- **`assets/`**: `css/` holds the precompiled stylesheet (`main.css`, `noscript.css`,
  `fontawesome-all.min.css`) actually linked from `head.html` — there is no Sass build
  step in this repo, so `css/` is the only styling source that matters. `js/` and
  `webfonts/` are the Forty template's vendor scripts and Font Awesome font files.
- **`images/`** (resized to ≤1600 px, ≤1920 px for `countries/` banners; keep new
  photos in that range): `covers/` (per-country card images on the home page), `cities/` and
  `countries/` (per-city/country banner images on the country pages), `logos/`
  (the gluten-free/vegetarian rating icons, plus the favicons and `og-image.png`
  link-preview image referenced from `head.html`).

## Conventions

- Each country page sets `description: Gluten-Free and Vegetarian in <Country>` in its
  front matter (used for search results and link previews).
- New country pages go in `countries/` and follow the `japan.html`/`usa.html` pattern: a menu `<nav>`
  linking to `#<city>` anchors, one `spotlights` section + one `<city>-food` section
  per city, and ratings formatted as `<img src="images/logos/gf_logo.png"> X/5: ...`.
  Ratings are city-relative (a 5/5 is the best *in that city*, not a global scale).
- `_site/` and `.jekyll-cache/` are build output — gitignored, safe to delete/regenerate
  anytime.
- The `/publish-blog` skill (`.claude/skills/publish-blog/`) proofreads, comments
  out unfinished bits, checks the build, and pushes when asked.
