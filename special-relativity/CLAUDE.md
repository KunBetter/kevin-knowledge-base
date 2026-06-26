# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Reading notes for **狭义相对论通俗入门讲义** (Special Relativity — A Popular Introduction) by 王一 (Yi Wang), Department of Physics, HKUST. This is a note-taking repo — no build system, no code, no tests.

## Repository Structure

- **special-relativity/** — book content
  - `狭义相对论通俗入门讲义.pdf` — the lecture notes PDF (36 pages, used as reference for note-taking)
  - `notes/` — section-by-section reading notes in Chinese (`.md` files)
    - `README.md` — index with section titles and completion status

## Note-Taking Conventions

- Notes per section, named `chapter-XX-slug.md`
- Each note starts with a `# 第X节：标题 (English Title)` heading
- Content organized by `##` subsections matching the handout's structure
- Dense use of **bold** for key terms and concepts
- Tables used for comparisons, summaries, and exercise lists
- Code snippets in fenced blocks where the handout includes formulas
- Chinese prose with English technical terms kept in English
- Each section ends with a summary of key takeaways
- Update `notes/README.md` when a section is completed (status → ✅, current section pointer)

## Source

- PDF source: Compiled from LaTeX, part of "PHYS 2022, Yi Wang, Department of Physics, HKUST"
- GitHub: https://github.com/LLLgoyour/Handout
