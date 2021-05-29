This blog is powered by [Jekyll](https://jekyllrb.com/). Thanks @wild-flame for the awesome theme [Simple](https://github.com/wild-flame/jekyll-simple).

### Install Jekyll on macOS

Jekyll requires Ruby > 2.4.0. To run the latest Ruby version you need to install it through [Homebrew](https://brew.sh/).

```bash
# Install Homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Install Ruby
brew install ruby

# Add ruby path
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile

# Install Jekyll
gem install jekyll bundler
```

### Build and browse locally

Build the site and make it available on a local server.

```bash
bundle exec jekyll serve

# Incremental build
bundle exec jekyll serve --incremental
```

Browse to http://localhost:4000/

### Directory Structure

| FILE / DIRECTORY                                          | DESCRIPTION                                                  |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| `_config.yml`                                             | Stores [configuration](https://jekyllrb.com/docs/configuration/) data. Many of these options can be specified from the command line executable but it’s easier to specify them here so you don’t have to remember them. |
| `_drafts`                                                 | Drafts are unpublished posts. The format of these files is without a date: `title.MARKUP`. Learn how to [work with drafts](https://jekyllrb.com/docs/posts/#drafts). |
| `_includes`                                               | These are the partials that can be mixed and matched by your layouts and posts to facilitate reuse. The liquid tag `{% include file.ext %}` can be used to include the partial in `_includes/file.ext`. |
| `_layouts`                                                | These are the templates that wrap posts. Layouts are chosen on a post-by-post basis in the [front matter](https://jekyllrb.com/docs/front-matter/), which is described in the next section. The liquid tag `{{ content }}` is used to inject content into the web page. |
| `_posts`                                                  | Your dynamic content, so to speak. The naming convention of these files is important, and must follow the format: `YEAR-MONTH-DAY-title.MARKUP`. The [permalinks](https://jekyllrb.com/docs/permalinks/) can be customized for each post, but the date and markup language are determined solely by the file name. |
| `_data`                                                   | Well-formatted site data should be placed here. The Jekyll engine will autoload all data files (using either the `.yml`, `.yaml`, `.json`, `.csv` or `.tsv` formats and extensions) in this directory, and they will be accessible via `site.data`. If there's a file `members.yml` under the directory, then you can access contents of the file through `site.data.members`. |
| `_sass`                                                   | These are sass partials that can be imported into your `main.scss` which will then be processed into a single stylesheet `main.css` that defines the styles to be used by your site. |
| `_site`                                                   | This is where the generated site will be placed (by default) once Jekyll is done transforming it. It’s probably a good idea to add this to your `.gitignore` file. |
| `.jekyll-metadata`                                        | This helps Jekyll keep track of which files have not been modified since the site was last built, and which files will need to be regenerated on the next build. This file will not be included in the generated site. It’s probably a good idea to add this to your `.gitignore` file. |
| `index.html` or `index.md` and other HTML, Markdown files | Provided that the file has a [front matter](https://jekyllrb.com/docs/front-matter/) section, it will be transformed by Jekyll. The same will happen for any `.html`, `.markdown`, `.md`, or `.textile` file in your site’s root directory or directories not listed above. |
| Other Files/Folders                                       | Every other directory and file except for those listed above—such as `css` and `images` folders, `favicon.ico` files, and so forth—will be copied verbatim to the generated site. There are plenty of [sites already using Jekyll](https://jekyllrb.com/showcase/) if you’re curious to see how they’re laid out. |

### Creating Posts

To create a post, add a file to your `_posts` directory with the following format:

```
YEAR-MONTH-DAY-title.md
```

All blog post files must begin with YAML front matter:

```md
---
layout: post
title: Blogging Like a Hacker
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: jekyll update
tags: jekyll blog
published: true
---
```

- categories/tags: A spece-separeted string or a [YAML list](https://en.wikipedia.org/wiki/YAML#Basic_components).

- layout: If set, this specifies the layout file to use. If not set, the default layout will be used.
- published: Set to false if you don’t want a specific post to show up when the site is generated.

###  Hosting Issues

If the page is hosted on GitHub, GitHub hosts the page with URL: [user.github.io/repository](#).
This requires adding `/repository` as the `baseurl` in `_config.yml`.
Besides, relative URLs in all pages need to be modified to go through the `baseurl`.
For example, referencing a stylesheet:

```HTML
<link rel="stylesheet" href="{{site.baseurl}}/css/theme.css" />
```

Referencing an image within a post:

```MD
![image]({{ site.baseurl }}/assets/images/pic.jpg)
```

If the page is hosted on a custom domain, `baseurl` is usually not required.
