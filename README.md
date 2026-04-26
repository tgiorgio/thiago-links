# thiago-links

Personal links page for [@thiago_digi](https://instagram.com/thiago_digi) — free AI tools, prompts, and resources.

Live at: `https://links.cyber353.ai` *(once deployed)*

## Files

| File | What it does | When to edit |
|---|---|---|
| `index.html` | The home page layout and styling | Rarely — only for design changes |
| `links.json` | All content for the home page | Every time you add/remove a link |
| `prompts.html` | The prompt library page layout | Rarely — only for design changes |
| `prompts.json` | All prompts (title, body, category, tags) | Every time you add/remove a prompt |
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

## Prompt library (`prompts.json`)

The prompt library page lives at `/prompts.html` and reads its content from `prompts.json`. Same workflow as `links.json`: edit on GitHub, commit, Cloudflare redeploys.

### Add a prompt

Add an object to the `prompts` array:

```json
{
  "id": "unique-slug",
  "icon": "✍️",
  "title": "Short, action-style title",
  "category": "instagram",
  "description": "1–2 line explanation of what this prompt does and when to use it.",
  "tags": ["caption", "hook"],
  "prompt": "The full prompt text.\n\nUse \\n for line breaks.\nReplace fields with [BRACKETS] so users know what to swap."
}
```

- `id` — any unique slug (used internally; lowercase + dashes)
- `category` — must match an `id` in the `categories` array
- `tags` — optional, shown as `#tag` chips
- `prompt` — the meat. Use `\n` for line breaks; use `[BRACKETS]` for placeholders the reader should replace
- `post` *(optional)* — link back to the Instagram post where you shared this prompt. Date is ISO format (`YYYY-MM-DD`); shows as a small clickable badge on the card:

```json
"post": {
  "url": "https://instagram.com/p/SHORTCODE",
  "date": "2026-04-25",
  "label": "From this post"
}
```

### Share a direct link to one prompt

Every prompt is reachable via `#id`, e.g. `https://links.cyber353.ai/prompts.html#ig-caption-hook`. Drop that URL in your post caption / bio and visitors land directly on the prompt (it auto-scrolls and pulses to confirm). The 🔗 icon on each card copies that URL.

### Add a category

Add an object to the `categories` array:

```json
{ "id": "marketing", "label": "Marketing", "icon": "📣" }
```

Then use that `id` in the `category` field of any prompt. Empty categories (no prompts assigned) are hidden automatically from the filter pills.

### Edit the page title / tagline

Edit the `profile` block at the top of `prompts.json`. HTML allowed in `tagline` and `howto`.

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
