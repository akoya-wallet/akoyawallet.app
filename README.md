# akoyawallet.app

The website for [Akoya](https://github.com/akoya-wallet/akoya-extension), the open-source Pearl (PRL) wallet.

Plain static HTML and CSS, with no build step, no JavaScript and no third-party requests. That is deliberate: a
wallet's website is a phishing target, so it should be easy to audit and hard to tamper with.

| Path | What |
|---|---|
| `index.html` | English page |
| `zh/index.html` | Chinese page (keep in sync with the English one) |
| `assets/site.css` | All styles and every animation (pure CSS, including the "Pause motion" toggle). Colours mirror the extension's `src/ui/styles.css` |
| `assets/fonts/` | Manrope variable font, self-hosted (SIL OFL, see `OFL.txt`) |
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

GitHub Pages serves `main` (`/`), so a push to `main` is a deploy. Cloudflare sits in front as a proxy
(orange cloud). It terminates TLS with its own certificate and adds the security headers through a Transform
Rule ("akoyawallet.app security headers": CSP, HSTS, X-Frame-Options and others). SSL mode is Full, minimum
TLS is 1.2, and Always Use HTTPS is on.

GitHub's own certificate for the custom domain was stuck in its queue for over an hour on 2026-10-14, which is
why Cloudflare's proxy is used. Because Cloudflare doesn't verify the GitHub origin certificate, the
Cloudflare-to-GitHub hop isn't hostname-verified.

If you change the CSP, change it in both places: the `<meta>` tag in each page and the Cloudflare Transform
Rule. Browsers enforce both.

## Keep in sync

- When the Chrome Web Store listing is live, put the official extension ID and store link in the Install and
  Stay safe sections, on both pages.
- Renew `Expires` in `.well-known/security.txt` before 2027-10-14.
