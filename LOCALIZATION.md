# Translating these docs

**Status: English only, deliberately.** The Coterie app now ships **seven**
languages — English, Spanish, German, French, Portuguese, Indonesian and Hindi
— at 1,185 Coterie UI strings each plus 386 strings of platform chrome. These
docs have not followed, and this file explains what it would take and why it
hasn't yet, so the decision doesn't have to be rediscovered every time a
language is added to the app.

**The gap is now six languages wide, not one.** That makes the "all-or-nothing"
problem below the deciding factor rather than a footnote: translating these
docs is not one job, it is six, and each one is bigger than the entire app UI.

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
terminology pass. Times six languages, that is ~99,000 words.

There is also ongoing cost: docs change more often than UI strings, and every
edit becomes one edit per language — seven edits, at today's count.

## If you do it

1. Restructure `documentation.json`'s `navigation` into a `languages` array,
   English first.
2. Move existing pages under `en/` and mirror the tree under `es/`.
3. Translate all 42 pages — partial coverage is the failure mode described
   above, not a staging post.
4. Keep the vocabulary consistent with the app — docs that disagree with the
   UI are worse than docs in English. Every language already answers the same
   six questions; copy its answers rather than inventing new ones:

   | English     | Spanish       | German          | French     | Portuguese     | Indonesian   | Hindi        |
   | ----------- | ------------- | --------------- | ---------- | -------------- | ------------ | ------------ |
   | Engagement  | Participación | Engagement      | Engagement | Engajamento    | Engagement   | एंगेजमेंट     |
   | circle      | círculo       | Kreis           | cercle     | círculo        | lingkaran    | मंडली         |
   | standing    | reputación    | Ansehen         | réputation | reputação      | reputasi     | प्रतिष्ठा      |
   | streak      | racha         | Serie           | série      | sequência      | rentetan     | सिलसिला       |
   | contribution| contribución  | Mitwirkung      | contribution | contribuição | kontribusi   | योगदान        |
   | reliability | fiabilidad    | Zuverlässigkeit | fiabilité  | confiabilidade | keandalan    | विश्वसनीयता   |

   Register: informal throughout — *tú*, *du*, *tu*, *você*, *kamu*. Hindi is
   the exception and uses आप, which is the polite-neutral default for written
   Hindi UI; तुम would read as over-familiar rather than warm, so आप IS the
   equivalent register choice, not a departure from it. "Coterie" stays the
   brand, untranslated and in Latin script, in all seven.

## When

Same trigger as the app: a customer who needs it. Localising docs for a language
with no readers costs 16,500 words and buys nothing — and unlike the app, it
can't be done half way.

Note that the app's seven languages are NOT that trigger. They were added while
pre-launch precisely because that is when they are cheap: the strings had
stopped moving, and a mistake cost nothing. Docs have neither property — they
change constantly, and a missing page is invisible to the reader rather than
falling back to English. **Adding a language to the app does not oblige us to
add it here.** The first Coterie whose members actually read one of these
languages does.

## Also worth knowing

The app's font stack now names Devanagari faces (Noto Sans/Serif Devanagari,
Nirmala UI, Kohinoor) so Hindi renders in something deliberate. If these docs
ever carry Hindi, check the same thing on documentation.ai's side — the
platform picks its own typography, and Latin-only webfonts are the usual
default.
