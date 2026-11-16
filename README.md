# ems-intl-trading.com — EMS International Trading Co., Ltd.

The corporate website for EMSインターナショナルトレーディング株式会社 (EMS International Trading Co., Ltd.) in Japanese and English.

## How the site is built

The site is a static build. There is no server, database or tracking.

| Path | What it holds |
|---|---|
| `content/site.json` | Facts shared by both languages: domain, email, phone, the page list and image sizes |
| `content/ja.json`, `content/en.json` | Every visible word, one file per language. Both files must have the same keys, and the build stops if one is missing |
| `templates/` | Jinja2 templates |
| `assets/` | CSS, JavaScript and WebP images |
| `build.py` | Writes the finished site to `dist/` |
| `check.py` | Fails the build on broken links, missing SEO tags, a missing `alt` or a wrong `lang` attribute |

To work on the site locally:

```bash
pip install jinja2==3.1.6
python build.py && python check.py
python -m http.server -d dist 8000   # then open http://localhost:8000/ja/
```

Pushing to `main` deploys the site through GitHub Actions (`.github/workflows/pages.yml`).

## Where the content came from

Everything was restored from the Wayback Machine captures of ems-intl-trading.com, taken between 2014 and 2024.

- **Contact details:** address, telephone, fax and `info@ems-intl-trading.com` are as published in the 2016–2024 captures. The office has been at Ise-cho, Kawasaki since 1 February 2016.
- **Online shop and prices:** the shop (cart, account and payment pages) was not rebuilt. This site is a corporate site, and visitors are asked to send an inquiry for prices.
- **Health claims:** nutrition and health claims (for example the mineral content of date syrup) were left out to stay within Japan's 景品表示法 and 健康増進法. Origins, certifications and recipes were kept.
- **Brand logos:** partner and brand logos are not used. Brand names appear as plain text, and the EMS logo has been redrawn as SVG.

## Going live

1. In GitHub, go to **Settings → Pages → Source** and choose **GitHub Actions**. Then go to **Settings → General** and set the default branch to `main`.
2. At the domain's DNS provider, add these records:
   - `A` records on `@` pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`
   - `AAAA` records on `@` pointing to `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153` and `2606:50c0:8003::153`
   - a `CNAME` record on `www` pointing to `slim7505.github.io`
3. Go to **Settings → Pages**, set the custom domain to `ems-intl-trading.com` and tick **Enforce HTTPS**.

> Changing the DNS records does not touch email. Leave the `MX` records for `info@ems-intl-trading.com` exactly as they are.
