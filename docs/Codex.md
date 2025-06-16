# Beginner’s Guide - MkDocs

## Introduction

Looking to build a sleek, straightforward website for documentation, tutorials, or project notes? MkDocs makes it incredibly simple and efficient. This guide covers everything from installing MkDocs to launching your very own website online.

## What is MkDocs?

MkDocs is a tool that transforms your Markdown files into a fully static website. It’s specially crafted for documentation but works perfectly for any content written in Markdown.

- Markdown: A lightweight syntax for formatting text using plain characters (e.g., # for headers, - for lists, [link](url) for hyperlinks).

- Static Website: A site composed of fixed files like HTML, CSS, and JavaScript—no backend or database needed, resulting in fast loading and simple hosting.

## Setting Up Your Environment

* **Python** installed on your computer.
  MkDocs runs with Python, so this is required.
  To check if you have Python installed, open your terminal (or Command Prompt) and run:

  ```bash
  python --version
  ```

  or

  ```bash
  python3 --version
  ```

  If you don’t have Python installed, download it from [python.org](https://www.python.org/downloads/) and follow the installation instructions.

### Install MkDocs

Once Python is ready, install MkDocs using Python’s package manager, `pip`:

```bash
pip install mkdocs
```

* **pip**: The tool that installs Python packages.
* After this, you have MkDocs installed on your machine.

## Create Your First MkDocs Project

Now, create a new folder for your site project.

In your terminal, run:

```bash
mkdocs new my-site
```

This command does a few things:

* Creates a folder named `my-site`.
* Inside `my-site`, you’ll find:

  * A configuration file called `mkdocs.yml`
  * A folder named `docs` with a sample Markdown file `index.md`

!!! note "What’s in `mkdocs.yml`?"
    This file controls how your website looks and behaves. It tells MkDocs the site’s title, what theme to use, and how to structure navigation.

## Understanding the Project Structure

Your MkDocs project folder contains:

* `mkdocs.yml`: The configuration file for your site.
* `docs/`: Folder that contains all the Markdown files which form the content of your website.

  * `index.md`: This is your homepage content file.

!!! "Markdown"
    Markdown is a simple text format for writing content that converts easily into formatted HTML. It’s easy to read and write.

## Writing Your Content

Open the file `docs/index.md` with any text editor (Notepad, VSCode, Sublime Text, etc.).

Try writing:

```markdown
# Welcome to My Documentation Site

This is my **very first** documentation page made with MkDocs!

## What can I do here?

- Write documentation easily
- Preview live changes
- Publish online
```
??? note "Explanation of Markdown used"
    
    `#` — Main heading (H1).
    `##` — Subheading (H2).
    `**text**` — Bold text.
    `-` — Unordered list.

## Add More Pages and Setup Navigation

Suppose you want to add an About page:

- Create a new file inside `docs/` called `about.md`.

- Add some content in `about.md`:

```markdown
# About This Site

This website is created using MkDocs to demonstrate documentation.
```

Open `mkdocs.yml` and find the navigation section (it may look like this by default):

```yaml
nav:
  - Home: index.md
```

Update it to include your new page:

```yaml
nav:
  - Home: index.md
  - About: about.md
```

- Each item consists of a label and a corresponding Markdown file.

- You can create nested navigation like this:

```yaml
nav:
  - Home: index.md
  - Guide:
      - Introduction: guide/introduction.md
      - Installation: guide/installation.md
```

This creates a dropdown menu "Guide" with two subpages.

## Choose a Theme

Themes control how your site looks — colors, fonts, layout.

### How to set a theme?

In `mkdocs.yml`, look for the `theme` section:

```yaml
theme:
  name: readthedocs
```

Some popular themes:

* `readthedocs` (default)
* `material` (modern, clean)
* `mkdocs` (basic)

**Material theme** is very popular and professional looking. To use it:

```yaml
theme:
  name: material
```
!!! "Note"
    For some themes, you may need to install extra dependencies. But `material` works directly with MkDocs.

## Preview Your Site Locally

After writing some content, see it live on your computer before publishing.

Run this command inside your project folder:

```bash
mkdocs serve
```

* MkDocs starts a local web server.
* Open your browser and visit: `http://127.0.0.1:8000/`
* Your site will appear!
* Any changes to Markdown files will automatically reload the page — so you can edit and instantly preview.

## Build Your Site for Deployment

Once you’re happy with your content and layout, you need to **build** the site.

Building converts your Markdown into HTML, CSS, and JS files inside a folder named `site/`.

Run:

```bash
mkdocs build
```

* The `site/` folder is ready to be uploaded to any static web host.

## Publish Your Site Online

1. **GitHub Pages**

   * Free hosting service for static sites.
   * Works great with MkDocs.
   * You push your built site to a special branch (`gh-pages`) on your GitHub repo.

2. **Netlify or Vercel**

   * Easy to connect to your GitHub repo.
   * Automatically deploy when you push changes.
   * Supports custom domains and HTTPS.

## Deploy Directly to GitHub Pages Using MkDocs

If you have a GitHub repo for your project, MkDocs can deploy your site in one step.

Run:

```bash
mkdocs gh-deploy
```

What happens:

* MkDocs builds the site.
* Pushes the `site/` folder content to the `gh-pages` branch of your GitHub repository.
* Your website is then available at:

```
https://<your-github-username>.github.io/<repo-name>/
```

## Important Tips

### Headings and Structure Matter

* Use proper heading levels (`#`, `##`, `###`) to organize your content.
* MkDocs generates a **Table of Contents (ToC)** from headings — helps visitors navigate pages easily.

### Navigation (`nav`) is your website menu

* The order and nesting in the `nav` section controls how your menu looks.
* Keep it simple and logical.

### Markdown makes writing easy

* No need to learn HTML.
* Supports links, images, lists, tables, code blocks, and more.

## Summary of Commands You’ll Use

| Command              | What it does                              |
| -------------------- | ----------------------------------------- |
| `pip install mkdocs` | Install MkDocs                            |
| `mkdocs new my-site` | Create a new project                      |
| `mkdocs serve`       | Start local server and preview site       |
| `mkdocs build`       | Generate static files to publish          |
| `mkdocs gh-deploy`   | Deploy site to GitHub Pages automatically |



