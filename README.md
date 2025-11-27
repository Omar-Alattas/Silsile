# About This Repo

This repository distributes the binaries and documentation for my proprietary SystemVerilog-2023 parser.
- The parser itself is closed-source.
- Binaries are available under the Releases tab.
- This repo is used for issues, feedback, and release notes.

# What’s Included

## 1. SystemVerilog-2023 Parser (C++ CLI)

- Fully custom tokenizer and parser written in C++.
- Parses entire project trees in one run.
- Outputs:
   - AST JSON
   - Diagnostics JSON
- Designed as the backend engine for future elaboration, simulation, and waveform tooling.

## 2. Desktop GUI (Alpha)

A lightweight front-end that manages .svproj workspaces and runs the parser without the command line.
- Project explorer automatically discovers .sv / .v files under the project root.
- GUI manages project creation, opening, and refreshing sources.
- Parser path, AST output path, and diagnostics path are stored in the .svproj.
- Console displays stdout/stderr in real time.
- “Run Parser” and “Stop” actions available from UI.
- Future tools (elaborator, waveform viewer, editor) will plug into the same workflow.

# Project File Format (.svproj)

The GUI stores project metadata using a simple, human-editable JSON schema.
- Fields include project name, root directory, parser path, AST/diagnostic outputs, source file list, include directories, and defines.
- All paths support relative resolution based on rootDir.
- Missing fields fall back to defaults.
- Designed to support automation, scripting, and CI flows.
- GUI regenerates source file lists on refresh, keeping the project synchronized.

Example schema (v1) is included in docs/gui_project_format.md.

# Current Purpose of This Alpha

This release is focused on:
- Testing parser stability on real-world SystemVerilog code.
- Gathering crash reports, incorrect tokenization cases, and malformed AST issues.
- Verifying GUI project management behavior.
- Collecting feedback before integrating elaboration and event-driven simulation.

This alpha is **not** feature-complete.
Many roadmap components are planned but intentionally not included yet.

# How to Use

1. Launch toolchain_gui.exe.
2. Create or open a project directory.
3. Place your .sv / .v files under the project root.
4. Refresh the source tree from the GUI.
5. Press Run Parser to generate AST + diagnostics.
6. Check the console for logs and parser output.

Detailed GUI workflow is documented in docs/gui_overview.md.

# Known Limitations (Alpha)

- Parser may crash on complex or unusual syntax.
- No elaboration or simulation yet.
- Include paths & macros are stored in .svproj but not yet forwarded to the CLI.
- GUI is minimal by design.

# How to Report Issues

Please include:
- The diagnostics JSON. (That'll be enough in general)
- The .svproj (if possible)
- The SystemVerilog sources that triggered the issue.

This is extremely helpful at this stage of development.

# Thank you for Testing

This project is still early, but your feedback directly influences how the toolchain evolves.
Thank you for trying the alpha and helping improve the future of EDA tooling.
