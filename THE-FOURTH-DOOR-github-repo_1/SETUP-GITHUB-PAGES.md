# Putting this on thefourthdoor.co.uk with GitHub Pages

Everything in this folder is ready to go into a repo. Nothing needs building.

---

## Step 1 — the repo

Create a repository on GitHub, public, and put **the contents of this folder** at its root. Not the folder itself, its contents. `index.html` must sit at the top level of the repo.

Two files are already included that GitHub Pages needs:

**`CNAME`** contains `thefourthdoor.co.uk`. This tells GitHub Pages which domain to serve. Do not delete it — GitHub rewrites it when you set the domain in the interface, so leaving it in place saves a step.

**`.nojekyll`** stops GitHub from running the files through Jekyll, which would otherwise ignore anything in folders beginning with an underscore.

## Step 2 — turn Pages on

In the repo: **Settings → Pages**.

Source: **Deploy from a branch**. Branch: **main**, folder: **/ (root)**. Save.

Under **Custom domain**, enter `thefourthdoor.co.uk` and save.

**Do this before touching DNS.** GitHub's own guidance is explicit about the order: if you point DNS at GitHub before claiming the domain in your repo, somebody else can potentially host a site on your address.

## Step 3 — DNS at GoDaddy

In GoDaddy: **My Products → the domain → DNS → Manage Zones**.

**Delete** any A record or CNAME that GoDaddy created automatically for `@` or `www`. GoDaddy usually adds a parking record and it will fight yours.

Then add **five records**:

| Type | Name | Value | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | default |
| A | @ | 185.199.109.153 | default |
| A | @ | 185.199.110.153 | default |
| A | @ | 185.199.111.153 | default |
| CNAME | www | *yourusername*.github.io | default |

Replace *yourusername* with your GitHub username, and keep the `.github.io` on the end. No repo name, no trailing path.

Optionally, for IPv6, four AAAA records on `@`:

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

GitHub recommends keeping the A records even if you add these.

## Step 4 — HTTPS

Back in **Settings → Pages**, wait for the domain check to go green, then tick **Enforce HTTPS**. The certificate is issued automatically and is free.

DNS can take anywhere from a few minutes to 24 hours to propagate. If Enforce HTTPS is greyed out, the check has not passed yet. Give it time before assuming something is wrong.

---

## One piece of tidying up

I added `thefourthdoor.co.uk` to the Netlify project before you told me you wanted GitHub. It is harmless, because DNS decides where traffic actually goes, but it is untidy and Netlify will keep reporting a failed verification.

To remove it: `app.netlify.com/projects/moonlit-khapse-f9cbbe/domain-management`, click **Options** next to `thefourthdoor.co.uk`, then **Remove domain**.

liasi.io is untouched and still points at Netlify, as you asked.

---

## Still outstanding before this is a real site

1. **Form endpoint** on both forms. Until set, they refuse to send and nothing is captured.
2. **Real company details** in the footer, currently test data.
3. **Real telephone number.** `020 7946 0100` is an Ofcom drama-range placeholder.
4. **Privacy notice** at `/privacy`.
5. **Remove `noindex`.** It is still in the file, marked `PREVIEW ONLY`. Google will not list the site until it goes. **This one matters most now you are on the real domain.**
6. **Remove the "Read it now, no email" button**, also marked `PREVIEW ONLY`.
7. **Pete has not reviewed** his bio, role label or photograph.
8. **Reconcile the numbers** between tenfoldpartners.co.uk and this site: 50+ against 65+ acquisitions, 200+ against "hundreds" of leaders coached.
