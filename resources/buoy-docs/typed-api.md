---
title: "normalizationkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: []
dependencies: []
symbols: ["NormalizationUnicodeVersion", "NormalizeNFC", "NormalizeNFD", "NormalizeNFKC", "NormalizeNFKD"]
related: ["api.md", "getting-started.md", "index.md"]
---

# normalizationkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## NormalizationKit functions

### NormalizationUnicodeVersion

`Public Function NormalizationUnicodeVersion() As String`

Unicode data version used by every form, independently of the host OS.

No parameters.

#### Returns

| Type |
| --- |
| `String` |

### NormalizeNFC

`Public Function NormalizeNFC(text As String, maxScalars As Integer = 1000000) As String`

Canonical decomposition followed by canonical composition (Unicode 18.0.0).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |
| `maxScalars` | `Integer` | `ByVal` | `1000000` |

#### Returns

| Type |
| --- |
| `String` |

### NormalizeNFD

`Public Function NormalizeNFD(text As String, maxScalars As Integer = 1000000) As String`

Canonical decomposition (Unicode 18.0.0).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |
| `maxScalars` | `Integer` | `ByVal` | `1000000` |

#### Returns

| Type |
| --- |
| `String` |

### NormalizeNFKC

`Public Function NormalizeNFKC(text As String, maxScalars As Integer = 1000000) As String`

Compatibility decomposition followed by canonical composition (Unicode 18.0.0).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |
| `maxScalars` | `Integer` | `ByVal` | `1000000` |

#### Returns

| Type |
| --- |
| `String` |

### NormalizeNFKD

`Public Function NormalizeNFKD(text As String, maxScalars As Integer = 1000000) As String`

Compatibility decomposition (Unicode 18.0.0).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |
| `maxScalars` | `Integer` | `ByVal` | `1000000` |

#### Returns

| Type |
| --- |
| `String` |
