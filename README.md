# PiggySweep PWA

This package uses the newly supplied `index.html` as its source of truth. The embedded launch-screen background, app background, and embedded PiggySweep logo data URI are preserved.

## Run locally
Serve this folder from `localhost` (not by opening `index.html` as a `file://` URL), for example:
`python -m http.server 8000`

Open `http://localhost:8000`.

## Deploy
Upload the contents of this folder to the same directory on a static HTTPS host such as GitHub Pages.

## Notes
- The login flow in this front-end is a local demo gate, not secure account authentication.
- App data is stored in the browser's local storage; it is not synced across devices.
- JavaScript syntax and manifest JSON were checked. A full browser/device functional test has not been performed.
