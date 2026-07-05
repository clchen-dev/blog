# Zenlab Blog

A personal blog built with Hugo and the [Diary](https://github.com/AmazingRise/hugo-theme-diary) theme.

Site: https://blog.zenlab.top

This project is a fork of [riba2534/blog](https://github.com/riba2534/blog). The original theme structure is kept, but the upstream articles and personal information have been removed and replaced with my own content.

# Build

> Requires the extended version of Hugo.

```bash
# Clone the repository
git clone https://github.com/clchen-dev/blog.git
cd blog

# Start the local dev server
hugo server --disableFastRender

# Build the static site
hugo --minify
```

Or via the bundled `Makefile` (`make help` lists all targets): `make serve`, `make build`, `make new title="..."`, `make preview`.

# Deployment

Deployed to Cloudflare Pages.

- Project name: `blog`
- Production branch: `main`
- Build output: `public`
- Custom domain: `blog.zenlab.top`

A GitHub Actions workflow (`.github/workflows/deploy.yml`) runs on every push to `main`:

1. Installs Hugo Extended
2. Runs `hugo --minify`
3. Publishes via `wrangler pages deploy public --project-name blog --branch main`

Required GitHub Secrets:

- `CLOUDFLARE_ACCOUNT_ID`
- `CLOUDFLARE_API_TOKEN`

# Credits

- Theme: [hugo-theme-diary](https://github.com/AmazingRise/hugo-theme-diary), bundled directly under `themes/diary`
- Forked from [riba2534/blog](https://github.com/riba2534/blog)
