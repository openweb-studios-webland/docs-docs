---
title: Redirects
---

When moving documentation around, it's important to include redirects from
the old content to the new content to not break existing links in content
which links into the documentation from outside repositories which we don't
control.

Redirects are handled in two ways:

* Server-based redirects
* Client-based redirects

Client-based redirects are less preferrable than server-side redirects since
they require the client loading the JavaScript and acting on the redirects by
comparing the page's `location.href` to a list of redirects and acting on any
matches.  For search engines — and even clients — this is less than ideal since
there's a lot of overhead to loading a page.  Server redirects are much more
efficient since the server can make the decision and redirect the client using
the `Location:` header, without serving any other content.

However, **client-based redirects are important in one particular case**: When
redirecting **from** a page anchor (e.g. `document.html#specific-page-anchor`)
to another page.  This is true because servers do not receive the hash portion
of the URL when serving a request.  So when a browser requests `page.html#hash`,
the server only knows that it is handling `page.html`.

This means that when content is moved from a sub-section of a particular page
and moved to a new page, the server must serve the existing page without knowing
there is an upcoming redirect for a page anchor that has moved and the client
will then act on the `location.hash` (which it will still receive) and apply the
redirect itself using `location.hash`.

### Implementing server-based redirects

Server side redirects are handled with the Netlify `_redirects` file.  For more
information on the format of this file and how it should be organized, see [the
Netlify `_redirects` documentation](https://www.netlify.com/docs/redirects/).

#### Where is the `_redirects` file?

There are two possibilities on where the file should be.

* If the repository is using the `hexo-versioned-netlify-redirects` module,
  as indicated by its presence in the docs repository's `package.json` (e.g.
  `docs/package.json`) then the redirects should go in `source/_redirects`.
  If that file doesn't already exist, it's perfectly it can be created.
* If the repository is **not** using `hexo-versioned-netlify-redirects`, then
  the file should be placed in `public/_redirects`.
  
The reason for the difference is that other redirects are generated dynamically
when the `hexo-versioned-netlify-redirects` package is used.  In that case, the
`source/_redirects` file is used as a template.  When the package is not used,
the file in `public/_redirects` is simply an asset which is published without
changes.

### Implementing client-based redirects

Client-based redirects live in the documentation repository's `_config.yml` file
in a `redirects:` dictionary.  Each entry in the `redirects` dictionary should be
a map from the source path to the destination, with the source-path anchored and the
destination not anchored (i.e. prefixed with a slash):


```yaml
redirects:
  /path/repo/from.html#page-fragment: path/repo/to.html#optionally-fragment
```
  
> For an example, see [this portion](https://github.com/apollographql/apollo-client/blob/453e9488/docs/_config.yml#L61)
of the Apollo React documentation `_config.yml`.
