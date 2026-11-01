# NormalizationKit 0.1.0

Portable Unicode 18.0.0 normalization for Buoy. `Import normalizationkit` exposes
`NormalizeNFC`, `NormalizeNFD`, `NormalizeNFKC`, `NormalizeNFKD` and
`NormalizationUnicodeVersion()`. Copy `packages/normalizationkit-0.1.0.buipkg`
into a consumer's packages directory. No native libraries or other packages are required.

| Function | Behavior |
| --- | --- |
| `NormalizeNFC(text, maxScalars = 1000000)` | Canonical decomposition, combining-mark ordering and canonical composition |
| `NormalizeNFD(text, maxScalars = 1000000)` | Canonical decomposition and combining-mark ordering |
| `NormalizeNFKC(text, maxScalars = 1000000)` | Compatibility decomposition, ordering and canonical composition |
| `NormalizeNFKD(text, maxScalars = 1000000)` | Compatibility decomposition and combining-mark ordering |
| `NormalizationUnicodeVersion()` | The pinned data version, `18.0.0` |

Functions return fresh String values and leave input unchanged. Empty input stays
empty. Hangul syllables and conjoining jamo use algorithmic decomposition and
composition; other mappings, combining classes and composition exclusions use
bundled Unicode tables. Equal combining classes retain their original order.
The same data and algorithm run on macOS, Windows and Linux, independently of
installed ICU or operating-system Unicode versions. Scalars without mappings
in Unicode 18.0 are retained, rather than interpreted using a newer host database.

Use NFC when canonically equivalent spellings should compare the same, such as
precomposed `é` and `e` followed by U+0301. NFKC/NFKD also remove compatibility
distinctions: `ﬃ①Ａ` becomes `ffi1A`. Choose compatibility forms explicitly when
those distinctions can be discarded. Normalization does not perform case folding,
locale collation, grapheme segmentation, transliteration or confusable detection.
Normalizing separate pieces and concatenating them need not produce normalized text;
normalize the whole combined string when equivalence across that boundary matters.

## Limits

`maxScalars` bounds both input codepoints and the fully decomposed intermediate
sequence, before recomposition. A negative limit, oversized input or oversized
decomposition throws `InvalidArgumentException`; no partial result is returned.
Zero permits empty input only. For example, NFC of `é` needs a limit of at least
2 because its decomposition has two scalars, even though the result has one.

Combining-mark runs use stable counting sort instead of quadratic insertion
sorting. Table lookup uses binary search; working storage grows with the bounded
scalar sequence. This is a whole-string API, not a streaming normalizer, and it
does not insert stream-safe combining grapheme joiners. It accepts Buoy UTF-8
Strings; byte decoding and its validation remain the caller's responsibility.

## Build and verification

```sh
/usr/bin/buoy pkg seal . -o packages/normalizationkit-0.1.0.buipkg
```

The verifier checks source hashes and reproducible tables, seals a fresh package,
checks the module and consumer on six desktop targets, and executes every
relationship from every row of Unicode 18's NormalizationTest.txt and retains
Unicode 17's vectors as a compatibility check. It also checks
1,000 deterministic random sequences against Python's normalizer over a repertoire
supported by that normalizer, plus size limits, a long combining-mark run,
supplementary text, compatibility distinctions, exclusions and Hangul. Execution
is tested on the current Linux host; macOS and Windows are compiler checks.
The vector suite does not exhaustively test every unlisted Unicode scalar.

`BUOY` selects the compiler and `BPM_PACKAGER` the sealing command. Source data is
checked in for offline reproduction; ordinary builds and tests need no download.
See [provenance](../PROVENANCE.md) and the bundled
[Unicode license](../resources/unicode-LICENSE.txt).

Test suites and fixtures are maintainer-local and are not part of this public repository.
