Twid's !nstant-markdown:
========================
[!nstant-markdown-d](https://github.com/suan/instant-markdown-d) is a small Node.js server that enables instant compilation and previewing of Markdown files. A plugin can easily be written for any text editor to interface with it.

One such client currently exists in the form of a plugin for Neovim (and possibly compatible with Vim): [twidxuga/vim-instant-markdown](https://github.com/twidxuga/vim-instant-markdown)

This fork also additionally allows:
**Great new** look, no borders, resizes better, usable in a 50/50 split screen scenario. 
- **Major performance improvement**, over the original version, due to a new 1 second (configurable) polling of markdown documents. No more slow mode! Plus Katex makes formula rendering fly, no more waiting on old MathJax.
- **Links to other markdown files are now clickable** and their destination is rendered. This happens as long as the liked files are within the folder tree of the markdown document for which InstantMarkdownPreview was started.
  + URLs contain the name of the file. To go back to seeing the file being edited in Neovim, a user must click the browser's back button to return to the landing page (root path, e.g. `http://localhost:8090`)
- **Changing to another markdown buffer immediately displays that buffer**, as long as it is within the same folder or subfolder of the first markdown document for which InstantMarkdownPreview was called.
  + As long as that buffer is in the folder or a sub-folder of the first markdown document for which InstantMardownPreview was started. 
- **Mermaid diagrams** are now rendered.
- Running **InstantMarkdownPreview now restarts the server**. However, there is little need to restart the server when changing documents though, as it happens automatically.
- **Task lists** (GitHub-style) are now rendered. 
- **TOC** are rendered with the `[[TOC]]` tag.
- **Serves all content** within the folder tree where the initial markdown document is - e.g. display images, download pdfs, etc.

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
  # for user specific installations (recommended), and link to a folder in path
  npm install
  ln -sfv $PWD/instant-markdown-d ~/.local/bin
  # OR alternativey system wide installation 
  sudo npm install
```

REST API
--------
 | Action                   | HTTP Method   | Request URL                 | Request Body                   | 
 | ---------------------    | ------------- | --------------------------- | --------------------           | 
 | Refresh Markdown on page | PUT           | http://localhost:\<port\>   | \<New Markdown file contents\> | 
 | Refresh Markdown on page | PUT           | http://localhost:\<port\>/path/to/markdown.md   | \<New Markdown file in folder tree\> | 
 | Close Webpage            | DELETE        | http://localhost:\<port\>   |                                | 
 | Render page from markdown file link clicked  | GET        | http://localhost:\<port\>/path/to/markdown.md   |                                | 
 | Download resource  | GET        | http://localhost:\<port\>/path/to/image.jpg   |                                


By default, `<port>` is 8090

Environment variables
---------------------

* `INSTANT_MARKDOWN_OPEN_TO_THE_WORLD=0` - By default, the server only listens
  on localhost. To make the server available to others in your network, set this
  environment variable to a non-empty value. Only use this setting on trusted
  networks!

* `INSTANT_MARKDOWN_ALLOW_UNSAFE_CONTENT=1` - by default, scripts are blocked.
  Use this preference to allow scripts (Recommended).

* `INSTANT_MARKDOWN_BLOCK_EXTERNAL=0` - By default, external resources such as
  images, stylesheets, frames and plugins are *allowed*. Use this setting to
  *block* such external content.

* `INSTANT_MARKDOWN_SERVE_FOLDER_TREE=1` - Enables serving all content files without restriction of file type, starting from the base folder from which the instance is run, and including files under any of its sub-folders. This is disabled by default (set to 0), as it can potentially be a security concern in specific scenarios (Recommended).

* `INSTANT_MARKDOWN_PORT=8090` - Specifies the port in which `instant-markdown-d` will be listening to connections.

