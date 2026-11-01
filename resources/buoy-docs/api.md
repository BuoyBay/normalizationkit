---
title: "NormalizationKit API"
summary: "Normalization forms, data version and scalar-budget contracts."
category: "Reference"
order: 20
keywords: ["unicode", "normalization", "limits"]
symbols: ["NormalizeNFC", "NormalizeNFD", "NormalizeNFKC", "NormalizeNFKD", "NormalizationUnicodeVersion"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

Each normalization function takes `text As String` and optional
`maxScalars As Integer = 1000000`, and returns a String.

| Function | Form |
| --- | --- |
| `NormalizeNFC` | Canonical decomposition, ordering and composition |
| `NormalizeNFD` | Canonical decomposition and ordering |
| `NormalizeNFKC` | Compatibility decomposition, ordering and composition |
| `NormalizeNFKD` | Compatibility decomposition and ordering |
| `NormalizationUnicodeVersion()` | Returns `18.0.0` |

Input is unchanged and an empty string normalizes to empty. Full composition
exclusions, composition blocking, stable combining order and Hangul are supported.
Scalars with no Unicode 18 mapping remain unchanged.

The nonnegative scalar limit applies to input and fully decomposed intermediate
text, even if recomposition would reduce the result. Exceeding either bound or
passing a negative limit throws `InvalidArgumentException`; no partial text is
returned. A limit of zero permits empty input. Working storage is proportional
to the bounded sequence. Counting sort prevents quadratic combining-mark ordering.

This API normalizes whole Strings; it provides neither streaming normalization
nor stream-safe text insertion, case folding, collation or grapheme segmentation.
Normalize concatenated text again when combining marks can cross the boundary.

[Package overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
