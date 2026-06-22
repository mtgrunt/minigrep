# minigrep

A tiny clone of `grep`, built while working through **Chapter 12** of
*The Rust Programming Language* ("An I/O Project: Building a Command Line
Program").

## Usage

```sh
cargo run -- <query> <file_path>

# case-insensitive search
$env:IGNORE_CASE=1; cargo run -- <query> <file_path>
```

Example:

```sh
cargo run -- to poem.txt
```

## Chapter 12 synopsis

The chapter builds this project up section by section, using it as a
capstone that ties together structs, traits, lifetimes, closures, iterators,
and error handling.

- **12.1 — Accepting Command Line Arguments**
  Read args with `std::env::args()` and pull out the query and file path by
  position.

- **12.2 — Reading a File**
  Load the file's contents with `std::fs::read_to_string`.

- **12.3 — Refactoring to Improve Modularity and Error Handling**
  The core lesson: extract a `Config` struct and a `run` function out of
  `main`, return `Result` from fallible operations and propagate with `?`,
  and follow the book's "separation of concerns for binary projects"
  guideline — push logic into `src/lib.rs` and keep `main.rs` thin (parse
  config, call `run`, handle errors).

- **12.4 — Developing the Library's Functionality with TDD**
  Write a failing test for a `search` function first, implement it, then
  refactor to use iterators (`.lines().filter(...)`) instead of manual
  loops.

- **12.5 — Working with Environment Variables**
  Add case-insensitive search toggled by an `IGNORE_CASE` environment
  variable, read via `std::env::var` and plumbed through `Config`.

- **12.6 — Writing Error Messages to Standard Error Instead of Standard
  Output**
  Switch error output from `println!` to `eprintln!` so errors aren't
  mixed into redirected stdout.

The point of the chapter isn't `grep` itself — it's the workflow of
growing a single-file prototype into a testable, modular CLI with idiomatic
error handling.
