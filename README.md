# Quiz CLI

This repository contains the source of the **Quiz CLI project blog**, created as part of the **PyLadies** community.

The blog documents the development of a team project whose goal is to build a quiz application running on a server and communicating with multiple clients over the network.

The blog is published using **GitHub Pages** and generated with **MkDocs**.

Live version: https://quiz-cli.github.io/



## Repository structure

This blog repository contains:
> Markdown blog posts

> MkDocs configuration

> static site configuration for GitHub Pages



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

Now you can see the blog exactly as it will look after deployment.

### 4. Writing a new blog post

> All blog posts live in the docs/ directory.

> Each post is one Markdown file

> Named for example: *2026-02-05-prvni-sraz.md*

> The post will automatically appear in the navigation if it is listed in mkdocs.yml.

### 5. Navigation configuration
Navigation is defined in mkdocs.yml:

```bash
nav:
  - První sraz: 2026-02-05-prvni-sraz.md
```
You can reorder posts or add new ones here.


## Deployment (GitHub Pages)

The blog is deployed automatically using GitHub Pages.

How it works:

> GitHub Pages is enabled for this repository

> source branch: main

> root folder: /docs

Every push to main updates the public website.

### Manual deploy (if needed)

```bash
mkdocs gh-deploy
```

### Contributing workflow

1. Create a new branch:

```bash
git checkout -b branch-name
```

2. Write your article in docs/

3. Commit changes:

```bash
git add .
git commit -m "Add blog post about first meeting"
```
4. Push branch:

```bash
git push origin new-blogpost
```

5. Create a Pull Request on GitHub.


