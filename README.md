![Archon](./public/archon-wordmark-dark.svg)

# archon-site

Static site for [archon.custodyzero.com](https://archon.custodyzero.com). Deployed to Cloudflare Pages on push to `main`.

---

## Structure

```
archon-site/
├── public/
│   ├── index.html                    # Landing page
│   ├── archon-icon-dark.svg          # Brand asset (not covered by Apache 2.0 — see LICENSE)
│   ├── archon-icon-dark.ico          # Favicon
│   ├── archon-wordmark-dark.svg      # Brand asset (not covered by Apache 2.0 — see LICENSE)
│   ├── archon-wordmark-blue.svg      # Brand asset (not covered by Apache 2.0 — see LICENSE)
│   ├── apple-touch-icon.png          # iOS home screen icon
│   └── social-card.png               # Social share image
├── .github/
│   └── workflows/
│       └── deploy.yml                # CI/CD → Cloudflare Pages
├── _headers                          # Cloudflare response headers + redirects
├── wrangler.toml                     # Cloudflare Pages configuration
└── README.md
```

---

## Local Development

No build step. Edit `public/index.html` directly and open in a browser.

For a local Cloudflare Pages preview:

```bash
npx wrangler dev --port 8787
```

---

## Deployment

Push to `main` triggers automatic deployment via GitHub Actions to Cloudflare Pages.

**Required GitHub Secrets:**

| Secret | Description |
|--------|-------------|
| `CLOUDFLARE_API_TOKEN` | Cloudflare API token with Pages edit permissions |
| `CLOUDFLARE_ACCOUNT_ID` | Your Cloudflare account ID |

The Pages project is named `archon-site`. The custom domain `archon.custodyzero.com` is configured in the Cloudflare dashboard — not in this repo.

---

## Email Capture

Form submissions POST to `https://api.custodyzero.com/waitlist` with source `archon.custodyzero.com`. The API validates input and writes to DynamoDB. Source lives in [CustodyZero/cz-capture](https://github.com/CustodyZero/cz-capture).

---

## Headers & Security

Security headers and redirects are defined in `_headers` and applied by Cloudflare Pages on all responses. CSP is intentionally strict — if you add external resources, update the policy.

---

## License

Apache 2.0 — see [LICENSE](./LICENSE).

CustodyZero brand assets — including all wordmarks, logomarks, product names, and taglines — are all rights reserved and explicitly excluded from the Apache 2.0 license. See [LICENSE](./LICENSE) for the full brand reservation notice.

---

*The coordination layer that doesn't guess.*
