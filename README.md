# Instructions for setting up the blog

Prerequisites: `hugo`, `ox-hugo`

1. Clone this repo somewhere, e.g. `~/blogging/blog_source`.
2. Clone the output repo into `public/`, so `git clone git@github:lordgrenville/lordgrenville.github.io.git ~/blogging/blog_source/public/`
3. Create an org buffer in `content/posts`, following the format. When done convert to markdown with `org-hugo-export-as-md` and save in that folder as a markdown file.
4. Then run `hugo` to build and update the changes in `public`.
