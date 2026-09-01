# yakuru-legal

Static legal site for Yakuru — the privacy policy and account-deletion pages that
the App Store, Play Store and Meta app reviews link to.

Deployed on Vercel as a plain static site: everything under `public/` is served
at the site root, with no build step.

## Layout

```
public/
  index.html           # Legal & Privacy landing page
  privacy.html         # Privacy Policy            -> /privacy
  delete-account.html  # Account deletion request  -> /delete-account
  styles.css
vercel.json            # clean URLs, legacy redirects, security headers
```

`vercel.json` sets `cleanUrls`, so pages are served without the `.html`
extension. It also redirects the older paths the stores and in-app links have
used (`/privacy-policy`, `/policy`, `/policies/privacy-policy`, `/pages/privacy`,
`/delete`, `/account-deletion`, `/data-deletion`, `/pages/delete-account`) to the
two canonical pages, and adds `X-Content-Type-Options`, `Referrer-Policy`,
`Strict-Transport-Security` and `Permissions-Policy` headers to every response.

## Local preview

Serve `public/` with any static server, e.g.:

```sh
npx serve public
```

Clean URLs and redirects are Vercel behaviour, so locally the pages resolve at
their `.html` paths. To exercise the real routing, use `vercel dev`.

## Deploying

Pushes to `main` deploy to production via the Vercel Git integration; other
branches get preview deployments.

## Editing the policies

The pages are hand-written HTML with no templating — edit them directly. Keep
the "last updated" date in each page current, and keep the contact addresses
(`privacy@yakuruhealth.com`, `legal@yakuruhealth.com`,
`support@yakuruhealth.com`) in sync with what the store listings declare.

When a URL changes, add a redirect in `vercel.json` rather than breaking a link
that a store listing or a shipped app build already points at.
.
