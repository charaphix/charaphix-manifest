# Adding manifest.json to a Framer-Hosted Site to Hide the Browser Search Bar

This guide explains how to add a `manifest.json` to your Framer site so that when it runs as a PWA (Progressive Web App), the browser's search/address bar is hidden.

---

## Option 1 — Host the manifest externally & link to it

**Best if you want to stay on Framer hosting.**

1. **Create `manifest.json`** on your computer with this minimal example:

```json
{
  "name": "My App Name",
  "short_name": "MyApp",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#ffffff",
  "icons": [
    {
      "src": "/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

2. Upload it somewhere public, such as:
   - GitHub Pages
   - Netlify
   - Cloudflare Pages
   - Your own server

3. Get the public URL, for example:
```
https://yourcdn.com/manifest.json
```

4. In Framer:
   - Go to **Settings → Custom Code → Head**.
   - Paste:
     ```html
     <link rel="manifest" href="https://yourcdn.com/manifest.json">
     ```

5. Publish the site.  
   The browser will fetch your manifest from that external URL.

---

## Option 2 — Export site from Framer and self-host

**Best if you control your hosting (e.g., Vercel, Netlify, or your own server).**

1. In Framer, click **File → Export**.
2. Save your exported files.
3. Place `manifest.json` in the **root** of your site folder (same level as `index.html`).
4. In your HTML `<head>` add:
   ```html
   <link rel="manifest" href="/manifest.json">
   ```
5. Deploy your site.

---

## Option 3 — Framer + Worker/Proxy Injection

**For advanced setups.**  
Use a Cloudflare Worker or Vercel Edge Function to intercept `/manifest.json` requests and serve the JSON.  
Point your `<link rel="manifest">` tag in Framer to `/manifest.json`.

---

## Notes

- **Android (Chrome)**: Requires `"display": "standalone"` in the manifest.
- **iOS (Safari)**: Also requires these meta tags in Framer's Head code:

```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="MyApp">
```

- Launch the PWA **from the home screen icon** for the search bar to be hidden.

---

**Recommendation:**  
If you want the easiest path and to stay on Framer hosting, **use Option 1 with GitHub Pages** to host the manifest externally and link to it.
