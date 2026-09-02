# The Vault Network — static site

Live: https://vault-network.vercel.app/

Nine pages, no build step, no server requirement. Open `index.html` or deploy
the folder as-is; Vercel and GitHub Pages both serve it unchanged.

```
index.html          home
vaults.html         the register
partners.html       for partners
about.html
faq.html
checkout-demo.html  the purchase flow, interactive
wallet.html         your vaults, sign-in gate (demo code 374912)
terms.html
privacy.html
vaults/             four tier renders and the archive still
logo.svg            brand lockup (also inlined in every page)
favicon.*, icon-*.png, apple-touch-icon.png, site.webmanifest, og.png
HOME-PAGE-SPEC.md   how the home page is built, section by section
CHANGELOG.md        what changed on 2 September 2026
```

External dependencies, all optional — the pages render without them:
Google Fonts (Archivo, JetBrains Mono), GSAP 3.12.5 with ScrollTrigger and
CustomEase, Three.js r128, all from cdnjs.

Social tags use absolute URLs against the live host. Moving domains means
regenerating the pages with the new base, not editing nine files.
