# bun-winmd

The `winmd` plugin of the Aphrody Bun fork: the `bun-winmd` executable that
`bun winmd` dispatches to (`src/runtime/cli/plugin_command.rs` in
[aphrody-labs/bun](https://github.com/aphrody-labs/bun)).

Imported from aphrody-labs/bun commit `f31829d8aa36e9f34e662c8a9e5edf6e25705c86` (src/plugins/winmd; find-msvc-tools stays in the Bun checkout's vendor/). That repository keeps the
earlier history.

## Install

Nothing to install: the first `bun winmd ...` downloads `bun-winmd-<target>` from the
release of the running bun, checks it against that release's `SHA256SUMS.txt`
and caches it in the plugin directory. A `bun-winmd` next to the bun executable
takes precedence.

## Build from source

This workspace path-depends on crates of the Bun checkout, so it builds only
mounted in it as `plugins/winmd` (an optional submodule, `update = none`):

```sh
git -C <bun checkout> submodule update --init --checkout --recursive plugins/winmd
bun bd --target=plugins          # build/<profile>/bun-winmd next to bun
# or directly:
cd <bun checkout>/plugins/winmd && cargo build --locked --profile plugin -p bun_plugin_winmd --bin bun-winmd
```

The toolchain is the Bun checkout's `rust-toolchain.toml`. `Cargo.lock` was
derived from the Bun workspace lockfile, so dependency versions match what the
fork built before the move.
