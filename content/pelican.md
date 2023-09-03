Title: Getting Started with the Pelican Static Site Generator
Date: 2021-08-30 10:48:00
Modified: 2021-08-30 10:48:00
Category: 
Tags: 
Slug:
Status: published

# What are Static Site Generators?

Static site generators are software tools that create static HTML websites from raw data and templates. Unlike dynamic websites, which generate pages on-the-fly with each request, a static site generator builds the entire website beforehand. 

## Typical Workflow

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

## Use Cases

Static site generators are popular for:
- Blogs
- Portfolios
- Documentation sites
- Other projects where content doesn't change frequently or require server-side interaction.

## Popular Static Site Generators
- Jekyll
- Hugo
- Gatsby
- Next.js

## Integration
- Version control systems like Git
- Headless content management systems (CMS) for more flexibility in content management.

# Pelican
Pelican is a SSG written in Python.  It offers a simple workflow, a strong featureset and is easy to use.

Setting up a static website using the Pelican static site generator involves several steps. Below are the basic steps to get you up and running:

## Prerequisites

- Python
- Pip (Python package installer)
- Optional: virtualenv for isolated Python environments

## Installation

1. **Install Pelican and Markdown**

    ```
    pip install pelican markdown
    ```

    Optionally, you can create a Python virtual environment before installing the packages:

    ```
    python3 -m venv myenv
    source myenv/bin/activate
    ```

## Project Setup

2. **Create a New Pelican Project**

    ```
    pelican-quickstart
    ```

    This command will ask you a series of questions about your project and generate the project scaffolding.

## Content Creation

3. **Create Content**

    Create new `.md` (Markdown) or `.rst` (reStructuredText) files inside the `content` folder. These will be converted into HTML pages.

    ```
    Title: My First Post
    Date: 2023-09-03
    Category: Blog

    This is my first blog post!
    ```

## Generate Site

4. **Generate the Site**

    Run the following command to generate the site:

    ```
    pelican content
    ```

    This will generate the HTML files and place them in the `output` folder.

## Local Testing

5. **Preview the Site Locally**

    Pelican comes with a simple HTTP server for local testing.  You can start this via:

    ```
    pelican --listen --autoreload
    ```

    The ```autoreload``` parameter will regenerate the site automatically whenever you update a page, saving you from having to stop the server and rebuild every time you make a change.

    Now, open your web browser and go to `http://localhost:8000` to view your site.

## Deployment

6. **Deploy**

    Once you're happy with your site, you can deploy it. A simple way to deploy is to copy the contents of the `output` folder to your web server.

7. **Automate Deployment (Optional)**

    You can automate the deployment using various methods such as Git hooks, CI/CD pipelines, or specialized deployment tools.

This is a basic guide and Pelican offers many other features like theming, plugins, and settings you can customize. For more information, you can refer to the [official documentation](http://docs.getpelican.com/).

# Docs
https://docs.getpelican.com/en/latest/

Example Page Metadata:

    Title: My super title
    Date: 2010-12-03 10:20
    Modified: 2010-12-05 19:30
    Category: Python
    Tags: pelican, publishing
    Slug: my-super-post
    Authors: Alexis Metaireau, Conan Doyle
    Summary: Short version for index and feeds

Other metadata options:

| title | Title of the article or page |
|-------|------------------------------|
| date | Publication date (e.g., YYYY-MM-DD HH:SS) |
| modified | Modification date (e.g., YYYY-MM-DD HH:SS) |
| tags | Content tags, separated by commas |
| keywords | Content keywords, separated by commas (HTML content only) |
| category | Content category (one only — not multiple) |
| slug | Identifier used in URLs and translations |
| author | Content author, when there is only one |
| authors | Content authors, when there are multiple |
| summary | Brief description of content for index pages |
| lang | Content language ID (en, fr, etc.) |
| translation | If content is a translation of another (true or false) |
| status | Content status: draft, hidden, or published |
| template | Name of template to use to generate content (without extension) |
| save_as | Save content to this relative file path |
| url | URL to use for this article/page |

**Markdown Formatting:**

https://daringfireball.net/projects/markdown/syntax