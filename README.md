# D77orphaned Docs

Community documentation of D77orphaned, a Void Linux live system for
recovery, diagnostics and careful forensics.

The pages are plain Markdown in [`src/`](src/). You can read them on GitHub,
in any editor or with `less`. [`src/SUMMARY.md`](src/SUMMARY.md) is the table
of contents and the only place where the order of the chapters is defined.

## Building the website

The website is generated with [mdBook](https://rust-lang.github.io/mdBook/),
using its default theme and no plugins. mdBook is only needed to build the
site; D77orphaned itself does not need it.

```sh
mdbook build    # the site goes to book/
mdbook serve    # preview at http://localhost:3000, rebuilt on every change
```

A link in `SUMMARY.md` to a page that does not exist stops the build
(`create-missing = false` in `book.toml`).

## Rules for the content

- Everything here is specific to D77orphaned. General Void Linux topics are
  covered in the [Void Linux Handbook](https://docs.voidlinux.org/).
- Nothing is written from memory. Commands, file names and behaviour are
  checked against the [system's code](https://github.com/d77void/d77orphaned)
  and its test report. Anything not verified yet is marked as such.
- The documentation shows commands; nothing here runs them.

## SourceForge wiki

On every change to `src/` on `main`, the workflow `wiki.yml` copies the pages
to the [d77void wiki on SourceForge](https://sourceforge.net/p/d77void/wiki/Orphaned%20Docs/)
using `tools/sf-wiki-sync.py` and the `SF_WIKI_TOKEN` secret.

Pages are written here only: the wiki copy is overwritten each time. A page
removed from `SUMMARY.md` stays on the wiki until it is deleted there by
hand. The wiki's Home page comes from the
[d77void/docs](https://github.com/d77void/docs) repository (`wiki/Home.md`).

## License

The documentation is licensed under
[Creative Commons Attribution-ShareAlike 4.0 International](LICENSE)
(CC BY-SA 4.0).
