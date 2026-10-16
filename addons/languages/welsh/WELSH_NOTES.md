# Welsh (Cymraeg) pack — work in progress

Status (2026-10-16): builds and installs. `./gradlew
:addons:languages:welsh:apk:assembleDebug` succeeds; the resulting
`com.menny.anysoftkeyboard.welsh` debug APK was installed and
type-tested on a Pixel 8 Pro ("Bore da, dwi'n byw yng Nghymru" —
apostrophe words and the nasal mutation Nghymru are in the
dictionary).

## Not in this push (and why)

- `pack/dictionary/inputs/cywiki_sample.txt` — the dictionary source:
  a 12.3 MB slice of Welsh Wikipedia text (first ~3,900 articles of the
  cywiki dump, markup crudely stripped). Too large for the push route
  used here; it will land with the production dictionary pass. The
  build regenerates `res/raw/welsh_words_*.dict` from it via the
  project's own `makeDictionary` tooling, using the Welsh character
  set configured in `pack/build.gradle`
  (`dictionaryInputPossibleCharacters` — circumflexes ŵ ŷ â ê î ô û
  included; without it the parser splits words like `dŵr`).
- PNG icons — the in-tree icons are still the Scottish Gaelic
  template art (this pack was scaffolded from `scottishgaelic`);
  the status icons still read "gd" and will be regenerated as "cy".
- Binary `.dict` files — build outputs, regenerated on every build.

## Known issues

- The prototype corpus leaks some Wikipedia markup tokens (`ref`,
  `td`, table vocabulary) into the suggestion ranks. A production
  corpus pass (full dump, proper cleaner, frequency threshold,
  top-1000 review) is the next step.
- `ext.shouldBePublished = false` — not for release yet.
- Licence homework before any upstream PR: dictionary frequencies
  derive from Welsh Wikipedia text (CC BY-SA); a vocabulary
  cross-check against Techiaith hunspell-cy (LGPL-3.0) is planned,
  and the mix needs a word with the AnySoftKeyboard maintainer first.
