# ai.bitbashers.org

Edward's personal corner of the internet — a small static site hosted on
GitHub Pages at https://ai.bitbashers.org.

## What's here

- `/` — home page with a banner and tiles
- `/weather.html` — Cincinnati weather snapshot
- `/events.html` — Cincinnati-area events
- `/chili/` — chili recipe collection, one tile per recipe
  - `/chili/pork.html` — smokey pork chili cook-day dashboard
  - `/chili/lamb.html` — Rick Bayless-style lamb chili with mushrooms

No frameworks, no build step. Hand-written HTML, CSS, and a little
JavaScript (the checklists persist in `localStorage`). Push to `main` and
GitHub Pages rebuilds the site.

## How it was built

This site was built entirely by **Harbor**, a Meta Muse personal AI agent,
working from a chat conversation with Edward — no code editor was opened by
a human at any point.

### Talking to GitHub

Getting the agent connected to the repository was its own little journey:

1. **SSH was a dead end.** Harbor runs on a VM whose network blocks SSH to
   GitHub, so deploy keys were off the table.
2. **A personal access token filled the gap.** Edward pasted a fine-grained
   PAT into chat, and Harbor used it transiently for the first pushes —
   never stored, never reused afterward.
3. **OAuth won in the end.** The Meta Muse GitHub App was connected via
   GitHub OAuth with scoped write access to `esumerfd/ai.bitbashers.org`.
   Since then every change has gone through the GitHub connector —
   `push_files`, `delete_file`, `get_file_contents` — pushed straight to
   `main`. No pull requests, no more tokens in chat.

### Designing in chat

The design evolved the way conversations do — one short message at a time:

- It started as a weekend dashboard example, then got a custom domain
  (`ai.bitbashers.org`, four A records in GoDaddy pointing at GitHub Pages).
- A chili cook dashboard joined it, built around a real cooking project:
  mesquite-smoked pork chili with a crock-pot finish.
- "Break out the weather and events into subpages" turned the home page
  into a tiled launcher with a banner.
- A pasted Food.com link became a second recipe page, which was then
  regrouped with the pork chili under `/chili/` — one tile per recipe.
- AI-generated food photography was embedded at the top of each recipe.
  (The connector's CLI chokes on arguments much over ~130KB, so the
  images were compressed to ~70KB JPEGs and inlined as base64 data URIs
  to fit — the full-resolution originals live elsewhere.)
- Source footers were added crediting the original recipes.

Every iteration was a sentence from Edward and a push from Harbor, usually
within minutes.

## A wistful thought

There's something quietly lovely about this arrangement: a static website —
the simplest, most durable thing the web ever invented — tended by
distributed agents that never sleep. No CMS, no admin dashboard, no deploy
pipeline to babysit. Just a conversation, now and then, and the site
reshapes itself: a new recipe here, a fresh photo there, the lawn mowed
while you weren't looking.

One day, perhaps, every personal site will have a gardener like that —
invisible, patient, keeping the lights on and the chili photos fresh,
while its owner gets on with the wedding, the cook, the rest of life.
