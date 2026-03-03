# Title: Hosting your Static Website on Github Pages with Pelican

___Statement of Purpose: This document is a practical guide which walks you through hosting a static resume site using Git, GitHub, Pelican and Markdown, additionally demonstrating Andrew Etter's core principles in the process.___

---
## Table of Contents

- [Pre-requisites](#pre-requisites)
- [Instructions](#instructions)
    -[Step 1 - Install Pelican](#step-1--install-pelican)
    -[Step 2 -](#step-2--create-your-github-repository)
    -[Step 3 - Set up your local project](#step-3--set-up-your-local-project)
    -[Step 4 - Write your resume in Markdown](#step-4--write-your-résumé-in-markdown)
    -[Step 5 - Choose a theme (optional)](#step-5--choose-a-theme-optional)
    

- [Features at a Glance](#features-at-a-glance)
    - [Drawing](#drawing)
    - [Input Handling](#input-handling)
    - [Layering](#layering)
    - [Text GUI Components](#text-gui-components)
    - [Animations](#animations)
    - [Shape and Box Drawing](#shape-and-box-drawing)
    - [Fonts and Tilesets](#fonts-and-tilesets)
    - [License](#license)
    - [Credits](#credits)
    - [Thanks](#thanks)

---

## PRE-REQUISITES
Before you begin, make sure you have the following installed and configured:

- **Git** — [git-scm.com](https://git-scm.com)
- **Python 3.8+** — [python.org](https://www.python.org)
- **pip** — comes with Python, used to install Pelican
- **A GitHub account** — [github.com](https://github.com)
- **A code text editor** — recommend Visual Studio Code (lets you see the markdown content preview in real time)
---
## INSTRUCTIONS

### Step 1 — Install Pelican

Open a command prompt terminal and install Pelican along with Markdown support:

```cmd
pip install pelican markdown
```

Verify the installation:

```cmd
pelican --version
```

### Step 2 — Create Your GitHub Repository

1. Log in to GitHub and click **New repository**.
2. Name it `your-username.github.io` (replace `your-username` with your actual GitHub username). Using this naming convention tells GitHub to treat the repository as a personal Pages site.
3. Set visibility to **Public**.
4. Do **not** initialize with a README — you will push your own content.
5. Click **Create repository**.

### Step 3 — Set Up Your Local Project

Clone the empty repository to your machine:

```cmds
git clone https://github.com/your-username/your-username.github.io.git
cd your-username.github.io
```

Run Pelican's quickstart to scaffold the project:

```cmd
pelican-quickstart
```

Answer the prompts as they appear. When asked for your site URL, enter `https://your-username.github.io`. When asked whether you want to use GitHub Pages, enter `y`.

The quickstart generates a structure like this:

```
your-username.github.io/
├── content/          ← your Markdown résumé goes here
├── output/           ← Pelican writes built HTML here (do not edit manually)
├── pelicanconf.py    ← site settings
├── publishconf.py    ← production settings
└── Makefile
```

### Step 4 — Write Your Résumé in Markdown

Create a file at `content/resume.md`. Pelican requires a small metadata header at the top, for example the .md file could look like:

```markdown
### METADATA (dont include)

Title: Resume
Date: 2026-01-01
Save_as: index.html

---

### RESUME (dont include)

## Jane Smith

jane@example.com | github.com/jane | linkedin.com/in/jane

---

## Education

**University of Manitoba** — B.Sc. Computer Science, 2024

---

## Experience

**Software Developer Intern — Acme Corp** *(May–August 2023)*

- Built and maintained REST APIs using Python and Flask
- Reduced average response time by 30% through query optimization
- Wrote internal documentation adopted by three other teams

---

## Skills

Python, Git, Linux, SQL, Markdown, Technical Writing
```

The `Save_as: index.html` directive tells Pelican to make this page the site root, so visitors who go to `https://your-username.github.io` land directly on your résumé.

### Step 5 — Choose a Theme (Optional)

Pelican's default theme is functional but plain. You can browse community themes at [github.com/getpelican/pelican-themes](https://github.com/getpelican/pelican-themes). To install one:

```cmd
git clone --recursive https://github.com/getpelican/pelican-themes themes
```

Then reference it in `pelicanconf.py` by copying the path depending on your folder structure to the theme like below:

```python
THEME = "path to pelican theme goes here" 
e.g
THEME = 'pelicanthemes/sneakyidea'  # or whichever theme you chose
```

### Step 6 — Build the Site

Generate the static output:

```cmd
pelican content -s pelicanconf.py
```

Pelican writes everything to the `output/` directory. You can preview it locally with:

```cmd
pelican --listen
```

Open `http://localhost:8000` in your browser to review your site before publishing.

### Step 7 — Publish to GitHub Pages

GitHub Pages can serve from the root of a branch or from a `docs/` folder. The simplest approach is to build into a `docs/` folder and push everything to `main`.

Update `pelicanconf.py` to write output there:

```python
OUTPUT_PATH = "docs/"
```

Rebuild:

```cmd
pelican content -s pelicanconf.py
```

Now commit and push everything:

```cmd
git add .
git commit -m "Publish résumé site"
git push origin main
```

Finally, configure GitHub Pages:

1. Go to your repository on GitHub.
2. Click **Settings → Pages**.
3. Under **Branch**, select `main` and set the folder to `/docs`.
4. Click **Save**.

GitHub will display a confirmation banner with your live URL. It typically takes one to two minutes to go live.   

---
## MORE RELEVEANT RESOURCES/READINGS  
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/) - Helpful with reminding me of the specific syntax that markdown uses for certain features. 
- [Pelican documentation](https://docs.getpelican.com)
- [GitHub Pages documentation](https://docs.github.com/en/pages)
- [Markdown guide](https://www.markdownguide.org)
- Andrew Etter, *Modern Technical Writing: An Introduction to Software Documentation* (2016)  

---
### FAQ
| Question | Answer|
| :---     |  :--- |
| "**Why is Markdown better than writing raw HTML?**| Markdown provides an abstraction layer that lets you express the same document structure with far less syntax than raw HTML requires. A second-level heading in Markdown is `## My Heading`; in HTML it is `<h2>My Heading</h2>` — and that gap grows quickly across a full document. More importantly, Markdown keeps the source file readable as plain text, so you can review and edit your résumé in any editor without needing to mentally parse angle brackets and closing tags. Etter highlights exactly this point: lightweight markup languages lower the barrier to contribution and keep the source of truth human-friendly.|  
| **I changed the Markdown version of my resume, so why don’t I see the changes when I refresh the website in my browser?** | Pelican is a static-site generator, which means it reads your Markdown source files and produces finished HTML files once, on demand. It does not watch for changes automatically. Every time you edit `resume.md`, you must rerun `pelican content -s pelicanconf.py` in your terminal to regenerate the `docs/` folder. After rebuilding, refresh your browser to see the updated output locally. When you are ready to publish the updated version, commit the regenerated files and push to GitHub as described in Step 7.|
| **Do I need to pay anything to host my résumé this way?** | No. GitHub Pages is free for public repositories, and Pelican is open-source software. The only cost is your time. This is one of the practical advantages of the toolchain Etter recommends: the entire pipeline from writing to publishing uses freely available, community-maintained tools. |


---
## Credits
**Author:** Gideon Ashiru  
**Peer Reviewers:** Anne, William  
**Third-party theme:** [SneakyIdea for Pelican](https://pelicanthemes.com/sneakyidea/) - used to style the published résumé site.  