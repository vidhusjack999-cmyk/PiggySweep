# PiggySweep

Mobile-first personal finance PWA with a Capacitor Android project.

## Project structure
- `index.html`: GitHub Pages browser entry point.
- `www/`: Capacitor web assets, synchronised with the root entry point.
- `vendor/`: locally bundled Firebase Authentication compat SDK.
- `fonts/`: locally bundled Plus Jakarta Sans font files.
- `icons/`: PWA icons.
- `sw.js`: browser service worker; registration is skipped in native Capacitor.
- `android/`: Android Studio project.

## Authentication and data
- Firebase Authentication provides email/password sign-in.
- Financial records are stored locally under a Firebase UID-specific key; they are not stored in Firestore.
- JSON backups are manual, plain, unencrypted files. Store them securely.
- Browser/device Local Storage is not encrypted by default.
- Piggy AI is a rule-based assistant; an LLM backend is future work.

## GitHub Pages
Publish root `index.html`, `manifest.webmanifest`, `sw.js`, and the `icons/`, `fonts/`, and `vendor/` folders. Configure Pages to deploy from `main` and `/ (root)`.

## Android
From this folder run:
```bash
npm install
npx cap sync android
npx cap open android
```
Filesystem and Share plugins are included for native JSON backup sharing. `cap sync` copies `www/` into Android. Keep `androidScheme: "https"` stable after users save data because changing the app origin can make existing origin-scoped data inaccessible.

## Release checks
- Configure Firebase Authentication authorized domains and restrict the Firebase web API key to required web referrers.
- Test new-account signup, login, onboarding, logout/login, backup/restore, and second-account isolation.
- Verify offline operation in airplane mode; offline support is not claimed as verified until tested.
- Test native backup/share on an Android emulator and a real device.
