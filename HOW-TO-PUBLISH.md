# Putting Ashfall on Google Play

The game is a Progressive Web App (PWA). Google Play accepts PWAs wrapped as a "Trusted Web Activity": a tiny Android app that opens your hosted game full-screen, with no browser bar. You don't need Android Studio.

## 1. Host the folder (free)
Upload everything in this folder to any HTTPS host, for example:
• **GitHub Pages:** create a repo, upload the files, then turn on Settings › Pages.
• **Vercel or Netlify:** drag and drop the folder.
Open the address on your phone. The game should load, and your browser should offer "Install app" or "Add to Home screen".

## 2. Make the Android package
1. Go to **pwabuilder.com** and paste your game's address.
2. Choose **Package for stores › Android**. Keep the package ID it suggests (e.g. com.yourname.ashfall), or change it now: it can never change later.
3. Download the zip. It contains an **.aab** (what you upload to Play), a **signing key** (back it up, because you can't update the app without it), and an **assetlinks.json** file.
4. Upload **assetlinks.json** to your site at `/.well-known/assetlinks.json`. This file is what removes the browser address bar.

## 3. Google Play Console
1. Create a developer account at play.google.com/console: a one-time $25 fee and an identity check.
2. Create the app and fill in the listing from STORE-LISTING.md. Privacy policy URL: `https://YOUR-SITE/privacy.html`.
3. New personal accounts must first run a **closed test with at least 12 testers for 14 days in a row** before they can publish to everyone. Friends who play on Android count. Each one opts in with the test link and plays.
4. After the 14 days, apply for production access and publish.

## 4. The Supporter Pack (optional, one-time purchase)
The game already contains the Supporter Pack screen (title screen › 🔥 Support Ashfall). It is cosmetic only: 9 hero looks, 5 colour themes, an ember trail, a golden name, the "Patron of the Ash" title and a 🔥 rankings badge. Inside the Play Store app it buys through **Google Play Billing**; everywhere else it just says it's available in the Play Store version. As the creator, you always have it in the claude.ai version.

To switch it on:
1. In Play Console, set up a **payments profile** (Settings › Payments profile). Selling anything needs one.
2. Go to **Monetise › Products › In-app products** and create a product with the ID **`supporter_pack`** (exactly that), as a one-time (non-consumable) product. Set your price, e.g. €2.99. Activate it.
3. When you package on PWABuilder, open **Options** and turn on **Play Billing** (the "Digital Goods API" / `playBilling` feature). Without it, the game can't see Google Play.
4. Add the same Google accounts as **licence testers** (Settings › Licence testing) so you can test buying without being charged.
5. Test in the closed-test build: buy it, then uninstall, reinstall and tap **Restore purchase**.

Google requires purchases to be **acknowledged** within 3 days or it refunds them automatically. The Play Billing bridge in a Trusted Web Activity normally acknowledges when the purchase completes. Check that your test purchase shows as "Acknowledged" in Play Console › Order management; if it doesn't, tell me and we'll add a small server step.

Google takes 15% of the first $1M a year. The listing must say "Contains in-app purchases".

## Updating the game later
Replace index.html on your host and change the VERSION line in sw.js (any new text), so players get the new version. You don't need to upload a new .aab for game changes, only if the icon or name changes.

## About the AI story bonus
The AI storytelling only works inside Claude. The app version uses the full pre-written library: 200+ events, 9 arcs, and the companion, class and character storylines. If you later want AI in the app, the options are (a) a server you run with your own API key, paid for by app sales or a subscription, or (b) players entering their own key.
