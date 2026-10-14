# akoyawallet.app

The website for [Akoya](https://github.com/akoya-wallet/akoya-extension), the open-source Pearl (PRL) wallet.

Plain static HTML and CSS, with no build step, no JavaScript and no third-party requests. That is deliberate: a
wallet's website is a phishing target, so it should be easy to audit and hard to tamper with.

| Path | What |
|---|---|
| `index.html` | English page |
| `zh/index.html` | Chinese page (keep in sync with the English one) |
| `assets/site.css` | All styles. Colours mirror the extension's `src/ui/styles.css` |
| `assets/` | Brand mark and lockup (© PRLFlipBTC, not MIT) |
| `og.png` | 1200×630 social preview |
| `CNAME` | Custom domain for GitHub Pages |
| `.well-known/security.txt` | Vulnerability contact. Renew `Expires` yearly |

## Preview locally

```bash
python3 -m http.server 5288 --bind 127.0.0.1
```

Then open <http://127.0.0.1:5288/>.

## Deploy

Hosted on GitHub Pages from `main` (`/`). A push to `main` is a deploy. DNS lives on Cloudflare as DNS-only
(grey cloud) records pointing at GitHub Pages, and GitHub issues the TLS certificate.

GitHub Pages can't send custom headers, so the CSP is set with a `<meta>` tag in every page. `.app` is on the
HSTS preload list, so HTTPS is enforced by browsers regardless.

## Keep in sync

- When the Chrome Web Store listing is live, put the official extension ID and store link in the Install and
  Stay safe sections, on both pages.
- Renew `Expires` in `.well-known/security.txt` before 2027-10-14.
