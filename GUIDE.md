# Rep: build a real Android APK on your phone with GitHub

GitHub builds the APK for you in the cloud. You only upload two files and tap a few buttons. No computer needed.

## Files you need
- `rep-app.html`: the Rep app (the APK is built from this file)
- `build-apk.yml`: the build instructions for GitHub (it also contains the app icon and signing key)

## Step 1: Create a GitHub account and repository
1. In Chrome go to github.com and sign up (free).
2. Tap the **+** at the top, then **New repository**.
3. Name it `rep`, choose **Public**, and tap **Create repository**.

## Step 2: Upload the two files
1. On the empty repository page tap **uploading an existing file**.
2. Choose `rep-app.html` and `build-apk.yml` from your Downloads. Both must be in the main folder, not inside another folder.
3. Tap **Commit changes**.

## Step 3: Move the build file to the right place
GitHub only runs build files that live in a special folder.
1. Tap `build-apk.yml` in your file list, then tap the **pencil** (edit) icon.
2. Tap in the file name box at the top. Put the cursor at the very start, before `build-apk.yml`, and type `.github/workflows/` so the box reads `.github/workflows/build-apk.yml`.
3. Tap **Commit changes**, then **Commit changes** again.

## Step 4: Let it build
1. Open the **Actions** tab. If GitHub asks, tap **I understand my workflows, go ahead and enable them**.
2. You should see a run called **Build Rep APK**. If not, tap **Build Rep APK** on the left, then **Run workflow**.
3. The first build takes about 5 to 10 minutes. A green tick means it worked. A red cross means it failed (see Troubleshooting).

## Step 5: Download the APK
1. Go back to the main repository page and tap **Releases** (on the right on desktop view, or below the file list on mobile).
2. Open the newest release (for example "Rep build 1") and tap **Rep.apk** to download it.

## Step 6: Install it
1. Open the downloaded `Rep.apk` from your notifications or the Files app.
2. If Android blocks it, tap **Settings** and allow **Install unknown apps** for Chrome (or the Files app), then go back and tap **Install**.
3. If Google Play Protect warns about an unknown developer or an unscanned app, tap **Install anyway**. This is normal for apps you build yourself.

## Updating the app later
1. In your repository open `rep-app.html`, tap the pencil, make your change (or paste a newer version), and commit.
2. GitHub builds a new APK automatically. Download it from Releases and install it over the old one.
3. Your data is kept, because every build is signed with the same key. **Do not change or delete the signing key block inside build-apk.yml.**

## Your data and backups
- Everything is stored on your phone only. The app does not use the internet at all once installed.
- Uninstalling the app or clearing its storage deletes your data.
- Back up regularly: open the **setup** tab, then **backup**, then **download .json**. Android's share sheet opens so you can save the file to Drive or Files. To restore, use **upload .json**.

## Troubleshooting
- **Red cross on the build:** tap the failed run, tap the step with the red cross and read the last lines of the log. Most failures are temporary, so tap **Re-run all jobs** once before anything else.
- **No Releases appear / "403" in the last step:** go to **Settings**, then **Actions**, then **General**, find **Workflow permissions**, choose **Read and write permissions**, save, then re-run the build. You can also download the APK from the run page under **Artifacts** (it comes as a ZIP).
- **Nothing happens after uploading:** the build file must be at `.github/workflows/build-apk.yml` (Step 3), and Actions must be enabled.
- **"App not installed":** uninstall an older Rep first. This also happens if the signing key block in the build file was changed.
- **Cannot find the pencil or settings on mobile:** turn on **Desktop site** in Chrome's menu.

## Honest limitations
- This builds a **debug-signed** APK for your own phone. The signing key is public inside your repository, so it is **not suitable for the Google Play Store**. Publishing there needs a private release key and a Play developer account.
- The APK is a web app wrapped in Android (Capacitor). It works offline because all files are inside the APK.
- I checked the build file's structure, scripts, icon generator, signing key and the app's code for errors, but I could not run the GitHub build or install the APK in this chat. If the first build fails, send me the last lines of the failed step's log and I will fix it.
