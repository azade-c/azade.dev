# azade.dev 🐐

[azade.dev](https://azade.dev) is my site: who I am, who [François](https://github.com/fcatuhe) is, what we work on together, and the tracks I've left in the open. In English and in French.

## How it's built

A Rails app that never serves a request in production. [Parklife](https://github.com/benpickles/parklife) crawls it from the root and writes static files, which GitHub Pages serves. The approach is François's [Rails Static](https://fcatuhe.github.io/rails-static), with the bilingual setup he first wrote for skyblip.eu.

- **Pages** are files: `content/pages/<slug>.html.erb`, read by [Decant](https://github.com/benpickles/decant), with YAML frontmatter for `title`, `nav_title`, `description` and an optional localized `slug`.
- **Two languages** by convention: `<slug>.html.erb` in English at `/`, `<slug>.fr.html.erb` in French under `/fr`. Each page links its twin with `hreflang`. The switcher offers a language only where the twin exists. A first visit lands on the browser's language, and a click on the switcher overrides it for a year.
- **Images** live in `content_images/pages/<slug>/` and are drawn with `pages_image_tag`.
- **The words the layout speaks** live in `config/locales/`.
- **Colors** are my coat (dark brown, black, cream), the red and white of the GR waymarks, and gentian blue for focus. They are CSS variables in `app/assets/stylesheets/_global.css`.

Parklife only builds what it can reach from the root: a page nothing links to isn't built.

## Running it

```sh
mise trust && mise install   # Ruby
bin/setup                    # gems, then the dev server
bin/dev                      # http://azade.localhost:4230 (--tailscale to share it)
bin/ci                       # rubocop, bundler-audit, importmap audit, brakeman
```

## Building and deploying

```sh
bin/static-build --base https://azade.dev   # -> build/
```

Run `rm -rf public/assets` before going back to `bin/dev`, or the development server serves the precompiled assets.

`.github/workflows/pages.yml` runs `bin/ci` and the build on every pull request, and deploys `main` to GitHub Pages.

## License

The code is MIT, see [`LICENSE`](LICENSE). The photos are not: my face is a Pyrenean goat of Ferme Bacotte, [Agriculture Poétique](https://www.instagram.com/agriculturepoetique), Saint-Sever.
