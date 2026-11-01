# MaskKit 0.1.0

Pure Buoy compiled text masks for validating pasted values, recognizing partial
entry and formatting raw slot data. `Import maskkit`. No native dependencies.

## API

`New TextMask(pattern)` compiles an immutable mask. `mask.Match(formatted)`
requires literal punctuation in the input; `mask.Format(raw)` consumes only slot
characters and inserts literals. Neither guesses whether a paste is raw or
formatted: the caller chooses the operation.

Both return an immutable `MaskMatch`: `IsValid`, `IsComplete`, normalized `Text`
and `ErrorPosition`. A valid prefix is valid but incomplete. Failure reports the
zero-based input codepoint index and accepted output prefix; valid results have
`ErrorPosition = -1`. Upper/lower slots normalize accepted text in both operations.
This result is a value to inspect, not an automatic edit to a native control.

| Pattern token | Accepted slot data |
| --- | --- |
| `#` | ASCII digit 0–9 |
| `L` | ASCII letter, converted to uppercase |
| `l` | ASCII letter, converted to lowercase |
| `A` | ASCII letter, case preserved |
| `*` | ASCII letter or digit |
| `.` | One codepoint excluding ASCII controls 0–31 and 127 |
| `\` followed by a character | That exact literal character |
| Any other character | That exact literal character |

The grammar is case-sensitive: lowercase `a` is literal. `^` is also literal;
this package does not implement upstream negated classes. ASCII control
characters and trailing escapes in patterns throw `InvalidArgumentException`.

`mask.SlotCount` reports data slots. All positions count Unicode codepoints,
not graphemes: emoji count as one slot; `e` plus combining acute counts as two.
Character classes deliberately do not infer Unicode letters/digits or apply
locale rules. String validity follows Buoy's String primitives; this package is
not a UTF-8 validator.

For `(###) ###-####`, raw `2125550199` becomes `(212) 555-0199`.
Raw `212` produces `(212`, delaying punctuation for the next incomplete field.
An empty raw value produces empty text when slots remain. Once all slots are
filled, trailing literals are inserted. A literal-only mask formats empty raw
data to its constant value. An empty mask accepts only empty input as complete.

`MatchMasks(masks, text, rawInput = False)` prefers the first complete match;
otherwise it returns the first valid partial match, or the first failure. The
list must contain 1–64 non-Nil masks and is validated before matching. This is
stable explicit preference, not inferred specificity. It returns a match value,
not the selected mask identity.

## Limits and integration

Patterns and inputs are limited to 4096 codepoints and 16384 bytes. Limits,
malformed patterns, empty/oversized alternative lists and Nil masks throw.
Ordinary input mismatches return invalid results. Evaluation uses bounded arrays
and scans each mask once after decoding the input. Alternative matching is at
most 64 scans. Results do not modify the input or compiled pattern.

Use this model after receiving committed input or on an explicit Format/Validate
action. Native selection, deletion, undo, accessibility, caret mapping and IME
composition need a separate adapter. Rejecting individual KeyDown events is not
proof of correct paste/IME behavior. The provided console example demonstrates
full values, partial input and alternative masks without asserting those UI
guarantees.

## Build and verification

The source package has compiler and BPM manifests. Seal it with
`buoy pkg seal . -o packages/maskkit-0.1.0.buipkg` using the real
compiler package command (on this host use `/usr/bin/buoy` for `pkg`).

Maintainers run the private validation suite before release. See the repository README for public build instructions.

See [provenance](../PROVENANCE.md) and the
example (not included in this repository).
