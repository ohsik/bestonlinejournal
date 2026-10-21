# SEO article playbook

Read this before writing or publishing any article in this repository.
Everything here is a constraint that was hit for real, not a style preference.

## Hard constraints

**Never state Goodnight Journal's pricing, launch year, or headquarters.**
The copy that was here before claimed "annual $39.99 / monthly $4.99" and
"built in California and launched in 2013". Public sources point to Chicago and
list the developer as Allspectives LLC, so the old text was probably simply
wrong. Describe what the product does — private-by-default entries, the
optional community, cross-device consistency — none of which goes stale.
The same applies to competitors: no prices. The previous copy listed Penzu at
"$49.99 and $19.99" in one paragraph and "Free, $9.99 monthly, or $49.99
Annual" two lines later.

**Never use a future date in front matter.** Jekyll's default `future: false`
drops a future-dated document from the build **with no warning**. Three pages
vanished this way. Use `00:00:00+00:00` on the publish date, never `12:00`.
Netlify builds in UTC.

**Never rename an existing file to change its title.** URLs here come from the
filename, not the front-matter `title`. Retitle freely; renaming throws away
the page's rankings and backlinks, and there is no redirect plugin installed.

**Headings start at `##`.** The `post` layout renders `page.title` as the
`h1`, so an in-content `# ` produces a second one.

**Never reference an image that does not exist.** It ships a broken image.
Either reuse something already in `images/`, or omit the image and say so in
the pull request.

**Always include the ownership disclosure** on any page that recommends or
reviews Goodnight Journal:

```html
<p class="disclosure"><strong>Disclosure:</strong> we make Goodnight Journal,
one of the apps recommended below. We have tried to be fair and specific about
what every app here does well, but you should weigh our recommendation knowing
that.</p>
```

The site-wide footer disclosure covers passing mentions; roundups and
comparisons need the inline one too.

**Health-adjacent topics carry a care note.** Anything touching anxiety,
depression, grief or sleep must say plainly that journaling is not a substitute
for professional care and that persistent or worsening symptoms warrant a
doctor or therapist.

## Writing standard

The content this site shipped for years was machine-spun and it is the reason
nothing ranked. Real examples that were removed: "albeit you think that it's
silly", "connected with other journal writers everywhere the planet", "you get
to proportion your memories", "even half a song of your events", and a stray
"View Original" fragment left mid-article.

Write plainly, in specifics, the way a knowledgeable person talks. 700–1000
words. Name the cases where a competitor is the better choice — a comparison
that only flatters the house product converts worse and reads as promotional.

Cross-link two or three genuinely related existing pages. Check they resolve.

## Front matter and filename for `_posts`

```yaml
---
layout: post
title: Sentence case title with a hyphen - not a colon
---
```

The **filename** sets the URL: `YYYY-MM-DD-slug.md` publishes at `/slug/`, with
the date prefix stripped. The date prefix can therefore be changed freely
without affecting the URL, but it must not be in the future. Posts appear on
the index automatically.

This site mixes Markdown and raw HTML inside posts (`<h2 id="...">`, `<p>`,
`<a class="btn-cta">`). Match the surrounding convention rather than converting
a post wholesale to one form or the other. Images live in `images/post/`.

## Before opening the pull request

1. `jekyll build` — must pass with no errors. This repo has no Gemfile; the
   plugins it needs are `jekyll-seo-tag`, `jekyll-sitemap` and `jekyll-feed`,
   which GitHub Pages supplies but a local build does not. SCSS deprecation
   warnings are pre-existing and expected.
2. Confirm the new post actually built: `ls _site/<slug>/index.html`.
   If it is missing, the date is in the future.
3. Confirm exactly one `<h1>` on the new page.
4. Confirm every internal link resolves against `_site`.
5. Diff the full generated URL list against `master` and confirm **additions
   only**. No existing URL may change.
6. Tick the item in `SEO-BACKLOG.md` in the same commit.

Open a pull request. Do not merge it.
