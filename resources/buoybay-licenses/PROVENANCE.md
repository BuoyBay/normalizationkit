# NormalizationKit provenance

NormalizationKit is an independent Buoy implementation of Unicode normalization.
The normalization methods in declaresub/REALbasicStandardLibrary motivated this
package; none of that project's implementation, OS bindings or artwork is copied.

The algorithm follows [Unicode 18 UAX #15 revision 58](https://www.unicode.org/reports/tr15/tr15-58.html).
It implements canonical/compatibility recursive decomposition, stable canonical
ordering, composition blocking, full composition exclusions and algorithmic Hangul
handling. The generator expands recursive mappings; runtime ordering and composition
operate on the complete decomposed sequence.

Pinned inputs under `data/unicode-18.0.0` come from the official
[Unicode 18.0.0 UCD](https://www.unicode.org/Public/18.0.0/ucd/):

- UnicodeData.txt supplies decomposition mappings and canonical combining classes.
- DerivedNormalizationProps.txt supplies Full_Composition_Exclusion.
- NormalizationTest.txt supplies the version-matched test relationships.
- LICENSE.txt contains the Unicode License V3 notice accompanying the data.

`sources.json` records download URLs and SHA-256 hashes. The generator and verifier
check these hashes before using the inputs. `tools/generate_normalization_tables.py`
produces deterministic little-endian lookup tables stored as Base64 in the Buoy
module; it does not derive mappings from Python's installed Unicode version.
The Unicode license is also included under package resources so sealed consumers
receive the attribution. Unicode 18 is an explicit supported version, not a claim
that this package tracks the newest Unicode release automatically.

The previous `data/unicode-17.0.0` inputs remain pinned for compatibility tests.
The verifier checks both versions' source hashes and normalization vectors;
only Unicode 18 data generates the runtime tables. New regression cases cover
Unicode 18 Armenian compatibility mappings and Hebrew combining-mark ordering.

The runtime uses no platform normalization APIs and has no mutable normalization
cache. Its private shared buffers hold generated tables and are only read after
initialization. Per-call working arrays are independent.
