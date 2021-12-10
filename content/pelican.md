Title: Pelican
Date: 2021-08-30 10:48:00
Modified: 2021-08-30 10:48:00
Category: 
Tags: 
Slug: 
Summary: 
Status: published

tl;dr;
* github new repo
* AWS Amplify
* Amplify CI from GitHub > master, then release
* AWS Rt 53 config for domain
...
* pip install pelican
* pip install markdown (*.md pages will just be ignored without this manually installed)
* (type type type)
* pelican content
* pelican --listen
* git push \master
* git merge \master >> \release

Docs:
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
title	    Title of the article or page
date	    Publication date (e.g., YYYY-MM-DD HH:SS)
modified	Modification date (e.g., YYYY-MM-DD HH:SS)
tags	    Content tags, separated by commas
keywords	Content keywords, separated by commas (HTML content only)
category	Content category (one only — not multiple)
slug	    Identifier used in URLs and translations
author	    Content author, when there is only one
authors	    Content authors, when there are multiple
summary	    Brief description of content for index pages
lang	    Content language ID (en, fr, etc.)
translation	If content is a translation of another (true or false)
status	    Content status: draft, hidden, or published
template	Name of template to use to generate content (without extension)
save_as	    Save content to this relative file path
url	        URL to use for this article/page

Markdown Formatting:
https://daringfireball.net/projects/markdown/syntax