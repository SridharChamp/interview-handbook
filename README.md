# Interview handbooks — static site

Drop-in folder for any static host. No build step, no dependencies, no server
code. Every page is a single self-contained HTML file with the CSS, JavaScript
and diagrams inlined — there is not one external request in either file, so it
also works offline once loaded.

```
index.html      Full Stack SDE Interview Handbook   (1.8 MB)
sql/index.html  SQL & Excel Interview Handbook      (1.5 MB)
.nojekyll       tells GitHub Pages to serve the files as-is
```

Once deployed:

- `https://<you>.github.io/<repo>/` → the SDE handbook
- `https://<you>.github.io/<repo>/sql/` → the SQL & Excel handbook

---

## Read this first: your progress will not follow the move

Your day progress, card schedule and solved problems are stored by the
**browser, per web address**. A file opened from `C:\Users\...` and the same
file served from `github.io` are two different addresses, so the hosted copy
starts empty. Nothing is lost — it is still under the old address — but you
have to carry it across once:

1. Open your current local copy.
2. **Today's Session → Your data → Show backup**. Copy the whole block of text.
3. Open the new hosted URL.
4. **Your data → Restore from backup**, paste, confirm.

Do this once, on the day you switch, and then use only the hosted URL. The same
applies if you ever move hosts again.

---

## Option 1 — GitHub Pages (no git required)

1. Create a new repository on GitHub. **Public** (see the note below).
2. On the repo page: **Add file → Upload files**. Drag in `index.html`,
   `.nojekyll`, and the `sql` folder. Commit.
3. **Settings → Pages**. Under *Build and deployment*, set
   Source = **Deploy from a branch**, Branch = **main**, Folder = **/ (root)**.
   Save.
4. Wait a minute or two. The URL appears at the top of that same Pages screen.

With git instead:

```bash
git init -b main
git add .
git commit -m "Interview handbooks"
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
# then do step 3 above
```

**On privacy:** GitHub Pages from a free account requires a public repository,
so anyone with the URL can read the handbook. The content is yours and there is
nothing sensitive in it, and your progress never leaves your browser — it is
never committed to the repo. But the page is public. If you would rather it
were not, use option 3.

---

## Option 2 — Netlify Drop (fastest, about 30 seconds)

1. Go to <https://app.netlify.com/drop>.
2. Drag this whole folder onto the page.
3. You get a live URL immediately. Sign in to keep it and rename it.

No repo, no settings. Good if you just want it reachable today. To update later,
drag the folder again onto the same site.

---

## Option 3 — Cloudflare Pages (free, and can be kept private)

1. <https://dash.cloudflare.com> → **Workers & Pages → Create → Pages →
   Upload assets**. Upload the folder.
2. To make it private: **Zero Trust → Access → Applications → Add an
   application → Self-hosted**, point it at your Pages URL, and add a policy
   allowing only your own email. You then get a one-time code by email to open
   it.

This is the only one of the three that is both free and genuinely private.

---

## Updating later

Every page is one file. To publish a new version, replace `index.html` (or
`sql/index.html`) and redeploy. Nothing else changes, and your saved progress is
untouched because the address stays the same.

## Custom domain

All three hosts accept one. In each case you add a CNAME record at your DNS
provider pointing at the host, and enter the domain in the host's settings.
Note that moving to a custom domain changes the address, so carry your progress
across with Show backup / Restore from backup as above.

## Troubleshooting

**Page is blank or 404 right after deploying** — give it two or three minutes;
the first build is the slow one. Then force-reload with Ctrl+F5.

**A banner says progress is not being saved** — the browser is blocking storage
for the site. Check that you are not in a private window, and that cookies and
site data are allowed for the domain.

**It looks unstyled** — on GitHub Pages this means Jekyll processed the files.
Confirm `.nojekyll` is in the repository root. Uploading through the web UI can
silently drop dotfiles; if so, use **Add file → Create new file**, name it
`.nojekyll`, leave it empty, and commit.
