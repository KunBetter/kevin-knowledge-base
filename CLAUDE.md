# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Reading notes for **Think Complexity 2** by Allen B. Downey (Version 2.6.3, Green Tea Press). This is a note-taking repo — no build system, no code, no tests.

## Repository Structure

- **thinkcomplexity2/** — book content
  - `thinkcomplexity2.pdf` — the book PDF (used as reference for note-taking)
  - `notes/` — chapter-by-chapter reading notes in Chinese (`.md` files)
    - `README.md` — index with chapter titles and completion status
    - `chapter-01-*.md` through `chapter-06-*.md` — completed (6/12)
    - Chapters 7–12 + Appendix A remain unread

## Note-Taking Conventions

- Notes per chapter, named `chapter-XX-slug.md`
- Each note starts with a `# 第X章：标题 (English Title)` heading
- Content organized by `##` subsections matching the book's structure
- Dense use of **bold** for key terms and concepts
- Tables used for comparisons, summaries, and exercise lists
- Code snippets in fenced Python blocks where the book includes algorithms
- Chinese prose with English technical terms kept in English
- Each chapter ends with an exercise table
- Update `notes/README.md` when a chapter is completed (status → ✅, current chapter pointer)

## Book Source & Resources

- Official site: https://greenteapress.com/complexity/
- PDF: https://greenteapress.com/complexity/thinkcomplexity2.pdf
- GitHub repo (author's code): https://github.com/AllenDowney/ThinkComplexity2
- Key Python libraries used in the book: `networkx`, `numpy`, `scipy`
