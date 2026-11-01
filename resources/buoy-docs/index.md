---
title: "NormalizationKit"
summary: "Portable Unicode 18.0 NFC, NFD, NFKC and NFKD normalization."
category: "Overview"
order: 0
keywords: ["unicode", "normalization", "NFC", "NFD", "NFKC", "NFKD"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# NormalizationKit

Import `normalizationkit` for deterministic Unicode normalization in pure Buoy,
with no platform library dependencies. Unicode 18.0.0 tables and the Unicode data
license are bundled with the package. Operating-system Unicode versions do not
affect the result.

Choose NFC/NFD to preserve compatibility distinctions. NFKC/NFKD deliberately
fold forms such as ligatures, circled numbers and fullwidth letters. These
operations do not change letter case or implement locale-sensitive comparison.

See the [API reference](api.md) for forms and resource limits.
