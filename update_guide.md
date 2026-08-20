# Handbook Update Guide

This guide explains how contributors should update an existing handbook or add a new handbook to this repository.

The repository is used by a website, so folder structure, file names, and navigation files should be kept clean and predictable.

## Basic Rules

- Do not edit `LICENSE` unless the repository owner asks for a license change.
- Do not edit `README.md` unless the repository owner asks for a root README update.
- Keep handbook content in Markdown files with the `.md` extension.
- Use clear folders and subfolders so learners can browse by topic.
- Keep filenames descriptive and consistent.
- Avoid duplicate handbooks for the same topic.
- Check spelling, formatting, links, and examples before submitting changes.

## Updating an Existing Handbook

Use this process when improving, fixing, expanding, or reorganizing an existing handbook.

1. Find the correct handbook file inside the subject folder.
2. Read the existing table of contents and structure before editing.
3. Keep the current learning flow unless a reorganization is clearly needed.
4. Improve the content with useful explanations, examples, exercises, troubleshooting notes, diagrams, or references.
5. Fix outdated, unclear, incorrect, or duplicate content.
6. Keep headings consistent with the rest of the handbook.
7. Update the handbook's internal table of contents if headings were added, removed, or renamed.
8. Check all internal links and heading anchor links.
9. Make sure code examples are readable, safe, and beginner-friendly.
10. Review the final file for spelling, formatting, and copyright-safe content.

## Adding a New Handbook

Use this process when creating a new handbook that does not already exist.

1. Search the repository for the topic first.
2. If the topic already exists, improve the existing handbook instead of creating a duplicate.
3. Choose the correct top-level category.
4. Choose or create a useful subcategory folder.
5. Create the new handbook file inside that subcategory.
6. Add or update the nearest `INDEX.md` file so the new handbook appears in navigation.
7. If a new subcategory was created, update the parent folder's `INDEX.md`.
8. If a new top-level category was created, update `HANDBOOK_INDEX.md`.
9. Check that all navigation links work.
10. Review the handbook for quality, accuracy, and copyright safety.

## Folder Structure Pattern

Use this structure for organized navigation:

```text
Category/
  INDEX.md
  Subcategory/
    INDEX.md
    new_handbook_file.md
```

Example:

```text
JS/
  INDEX.md
  Frameworks/
    INDEX.md
    Angular/
      INDEX.md
      Angular_Master_Handbook.md
```

## Choosing a Category

Put the handbook where learners would naturally expect to find it.

Examples:

- JavaScript frameworks go under `JS/Frameworks/`.
- PHP frameworks go under `PHP/`.
- Python libraries go under `Python/`.
- Database handbooks go under `SQL/`.
- Personal development topics go under `PD/`.
- DevOps topics go under `Docker, Kubernetes, CI CD/` or a future `DevOps/` category if created.
- AI tools, agents, and generative AI topics go under `AI/`.

If the correct category does not exist, create a new top-level folder only when the topic is large enough to become a long-term section.

## Naming New Files

Use clear, descriptive Markdown filenames.

Good examples:

```text
React_Performance_Master_Handbook.md
Laravel_Testing_Master_Handbook.md
database_design_master_handbook.md
web_accessibility_master_handbook.md
```

Avoid names like:

```text
notes.md
new.md
handbook.md
final-final.md
topic1.md
```

## What To Include In a New Handbook

A useful handbook should include:

- A clear title.
- Who the handbook is for.
- Prerequisites.
- A table of contents.
- Beginner-friendly explanations.
- Practical examples.
- Common mistakes.
- Troubleshooting guidance.
- Best practices.
- Exercises or practice tasks.
- Interview or review questions where useful.
- Glossary for important terms.
- References to official or reliable sources where needed.

## Updating `INDEX.md`

Every folder that contains handbooks or subfolders should have an `INDEX.md`.

The index should include:

- A heading with the section name.
- A short navigation sentence.
- A `Subcategories` section if the folder contains subfolders.
- A `Handbooks` section if the folder contains handbook files.

Example:

```markdown
# JavaScript / Frameworks

Navigation index for this handbook section.

## Subcategories

- [Angular](Angular/INDEX.md)
- [React](React/INDEX.md)

## Handbooks

- [Next.js Master Handbook](Next.js/nextjs_master_handbook_in_depth.md)
```

## Updating `HANDBOOK_INDEX.md`

Update `HANDBOOK_INDEX.md` only when a new top-level category is added.

Example:

```markdown
- [Testing](Testing/INDEX.md)
```

Do not add every handbook directly to `HANDBOOK_INDEX.md`. That file should stay as a clean list of main categories.

## Navigation Checklist

Before finishing a change, check:

- The new or updated handbook is in the correct folder.
- The nearest `INDEX.md` links to the handbook.
- Parent `INDEX.md` files link to any new subcategory.
- `HANDBOOK_INDEX.md` links to any new top-level category.
- Links use relative paths.
- File and folder names in links match the actual names.
- The website can discover the `.md` file recursively.

## Content Quality Checklist

Before submitting, confirm:

- The handbook teaches in a clear order from basic to advanced.
- Examples are correct and easy to follow.
- Important terms are explained.
- Outdated claims are checked against reliable sources.
- Third-party content is not copied without permission.
- AI-assisted content has been reviewed by a human.
- Headings, tables, lists, and code blocks render correctly.
- The table of contents matches the headings.

## Suggested Workflow

```text
Search existing handbooks
      |
Choose update or new handbook
      |
Edit or create handbook
      |
Update local INDEX.md navigation
      |
Update parent INDEX.md if needed
      |
Update HANDBOOK_INDEX.md only for new top-level categories
      |
Check links and formatting
      |
Review quality and copyright safety
      |
Submit changes
```

## Final Rule

Make the repository easier for the next learner to browse and easier for the next contributor to maintain.
