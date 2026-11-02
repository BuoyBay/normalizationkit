# Unicode NFC / NFD / NFKC / NFKD

Portable Unicode 18.0.0 normalization. `Import normalizationkit` exposes
`NormalizeNFC`, `NormalizeNFD`, `NormalizeNFKC`, `NormalizeNFKD` and
`NormalizationUnicodeVersion()`. Copy `packages/normalizationkit-0.1.0.buipkg`
into a consumer's packages directory. No native libraries or other packages are required.

Functions return fresh String values and leave input unchanged. Empty input stays
empty. Hangul syllables and conjoining jamo use algorithmic decomposition and
composition; other mappings, combining classes and composition exclusions use
bundled Unicode tables. Equal combining classes retain their original order.
The same data and algorithm run on macOS, Windows and Linux, independently of
installed ICU or operating-system Unicode versions. Scalars without mappings
in Unicode 18.0 are retained, rather than interpreted using a newer host database.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add normalizationkit --git https://github.com/BuoyBay/normalizationkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API entrypoints

- `Import normalizationkit`
- `NormalizeNFC`
- `NormalizeNFD`
- `NormalizeNFKC`
- `NormalizeNFKD`

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer normalizationkit
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
