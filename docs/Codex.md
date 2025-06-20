# Material for MkDocs

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) is a powerful tool for building beautiful, interactive documentation websites. It comes packed with features that make your content more engaging, organized, and easy to navigate.

Some of the standout features include:

* Customizable color themes to match your brand or style
* Smart code blocks that automatically adjust based on the programming language
* Content tabs to keep related information neatly grouped
* Callouts (also known as admonitions) to highlight key points or warnings
* Built-in support for diagrams that render directly in your documentation

## Prerequisites

Before you get started, make sure you have the following tools installed:

* **Python** – Required to run MkDocs
* **pip** – Python's package manager (comes bundled with Python 3.4 and above)
* **Visual Studio Code** (or any code editor of your choice)
* **GitHub Account** – We'll use this to deploy the site using GitHub Pages

## Initial Setup

Follow these steps to set up your environment and create your documentation project:

### 1. **Open a Terminal**

Navigate to the folder where you want to create your project.

### 2. **Verify Python Installation**

Run one of the following commands to check if Python is installed:

```bash
which python
```

or

```bash
which python3
```

### 3. **Set Up a Virtual Environment**

Create a virtual environment:

```bash
python -m venv venv
```

Activate the virtual environment:

* On **macOS/Linux**:

  ```bash
  source venv/bin/activate
  ```

* On **Windows**:

  ```bash
  .\venv\Scripts\activate
  ```

### 4. **Check pip Version**

Ensure `pip` is available:

```bash
pip --version
```

### 5. **Install MkDocs with Material Theme**

Install the necessary package:

```bash
pip install mkdocs-material
```

---

## Set Up the Project

### 6. **Open the Project in Visual Studio Code**

From the terminal, launch VS Code in the current directory:

```bash
code .
```

Then open the integrated terminal inside VS Code and reactivate your virtual environment if needed.

---

### 7. **Create a New MkDocs Site**

Initialize a new site in the current folder:

```bash
mkdocs new .
```

---

### 8. **Basic Configuration**

Edit the generated `mkdocs.yml` file and update it like so:

```yaml
site_name: My MkDocs Material Documentation
site_url: https://sitename.example
theme:
  name: material
```

> 🔧 You can change the `site_name` and `site_url` to match your project.

---

### 9. **Preview Your Site**

To start the local development server:

```bash
mkdocs serve
```

Open your browser and visit: [http://localhost:8000](http://localhost:8000)

You should now see your MkDocs site running with the Material theme!



## Enable YAML Schema Validation

To unlock many powerful features in **Material for MkDocs**, you'll often need to edit the `mkdocs.yml` file. YAML schema validation makes this process easier by providing helpful tooltips, suggestions, and error highlighting right inside your editor.

### Step 1: Install YAML Extension

In **Visual Studio Code**, install the **Red Hat YAML extension**:

1. Go to the **Extensions** tab on the left sidebar.
2. Search for **"YAML" by Red Hat**.
3. Click **Install**.

### Step 2: Open `settings.json`

To access your user settings file:

* Click the ⚙️ **gear icon** in the lower-left corner of VS Code.
* Then click the 📄 **document icon** in the top-right corner of the Settings pane.

This opens your `settings.json` file for editing.

### Step 3: Add Schema and Custom Tags

At the bottom of your `settings.json` file, add the following:

```json
"yaml.schemas": {
  "https://squidfunk.github.io/mkdocs-material/schema.json": "mkdocs.yml"
},
"yaml.customTags": [
  "!ENV scalar",
  "!ENV sequence",
  "!relative scalar",
  "tag:yaml.org,2002:python/name:material.extensions.emoji.to_svg",
  "tag:yaml.org,2002:python/name:material.extensions.emoji.twemoji",
  "tag:yaml.org,2002:python/name:pymdownx.superfences.fence_code_format"
]
```

Once added, you’ll start seeing tooltips when you hover over entries in `mkdocs.yml`, along with real-time error highlighting to prevent syntax issues.

## Customize the Color Scheme

Now let’s enhance the visual appearance of your documentation using **Material’s color palette system**.

### Enable Dark Mode

To start, change the theme to use a dark color scheme. In your `mkdocs.yml`, add:

```yaml
theme:
  name: material
  palette:
    scheme: slate
```

### Set a Primary Color

You can also set a **primary color**, which controls the color of the site banner and links:

```yaml
theme:
  name: material
  palette:
    scheme: slate
    primary: green  # 🟢
```

### Add a Light/Dark Mode Toggle

You can let users switch between light and dark modes with a toggle. Here's how to configure it:

```yaml
theme:
  name: material
  palette:
    # Dark Mode
    - scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Dark mode
      primary: green
      accent: deep purple

    # Light Mode
    - scheme: default
      toggle:
        icon: material/weather-night
        name: Light mode
      primary: blue
      accent: deep orange
```

This setup displays a toggle button in the site header that lets users switch themes manually.

## Want to Do More?

Material for MkDocs supports many more customization options, from setting your own color values, to auto-switching themes based on system preferences or even time of day.

🔗 For full details, check out the [Material for MkDocs color customization guide](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/).

## Publish Your Site to GitHub Pages

Once your MkDocs site is ready, you can publish it online for free using **GitHub Pages** and **GitHub Actions**. Follow the steps below to automate the deployment.

### 1. Create the Deployment Workflow

In your project folder, create the file:
`.github/workflows/ci.yml`

Then paste the following workflow configuration:

```yaml
name: ci

on:
  push:
    branches:
      - master
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com

      - uses: actions/setup-python@v5
        with:
          python-version: 3.x

      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV

      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-

      - run: pip install mkdocs-material

      - run: mkdocs gh-deploy --force
```

This GitHub Action will automatically build and deploy your MkDocs site whenever you push to the `main` or `master` branch.

### 2. Set Up the GitHub Repository

1. **Create a new repository** on [GitHub](https://github.com).

2. In your project terminal, initialize Git and connect your remote:

   ```bash
   git init
   git remote add origin https://github.com/your-username/your-repo-name.git
   ```

3. **Add, commit, and push your code** to the `main` branch:

   ```bash
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git push -u origin main
   ```

### 3. Configure GitHub Pages

1. Go to your repository on GitHub.
2. Click on **Settings** → **Pages**.
3. Under **Source**, select:

   * **Branch**: `gh-pages`
   * **Folder**: `/ (root)`

GitHub will now serve your site from the `gh-pages` branch. 





