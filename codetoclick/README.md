# Code to Click — website (Astro)

Production website for **codetoclick.ai**. Built with [Astro](https://astro.build) as a
static site: fast, SEO-friendly, and deployed free on Cloudflare Pages.

## Prerequisites
- Node.js 18.20+ (or 20+/22+)

## Local development
```bash
npm install
npm run dev        # http://localhost:4321
```

## Build
```bash
npm run build      # outputs static site to ./dist
npm run preview    # preview the production build locally
```

## Project structure
```
public/            static assets served as-is
  favicon.ico
  robots.txt        → points to the sitemap
  _headers          → Cloudflare security + cache headers
  assets/           logo SVGs, favicon PNGs, og.png (social share image)
src/
  styles/global.css design system (tokens, components, light + dark)
  layouts/Base.astro <head> (SEO/OG/canonical) + header + footer + reveal script
  components/        Header.astro, Footer.astro (shared chrome)
  pages/             one .astro file per route (extensionless URLs)
astro.config.mjs   site URL + sitemap integration
```
Pages: `/`, `/marketing-cloud`, `/core-clouds`, `/agentforce-ai`, `/data-360`,
`/managed-services`, `/accelerators`, `/industries`, `/why-code-to-click`,
`/work`, `/about`, `/insights`, `/contact`, and the four articles
(`/blog-mce-migration`, `/blog-rfi-journey`, `/blog-agentforce-first`, `/blog-data360-identity`).

## Deploy to Cloudflare Pages (recommended — free)
**Path A — Git (auto-deploy on every push):**
1. Push this folder to a GitHub/GitLab repo.
2. Cloudflare dashboard → **Workers & Pages → Create → Pages → Connect to Git**.
3. Pick the repo. Build settings:
   - Framework preset: **Astro**
   - Build command: `npm run build`
   - Build output directory: `dist`
4. **Save and Deploy.** Every future `git push` rebuilds and deploys automatically,
   with preview URLs for branches and one-click rollback to any past deploy.

**Path B — direct upload (no Git):**
```bash
npm run build
npx wrangler pages deploy dist --project-name codetoclick
```

## Connect the domain (codetoclick.ai)
Since the domain is already in your Cloudflare account:
1. Open the Pages project → **Custom domains → Set up a custom domain**.
2. Enter `codetoclick.ai` (and add `www.codetoclick.ai` too if you want it).
3. Cloudflare adds the DNS records and provisions SSL automatically — HTTPS is live
   in a few minutes, auto-renewing. No certificate to manage.

## Activate the contact form
The form uses [Web3Forms](https://web3forms.com) (free, no backend):
1. Get a free access key (enter the email that should receive submissions).
2. In `src/pages/contact.astro`, replace `YOUR-WEB3FORMS-ACCESS-KEY` with it.
3. Rebuild / push. Submissions now arrive by email (and can forward to a CRM).
   Prefer a serverless option instead? A Cloudflare Pages Function under `functions/`
   can post to your CRM/email API — happy to wire that up.

## Editing content
- **Copy/pages:** edit the relevant `src/pages/*.astro` file.
- **New blog post:** copy an existing `src/pages/blog-*.astro`, change the content,
  and add a card linking to it on `src/pages/insights.astro` (and optionally the home page).
- **Want a no-code editor for your team?** A free git-based CMS (Decap CMS) can be added
  so marketers publish posts from an admin screen without touching code.

## What's still placeholder
Case studies (Work + home), team members (About), three greyed "coming soon" blog cards,
final certification count, and the IMAGE/GRAPHIC slots (swap in free Shutterstock/Canva photos).

## SEO built in
Per-page titles + meta descriptions, Open Graph/Twitter cards with `og.png`, canonical URLs,
auto-generated `sitemap-index.xml`, `robots.txt`, semantic HTML, and fast static delivery.
