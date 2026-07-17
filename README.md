# sessiometer/homebrew-tap

The [Homebrew](https://brew.sh) tap for **[sessiometer](https://github.com/alexey-pelykh/sessiometer)** — manage multiple Claude Code accounts and swap credentials before exhaustion.

This tap delivers the **CLI + daemon** — sessiometer's headless, scripting channel for terminal and automation use. The macOS menu-bar `.app` will land here too, as a Homebrew **cask** in `Casks/` beside `Formula/`, once it is signed + notarized (not yet shipped).

## Install

```sh
brew tap sessiometer/tap
brew install --HEAD sessiometer/tap/sessiometer
```

sessiometer is still **pre-release** — there is no tagged version yet, so install from `HEAD` (the `main` branch of the source repo). `brew install --HEAD` compiles the Rust crate from source (with the committed `Cargo.lock`, via `--locked`, for a reproducible build) and puts the `sessiometer` binary on your `PATH`. It is locally compiled — no notarization or code-signing; those belong to the parallel GUI channel (the notarized `.app` / cask), not this one.

Once the first stable release is tagged, the formula gains a `url` + `sha256` stanza and a plain `brew install sessiometer/tap/sessiometer` (no `--HEAD`) will work too.

**No `brew trust` step is needed** for the commands above. Homebrew's default-on `HOMEBREW_REQUIRE_TAP_TRUST` won't load formulae from an untrusted third-party (non-official) tap — so `brew tap-info sessiometer/tap` reports it as `Untrusted` — but Homebrew treats naming the tap (`sessiometer/tap`) or the fully-qualified formula (`sessiometer/tap/sessiometer`) on the command line as explicit consent, so the gate never fires here. Each command above names one or the other on purpose.

The gate only fires if you refer to the formula by its **bare short name before it is installed** — e.g. `brew info sessiometer` on a clean machine — which Homebrew refuses with *"Refusing to load formula … from untrusted tap."* Use the fully-qualified name, or trust the tap once:

```sh
brew trust --formula sessiometer/tap/sessiometer   # or trust the whole tap: brew trust sessiometer/tap
```

Verify the build:

```sh
brew test sessiometer/tap/sessiometer
```

From there the swap/monitor loop runs headless: `sessiometer run` for a foreground daemon, or `sessiometer service install` to keep one running at login. See the [main README](https://github.com/alexey-pelykh/sessiometer#readme) for the full quickstart.

## What's here

| Path | What |
|------|------|
| [`Formula/sessiometer.rb`](Formula/sessiometer.rb) | The CLI + daemon formula (source build, HEAD-only) |

The formula is a **one-way mirror** of the canonical [`Formula/sessiometer.rb`](https://github.com/alexey-pelykh/sessiometer/blob/main/Formula/sessiometer.rb) that lives in the source repo — the source copy stays authoritative; do not hand-edit the copy here. Today the mirror is seeded and updated **by hand**; a release-CI job *will* sync it automatically on tagged releases ([sessiometer#559](https://github.com/alexey-pelykh/sessiometer/issues/559)).

## Unofficial

sessiometer is **not affiliated with, or endorsed by, Anthropic**, and is distributed under the [MIT license](LICENSE). "Claude Code" is referenced only nominatively — naming the tool sessiometer works with. This tap carries no third-party logos or marks, and its distribution-facing metadata stays neutral and factual.
