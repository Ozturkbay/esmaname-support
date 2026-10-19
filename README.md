# Esmaname — Privacy & Support site

Public support and privacy website for **Esmaname** (App Store name
"Esmaname: Esmaül Hüsna & Zikir") for iPhone. It provides the Privacy Policy
URL and Support URL required by App Store Connect. **Turkish is the primary
language** (site root); English lives under `/en/`.

- **Developer:** Fatih Öztürkbay
- **Support email:** `ESMA_SUPPORT_EMAIL` (placeholder — see below)

It is a plain static site: HTML and one CSS file. No framework, no build
step, no JavaScript, no external fonts, scripts or stylesheets.

## URLs

Intended for GitHub Pages from the `main` branch, repository root:

| Page | URL |
| --- | --- |
| Ana sayfa (TR) | https://ozturkbay.github.io/esmaname-support/ |
| Gizlilik Politikası (TR) | https://ozturkbay.github.io/esmaname-support/gizlilik/ |
| Destek (TR) | https://ozturkbay.github.io/esmaname-support/destek/ |
| Home (EN) | https://ozturkbay.github.io/esmaname-support/en/ |
| Privacy Policy (EN) | https://ozturkbay.github.io/esmaname-support/en/privacy/ |
| Support (EN) | https://ozturkbay.github.io/esmaname-support/en/support/ |

The app links to `gizlilik/` and `destek/` (see `src/constants/links.ts` in
the `ProjectEsma` repository). Use the same two URLs in App Store Connect's
Privacy Policy URL and Support URL fields.

## Structure

```
index.html              Ana sayfa (TR, with EN links)
gizlilik/index.html     Gizlilik Politikası (TR)
destek/index.html       Destek (TR)
en/index.html           Home (EN, with TR links)
en/privacy/index.html   Privacy Policy (EN)
en/support/index.html   Support (EN)
assets/css/styles.css   The only stylesheet
assets/images/          App icon, favicon, apple-touch-icon
.nojekyll               Serve files as-is (no Jekyll processing)
```

Every page has a language switch to its equivalent in the other language and
`hreflang` alternates (`tr`, `en`, and `x-default` pointing to Turkish).

All internal links are relative, so the site works under the
`/esmaname-support/` project path. The only absolute URLs are the
`<link rel="canonical">` and `hreflang` tags in each page's `<head>`. If the
site moves (for example, to a custom domain), update those tags too:

```sh
grep -rl "https://ozturkbay.github.io/esmaname-support/" --include='*.html' .
```

## Before publishing: set the support email

Every email address is the literal placeholder `ESMA_SUPPORT_EMAIL` (in
`mailto:` links and visible text). Files containing it:

- `index.html`
- `gizlilik/index.html`
- `destek/index.html`
- `en/index.html`
- `en/privacy/index.html`
- `en/support/index.html`
- `README.md` (this file — documentation only)

Replace it in the HTML files once the address is chosen, then confirm none
remain:

```sh
grep -rl ESMA_SUPPORT_EMAIL --include='*.html' . \
  | xargs sed -i '' 's/ESMA_SUPPORT_EMAIL/you@example.com/g'
grep -rn ESMA_SUPPORT_EMAIL --include='*.html' .
```

## Publish on GitHub Pages

1. On GitHub, create a **public** repository named `esmaname-support` under
   the `Ozturkbay` account (no README, license or .gitignore — this repository
   already has its content).
2. Push `main`:

   ```sh
   git remote add origin https://github.com/Ozturkbay/esmaname-support.git
   git push -u origin main
   ```

3. In the repository, open **Settings → Pages**. Under **Build and
   deployment**, set **Source** to *Deploy from a branch*, then choose branch
   `main` and folder `/ (root)`, and save.
4. After the first deployment finishes, open
   https://ozturkbay.github.io/esmaname-support/ and check every page.

## Local preview

From the repository root:

```sh
python3 -m http.server 8000
```

Then open http://localhost:8000/. (Opening the files directly with
`file://` won't resolve the directory-style links such as `gizlilik/`.)

## Updating the last-updated date

The privacy policies show their date near the top:

- `gizlilik/index.html` — `Son güncelleme: 19 Ekim 2026`
- `en/privacy/index.html` — `Last updated: October 19, 2026`

When the policy changes, edit both lines together and keep the Turkish and
English texts aligned section by section. Turkish month names: Ocak, Şubat,
Mart, Nisan, Mayıs, Haziran, Temmuz, Ağustos, Eylül, Ekim, Kasım, Aralık.

The policy describes what the app does today: free download with a one-time,
non-consumable Premium in-app purchase (no subscription, Family Sharing not
enabled); no accounts, ads, analytics, tracking or server; counts, favorites,
Zikirlerim, history and settings stored only on the device (SQLite and the
iOS Keychain); an optional, locally scheduled daily reminder; Diyanet source
pages opened in the browser only on "Kaynağı Aç". If the app adds iCloud
sync, an account, an SDK, analytics, push notifications, a server or a new
permission, review both privacy pages and the related Support sections before
releasing that version.

## App icon

`icon.png` (1024×1024) is a copy of `assets/images/icon.png` from the
`ProjectEsma` app repository. `apple-touch-icon.png` (180×180) and
`favicon.png` (64×64) were resized from it with macOS `sips`. The source file
was not modified, and nothing is hotlinked.

## Design

Colors follow the Esmaname palette: cream background (`#F6F3EA`), deep green
(`#0F4A3A`) for links and focus, gold (`#C7A35A`) as an accent for rules and
highlights only (never body text). Dark appearance follows
`prefers-color-scheme`: background `#0E1512`, primary `#78A48F`, accent
`#D3B36E`. Copy is factual and modest: no spiritual claims, prices not
hard-coded ("App Store'da gösterilen fiyat").

## Privacy of this website

This website contains no first-party analytics or tracking code: its own
code sets no cookies, uses no analytics, tracking scripts or marketing
pixels, loads no third-party fonts, scripts or stylesheets, and contains no
JavaScript. When hosted on GitHub Pages, see the
[GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement)
for how GitHub handles data.
