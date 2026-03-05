# Hosting your resume on a Static Website

___Purpose: This guide walks you through creating a personal resume website and publishing it online for free using platforms like Markdown, Pelican, Git, and GitHub Pages. If you are comfortable with Markdown, but have no prior experience with version control, static site generators, or web hosting, this guide will help you just fine. Along the way, it connects each step to the technical writing principles in Andrew Etter's *Modern Technical Writing*.___

---
## Table of Contents
- [Title](#title-hosting-your-static-website-on-github-pages-with-pelican)
- [Pre-requisites](#pre-requisites)
- [Instructions](#instructions)  
    - [Step 1 - Install Pelican](#step-1---install-pelican)
    - [Step 2 - Create your Github repository](#step-2---create-your-github-repository)
    - [Step 3 - Connect your computer to Github](#step-3---connect-your-computer-to-github)
    - [Step 4 - Set up the Pelican Project](#step-4-set-up-the-pelican-project)
    - [Step 5 - Write your resume in Markdown](#step-5---write-your-resume-in-markdown)
        - [Step 5.1 - Choose a theme (optional)](#step-51---choose-a-theme-optional)
    - [Step 6 - Build the Site & Preview the site Locally](#step-6---build-the-site--preview-the-site-locally)
    - [Step 7 - Publish to GitHub Pages](#step-7---publish-to-github-pages)
- [More resources & readings](#more-releveant-resourcesreadings)
- [Frequently Asked Questions](#faq)
- [Credits](#credits)


---

## PRE-REQUISITES
Before you start, you will need the following installed and set up on your computer.
- **Git** - a version control system used to keep track of changes in your code and can send your site to GitHub. Download at [git-scm.com](https://git-scm.com). 
- **Python 3.8 or later** - the programming language Pelican runs on. Download at [python.org](https://www.python.org). During installation, check the box that says **"Add Python to PATH"** 
- **pip** - used to install Python packages such as Pelican. It is included automatically when downloading Python.
- **A GitHub account** - a free account at [github.com](https://github.com). This platform will host your finished website.
- **A code editor** - Visual Studio Code is recommended for its live Markdown preview. Download at [code.visualstudio.com](https://code.visualstudio.com).
---

## INSTRUCTIONS

### Step 1 - Install Pelican

**Etter's Principle: Use lightweight, markup tools e.g. Markdown**  
Etter argues that writers should favour simple, open-source tools over expensive proprietary software, tools with defined standards and clean syntax that let you just focus on writing. Pelican is a static site generator that supports one of these lightweight markup tools 'Markdown'.

Open your terminal, navigate to the directory where you want to store this project and run the following to intall pelican with markdown support:
```
python -m pip install "pelican[markdown]"
```

To confirm installation:

```
pelican --version
```

You should see a version number such as `4.9.1` or `later`. If you see an error, re-run the Python installer, choose "Modify", and check "Add Python to environment variables".

---

### Step 2 - Create Your GitHub Repository

**Etter's Principle: Store documentation in a version-controlled, publicly accessible location.**  
Etter emphasises that documentation should live somewhere easy to find and always available to its audience. GitHub provides this and more through a permanent public URL, automatic version history, and a popular community supported platform.

1. Log in to GitHub and click the green **New** button near the top left.
2. In the **Repository name** field, give it an appropriate name.
3. Set visibility to **Public** - GitHub Pages requires this for free accounts.
4. Leave all "Initialize this repository with" checkboxes **unchecked**.
5. Click **Create repository** and leave the tab open.


### Step 3 - Connect your computer to Github


**Etter's Principle: Use distributed version control.**  
Etter makes a strong case for Git throughout *Modern Technical Writing*. For a non-developer, the practical benefit is simple: Git keeps a complete history of every change you make. If you accidentally delete a section of your resume, you can restore it. Nothing is ever permanently lost.

Download your empty repository onto your computer:

```
git clone https://github.com/your-username/your-username.github.io.git
```

Then move into the new folder:

```
cd your-username.github.io
```

All remaining commands should be run from inside this folder.

---

### Step 4 Set up the Pelican Project

Run Pelican's quickstart to create a website using:

```cmd
pelican-quickstart
```

Answer the prompts as they appear. When asked for your site URL, enter `https://your-username.github.io`. When asked whether you want to use GitHub Pages, enter `y`.


The quickstart generates a structure like this:

```
your-username.github.io/
├── content/          ← your Markdown resume goes here
├── output/           ← Pelican writes built HTML here (do not edit manually)
├── pelicanconf.py    ← site settings
└──publishconf.py     ← production settings

```

### Step 5 - Write Your Resume in Markdown

**Etter's Principle: Write content in a lightweight markup language.**  
Etter makes a strong case for Markdown: it is readable in its raw form, separates content completely from visual design, and is supported by virtually every modern publishing tool. Writing your resume in Markdown means you can change the entire look of your site by swapping themes, without changing a single word of content. If you are already familiar with Markdown, this step should feel natural.

Open the folder containing the pelican created website using your code editor, and create a file at `content/resume.md`. Pelican pages requires a small metadata header at the top of the file like so:  


```markdown
Title: Resume
Date: 2026-01-01
Save_as: index.html
---
Resume Content Here

```

The `Save_as: index.html` directive tells Pelican to make this page the site root, so visitors who go to `https://your-username.github.io` land directly on your resume.

### Step 5.1 - Choose a Theme (Optional)

Pelican's default theme is functional but plain. You can browse community themes at [github.com/getpelican/pelican-themes](https://github.com/getpelican/pelican-themes). To install one:

```cmd
git clone --recursive https://github.com/getpelican/pelican-themes themes
```

Then reference it in `pelicanconf.py` by copying the path depending on your folder structure to the theme like below:

```bash
e.g
THEME = 'pelicanthemes/sneakyidea'  # replace sneakyidea with your chosen theme
```

### Step 6 - Build the Site & Preview the site Locally

**Etter's Principle: Review your documentation before publishing it.**  
Etter mentions testing documentation in the same environment readers will encounter. Pelican's built-in preview functionality lets you see exactly what your site looks like in a real browser before anyone else can.

Generate the static output:

```bash
pelican content 
```

Pelican generates the content automatically. You can preview it locally with:

```cmd
pelican --listen
```

Open `http://localhost:8000` in your browser to review your site before publishing.

### Step 7 - Publish to GitHub Pages

**Etter's Principle: Make your documentation permanently accessible online.**  
Etter argues that documentation like PDFs or HTML system will depreceate and fails its readers. A public URL accessible on any device, at any time, with no account required is the standard he advocates. GitHub Pages delivers exactly that at no cost.


Update `pelicanconf.py` to write output to a `docs/` folder:

```python
OUTPUT_PATH = "docs/"
```

GitHub Pages can serve from a `docs/` folder. The simplest approach is to build into a `docs/` folder thorugh the command above and push everything to `main`.

Rebuild:

```cmd
pelican content 
```

Now, run these three commands one at a time. The first stages your files, the second saves a snapshot with a description, and the third sends everything to GitHub:


```cmd
git add .
git commit -m "Publish resume site"
git push origin main
```

Finally, configure GitHub Pages:

1. Go to your repository on GitHub.
2. Click **Settings -> Pages**.
3. Under **Branch**, select `main` and set the folder to `/docs`.
4. Click **Save**.
5. Your site will be live at `https://username.github.io/my-project-name` after a short while.


GitHub will display a confirmation banner with your live URL. It typically takes one to two minutes to go live.   

---
## MORE RELEVEANT RESOURCES/READINGS  
- [CommonMark Tutorial](https://commonmark.org/help/tutorial/) - An interactive, step-by-step Markdown tutorial based on the CommonMark standard; a solid next step beyond the basics.
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/) - Helpful with reminding me of the specific syntax that markdown uses for certain features. 
- [Pelican documentation](https://docs.getpelican.com)
- [GitHub Pages documentation](https://docs.github.com/en/pages)
- [Markdown guide](https://www.markdownguide.org)
- Andrew Etter, *Modern Technical Writing: An Introduction to Software Documentation* (2016)  

---
### FAQ
| Question | Answer|
| :---     |  :--- |
| "**Why is Markdown better than writing raw HTML?**| Markdown provides an abstraction layer that lets you express the same document structure with far less syntax than raw HTML requires. A second-level heading in Markdown is `## My Heading`; in HTML it is `<h2>My Heading</h2>` - and that gap grows quickly. More importantly, Markdown keeps the source file readable as plain text, so you can review and edit your resume in any editor without needing to mentally parse angle brackets and closing tags. Etter highlights exactly this point: lightweight markup languages lower the barrier to contribution and keep the source of truth human-friendly.|  
| **I changed the Markdown version of my resume, so why don’t I see the changes when I refresh the website in my browser?** | Pelican is a static-site generator, which means it reads your Markdown source files and produces finished HTML files once, on demand. It does not watch for changes automatically. Every time you edit `resume.md`, you must rerun `pelican content` in your terminal to regenerate the `docs/` folder. After rebuilding, refresh your browser to see the updated output locally. When you are ready to publish the updated version, commit the regenerated files and push to GitHub as described in Step 7.|
| **Do I need to pay anything to host my resume this way?** | No. GitHub Pages is free for public repositories, and Pelican is open-source software. The only cost is your time. This is one of the practical advantages of the toolchain Etter recommends: the entire pipeline from writing to publishing uses freely available, community-maintained tools. |


---
## Credits
**Author:** Gideon Ashiru  
**Peer Reviewers:** Anne, William  
**Third-party theme:** [SneakyIdea for Pelican](https://pelicanthemes.com/sneakyidea/) - used to style the published resume site.  
