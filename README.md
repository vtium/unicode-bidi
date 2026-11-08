# unicode-bidi

This crate implements the [Unicode Bidirectional Algorithm][tr9] for display of
mixed right-to-left and left-to-right text. It is written in safe Rust,
compatible with the current stable release.

[Documentation](https://docs.rs/unicode-bidi)

[![CI](https://github.com/servo/unicode-bidi/actions/workflows/main.yml/badge.svg)](https://github.com/servo/unicode-bidi/actions)
[![AppVeyor](https://img.shields.io/appveyor/ci/servo/unicode-bidi/main.svg)](https://ci.appveyor.com/project/servo/unicode-bidi)

[tr9]: https://www.unicode.org/reports/tr9/

## vtium's fork

This repository is vtium's fork of [servo/unicode-bidi](https://github.com/servo/unicode-bidi). vtium is a terminal for the Linux console, and its crate vtium-term uses this crate for right-to-left text. The branch `vtium/fixes` holds what vtium depends on: servo's main branch, merged in, plus the changes below. vtium-term pins an exact commit of that branch in its Cargo.toml. Nothing from this fork is sent upstream.

The branch changes three things from servo's main branch:

- `visual_runs` returns no level runs for an empty line. Before, it panicked with an index out of bounds on an empty line at the end of the text and on any line of an empty text, and `reorder_line`, which calls it, panicked with it. The deprecated free function `visual_runs` gets the same fix.
- The tables and the conformance test data are at Unicode 18.0.0. vtium-term's own Unicode tables are at the same version.
- `tools/generate.py` reads each codepoint's Bidi_Class from DerivedBidiClass.txt, so unassigned codepoints take the defaults the Unicode Character Database gives them. It used to take them from a list of ranges in the script, which had fallen behind the database.

The crate's licence (MIT or Apache-2.0, at your option), its authors and its copyright notices are unchanged. See LICENSE-MIT, LICENSE-APACHE, COPYRIGHT and AUTHORS.
