# PiggySweep — Build 3.4

Mobile-first personal-finance PWA with a Capacitor Android project.

## Project structure

- `index.html`: GitHub Pages browser entry point and source of truth.
- `www/`: Capacitor web assets; kept in sync with the root web files.
- `vendor/firebase-app-compat.js`: Firebase App SDK (compat).
- `vendor/firebase-auth-compat.js`: Firebase Authentication SDK (compat).
- `vendor/firebase-firestore-compat.js`: Firebase Firestore SDK (compat).
- `firestore.rules`: Firestore rules for the feedback collection; publish these in the Firebase Console.
- `fonts/`: locally bundled Plus Jakarta Sans fonts.
- `icons/`: PWA icons.
- `sw.js`: browser service worker; it is not registered inside native Capacitor.
- `android/`: Android Studio project.

## Authentication, feedback and financial data

- Firebase Authentication provides email/password sign-in.
- Firestore is used only for authenticated Write to Us feedback submissions.
- Feedback is written to the `feedback` collection. The app shows its success message only after Firestore confirms the write.
- The app does not read, update or delete feedback documents. The supplied rules allow signed-in users to create their own feedback record and deny client reads, updates and deletes.
- Income, expenses, budgets, goals and investment records remain in device Local Storage under a Firebase-UID-specific key. They are not uploaded to Firestore.
- JSON backups are manual, plain, unencrypted files. Store them securely.
- Browser/device Local Storage is not encrypted by default.
- Piggy AI is a rule-based assistant; an LLM backend is future work.

## Firebase setup required for Write to Us

1. In the Firebase Console for project `piggysweep`, create/enable Cloud Firestore.
2. Publish the contents of `firestore.rules` in Firestore Rules.
3. Ensure Email/Password Authentication is enabled and the deployed web domain is listed under Authentication authorized domains.
4. Deploy the updated root `index.html` and `vendor/` folder together.
5. Sign in to PiggySweep and submit a test feedback item. Confirm a new document appears in `feedback`. A client-side success message should appear only after the write is accepted.
6. Test validation: subject must contain at least 3 characters, description at least 10 characters, and the reply email must be valid.

Firestore billing/usage limits depend on the Firebase plan and current project usage. Check the Firebase Console for current quotas. Firestore does not automatically email you when a feedback document is created; check the collection or configure a separate notification service if email alerts are needed.

## GitHub Pages

Publish the repository root with:
- `index.html`
- `manifest.webmanifest`
- `sw.js`
- `icons/`
- `fonts/`
- `vendor/`

Configure GitHub Pages to deploy from `main` and `/ (root)`. Keep the files and folder paths unchanged.

## Android

From this project folder run:

```bash
npm install
npx cap sync android
npx cap open android
```

Run `npx cap sync android` after every change to the root web app or `www/` assets. This refreshes the Android WebView assets and registers the installed Capacitor plugins. The Android WebView assets in this package have been refreshed from the current Build 3.4 web files.

Filesystem and Share packages are declared in `package.json` for native JSON backup sharing. Verify native backup/share on an Android emulator and a real device after syncing and building.

Keep `androidScheme: "https"` stable after users save data because changing the app origin can make existing origin-scoped data inaccessible.

## Release checks

- Configure Firebase Authentication authorized domains and restrict the Firebase web API key to the required web referrers.
- Test new-account signup, login, onboarding, logout/login, backup/restore, and second-account isolation.
- Test Write to Us against the real Firestore project; a simulated write is not proof of a live database submission.
- Verify offline operation in airplane mode; offline support is not claimed as verified until tested.
- Test native backup/share on an Android emulator and a real device.
- Test Play Zone navigation, all four Play Zone tiles, Piggy Games levels, Money Quiz levels, scoring and return navigation.
