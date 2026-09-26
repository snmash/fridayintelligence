# Friday Intelligence — fridayintelligence.com

One-page static site for Friday Intelligence, the AI go-to-market advisory practice led by Steven Maheshwary. It is the sibling of the personal site (steven-m.com) and shares its design family: warm paper background, serif display type, hairline rules, and small-caps labels.

## Files

- `index.html` — the entire site
- `assets/css/site.css` — all styles; no build step, no frameworks, no web fonts
- `CNAME` — custom domain for GitHub Pages
- `robots.txt` — disallow all while in preview

There is no JavaScript and no form. The entrance sequence is pure CSS and respects `prefers-reduced-motion`.

GitHub Pages can't send custom response headers, so security policy lives in `index.html`. A `Content-Security-Policy` meta tag blocks all scripts, and a referrer-policy meta tag sets the referrer policy. Any analytics, embeds, or web fonts you add later need a matching change to that CSP tag. Framing protection and HSTS are not available on plain GitHub Pages.

This README is publicly reachable on the live site (GitHub Pages renders it via Jekyll), so keep it free of anything private.

## Preview locally

    python3 -m http.server 8000

Then open http://localhost:8000.

## Deploy (GitHub Pages)

1. Push this folder to a GitHub repository, with `index.html` at the repository root.
2. Go to Settings → Pages → Build and deployment. Set Source to "Deploy from a branch," Branch to `main`, and folder to `/ (root)`, then save.
3. Still in Settings → Pages, set Custom domain to `fridayintelligence.com` (the `CNAME` file already sets it) and save.
4. At your DNS provider, add these records:
   - Apex `fridayintelligence.com`, four `A` records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - Optional apex IPv6, four `AAAA` records: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - `www` as a `CNAME` to `<username>.github.io`

5. Once DNS resolves and the certificate is issued (minutes to a few hours), check "Enforce HTTPS" in Settings → Pages.

## Go-live checklist

- [ ] Verify `fridayintelligence.com` under your GitHub account (Settings → Pages → Verified domains) before or right after pointing DNS; this prevents domain takeover
- [ ] `dig fridayintelligence.com +short` returns the four GitHub Pages IPs, and `www` resolves to `<username>.github.io`
- [ ] "Enforce HTTPS" is checked, and `http://` and `www` both land on `https://fridayintelligence.com`
- [ ] `index.html`: delete `<meta name="robots" content="noindex, nofollow">` — with no header file on GitHub Pages, this tag is the only noindex signal
- [ ] `robots.txt`: replace contents with `User-agent: *` and `Allow: /`
- [ ] Check the "Book an intro call" link and the mailto link on desktop and phone
- [ ] Check the single-column layout at 375px width, the expertise strip wrapping cleanly, and keyboard focus through header → button → email
- [ ] Run Lighthouse; expect 100 on accessibility
- [ ] Submit the domain in Google Search Console once indexing is allowed