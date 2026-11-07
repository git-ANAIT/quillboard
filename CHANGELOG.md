# Changelog

All notable changes to Quillboard. Format: Keep a Changelog; versions are semver.

## [1.0.0] - 2026-11-06

First public release. Developed by Clear Theory.

### The keyboard
- QWERTY layout with shift (single tap = one letter, double tap = caps lock), backspace
  with press-and-hold repeat, space, return, a number row that is slightly shorter than
  the letter rows, and separate number/symbol pages.
- Light, dark and automatic themes; key height and haptic strength adjustable; the tone
  bar can be hidden.
- Key-press pop-up bubbles and keyboard-tap haptics.
- Return key label follows the app (`go`, `search`, `send`, `next`, `done`).
- Suggestion strip above the tone bar with up to three suggestions.

### Correction
- Instant spelling correction: SymSpell delete index over the 80k most frequent words,
  re-ranked with a QWERTY-aware typo model, unigram frequency and bigram context.
- 200k-word "known" set, so real words are never "corrected".
- 45 grammar rules: articles (a/an, vowel-sound exceptions, doubled articles),
  its/it's, your/you're, there/their/they're, then/than, to/too, subject-verb agreement,
  auxiliaries, doubled words, lowercase `i`, sentence and day/month capitalisation,
  spacing and punctuation, joined words and fixed phrases.
- Next-word predictions from 150k bigrams and 100k trigrams, with a precomputed
  next-word index.
- Personal dictionary (Room) that learns names and local words, with a full editor.

### Tone rewriting
- Professional, Academic and Casual rewrites from 286 Tier-A phrase rules plus a full
  grammar pass, with `Rewriting…` feedback and exact Undo.
- Works on the selection, the sentence under the caret, or the paragraph.
- Optional Tier B on-device model: import a quantized file, RAM-gated, 500-character
  cap, automatic fallback to Tier A.

### Privacy
- No `INTERNET` permission and no network code anywhere.
- Password, email, URL, phone and filter fields are never read or rewritten.
- No analytics, no account, no ads, no logging. Cloud backup disabled.
- The only stored data is the personal dictionary, pinned clips and settings — all
  visible and deletable in Settings.

### Also in this release
- Emoji page with categories and recents; long-press the emoji key for the clipboard
  page with pinned snippets.
- First-run onboarding.
- About screen with engine statistics and Clear Theory credits.

### Builds
- Signed release and debug APKs in `artifacts/`, with `SHA256SUMS.txt`.
- `apksigner` verifies (v2 scheme, `CN=Clear Theory`); the packaged manifest requests
  **no permissions of any kind** — checked with `aapt2 dump permissions`, not by grepping
  the source manifest. The one signature-level permission that `androidx.core` merges in
  (`DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`) is removed again at merge time, because
  Quillboard registers no receivers.
- Note for anyone rebuilding: AGP decompresses `.gz` assets at packaging time, so the APK
  contains `known.tsv`, not `known.tsv.gz`. `AssetSource` sniffs the gzip magic bytes and
  handles both, so the same code reads the repository form and the packaged form.

### Deliberately not included
- iOS version (planned later; platform restrictions).
- Any cloud feature, ever.
