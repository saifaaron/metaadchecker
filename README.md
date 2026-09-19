# Meta Ad Checker for Android

A signed Android app (APK) for your Ad Checker. It opens **https://suresocial.agency/ad-checker-app/** full screen, with its own icon, splash screen and no browser bars. It uses Chrome's engine, so sign in, file uploads, the share sheet and exports all work exactly like the web app.

## ⚠️ Keep these two files safe

`release.keystore` and `keystore.properties` are your app's permanent signing key and its password. Every future update must be signed with the same key, and your website uses its fingerprint to prove the app is yours. **Back them up somewhere private** (for example a password manager) and only put this folder in a **private** GitHub repository.

Your key's fingerprint (SHA256):
```
F5:79:A2:6B:70:40:56:E3:71:5B:56:36:30:EE:27:3B:84:16:B5:52:83:D0:13:CC:EA:58:63:47:72:3B:1F:78
```

## Build the APK (about 5 minutes, no software to install)

1. Create a **private** repository on github.com and upload everything in this folder (drag and drop works on the repository page).
2. Open the repository's **Actions** tab, choose **Build Android app**, then **Run workflow**.
3. When the run turns green, open it and download **meta-ad-checker-android** from **Artifacts**. Inside:
   * `Ad Checker.apk`: install on any Android phone.
   * `Ad Checker (Play Store).aab`: only needed if you publish on Google Play.

**Or with Android Studio:** open this folder, let it sync, choose **Build → Generate Signed App Bundle / APK → APK**, and point it to `release.keystore` with the password in `keystore.properties`.

## Install on a phone

1. Send `Ad Checker.apk` to the phone (WhatsApp to yourself, Google Drive or email all work) and tap it.
2. Android asks to allow installs from that app (Chrome, Files or WhatsApp). Tap **Settings → Allow from this source**, go back, and tap **Install**.
3. Open **Ad Checker** and sign in with your WordPress account once.

## Remove the address bar (one time)

Android shows a thin address bar at the top until your site confirms the app belongs to it. The WordPress plugin (version 1.2) does this automatically at `suresocial.agency/.well-known/assetlinks.json`, already set to this app's fingerprint.

To check it: open **https://suresocial.agency/.well-known/assetlinks.json** in a browser. You should see a short block of text containing `agency.suresocial.adchecker`. If you see "Page not found", go to WordPress **Settings → Permalinks** and click **Save** once. After that, uninstall and reinstall the app (Android checks this when the app is installed).

If your host blocks that address, create the file yourself: save the text the plugin shows under **Ad Checker → Settings → Android app** as `assetlinks.json` inside a `.well-known` folder at your site's root.

## Publishing on Google Play (optional)

Upload `Ad Checker (Play Store).aab` in the Play Console ($25 one time developer fee). Google re-signs Play downloads with its own key: copy the **SHA-256 certificate fingerprint** from Play Console → Setup → App signing and add it on a new line under **Ad Checker → Settings → Android app** in WordPress, so both the APK and the Play version stay verified.

## Changing the site or app name

Edit `gradle.properties` (`TWA_HOST`, `TWA_PATH`, `APP_NAME`). For each update you publish, raise `VERSION_CODE` by 1 and `VERSION_NAME` as you like, then run the build again.

## Troubleshooting

| Problem | Fix |
|---|---|
| "App not installed" | An older copy signed differently is on the phone. Uninstall it, then install again |
| Address bar shows at the top | assetlinks.json isn't reachable yet. See "Remove the address bar" |
| Build fails on GitHub | Open the failed step, copy the first red error, and send it over |
| Opens a browser tab instead of the app | Chrome is missing or disabled. Install or enable Chrome from the Play Store |
