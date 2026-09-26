# Place link site

Shared place links (`https://<LINK_HOST>/p/?ll=…&n=…&r=…&i=…`) point here.
If the app is installed, Android opens the app directly. If it isn't, this page shows the place and links to Google Maps.

## Setup (GitHub Pages)

1. Create a public repo named exactly `<username>.github.io`.
2. Upload everything in this folder to the repo root, including `.nojekyll` and `.well-known/`.
   GitHub Pages skips dot-folders without `.nojekyll`.
3. Repo → Settings → Pages: deploy from branch `main`, folder `/ (root)`.
4. Check that `https://<username>.github.io/.well-known/assetlinks.json` loads.
5. Add `LINK_HOST=<username>.github.io` to `local.properties`, then rebuild and reinstall the app.
6. Check the phone: `adb shell pm get-app-links pl.xirate.commutetimer` should show `verified`.
   To re-check after a fix: `adb shell pm verify-app-links --re-verify pl.xirate.commutetimer`.

## Signing keys

`assetlinks.json` lists the SHA-256 of every key the app is signed with. Right now that's only the debug key on this PC.
When you publish, add the release upload key's fingerprint, and also the **Play App Signing** key's fingerprint
(Play Console → Test and release → App integrity).
Otherwise links will stop opening the Play Store version of the app.
