---
title: "maskkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["MaskMatch", "TextMask"]
dependencies: []
symbols: ["MaskMatch", "TextMask"]
related: ["api.md", "getting-started.md", "index.md"]
---

# maskkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## MaskMatch

`Public Class MaskMatch`

Result coordinates count codepoints; ErrorPosition is -1 for valid input.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `IsValid` | `Boolean` | Yes | No | — | — |
| `IsComplete` | `Boolean` | Yes | No | — | — |
| `Text` | `String` | Yes | No | — | — |
| `ErrorPosition` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(valid As Boolean, complete As Boolean, text As String, errorPosition As Integer)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `valid` | `Boolean` | `ByVal` | Required |
| `complete` | `Boolean` | `ByVal` | Required |
| `text` | `String` | `ByVal` | Required |
| `errorPosition` | `Integer` | `ByVal` | Required |

Returns: no value.

## TextMask

`Public Class TextMask`

Immutable compiled text mask; input/mask limits are 4096 codepoints.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `SlotCount` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(pattern As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `pattern` | `String` | `ByVal` | Required |

Returns: no value.

### Match

`Public Function Match(text As String) As MaskMatch`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `MaskMatch` |

### Format

`Public Function Format(rawInput As String) As MaskMatch`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rawInput` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `MaskMatch` |

## MaskKit functions

### MatchMasks

`Public Function MatchMasks(masks As Array Of TextMask, text As String, rawInput As Boolean = False) As MaskMatch`

Prefer first complete match, otherwise first valid partial; stable input order.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `masks` | `Array Of TextMask` | `ByVal` | Required |
| `text` | `String` | `ByVal` | Required |
| `rawInput` | `Boolean` | `ByVal` | `False` |

#### Returns

| Type |
| --- |
| `MaskMatch` |
