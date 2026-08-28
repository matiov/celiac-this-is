# Celiac This Is

A Jekyll static site: a personal travel blog listing gluten-free/vegetarian-friendly
restaurants by city, for people with Celiac disease. Built on the "Forty" template by
HTML5 UP (see [LICENSE.txt](LICENSE.txt)).

## Running locally

See [README.txt](README.txt) for the exact `jekyll serve` invocation and the
non-standard `GEM_HOME` this machine needs.

## Structure

- **Content pages** (root `*.html`, each with Jekyll front matter for `title` /
  `header_class`): [index.html](index.html) is the home page linking out to one page
  per country. [japan.html](japan.html) and [usa.html](usa.html) are real,
  filled-in country pages — one `<section class="spotlights">` block per city, each
  followed by a `#<city>-food` section listing restaurants with gluten-free (🌾) and
  vegetarian ratings out of 5.
- **Placeholder pages**: [landing.html](landing.html) and [generic.html](generic.html)
  are unmodified Forty template pages still full of Lorem Ipsum. They are real link
  targets today — `index.html` points every country not yet written up (Peru, Ecuador,
  Portugal, Italy, Germany, Switzerland, Belgium, France) at `landing.html`, and
  `japan.html`/`usa.html` point unwritten cities at `generic.html`. Treat them as TODO
  stubs to eventually replace with real per-country pages, not as content to remove.
- **`_includes/`**: [head.html](_includes/head.html) (`<head>` boilerplate + CSS
  links) and [header.html](_includes/header.html) (site header/logo) are pulled into
  every page via `{% include %}`.
- **`assets/`**: `css/` holds the precompiled stylesheet (`main.css`, `noscript.css`,
  `fontawesome-all.min.css`) actually linked from `head.html` — there is no Sass build
  step in this repo, so `css/` is the only styling source that matters. `js/` and
  `webfonts/` are the Forty template's vendor scripts and Font Awesome font files.
- **`images/`**: `covers/` (per-country card images on the home page), `cities/` and
  `countries/` (per-city/country banner images on the country pages), `logos/`
  (the gluten-free/vegetarian rating icons used throughout).

## Conventions

- New country pages should follow the `japan.html`/`usa.html` pattern: a menu `<nav>`
  linking to `#<city>` anchors, one `spotlights` section + one `<city>-food` section
  per city, and ratings formatted as `<img src="images/logos/gf_logo.png"> X/5: ...`.
  Ratings are city-relative (a 5/5 is the best *in that city*, not a global scale).
- `_site/` and `.jekyll-cache/` are build output — gitignored, safe to delete/regenerate
  anytime.
