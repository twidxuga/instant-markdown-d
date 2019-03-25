Twid's fork of [!nstant-markdown-d](https://github.com/suan/instant-markdown-d)
================
[!nstant-markdown-d](https://github.com/suan/instant-markdown-d) is a small Node.js server that enables instant compilation and previewing of Markdown files. A plugin can easily be written for any text editor to interface with it.

One such client currently exists in the form of a plugin for Neovim (and possibly compatible with Vim): [twidxuga/vim-instant-markdown](https://github.com/twidxuga/vim-instant-markdown)

This fork also additionally allows:
  * Rendering latex markdown mathematical formulas via Katex. 
  * Serving files (not just images) under the folder within which the markdown document resides, or any of its sub-folders. 
  * Generating table of contents from the first 3 levels of header tags and insert it in the document with `[[TOC]]` .
  * Automatically scrolling to the current editing position.

Installation
------------

The following assumes installation on Linux:

1. Ensure that you have [git](https://git-scm.com/), [nodejs](https://nodejs.org/) and [npm](https://www.npmjs.com/) installed.  

2. Clone this repository

```bash
  cd <base dir>
  git clone https://github.com/twidxuga/instant-markdown-d`
```

3. Install the module

```bash
  cd <base dir>/instant-markdown-d
  # for user specific installations (recommended)
  npm install
  # OR alternatively system wide installation 
  sudo npm install
```

REST API
--------
 | Action                   | HTTP Method   | Request URL                 | Request Body                   | 
 | ---------------------    | ------------- | --------------------------- | --------------------           | 
 | Refresh Markdown on page | PUT           | http://localhost:\<port\>   | \<New Markdown file contents\> | 
 | Close Webpage            | DELETE        | http://localhost:\<port\>   |                                | 

By default, `<port>` is 8090

Environment variables
---------------------

* `INSTANT_MARKDOWN_OPEN_TO_THE_WORLD=1` - by default, the server only listens
  on localhost. To make the server available to others in your network, set this
  environment variable to a non-empty value. Only use this setting on trusted
  networks!

* `INSTANT_MARKDOWN_ALLOW_UNSAFE_CONTENT=1` - by default, scripts are blocked.
  Use this preference to allow scripts.

* `INSTANT_MARKDOWN_BLOCK_EXTERNAL=1` - by default, external resources such as
  images, stylesheets, frames and plugins are *allowed*. Use this setting to
  *block* such external content.

* `INSTANT_MARKDOWN_SERVE_FOLDER_TREE=1` - enables serving all content files without restriction of file type, starting from the base folder from which the instance is run, and including files under any of its sub-folders. This is disabled by default (set to 0), as it can potentially be a security concern in specific scenarios.
