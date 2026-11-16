# Shimmy for friends: guide for Claude

Shimmy is a tiny shared tracker, a social network for a small group of friends (up to four). Low pressure is the whole point: showing up counts, goals are shared, and nobody is ranked. The person you're helping wants their own copy for their own group.

## What's in the repo

- `index.html` is the whole app (markup, styles and script in one file).
- There are no image files. Friends without a photo get a pastel initial, and the kitten on the shimmy meter is an inline SVG.

## Making someone's own copy

1. Ask for the friends' names if you don't have them, then set `FRIENDS` near the top of the script (up to four, in order). Photos are optional: put square images next to `index.html` (for example `img/mira.jpg`), set `img:'img/mira.jpg'`, and publish them alongside the page.
2. Syntax-check the script: pull out everything inside the `<script>` tags into a scratch `.js` file and run `node --check` on it.
3. Publish `index.html` as a **new** artifact. Read how this session declares runtime capabilities first, then declare `user` and `db` with these 19 rules:
   - For each of `claims`, `logs`, `posts`, `photos`, `recipes`, `reacts`, `comments`, `cups`, `ideas`:
     - `{ path: "<name>", read: "view", write: "owner" }`
     - `{ path: "<name>/{self}", write: "interact" }`
   - `{ path: "rewards", read: "view", write: "interact" }`
4. Tell them to share the page with their friends as **Editors**. People who can only view can look around but can't post.

Each friend can write only her own documents (the `{self}` subtree). Rewards are shared and anyone can edit them.

## Data model

| Document | Shape | What it holds |
| --- | --- | --- |
| `claims/<uid>` | `{name, at}` | which friend this Claude user is |
| `logs/<uid>` | `{days:{"YYYY-MM-DD": text}}` | Shimmy: what she did to move that day |
| `rewards/<weekKey>` | `{r:[3 strings]}` | rewards for the three meter milestones |
| `posts/<uid>` | `{items:{pid:{date, cap, at, meal, ing?, hr?}}}` | Did you eat? posts (meal is breakfast, lunch, dinner or snack; `ing` is the ingredient list; `hr` means a recipe exists) |
| `photos/<uid>/p/<pid>` | `{d: dataURL}` | the meal photo, compressed in the browser to under 170 KB |
| `recipes/<uid>/r/<pid>` | `{steps}` | recipe steps for a post |
| `reacts/<uid>` | `{r:{"uid:pid":[emoji]}}` | her reactions on any post |
| `comments/<uid>` | `{c:{cid:{p, t, at}}}` | her comments (`p` is the post key) |
| `cups/<uid>` | `{days:{"YYYY-MM-DD": text}}` | Fill your cup: what filled her cup that day |
| `ideas/<uid>` | `{items:{id:{t, at}}}` | her ideas in the shared "Need an idea?" list |

Photos are stored as data URLs in documents on purpose, so the page doesn't need a separate file store.

## How the page is organised

Sections in the script are marked with `/* ---------- name ---------- */` comments:

- **your friends**: the `FRIENDS` list and the initial avatars.
- **who are you**: `drawWelcome` and `renderBanner`. The first screen says "Who are you?" and shows the friends with names underneath. Set `ALWAYS_WELCOME = true` to open on this screen on every visit.
- **grid**, **calendar**, **meter scaffolding**: the Shimmy tab, with the weekly jiggle grid, week picker and shimmy meter (milestones at 10 and 18, finish at 28; one jiggle point per logged day).
- **winner winner chicken dinner**: the Did you eat? tab (the old name stuck in the comment). It's a shared photo grid with date-range, person and meal filters, multi-photo posting, reactions, comments and captions.
- **recipes and "what can I make?"**: Get recipe opens in a stacked sheet (`#sheet2`). The pantry finder (`openFinder`) is built but switched off.
- **fill your cup**: a 7 × 4 weekly grid of mini cups, the fill sheet and the shared ideas list.
- **connect to the shared store**: subscribes to every collection with `onSnapshot`.

## Design rules

- Cute, pastel, light and breezy. **No black anywhere.** Keep it minimal, with few lines and little text.
- Fonts: Pacifico for display, Quicksand for body.
- Colors are tokens on `:root`. Pink and wine set the page (`--pink`, `--rose`, `--wine`, `--milk`, `--cream`). Each friend has three shades: `--f1-*` sky, `--f2-*` cream, `--f3-*` lilac, `--f4-*` salmon.
- If the group wants different tabs, keep the same feel: one small thing a day, shared progress, no rankings.
