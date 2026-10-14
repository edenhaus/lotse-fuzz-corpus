# lotse-fuzz-corpus

The libFuzzer corpora of [edenhaus/lotse](https://github.com/edenhaus/lotse)'s fuzz targets: one
directory per target (`<target>/`, named as in lotse's `fuzz/Cargo.toml`), each input a file named
by its SHA-1.

lotse's CI reads them on every run, so each target starts from what earlier runs found. Only
lotse's CI on `main` writes here, with a deploy key: after each run it replaces a target's directory
with the corpus that run minimized (libFuzzer's `-merge=1`, as `cargo fuzz cmin` does), so inputs
that no longer add coverage go away. This is not a place for pull requests; a corpus change belongs
in a fuzz run.

## Use it locally

From a lotse checkout:

```sh
git clone https://github.com/edenhaus/lotse-fuzz-corpus fuzz/corpus
mise run fuzz <target> [secs]
```

`fuzz/corpus/` is gitignored in lotse, and `scripts/fuzz.sh` reads and minimizes
`fuzz/corpus/<target>/` in place.

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  <https://www.apache.org/licenses/LICENSE-2.0>)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or
  <https://opensource.org/licenses/MIT>)

at your option, the same as lotse.
