# Courses

Every Xenos training course: session decks, notes, and supporting files, organized one folder per course. Public so it can be served directly by GitHub Pages.

**Live hub:** https://smartvision-group.github.io/Courses/

## How this works

`index.html` fetches this repository's own file tree from the GitHub API at page-load time and renders it. There is nothing to hand-edit when you add a course, the hub reflects whatever is currently pushed to `main`.

```
You add a course folder, push to main
                │
                ▼
GitHub Pages serves this repository as-is
                │
                ▼
index.html asks the GitHub API "what's in this repo right now"
                │
                ▼
https://smartvision-group.github.io/Courses/
```

## Adding a new course

1. Create a new top-level folder in this repository, named for the course (for example `erpnext-fundamentals`). Folder names are title-cased automatically on the hub page (`erpnext-fundamentals` becomes "Erpnext Fundamentals"), so use readable, hyphen-separated names.
2. Add its files directly inside that folder. Subfolders are supported and rendered as nested, expandable sections, so a course can grow into `x/subfolder/...` without any changes to the hub.
3. Commit and push to `main`.
4. GitHub Pages redeploys automatically (usually under a minute). Refresh the live hub and the new course appears in the grid on its own.

Supported file types are recognized and labeled automatically (HTML decks, PDFs, Markdown notes, videos, images); anything else still shows up as a plain file.

## Structure

```
Courses/
  README.md
  index.html                  the dynamic hub page
  software-qa-testing/        example course: 3 session decks
    1-qa-fundamentals-intro.html
    2-developer-live-testing.html
    3-erpnext-implementer-live-testing.html
```
