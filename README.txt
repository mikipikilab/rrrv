Clinic Status — Netlify bundle

Files:
- index.html (public status page)
- admin.html (admin UI, languages: sr/ru/en)
- functions/overrides.js (hardened with safe JSON reads)
- functions/repair.js (temporary cleaner for invalid blob keys/values)
- netlify.toml (redirects /api/* to functions)
- package.json (ESM + @netlify/blobs)

Setup on Netlify:
1) Site settings → Environment variables → add NETLIFY_ADMIN_KEY with your secret key.
2) Deploy.
3) (Temporary) Clean bad blob records:
   • /.netlify/functions/repair?mode=list
   • /.netlify/functions/repair?mode=clean
4) Test:
   • /.netlify/functions/overrides → {} (or valid JSON map)
   • /.netlify/functions/overrides?date=YYYY-MM-DD
5) Open /admin.html, switch language if needed, login with the same NETLIFY_ADMIN_KEY, save an override.

Notes:
- Remove functions/repair.js after cleaning.
- If you previously stored non-ISO keys or “[object Object]” strings, the cleaner will delete them.
