# Silsile - Beta Release

This beta represents a major stabilization and capability jump from the last alpha.
Across the parser, elaborator, and GUI, the focus of the past cycle was:

- Correctness under real-world repositories.
- Deterministic, reproducible runs.
- Error tolerance instead of early aborts.
- Bringing elaboration from “experimental” to “usable”.

What follows is a concise but complete summary of what changed.

# What This Beta Is

This beta is an RTL-focused SystemVerilog frontend + elaboration pipeline, designed to:

- Parse large, imperfect, real repositories
- Preserve structure and intent even when code is broken
- Produce stable, structured outputs suitable for downstream tooling
- Provide a usable GUI for repository-scale work

Verification (UVM-heavy flows) is not the focus of this beta.
Support exists, but depth and polish will come later.

# Parser - Major Improvements
## 1. Real-World Robustness

The parser was hardened to survive code that other tools choke on:
- Aggressive error recovery (missing end, endmodule, malformed constructs)
- Unsupported or unknown constructs are skipped with diagnostics, not fatal errors
- Parsing continues even when diagnostics are severe

This alone eliminated hundreds of repo-blocking failures seen in alpha.

## 2. Class, Parameter, and Type System Fixes

Significant work went into correctness of modern SV features:
- Class parsing robustness and expanded AST coverage
- Full support for:
  - Type parameters in classes
  - Parameterized scope resolution
  - C#(...) specialization
- Correct elaboration of type parameters during parsing
- Resolution of constant member selects
- Accurate $bits width evaluation

These fixes remove a whole category of silent mis-elaborations present in alpha.

## 3. Constant Evaluation & Expression Fixes

- Correct handling of ({ ... }) expressions
- Fixed false-positive diagnostics around hand-picked real-world repositories
- Improved constant evaluation inside parameterized contexts
- Eliminated multiple repo-specific parse errors (Repo_1 class issues)

## 4. Verification & Language Coverage Expansion

While not the beta’s focus, coverage was extended:
- SVA, covergroups, coverage bins, options - parsed and preserved
- Strength-aware timing semantics implemented
- Specify blocks and timing checks supported
- Verification constructs retained through AST → elaboration

These are intentionally conservative but structurally sound.

# Elaborator - Newly Stabilized

This beta introduces the first stable elaboration pipeline.

## 1. Deterministic Runs

- Every elaboration run now produces:
  - A stable run_id
  - Grouped diagnostics
  - Deterministic ordering of results

Re-running the same inputs yields byte-stable outputs.

## 2. Parameter & Type Resolution

- Resolution of:
  - Type parameters
  - Constant member selects
  - $bits width evaluation
- Correct handling of:
  - defparam
  - Config / library units
  - Cross-unit references

This resolves multiple alpha-era inconsistencies.

## 3. Timing & Runtime Semantics

- Strength-aware timing semantics implemented
- Verification runtime added and validated
- Canonical file tables included in diagnostic reports
- Reports now clearly map diagnostics → source → elaborated context

# GUI — Usability & Scale Improvements

The GUI is still intentionally lightweight, but it is now repo-usable.

## 1. Repository-Scale Source Management

- Lazy file explorer (no full tree scan on load)
- Source autodetection for demo and repo runs
- Improved project flow when switching repositories

Large repos no longer freeze or stall the UI.

## 2. Elaboration Integration

- GUI flow updated to understand elaboration outputs
- Deterministic run reports surfaced cleanly
- Diagnostics grouped and presented consistently

## 3. Runtime Controls

- Exposed skip-zero-time-loops flag
- Persisted in project configuration
- Zero-time loop guards integrated end-to-end

This prevents common simulation-style hangs during elaboration.

# Diagnostics & Reporting

- Canonical file tables added to diagnostic outputs
- Diagnostics documentation expanded
- Reports now clearly separate:
  - Parse errors
  - Semantic issues
  - Elaboration-time failures
- Diagnostic stability improved (no random re-ordering)

# What This Beta Is Not (Yet)

To set expectations clearly:
- ❌ Not a full simulator
- ❌ Not a waveform viewer
- ❌ Not a UVM-complete verification engine
- ❌ Not performance-optimized for every corner case

Those are next-phase goals, not missing features.

# Why This Beta Matters

Compared to alpha, this release:

- Parses significantly more real code
- Survives broken repositories instead of aborting
- Produces deterministic, tool-grade outputs
- Establishes a solid elaboration foundation
- Makes the GUI practical for daily use

In short:
Alpha proved feasibility. Beta proves viability.

# Feedback & Next Steps

This beta exists to:

- Expose edge cases
- Validate elaboration semantics on real designs
- Prepare the ground for:
  - Simulator work
  - Waveform infrastructure
  - UVM-focused expansion
If it parses your repo, even imperfectly, it is doing its job.

# Thank you for testing the beta.
