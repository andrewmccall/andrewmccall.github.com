# andrewmccall.com

The Jekyll source for [andrewmccall.com](https://andrewmccall.com), hosted with GitHub Pages.

## Design direction

The site uses a custom technical-notebook theme:

- dark, low-contrast palette with a restrained green accent;
- fixed identity and navigation rail on wide screens;
- compact responsive header on smaller screens;
- system sans-serif type for reading and monospace type for navigation and metadata;
- dates formatted as `dd.MM.YYYY`;
- current work kept deliberately small and limited to public projects; and
- the complete historical writing archive retained at its existing URLs.

## Local build

The Gemfile uses the same `github-pages` dependency set as GitHub Pages.

```sh
bundle install
bundle exec jekyll serve
```

The site can also be verified without relying on the host Ruby version:

```sh
docker run --rm \
  -v "$PWD:/srv/jekyll" \
  -w /srv/jekyll \
  jekyll/jekyll:4.2.2 \
  sh -lc 'bundle install && JEKYLL_ENV=production bundle exec jekyll build'
```
