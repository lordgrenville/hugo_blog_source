# Instructions for setting up the blog

Prerequisites: `hugo`, `ox-hugo`

1. Clone this repo somewhere, e.g. `~/blogging/blog_source`.
2. Clone the output repo into `public/`, so `git clone git@github:lordgrenville/lordgrenville.github.io.git ~/blogging/blog_source/public/`
3. Create an org buffer in `content/posts`, following the format. When done convert to markdown with `org-hugo-export-as-md` and save in that folder as a markdown file.
4. Then run `hugo` to build and update the changes in `public`.


# Troubleshooting
Hugo is actively developed, and when you install it via Homebrew you are always on the latest version (downgrading is possible but annoying - it involves downloading an older formula, adding it as a local tap, and then pinning Homebrew to use only that). So things do break not infrequently.

When they do, searching for the error usually helps find what changes need to be made - it's in the Hugo syntax blocks (which are Go code, similar to Python in Jinja templates) added in the HTML files. Here are a few of the important ones:

`layouts/index.html` - this is the "home page"
`layouts/_default/single.html` - this is each individual blog post
`layouts/partials/footer.html` - footer at the bottom of each post
`layouts/partials/brand.html` - top matter with title/subtitle of the blog
`layouts/partials/post_nav_links.html` - navigation between previous and next post

# Ricing
In `static/css/hugo-tufte-override.css` there are some modifications to the default CSS. A common use-case is that I want to change the look of a specific `<h2>` or whatever. Rather than changing the div for the whole site, it's better to use a `class` in this case. I.e. tag the ones you want to change `<div class="foo">`, then in the CSS use the class name with a `.` before:

``` css
.foo {
 font-size:1.5rem;
}

```
