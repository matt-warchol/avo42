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

## 5. If a carrier (e.g. T-Mobile Poland) flags the site as dangerous

`index.html` now ships a meta description, Open Graph tags, a robots.txt
and sitemap.xml, and an Organization schema block — the trust signals a
one-page, form-only site is otherwise missing, which is what automated
phishing filters key off of. That reduces the odds of a fresh block, but
it can't retroactively clear one already in place; that block lives in
the carrier's own threat-intel system, not anywhere under your control.

T-Mobile Polska's filter (CyberTarcza / msec.t-mobile.pl) has no
self-service unblock form. To get avo42.com reviewed, email their CERT
directly (24/7 first-line):

- **cert@t-mobile.pl** — phone +48 602 900 000
- Say the domain is a legitimate new business site, ask for it to be
  reviewed and removed from the block list.

If it's also on CERT Polska's national warning list (many Polish carriers
pull from it), you can check/report at https://cert.pl/lista-ostrzezen/
or email cert@cert.pl; the formal appeal route if it's listed there is an
objection to the president of UKE under the Electronic Communications
Abuse Prevention Act — a heavier process, worth trying the T-Mobile
email first.
