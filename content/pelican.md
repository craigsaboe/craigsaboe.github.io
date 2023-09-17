Title: Getting Started with the Pelican Static Site Generator
Date: 2021-08-30 10:48:00
Modified: 2021-08-30 10:48:00
Category: howto
Tags: pelican
Slug:
Summary: A short guide to getting started with the Pelican SSG
Status: published

[TOC]

# What are Static Site Generators?

Static site generators are software tools that create static HTML websites from raw data and templates. Unlike dynamic websites, which generate pages on-the-fly with each request, a static site generator builds the entire website beforehand.

Static site generators are popular for:

- Blogs
- Portfolios
- Documentation sites
- Other projects where content doesn't change frequently or require server-side interaction.

# Popular Static Site Generators

- Jekyll
- Hugo
- Gatsby
- Next.js

# Typical Workflow

Here's how a typical workflow with a static site generator might look:

1. **Development**: 
    - Write your content, typically in a lightweight markup language like Markdown.
    - Define the site's layout and appearance using templates.
  
2. **Generation**: 
    - Run the static site generator to create static HTML, CSS, and JavaScript files.
  
3. **Deployment**: 
    - Upload the generated static files to a web server or hosting service.
  
4. **Serving**: 
    - Pre-generated static files are delivered to visitors' browsers without the need for server-side processing.

# Pelican
Pelican is a SSG written in Python.  It offers a simple workflow and a strong featureset.

Setting up a static website using the Pelican static site generator is relatively straightforward.  Here is a walkthrough on how to get your own Pelican-generated site up and running.

## Prerequisites

- Python
- Pip (Python package installer)
- Optional: virtualenv for isolated Python environments

## Installation

1. **Install Pelican and Markdown**

    `pip install pelican markdown`

    Optionally, you can create a Python virtual environment before installing the packages:
   
    `python3 -m venv myenv`

    `source myenv/bin/activate`
    

## Project Setup

2. **Create a New Pelican Project**

`pelican-quickstart`

This command will ask you a series of questions about your project and generate the project scaffolding.

**3. Create Content**

Create new `.md` (Markdown) or `.rst` (reStructuredText) files inside the `content` folder. These will be converted into HTML pages.

    Title: My First Post
    Date: 2023-09-03
    Category: Blog
    This is my first blog post!

**4. Generate the Site**

Run the following command to generate the site:

```
pelican content
```

This will generate the HTML files and place them in the `output` folder.

## Local Testing

**5. Preview the Site Locally**

Pelican comes with a simple HTTP server for local testing.  You can start this via:

```
pelican --listen --autoreload
```

The ```autoreload``` parameter will regenerate the site automatically whenever you update a page, saving you from having to stop the server and rebuild every time you make a change.

Now, open your web browser and go to `http://localhost:8000` to view your site.

## Deployment

**6. Deploy**

Once you're happy with your site, you can deploy it. A simple way to deploy is to copy the contents of the `output` folder to your web server.

**7. Automate Deployment (Optional)**

You can automate the deployment using various methods such as Git hooks, CI/CD pipelines, or specialized deployment tools.

## Wrap-up

This is a basic guide and Pelican offers many other features like theming, plugins, and settings you can customize. For more information, you can refer to the [official documentation](http://docs.getpelican.com/).

# Docs
https://docs.getpelican.com/en/latest/

## Page Headers
Here's one example of page metadata:

    Title: My super title
    Date: 2010-12-03 10:20
    Modified: 2010-12-05 19:30
    Category: Python
    Tags: pelican, publishing
    Slug: my-super-post
    Authors: Alexis Metaireau, Conan Doyle
    Summary: Short version for index and feeds

Other metadata options:

| Tag   | Description                  |
| ----- | ---------------------------- |
| Title | Title of the article or page |
| Date | Publication date (e.g., YYYY-MM-DD HH:SS) |
| Modified | Modification date (e.g., YYYY-MM-DD HH:SS) |
| Tags | Content tags, separated by commas |
| Keywords | Content keywords, separated by commas (HTML content only) |
| Category | Content category (one only — not multiple) |
| Slug | Identifier used in URLs and translations |
| Author | Content author, when there is only one |
| Authors | Content authors, when there are multiple |
| Summary | Brief description of content for index pages |
| Lang | Content language ID (en, fr, etc.) |
| Translation | If content is a translation of another (true or false) |
| Status | Content status: draft, hidden, or published |
| Template | Name of template to use to generate content (without extension) |
| Save_as | Save content to this relative file path |
| Url | URL to use for this article/page |

**Markdown Formatting:**

https://daringfireball.net/projects/markdown/syntax

***Markdown Extensions***

To get things like an auto-generated table of contents, table rendering, etc., you will need to add a configuration section to `pelicanconf.py`

```
MARKDOWN = {
    'extension_configs': {
        'markdown.extensions.codehilite': {'css_class': 'highlight'},
        'markdown.extensions.extra': {},
        'markdown.extensions.meta': {},
    },
    'output_format': 'html5',
}
```
You can add any of the extensions identified here: 
https://python-markdown.github.io/extensions/

## Themes
Themes can be "installed" simply by adding them into the /themes folder in the root of the site.  If it doesn't exist, you can go ahead and create it.

Then, edit `pelicanconf.py` and add an attribute like this:

`THEME='themes/{your theme name here}'`

If your site starts to render using the default theme again, check that you do have the `THEME` flag set properly.  If your site renders with no styling, there is most likely either a problem with the path you added to `THEME` or the theme itself.