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

`sources.json` records download URLs and SHA-256 hashes. Deterministic
little-endian lookup tables are stored as Base64 in the Buoy module. They derive
from the pinned Unicode 18 data, independently of Python's installed Unicode
version. Unicode 18 is an explicit supported version rather than an automatic
tracking policy. The Unicode license is retained under package resources.

The earlier Unicode 17 inputs remain pinned alongside the Unicode 18 data.
Only Unicode 18 data supplies the runtime tables.

The runtime uses no platform normalization APIs and has no mutable normalization
cache. Its private shared buffers hold generated tables and are only read after
initialization. Per-call working arrays are independent.
