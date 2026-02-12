# Quiz CLI – Project Blog

This repository contains the source of the **Quiz CLI project blog**, created as part of the **PyLadies** community.

The blog documents the development of a team project whose goal is to build a quiz application running on a server and communicating with multiple clients over the network.

The blog is generated using **MkDocs** and published via **GitHub Pages**.


Live version: https://quiz-cli.github.io



## Repository structure

This blog repository contains:
- Markdown blog posts (`docs/`)
- MkDocs configuration (`mkdocs.yml`)
- Generated static website (`site/`) used by GitHub Pages


The actual application code lives in separate repositories (server, client, admin, common).


## How to run the blog locally

### 1. Clone the repository (to your Quiz-CLI folder)

```bash
git clone https://github.com/quiz-cli/quiz-cli.github.io
cd quiz-cli.github.io
```

### 2. Install dependencies

```bash
pip install mkdocs mkdocs-material
```

### 3. Run local server

```bash
mkdocs serve
```
Open in browser: http://127.0.0.1:8000

This shows a development preview of the blog.


### 4. Build the static website

```bash
mkdocs build
```

This command generates the production-ready static website into the `site/` directory.

The content of this directory is what gets published publicly.

## Writing a new blog post
- All blog posts live in the `docs/` directory
- Each post is one Markdown file
- File name example: *2026-02-05-prvni-sraz.md*

The post will appear on the website once:
- It is added to the navigation in `mkdocs.yml`
- The site is rebuilt using `mkdocs build`


### 5. Navigation configuration
Navigation is defined in `mkdocs.yml`:

```yaml
nav:
  - První sraz: 2026-02-05-prvni-sraz.md
```
You can reorder posts or add new ones here.


## Deployment (GitHub Pages)

The blog is deployed using GitHub Pages.

How it works:

- GitHub Pages is enabled for this repository
- Source branch: `main`
- Published folder: `site/`
- The website is served as static HTML

GitHub does not run MkDocs itself — the static site must be generated locally using `mkdocs build` and committed to the repository.

Every push to `main` that updates the `site/` directory updates the public website.

### Contributing workflow
1. Create a new branch:
```bash
git checkout -b branch-name
```
2. Write or update content in docs/

3. Build the site:
```bash
mkdocs build
```
4. Commit changes (including the `site/` directory):
```bash
git add .
git commit -m "Update blog content"
```

5. Push branch:

```bash
git push origin branch-name
```

6. Create a Pull Request on GitHub.


