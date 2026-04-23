# asteisesdev.ru — deploy

Static site. Zero build step. Drop on any HTTP host.

## Contents
- `index.html` — the landing page (self-contained; pulls fonts from Google Fonts CDN)
- `robots.txt` — allow-all
- `sitemap.xml` — single URL
- `404.html` — simple not-found fallback

## Deploy

### nginx (typical VPS)
```
server {
  listen 443 ssl http2;
  server_name asteisesdev.ru;
  root /var/www/asteisesdev;
  index index.html;
  error_page 404 /404.html;

  location / { try_files $uri $uri/ =404; }
  location ~* \.(html)$ { add_header Cache-Control "public, max-age=300"; }
}
```

### GitHub Pages / Netlify / Vercel / Cloudflare Pages
Upload the contents of this folder as the publish directory. No build command.

### rsync
```
rsync -avz --delete ./deploy/ user@asteisesdev.ru:/var/www/asteisesdev/
```

## Notes
- Replace the `href="#"` on the GitHub / LinkedIn / Telegram icons with real URLs before deploying.
- Favicon not yet set — add `<link rel="icon" ...>` once you have one.
