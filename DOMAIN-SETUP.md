# Setting Up a Custom Domain for Your Marketing Site

Your marketing site is a standalone HTML file (`index.html`) that can be hosted anywhere. Below are your main options for putting it on its own domain.

---

## Option A: Host on Vercel (Recommended — matches your app)

Since your app is already on Vercel, this is the simplest path.

1. **Create a new Vercel project** for the marketing site:
   - Push the `marketing-site/` folder to a new GitHub repo (or a subfolder of your existing repo).
   - In the Vercel dashboard, click **Add New → Project** and import the repo.
   - Set the **Root Directory** to the folder containing `index.html`.
   - Framework Preset: **Other** (it's plain HTML, no build step needed).

2. **Add your custom domain** in the Vercel project settings:
   - Go to **Settings → Domains** and type in your domain (e.g., `mylittlelibrary.com` or `www.mylittlelibrary.com`).
   - Vercel will give you DNS records to add.

3. **Update DNS at your domain registrar** (Namecheap, Google Domains, Cloudflare, etc.):
   - For an **apex domain** (e.g., `mylittlelibrary.com`):
     - Add an **A record** pointing to `76.76.21.21`
   - For a **subdomain** (e.g., `www.mylittlelibrary.com`):
     - Add a **CNAME record** pointing to `cname.vercel-dns.com`
   - DNS propagation typically takes 5–30 minutes, but can take up to 48 hours.

4. **SSL is automatic** — Vercel provisions a free certificate once DNS is verified.

---

## Option B: Use a Subdomain of Your Existing Domain

If you want the marketing site at something like `about.mylittlelibrary.net` while keeping the app at `mylittlelibrary.net`:

1. Deploy the marketing site as a separate Vercel project (same steps as above).
2. In the marketing site's Vercel project, add the domain `about.mylittlelibrary.net`.
3. At your DNS provider, add a **CNAME record**:
   - Name: `about`
   - Value: `cname.vercel-dns.com`

---

## Option C: Host as a Landing Page Route in Your Next.js App

If you'd rather keep everything in one codebase and one deployment:

1. Create a file at `src/app/(public)/page.tsx` in your Next.js app.
2. Use a server component that renders the marketing HTML (or convert it to a React component).
3. Update your middleware (`src/app/middleware.ts`) to allow unauthenticated access to the root `/` route.
4. Redirect authenticated users from `/` to `/dashboard` (or wherever the main app lives).
5. No new domain needed — it lives at `mylittlelibrary.net/`.

---

## Where to Buy a Domain

If you don't already own a separate domain for the marketing site:

- **Cloudflare Registrar** — at-cost pricing, great DNS management
- **Namecheap** — affordable, good UI
- **Google Domains** (now Squarespace Domains) — simple integration with Google services
- **Porkbun** — low prices, clean interface

Expect to pay roughly $10–15/year for a `.com` domain.

---

## Checklist

- [ ] Choose a hosting option (A, B, or C)
- [ ] Purchase/configure domain if needed
- [ ] Deploy the marketing site
- [ ] Add DNS records and verify in Vercel
- [ ] Confirm SSL certificate is active
- [ ] Update the "Open App" links in `index.html` if your app URL differs
- [ ] Test on mobile and desktop
