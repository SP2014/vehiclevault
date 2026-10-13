# appcraft.solutions

The AppCraft Solutions website: company home, the VehicleVault features
page, its help guide and its privacy policy (the URL Play Console needs).

Plain HTML and one stylesheet, with no build step. GitHub Pages serves the
files as they are.

```
index.html                    company home
vehiclevault/index.html       features and screenshots
vehiclevault/help/            help guide
vehiclevault/privacy/         privacy policy  ← Play Console URL
404.html                      "−404d: this page has expired"
assets/site.css               "Forest garage" design language, light + dark
assets/fonts/                 the app's fonts as woff2, with OFL licences
assets/img/                   screenshots, icon, social preview
CNAME                         tells GitHub Pages the custom domain
```

Preview locally: `python3 -m http.server 8000`, then open
http://localhost:8000.

## Keep in step with the app

- **Screenshots** come from `vehicle_vault/store/screenshots`, resized to
  540×1080 WebP. Regenerate them there first, then convert again.
- **Help text** quotes the app's button labels. If a label changes in the
  app, search this folder for it.
- **Privacy policy**: change it here *and* in `vehicle_vault/RELEASE.md`,
  and update the "Last updated" date.
- **Play link**: once the app is live, replace the "Coming soon on Google
  Play" button in `vehiclevault/index.html` with
  `https://play.google.com/store/apps/details?id=solutions.appcraft.vehiclevault`.

## Publish on GitHub Pages

1. Create a public repo (e.g. `Ash415-pixel/appcraft.solutions`) and push
   this folder to its `main` branch.
2. Repo → Settings → Pages → Source: **Deploy from a branch**, `main`,
   `/ (root)`.
3. Same page → Custom domain: `appcraft.solutions` (the `CNAME` file
   already says so).
4. Once DNS (below) has propagated, tick **Enforce HTTPS**. The
   certificate can take up to an hour to issue.
5. Recommended: your GitHub profile → Settings → Pages → **Add a verified
   domain**. Add the TXT record it shows. This stops anyone else from
   claiming your domain on GitHub Pages if the site is ever unpublished.

## DNS at your domain registrar

| Type  | Name / Host | Value                    |
|-------|-------------|--------------------------|
| A     | `@`         | `185.199.108.153`        |
| A     | `@`         | `185.199.109.153`        |
| A     | `@`         | `185.199.110.153`        |
| A     | `@`         | `185.199.111.153`        |
| AAAA  | `@`         | `2606:50c0:8000::153`    |
| AAAA  | `@`         | `2606:50c0:8001::153`    |
| AAAA  | `@`         | `2606:50c0:8002::153`    |
| AAAA  | `@`         | `2606:50c0:8003::153`    |
| CNAME | `www`       | `ash415-pixel.github.io` |

Remove any parking-page A records the registrar added. Check with
`dig appcraft.solutions +short`: it should list only the four IPs above.
`www.appcraft.solutions` then redirects to the apex automatically.

## support@appcraft.solutions

The site and the privacy policy use this address, so it must work before
the Play listing goes live. Pick one free option:

- **ImprovMX** (works with any registrar): sign up, add the domain, set up
  forwarding to your Gmail, then add the records it shows. At the time of
  writing those are:

  | Type | Name | Value                                     | Priority |
  |------|------|-------------------------------------------|----------|
  | MX   | `@`  | `mx1.improvmx.com`                        | 10       |
  | MX   | `@`  | `mx2.improvmx.com`                        | 20       |
  | TXT  | `@`  | `v=spf1 include:spf.improvmx.com ~all`    |          |

- **Cloudflare Email Routing**: free, but only if the domain's DNS is
  moved to Cloudflare. If you do that, add the GitHub records above in
  Cloudflare with the proxy turned **off** (grey cloud) for the A, AAAA
  and CNAME records.

Send a test email to support@appcraft.solutions from another account to
confirm it arrives.

To reply *as* support@ from Gmail, use Gmail → Settings → Accounts → "Send
mail as". This needs an SMTP service; ImprovMX's paid plan includes one.

## Licences

The fonts are under the SIL Open Font License; the texts are in
`assets/fonts/`. Everything else © 2026 AppCraft Solutions.
