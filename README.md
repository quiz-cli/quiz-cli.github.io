# Quiz CLI – Project Blog

This repository contains the source of the **Quiz CLI project blog**, created as part of the **PyLadies** community.

The blog documents the development of a team project whose goal is to build a quiz application running on a server and communicating with multiple clients over the network.

The blog is generated using **MkDocs** and published via **GitHub Pages**.


Live version: https://quiz-cli.github.io



## Repository structure

- Markdown blog posts (`docs_src/`)
- Generated static website (`docs/`)
- MkDocs configuration (`mkdocs.yml`)


The actual application code lives in separate repositories (server, client, admin, common).


## How to run the blog locally

### Clone the repository

```bash
git clone https://github.com/quiz-cli/quiz-cli.github.io
cd quiz-cli.github.io
```

### Install dependencies

```bash
pip install mkdocs mkdocs-material
```

### Run local server

```bash
mkdocs serve
```
Open in browser: http://127.0.0.1:8000

This shows a development preview of the blog.


## Writing a new blog post
- All blog posts live in the `docs_src/` directory
- Each post is one Markdown file
- File name example: *2026-02-05-prvni-sraz.md*

The post will appear on the website once:
- It is added to the navigation in `mkdocs.yml`
- The site is rebuilt using `mkdocs build`
- The changes are pushed to GitHub


### Navigation configuration
Navigation is defined in `mkdocs.yml`:

```yaml
nav:
  - Úvod: index.md
  - První sraz: 2026-02-05-prvni-sraz.md
# - Druhý sraz:
# - Třetí sraz:
# - Čtvrtý sraz:
```
You can reorder posts or add new ones here.


## Deployment (GitHub Pages)

The blog is deployed using GitHub Pages.

How it works:

- GitHub Pages is enabled for this repository
- Source branch: `main`
- Published folder: `docs/`
- The website is served as static HTML

GitHub does not run MkDocs itself — the static site must be generated locally.

## Build and publish
To publish changes:
```bash
mkdocs build
git add docs
git commit -m "Build static site"
git push
```
Every push to `main` that updates the `docs/` directory updates the public website.

### Contributing workflow
1. Create a new branch:
```bash
git checkout -b branch-name
```
2. Write or update content in `docs_src/`

3. Build the site:

```bash
mkdocs build
```

4. Commit changes:
```bash
git add .
git commit -m "Update blog content"
```

5. Push branch:

```bash
git push origin branch-name
```

6. Create a Pull Request on GitHub.


