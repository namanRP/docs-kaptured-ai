# Kaptured AI Help Center

Customer help center for the Kaptured AI app ([outfit-maker-lab](../outfit-maker-lab)), built with [Mintlify](https://mintlify.com). It follows the same layout as the CapitalxAI Outreach help center: collections, then sub-collections, then articles. Troubleshooting and FAQ entries sit next to the how-tos, and each article ends with **Related articles**.

It covers only what customers can reach: AI Photo Studio, Library, Products Management, Style Customers, Shop Settings, API Keys, Billing & Plans, Account Security and the Claude connector. Internal staff tools (video editor, `/tools`, admin pages, generation workflows, cloud bulk jobs) are left out on purpose.

See [INDEX.md](INDEX.md) for the full article map.

## Run locally

```bash
npm install
npm run dev          # http://localhost:3000
```

Requires Node 20.17+.

> `mint broken-links` reports false positives on Windows (path separators). Check links on macOS/Linux or in CI.

## Adding an article

1. Create an `.mdx` file in the right collection folder, for example `ai-photo-studio/my-article.mdx`.
2. Give it frontmatter with `title` (a full, question-style or how-to title), `sidebarTitle` (short) and `description`.
3. Follow the house format:
   - An intro paragraph saying what the article covers.
   - `##` sections. For troubleshooting, use numbered problems, each followed by a **✅ Solution:** line.
   - Optional `## Q: …` FAQ entries.
   - End with `## Related articles` and 2 to 4 links.
4. Add its path (without `.mdx`) to the right group in `docs.json` → `navigation`, and add a line to `INDEX.md`.

House rules: plain language, exact UI labels in **bold**, no em dashes, and never name the AI vendors behind the engines (say v1 / v2 / v3, Standard / Pro, Fast / Lite / Quality).

## Where facts come from

All labels, limits and defaults come from the app's source code. When the app changes, update the affected articles.

| Question | Where the answer lives (outfit-maker-lab) |
|---|---|
| Studio steps, options, error messages | `src/components/dashboard/GenerationOptions.tsx`, `src/components/dashboard/generationOptions/` |
| Viewer, edit presets, downloads | `src/components/dashboard/GeneratedImagesDisplay.tsx`, `src/lib/editPresets.ts`, `src/components/gallery/` |
| Crop sizes for marketplaces | `src/components/dashboard/CropModal.tsx` (`PLATFORM_SIZES`) |
| Credit costs | `src/utils/usageRules.ts` (defaults; per-account overrides in `user_credits.usage_rules`) |
| Plans, top-ups, billing copy | `src/pages/Billing.tsx`, `supabase/functions/fashion-stripe-*` |
| Product fields and limits | `src/features/items/`, `src/lib/imageCategories.ts` |
| Library and 30-day expiry | `src/pages/Library.tsx`, `src/lib/generationsGalleryApi.ts` |
| Claude connector tools | `supabase/functions/fashion-mcp/index.ts` (edgeFunctions repo) |

Marketing copy for plans and features: `outfit-website/src/pages/product.astro` and `_pricing.astro.disabled`.

## Deploy

Push this folder to a GitHub repo and connect it in the [Mintlify dashboard](https://dashboard.mintlify.com). Every push to the default branch redeploys.
