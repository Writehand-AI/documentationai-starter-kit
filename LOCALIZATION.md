# Translating these docs

**Status: English only, deliberately.** The Coterie app itself ships English and
Spanish (1,188 UI strings). These docs have not followed, and this file explains
what it would take and why it hasn't yet — so the decision doesn't have to be
rediscovered.

## What documentation.ai needs

Per [their localization docs](https://documentation.ai/docs/organize/localization),
languages are a **dimension in `documentation.json`'s navigation**, not a
per-page setting. Each language gets:

- a `language` display name (e.g. `"Español"`)
- an `icon`
- **its own complete content tree** — its own `tabs`, `groups`, page titles and
  page paths

Their own recommendation for paths is a per-language prefix, `en/...` and
`es/...`, so page paths stay predictable. Today `navigation` is a bare `tabs`
array with no language dimension, so adding one means restructuring it.

## The two things that make this harder than the app

**1. There is no fallback.** In the app, a key missing from Spanish falls back
to English automatically — that's why Spanish could ship a member-facing half
before the admin half without looking broken. Their localization docs describe
no default-language fallback: a page absent from a language branch simply
doesn't appear to readers in that language. So a half-translated docs site shows
a Spanish reader an incomplete site with pages silently missing, rather than
English ones. **Docs localization is all-or-nothing per language in a way the
app is not.**

**2. It is the bigger job of the two.** 42 pages, ~16,500 words — roughly 2.4×
the ~6,900 words of the entire app UI, and long-form prose rather than short
labels, so it needs a translator with the product's voice rather than a
terminology pass.

There is also ongoing cost: docs change more often than UI strings, and every
edit becomes one edit per language.

## If you do it

1. Restructure `documentation.json`'s `navigation` into a `languages` array,
   English first.
2. Move existing pages under `en/` and mirror the tree under `es/`.
3. Translate all 42 pages — partial coverage is the failure mode described
   above, not a staging post.
4. Keep the vocabulary consistent with the app. The app's Spanish uses:
   Participación (Engagement), reputación (standing), círculo (circle),
   racha (streak), nicho (niche), Sesiones (Sessions), informal *tú*, and
   leaves "Coterie" as the brand. Docs that disagree with the UI are worse
   than docs in English.

## When

Same trigger as the app: a customer who needs it. Localising docs for a language
with no readers costs 16,500 words and buys nothing — and unlike the app, it
can't be done half way.
