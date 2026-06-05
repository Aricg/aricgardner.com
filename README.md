# aricgardner.com

Business website for [aricgardner.com](https://aricgardner.com), built as a static Astro site with TypeScript.

## Development

```bash
corepack enable
pnpm install
pnpm dev
```

## Build

```bash
pnpm build
```

Astro writes the production site to `dist/`. Nginx should serve that directory, or a copy of that directory, instead of reading from the repo in the home folder.

This project uses pnpm so dependency install scripts are not silently allowed. If pnpm reports ignored builds, review them with:

```bash
pnpm approve-builds
```

Only approve packages when there is a clear reason they need an install-time build script.

Example Raspberry Pi deployment path:

```text
/home/agardner/aricgardner.com        source repo
/var/www/aricgardner.com              built static site
```

Example deploy commands on the Pi:

```bash
cd /home/agardner/aricgardner.com
git pull
corepack enable
pnpm install --frozen-lockfile
pnpm build
sudo rsync -a --delete dist/ /var/www/aricgardner.com/
sudo nginx -t
sudo systemctl reload nginx
```
