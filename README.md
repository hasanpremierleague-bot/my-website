# Midterm Mastery (IT7101)

A study site with 330 practice questions from Lectures 1 to 5.1. It is one self-contained page: `index.html` holds the site and the full question bank. It needs no server code, database or API key. `questions.json` is a copy of the bank for reference; the site does not need it.

## Put it online with GitHub Pages (free)

1. Sign in at github.com and click **New repository**. Name it, for example, `midterm-mastery`, and make it **Public** (Pages on a free account needs a public repo).
2. On the new repo page, click **uploading an existing file**. Drag in every file from this folder (`index.html`, `questions.json`, `README.md`, `.nojekyll`) and click **Commit changes**.
3. Go to **Settings → Pages**. Under *Build and deployment*, set Source to **Deploy from a branch**, Branch to **main** and folder to **/ (root)**, then **Save**.
4. Wait a minute or two, then refresh that page. It shows your link, like `https://YOUR-NAME.github.io/midterm-mastery/`. Open it on your phone, and use **Add to Home Screen** to get an app icon.

Any static host works the same way: Netlify Drop (drag the folder onto app.netlify.com/drop), Cloudflare Pages, or Vercel.

## How progress is saved

- Every answer, flag and unfinished exam is saved automatically in the browser you use, so it survives closing the tab, reloading or restarting the phone.
- Progress is per browser and per device: the phone and the laptop each keep their own.
- To move progress, or keep a safe copy, use **Back up or move progress** at the bottom of the dashboard. **Download backup** saves a small `.json` file, and **Load backup** on another device restores it.
- Progress is lost if you clear the browser's site data, or use a private / incognito tab. On iPhone, Safari may clear a site's data if you don't open it for about 7 days; adding the site to the Home Screen and taking a backup now and then avoids losing it.

## Updating questions

Edit the bank with the build scripts in the project's `midterm/source/` folder, rebuild `index.html` as described in `midterm/README.md`, and upload the new `index.html` to the repo. Saved progress is kept, because it is keyed by question id.
