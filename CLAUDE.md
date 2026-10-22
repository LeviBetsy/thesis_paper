# Levi's Thesis

UC Irvine PhD dissertation, written in LaTeX using the `uci-thesis-latex` template.

## Topic

The thesis is about a mobile robot ("**Cyclops rover**") that performs perception and
navigation using a single front-mounted camera. Instead of relying on LiDAR, stereo
rigs, or ultrasonic range finders, the rover recovers per-pixel obstacle distance via
**monocular depth estimation (MDE)** with a **vision transformer (ViT)** backbone, and
uses that depth information as the observation model for **Monte Carlo localization**.
The motivating argument (see chapter2/chapter3) is that dedicated depth sensors add
cost, weight, and power draw that are hard to justify on a small, resource-constrained,
battery-powered platform — a single camera can serve both scene understanding and
range-finding.

## Structure

- `thesis.tex` — root document. Sets up packages/document class, `\input{preliminaries}`
  for front matter, then `\include`s each chapter file in order, followed by the
  bibliography and (currently commented out) appendix. Compile this file.
- `preliminaries.tex` — front-matter macros (title, author, committee, degree info,
  copyright, dedication, acknowledgments, CV, abstract). Still placeholder text — needs
  to be filled in with real thesis title/author/committee before submission.
  `\preliminarypages` is currently commented out in `thesis.tex`, so these pages are not
  rendered in the build yet.
- `ucithesis.cls` — UCI-specific formatting class; defines the macros used above. Not
  meant to be edited casually — it implements official UCI Thesis & Dissertation Manual
  requirements (see `uci-manual/`).
- `chapter1.tex` – `chapter7.tex` — one file per chapter, `\include`d from `thesis.tex`:
  1. Introduction — still template boilerplate, not written
  2. Literature Review — sections: Robot Perception, Robot Localization, Monocular Depth
     Estimation
  3. Monocular Depth Estimation — sections: Introduction to MDE (drafted), Vision
     Transformer Architecture in MDE, Monocular Depth to Range Finder
     (`\label{sec:mde-to-range}`)
  4. Localization — sections: Monte Carlo Localization, Cyclops Rover Motion Model,
     Cyclops Rover Measurement Model (`\label{ch:localization}`)
  5. Embedded System — title only, unwritten
  6. Result — title only, unwritten
  7. Conclusion — title only, unwritten
- `appendix.tex` — Lorem Ipsum placeholder; not currently included in the build.
- `thesis.bib` — bibliography (BibTeX). Only 2 entries so far (`CNN_Maze`, `UAV_NPU`),
  cited in chapter2/chapter3. Many `\todo{cite ...}` markers in the drafted text still
  need real references added here.
- `uci-manual/` — scraped copy of UCI's official Thesis & Dissertation Manual plus
  `scrape_manual.py`, used to check the template/formatting stays compliant over time.

## Build

- `make` — compiles `thesis.tex` via `latex` + `dvipdf` into `build/thesis.pdf`
  (see `Makefile`).
- `make show` — build, then open the PDF in `evince`.
- `make clean` — remove build artifacts.
- VS Code's LaTeX Workshop extension is configured (`.vscode/settings.json`) to output
  into `build/` as well.

## Conventions in this project

- Open citation needs are marked with `\todo{...}` (via the `todonotes` package) rather
  than left as bare TODO comments — keep using that pattern so they show up in the
  compiled PDF margin.
- Cross-references use `\label{sec:...}` / `\label{ch:...}` with short, kebab-ish names
  (e.g. `sec:mde-to-range`, `ch:localization`), referenced via `\ref{}`. Add a label
  whenever you add a `\ref{}` pointing at it, or the build will show `??`.
- Chapter files end with an Emacs local-variables footer
  (`%%% TeX-master: "thesis.tex" ...`) — keep this in any new chapter file so editors
  know the root document for compilation.
- Not a git repository yet (`.gitignore` exists but no `.git`/history).
