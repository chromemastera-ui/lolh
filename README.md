# LOL (Android app)

App name: **LOL** · icon: the cat photo · inside: your Memory Lane app (`app/src/main/assets/www/index.html`).

## Option A: get the APK without installing anything (GitHub)
1. Make a free account at github.com, then create a new repository.
2. Upload everything from this folder to it. Use "Add file → Upload files" and drag in the contents, including the hidden `.github` folder.
3. Open the **Actions** tab. The "Build LOL APK" job starts by itself (about 3-5 minutes). If it doesn't, click it and press "Run workflow".
4. When it finishes, open the run and download **LOL-apk** from "Artifacts". Unzip it to get `app-debug.apk`.
5. Send the APK to your phone and open it. Allow "install unknown apps" when Android asks.

## Option B: Android Studio
1. Open this folder in Android Studio and let it sync (it downloads the Android SDK pieces it needs).
2. Menu: **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
3. The file is at `app/build/outputs/apk/debug/app-debug.apk`.


## Make your friends able to chat from different phones (one-time setup, ~5 minutes)
The app now syncs through a free Supabase database, so everyone sees the same accounts, posts, comments, chat and shop.

1. Go to supabase.com, sign up (free, no card), and click **New project**. Pick any name and password, then wait ~1 minute.
2. Left menu: **SQL Editor → New query**. Open `supabase-setup.sql` from this folder, paste all of it, press **Run**. It should say "Success".
3. Left menu: **Project Settings → API**. Copy the **Project URL** and the **anon / publishable key**.
4. Open `app/src/main/assets/www/cloud-config.js` and paste them between the quotes:
   `window.CLOUD = { url: "https://xxxx.supabase.co", key: "eyJ..." };`
5. Build the APK again (Option A or B above) and send it to your friends. Everyone installs the same APK.

How it behaves:
- Changes show up on other phones within ~3 seconds while the app is open.
- Photos and videos are uploaded online too. Max 50 MB per file (Supabase free limit); 1 GB total storage.
- Photos and videos already on your phone are uploaded the first time you open the new version while online.
- The app still opens without signal. Changes sync once you're back online.
- The admin account (new2026manish@gmail.com) is the same on every phone.

Privacy note: this is meant for a private friends group. The key in the APK lets anyone who extracts it read and edit the shared data, including each person's email and hashed password. Don't share the APK publicly and tell friends to use a password they don't use anywhere else.

## Notes
- Without the Supabase setup above, accounts, posts, coins and photos are stored on the phone itself and each phone has its own separate data.
- To change the app, edit `app/src/main/assets/www/index.html` and build again.
- To change the icon, replace the images in `app/src/main/res/mipmap-*`.
