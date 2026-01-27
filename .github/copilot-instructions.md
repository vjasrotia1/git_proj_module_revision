## Quick orientation

This is a small, single-module Java codebase with top-level source files (no packages or build tool detected). The main entrypoint is `Main.java` which prints a couple of lines. Other files (e.g., `A.java`, `B.java`, `C.java`, `hello/D.java`) are simple data-holder classes.

Key facts an automated coding agent should know immediately:

- Entrypoint: `Main.java` — run with `java Main` after compiling.
- No build system (no `pom.xml`, `build.gradle`, or `package.json`) found. Use `javac` for quick compile-and-run.
- Source layout: flat (root) plus a `hello/` subfolder. Files are not declared in packages.

## Quick start (commands)

Compile all sources and run Main (macOS / zsh):

```bash
javac *.java hello/*.java  # compile all .java files
java Main                  # run the entrypoint
```

If you add packages, update the compile/run commands accordingly (or add a build tool).

## Project structure & examples

- `Main.java` — application entrypoint. Example content: prints "Hello, World!" and a test line.
- `A.java`, `B.java`, `C.java` — small classes with only fields (POJO-like). Note: `B.java` currently defines class `b` (lowercase). This is an observable inconsistency; verify intent before renaming.
- `hello/D.java` — another small class in a subdirectory (no package declaration).

## Discoverable patterns and implications for edits

- No packages: files are in the default package. Adding package declarations is a breaking change for file locations and requires updating compilation commands and all `import` usages.
- Class/filename casing: Java convention is `ClassName` matching the filename. This repo has at least one mismatch (`B.java` -> `class b`). Avoid renaming or re-casing classes automatically; ask the human if you intend to normalize names.
- No test framework or CI detected. When adding tests, include a short README or a script to run them, and consider introducing a build tool (Maven/Gradle) if the project will grow.

## Tasks an AI agent can safely do (with examples)

- Small edits and text changes inside `Main.java` (e.g., change printed strings) — low risk.
- Add new helper classes in new files (follow existing flat layout) and reference them from `Main.java`.
- Add unit tests only after confirming preferred test framework (suggest JUnit) and adding a small README snippet on how to run them.

## Dangerous or high-friction changes — check with the user first

- Renaming or moving files (particularly changing package declarations or class names).
- Bulk refactors that assume a build system (introducing Maven/Gradle) without confirmation.

## Recommended short guidance for pull requests

- Keep changes minimal and compile locally with `javac` before creating a PR.
- If you change class names, include a short note explaining why and list the compilation command you used to verify correctness.

## Files to open first when investigating issues

- `Main.java` — to see the runtime behavior and entrypoint.
- `A.java`, `B.java`, `C.java`, `hello/D.java` — to understand data shapes and naming conventions.

If anything above is incomplete or you want me to include more examples (such as a suggested test runner or a starter `pom.xml`), tell me which direction to take and I will update this file.
