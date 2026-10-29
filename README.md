# couchpad.app

The website for Couchpad: plain HTML and CSS, no build step and no dependencies.

```
index.html          landing page
support/index.html  help and FAQ
privacy/index.html  privacy policy
404.html            not-found page
assets/             stylesheet and icons
CNAME               the custom domain (couchpad.app)
```

Preview locally: `python3 -m http.server` in this folder, then open http://localhost:8000.

## Before it goes live

- The Mac download button points at `https://github.com/addywaddy/couchpad-site/releases/latest/download/Couchpad.dmg`.
  It needs a published release with a file called exactly `Couchpad.dmg` (the Couchpad repo's `scripts/release-mac.sh`
  writes one to `dist/`). Change the link in `index.html` if the repository has another name.
- `support@couchpad.app` appears on the support and privacy pages. Set up a mailbox or forwarding for it, for example
  with Cloudflare Email Routing, or change the address.
- Add the App Store link next to "coming soon" in `index.html` once the iPhone app is live.

## Hosting on GitHub Pages

1. Create a **public** repository (for example `couchpad-site`) and push this folder to it. Pages on a private
   repository needs a paid GitHub plan.
2. Settings > Pages: deploy from the `main` branch, root folder.
3. Verify the domain: GitHub account settings > Pages > Add a domain, then add the TXT record GitHub shows. This stops
   anyone else claiming it.
4. DNS for `couchpad.app`:
   - four `A` records for the apex: 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
   - four `AAAA` records: 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153
   - a `CNAME` for `www` pointing at `<github-user>.github.io`
5. Settings > Pages: tick **Enforce HTTPS** once the certificate is ready. `.app` domains only work over HTTPS.
6. Check that https://couchpad.app/privacy/ and https://couchpad.app/support/ load. App Store Connect needs both URLs.

Check GitHub's current Pages documentation for the DNS values before relying on the ones above.

## Releasing the Mac app

Publish each Mac release as a GitHub Release in this repository with `Couchpad.dmg` attached; the download button
always serves the latest one.
