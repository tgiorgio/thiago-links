# thiago-links

Personal links page for [@thiago_digi](https://instagram.com/thiago_digi) — free AI tools, prompts, and resources.

Live at: `https://links.cyber353.ai` *(once deployed)*

## Files

| File | What it does | When to edit |
|---|---|---|
| `index.html` | The page layout and styling | Rarely — only for design changes |
| `links.json` | All content (links, titles, sections) | Every time you add/remove a link |
| `avatar.jpg` | Your profile photo | When you change the photo |

## How to edit

1. Open `links.json` on GitHub (click the file, then the pencil icon)
2. Edit the JSON
3. Commit the change
4. Cloudflare Pages redeploys automatically within ~30 seconds

### Add a link

Inside the relevant section's `links` array, add an object:

```json
{
  "icon": "🎯",
  "title": "Name shown on the button",
  "sub": "Small gray text underneath (optional)",
  "url": "https://example.com",
  "featured": true
}
```

`featured: true` gives it the highlighted green-tinted style. Use sparingly — 1–2 per page max.

### Reorder links

Cut and paste objects within the array to reorder them. Top links get the most clicks.

### Add a new section

Add a new object to the `sections` array:

```json
{
  "title": "My New Section",
  "links": [ ... ]
}
```

### Change the tagline, name, or avatar

Edit the `profile` block at the top of `links.json`. HTML is allowed inside `tagline` (e.g., `<br />`, `<strong>`).

## Deployment (Cloudflare Pages)

1. Push this repo to GitHub
2. Cloudflare Dashboard → Pages → Create a project → Connect to Git
3. Pick this repo, leave all build settings empty (no framework, no build command)
4. Deploy
5. Custom domain → add `links.cyber353.ai`

Any commit to `main` triggers an auto-redeploy.

## Local testing

You can't just double-click `index.html` — browsers block `fetch()` from `file://`. Run a tiny local server:

```bash
# Python
python3 -m http.server 8000

# Node
npx serve .
```

Then visit `http://localhost:8000`.
