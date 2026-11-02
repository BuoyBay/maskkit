# Partial-match text input masks

Compiled text masks for validating pasted values, recognizing partial
entry and formatting raw slot data. `Import maskkit`. No native dependencies.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add maskkit --git https://github.com/BuoyBay/maskkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API at a glance

`New TextMask(pattern)` compiles an immutable mask. `mask.Match(formatted)`
requires literal punctuation in the input; `mask.Format(raw)` consumes only slot
characters and inserts literals. Neither guesses whether a paste is raw or
formatted: the caller chooses the operation.

Both return an immutable `MaskMatch`: `IsValid`, `IsComplete`, normalized `Text`
and `ErrorPosition`. A valid prefix is valid but incomplete. Failure reports the
zero-based input codepoint index and accepted output prefix; valid results have
`ErrorPosition = -1`. Upper/lower slots normalize accepted text in both operations.
This result is a value to inspect, not an automatic edit to a native control.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer maskkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
