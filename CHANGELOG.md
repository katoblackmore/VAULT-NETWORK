# Vault Network — changelog, 2 September 2026

Scope: `site-04` only. `site-01` was retired the day before and is not part of
the deliverable.

## Home page

1. **3D model.** The rack is gone; the 63 safes stay in their positions. The
   model is 35% larger, done by moving the camera in rather than scaling the
   geometry. On scroll the safes scatter outward — along the row, by level, and
   forward — and return on the way back up. Progress is the hero's own travel,
   so the field is fully apart as the hero leaves the screen.
2. **The network remains.** Right-hand text is now *The seal holds until you
   decide it shouldn't.*, with the reveal animation.
3. **Nothing here opens by accident.** The three figures are back — 4 Tiers in
   the register, 1 Unlock per vault ever, 0% Vaults reissued after unlock — with
   counters. The vertical dividers between them were removed.
4. **Left edge aligned across the page.** Two causes: `.shaft-head` used the
   `padding` shorthand on an element that also carried `.wrap`, which reset the
   side padding to zero and slid the register block one gutter left; and the
   hero footer had no width cap, so above 1560px it diverged from every other
   section (180px at 1920, 500px at 2560).
5. **Register stack.** Reward pools removed from the home-page cards. The
   closing line and *Open the full register* moved inside the fourth card and
   sit 120px lower. The receding card now fades to zero — at 34% it was still
   drawn and its edges showed past the card in front.
6. **Purchase flow.** Heading changed to *Checkout that feels familiar.* and
   given the same word reveal as the other section headings. The terms line and
   *Open the checkout demo* moved into the left column under the seven steps;
   100px before the button. The *You will receive* block was removed from the
   preview.
7. **Subtitles.** One 22px gap and muted colour everywhere. The `.note` rule
   had been scoped to `.band`, so the leads in the partners and closing blocks
   had neither.
8. **Partners render.** The pointer tilt was removed from the whole cell and
   kept on the image only, at 9°, with a reset when the pointer leaves either
   the image or the cell.

## Footer, all pages

9. Top block rebuilt as a centred column after the supplied reference. *Seal
   intact across the register* and *Start an integration* removed. *The Network
   remains. / Collect, trade, unlock.* at display size, second line in the
   accent, animated line by line.

## Interior pages

10. **vaults.html** — pointer tilt on all four renders, same parameters as the
    partners block.
11. **about.html** — *Four kinds of holding* laid out after the reference:
    heading top left, paragraph offset to the right column, label, four ruled
    columns. Content unchanged.
12. **wallet.html** — the top block (kicker, *Your vaults*, lead) removed; the
    *Demo mode · nothing is sent and no account is created* line removed. An
    invisible `h1` keeps the document outline valid.
13. **terms.html, privacy.html** — the panel behind the text removed. The
    warning callout at the top of Terms was kept.

## Defects found and fixed

14. **Flash of the archive photograph before the model.** The fallback image
    was shown by default and hidden once the model came up, which is a frame or
    two of the photograph on every load. It is now hidden until Three.js is
    confirmed missing.
15. **Interior pages had no animations at all.** The reveal block was inserted
    into the script at the magnetic-button line; when those buttons were
    removed the anchor vanished and the insertion silently matched nothing.
    Every page except the home page lost its reveals from that point. The
    builder now asserts the anchor is found exactly once.
16. **Hero headline overflow.** Three causes: line width was read from the
    block's box rather than the text (block width is the column, so every ratio
    was 1 and the type pinned near maximum); available width included the
    parent's padding; and the fit lived inside the motion script, which returns
    early without GSAP. Now `scrollWidth`, the parent's content box, a
    frame-coalesced resize, and its own script.
17. **Footer statement broken by the word reveal.** Inside a centred flex
    column the inline-block words made the line shrink to its widest word, and
    the first line never showed. Replaced with a per-line reveal and
    `width:100%` on the block.

## New material

18. **`HOME-PAGE-SPEC.md`** — a build specification for the home page: tokens,
    dependencies, every section with its copy and layout values, the model's
    dimensions and framing maths, the motion layer, the footer, the palette
    switcher, breakpoints, accessibility, and a list of sixteen traps that
    shipped and had to be found.
19. **Favicon and Open Graph.** SVG, ICO (16/32/48/64), PNG 16/32, Apple touch
    180, Android 192/512, web manifest. OG card 1200×630 in the page's style,
    set in Archivo. Per-page `description`, `og:*` and `twitter:*` tags on all
    nine pages. `og:url` and `og:image` are absolute against
    `https://thevaultnetwork.world/`; change `SITE_URL` in the builder if the
    domain differs.
20. **Four logo directions** — Seal, Register, Core, Container. Each as a
    horizontal lockup for dark, a version for light, and the mark alone; the
    wordmark is Archivo 900 converted to outlines. Delivered separately in
    `logo-lockups.zip`.

## Later the same day

21. **Brand lockup.** The client's two-line logo replaced the mark and text in
    the header and footer. Inlined as SVG rather than linked: a page opened on
    its own showed a broken image. 36px in the header — below the 44px pill,
    so the bar did not grow.
22. **Footer simplified** to one row (lockup and the main menu in a line), a
    rule, and the legal line with Terms and Privacy. Statement, email form, link
    columns, contact block and facts row removed, with their styles.
23. **Hero gradient full width.** Capping the hero footer to the page column had
    capped the gradient too; it now paints on a viewport-wide pseudo-element
    while the copy stays in the column.
24. **Open Graph domain.** Tags had pointed at `thevaultnetwork.world`, where
    no image exists; they now use `https://vault-network.vercel.app/`.
25. **Favicon and OG card from the client's files.** The supplied `favicon.svg`
    rasterised to every size and the `.ico`; the supplied `OG.png` flattened
    to RGB and shipped as `og.png`.

## Reverted

- The footer statement was briefly returned to its original small setting on a
  misreading of "as it was"; the display-size version was restored.

## Deliverables

- `vault-network-site.zip` — the nine pages, assets, icons, OG card and the
  spec. Items 1–19.
- `logo-lockups.zip` — item 20.

Every rebuild today was followed by the same checks: markup balance, duplicate
ids, heading order, `alt` on images, internal links and anchors, asset
presence, undefined CSS tokens, and a DOM run of all nine pages that opens the
menu, switches every palette, works the FAQ, the checkout basket, the wallet
gate and the footer form. All green at the last build.
