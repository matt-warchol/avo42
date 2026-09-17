# Deploying avo42.com to GitHub Pages

This folder is ready to push as-is: `index.html` is the site, `CNAME`
tells GitHub Pages the custom domain.

## 1. Create the repo and push

```bash
cd avo42-site
git init
git add .
git commit -m "avo42 landing page"

# create the repo on GitHub (pick ONE):
gh repo create avo42-site --public --source=. --remote=origin --push
# — or, without the GitHub CLI —
git remote add origin https://github.com/<your-username>/avo42-site.git
git branch -M main
git push -u origin main
```

## 2. Turn on GitHub Pages

In the repo on github.com: **Settings → Pages**
- Source: `Deploy from a branch`
- Branch: `main`, folder `/ (root)` → Save

## 3. Point avo42.com at it (DNS)

At your domain registrar, on **avo42.com**, add:

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | `<your-username>.github.io` |

(Optional, IPv6: AAAA @ → `2606:50c0:8000::153`, `2606:50c0:8001::153`,
`2606:50c0:8002::153`, `2606:50c0:8003::153`)

DNS can take a few minutes to a few hours to propagate.

## 4. SSL certificate

Nothing to install — once GitHub sees `avo42.com` resolving to it (step 3),
it automatically issues and renews a free SSL certificate (Let's Encrypt).
Back in **Settings → Pages**, once the domain shows a green checkmark,
tick **Enforce HTTPS**. That's the whole SSL step.

## Contact form

The form on the page uses `mailto:m@avo42.com` — it opens the visitor's
own email app, addressed to you. No server or form service needed, but it
does mean m@avo42.com needs to exist as a real inbox for replies to land
somewhere. If you'd rather have submissions post silently in the
background, that needs a small form backend (e.g. Formspree) — say the
word and I'll wire it in.
