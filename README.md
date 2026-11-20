# Offside Social: club sign-up (GitHub Pages + Firebase)

Players open the link, type their name and pick a club. A picked club can't be chosen by anyone else.
The page only shows **names** of who has signed up. Nobody can see who picked which club, except you on the organiser view.

Firebase is free for this (the Spark plan, no card needed). Setup is about 10 minutes, once.

---

## 1. Create the Firebase project
1. Go to https://console.firebase.google.com and sign in with your Google account.
2. **Create a project** → name it `offside-social` → turn **off** Google Analytics → **Create project**.

## 2. Connect this page to it
1. On the project home, click the **web icon `</>`** ("Add app").
2. Nickname: `signup` → **Register app** (don't tick Hosting).
3. Firebase shows a block `const firebaseConfig = { apiKey: ..., authDomain: ..., ... }`.
4. Open **config.js** in VS Code and replace the six values inside `firebase: { ... }` with yours. Save.
   (These values are meant to be public. They're safe in GitHub.)

## 3. Turn on sign-in
1. Left menu → **Build → Authentication** → **Get started**.
2. **Sign-in method** tab → **Anonymous** → Enable → Save. (Players get an invisible login, so their phone remembers their pick.)
3. **Add new provider** → **Google** → Enable → choose your email as support email → Save. (Only for your organiser view.)

## 4. Create the database and lock it down
1. Left menu → **Build → Firestore Database** → **Create database**.
2. Location: **asia-south1 (Mumbai)** → Next → **Start in production mode** → Create.
3. Open the **Rules** tab. Delete everything there and paste in the whole of **firestore.rules**.
4. In what you pasted, change `YOUR-EMAIL@gmail.com` to your own Google email (the one you'll sign in with). **Publish**.

## 5. Put it on GitHub Pages
1. On GitHub: **New repository** → name `offside-signup` → **Public** → Create.
2. **Add file → Upload files** → drag in `index.html`, `config.js`, `firebase.js` → **Commit changes**.
3. Repo **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
4. After a minute your link is `https://YOUR-GITHUB-NAME.github.io/offside-signup/`. That's the one to share.

## 6. Allow your organiser sign-in on that address
Firebase → **Authentication → Settings → Authorized domains → Add domain** → `YOUR-GITHUB-NAME.github.io` → Add.

## 7. Your organiser view
Open `https://YOUR-GITHUB-NAME.github.io/offside-signup/?admin` → **Sign in with Google**.
You see every name with their club, plus **Copy list**, **Download CSV** and **Remove** (frees their place and club).

---

## Before you share it
Open the link on two phones. Pick a club on one, then search for it on the other: it should say *Already taken*.
If the page shows a red message, it tells you which step above to check.

## Good to know
- A player's pick is tied to the phone and browser they used. To change club or drop out, they open the same link on the same phone.
- Clubs that are taken are left out of the browse list. Searching for one shows *Already taken*, without saying who has it.
- Opening `index.html` before step 2 runs a preview that saves on that computer only.
- AC Milan, Inter, Atalanta, Lazio and Monza appear in the game under made-up names (Milano FC, Lombardia FC, Bergamo Calcio, Latium, Brianza Calcio), and Boulogne as Beauleroix FC. The list shows both names.
- Want more than 12 places? Change `maxPlayers` in config.js and upload it again.
