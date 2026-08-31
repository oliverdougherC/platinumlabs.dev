# Blog

A standalone, static blog.

## How it works

`index.html` is a static page. On load, `js/blog.js`:

1. Fetches `blogs/manifest.json`.
2. Fetches each markdown file listed there from `blogs/`.
3. Renders the selected post (via [marked](https://marked.js.org/)) into the page, with a
   sidebar of all posts. The current post is tracked in the URL hash (`#post=<slug>`).

Extras: [KaTeX](https://katex.org/) for `$$…$$` math, [Prism](https://prismjs.com/) for
fenced-code syntax highlighting + copy buttons.

## Project layout

```
index.html                      # the blog page (root)
blogs/                          # markdown posts + manifest.json
css/                            # design-system, schematic, blog, cursor styles
js/
  blog.js                       # blog engine
  blog-math.js                  # KaTeX rendering
  blog-code-highlight.js        # Prism + copy buttons
assets/                         # cursor .cur files + light-mode icons used by the CSS
favicon.svg                     # tab icon (book)
scripts/build-blog-manifest.js  # regenerates blogs/manifest.json from the .md files
```

## Writing a post

1. Drop a `.md` file into `blogs/`. Add YAML frontmatter with a `title:` and a `date:`
   (the title drives the page heading and the sidebar entry).
2. Regenerate the manifest:

   ```bash
   npm run build:blog
   ```

## Running locally

The page uses `fetch()` for the markdown, so open it through a web server (not `file://`):

```bash
npm run serve
```

Then visit http://localhost:4173/.
