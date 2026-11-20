# PiggySweep PWA

PiggySweep is a mobile-first personal finance PWA packaged for Android with Capacitor.

## Run locally
Serve this folder from localhost (not by opening index.html as a file URL):

```bash
python -m http.server 8000
```

Open http://localhost:8000.

## Android
The Capacitor configuration uses `www` as its web asset directory. Keep `index.html`, `manifest.webmanifest`, `sw.js`, and the `icons` folder in sync with their copies under `www` before running `npx cap sync android`.

## Authentication and data
- Firebase Authentication uses email/password sign-in, account creation, and email-based password reset.
- Firebase stores authentication identity/session information; PiggySweep financial records are stored locally in the browser/WebView under a UID-specific local-storage key.
- Financial records are not uploaded to Firestore by this project.
- Passwords are never included in PiggySweep JSON backups.
- Local storage is not encrypted by default. Protect the device and keep exported backup files secure.
- Remember Email is optional; passwords are not remembered by the app.

## Backup and restore
Backup exports the signed-in account's financial data as a JSON file. Restore imports a supported PiggySweep JSON backup into the currently signed-in account after confirmation. Keep backup files private.

## Deploy
Upload the PWA web assets to the same directory on a static HTTPS host such as GitHub Pages. For Capacitor, copy the same updated web assets into `www` and sync the Android project.

## Copyright
**PiggySweep™**  
Designed & Developed by Vidyalakshmi Raghuraman  
© 2026 Vidyalakshmi Raghuraman. All rights reserved.
