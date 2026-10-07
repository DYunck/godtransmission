# Handoff: Cloud of Witnesses

Last updated: 7 October 2026 · Branch: `claude/biblical-theology-network-2p6dzf` · Last code commit: `3e61940`

**Read with:** `CLAUDE.md` (working rules for Claude sessions) and `SPEC.md` (who the app is for and what to build next, in priority order).

## What this app is

**Cloud of Witnesses** is a single web page with two interactive network maps, built for phones first so it can be shared with friends.

1. **Israel's God**: how Israel's God moved from person to person. It starts with Abraham (about 1800 BCE by tradition) and runs through Moses, the prophets, the exile, the Second Temple Jewish sects, Jesus, the apostles and the church fathers to the Council of Nicaea (325 CE).
2. **Scripture's journey**: how the Bible itself was copied, translated and argued over. It starts with the Temple scribes and early rabbis and runs through the Septuagint, the Masoretes, Jerome, the Reformation and the King James to modern translations such as the NIV, ESV, NRSV, JPS and CSB.

Time runs down the page. Each node is a person, community, writing, translation or council. Each line connects two nodes. A solid line means an idea or text was passed on. A dashed line means one side clashed with or reacted against the other. A dotted line means scholars propose the link but still debate it.

## Where it lives

| What | Where | Notes |
|---|---|---|
| Source of truth | `index.html` on branch `claude/biblical-theology-network-2p6dzf` | The whole app is this one file. |
| Public site | https://dyunck.github.io/godtransmission/ | GitHub Pages. The repo is public and Pages deploys from the **feature branch** above, not `main`. Every push to that branch redeploys in about a minute. All 6 deploys so far have succeeded. |
| Claude link | https://claude.ai/artifact/7fqfoh143WtH5vFdMfLup3 | A private copy. Only people the owner shares it with can open it, using the page's Share menu. It does **not** update automatically (see below). |
| `main` | Only holds the original one-line README | Nothing has been merged into `main`. |
| `origin/claude/hardware-wars-game` | A separate branch | Unrelated to this app. It was not reviewed for this handoff. |

## How it's built

There is no build step, no framework, no dependencies and no server. The only external resource is two Google Fonts (Marcellus and Alegreya Sans), with system-font fallbacks.

`index.html` is laid out top to bottom like this:

| Lines (approx.) | Section |
|---|---|
| 11–380 | CSS. A single deliberate dark "night sky" theme: lapis blue, gold and ivory. The phone layout turns the detail panel into a bottom sheet below 900px width. |
| 385–428 | Page markup: header, sticky filter bar (tabs, search, thread chips, verse chips) and footer. |
| 431–693 | **Israel's God data**: `IDEAS` (10 threads), `ERAS` (11), `NODES` (68), `EDGES` (149). |
| 695–965 | **Scripture data**: `S_THREADS` (9), `S_ERAS` (7), `S_NODES` (57), `S_EDGES` (117), `VERSES` (2 verses), `ALSO` (7 nodes paired across the two maps). |
| 967–993 | `MAPS`: the settings for each map, such as labels, intro text, legend names and starting nodes. |
| 995 onward | Engine: `build()` turns the arrays into a graph model; `layout()` arranges the time bands; `render()` draws the SVG; `applyState()` handles highlighting; `renderPanel()` fills the detail panel; then search and startup. |

**Data formats** (one line per entry, so adding content is a one-line edit):

```js
// node: [id, eraIndex, kind, name, date, summary, keyTexts, verses?]
//   kind: p person · g community · w writing/manuscript · t translation (scripture map) · e council/event
//   verses (scripture map only): { deut: [text, gloss], isa: [text, gloss] }  — wrap the word to watch in *asterisks*
// edge: [fromId, toId, "space separated thread ids", note, flag?]   flag: "c" clash, "d" debated
```

Node ids must be unique across **both** maps, because links in the page address (like `#kjv`) look up a node by id alone. If an edge points to a missing node or unknown thread, or two nodes share an id, the browser console shows a warning.

**Updating the Claude link** is a manual step. The Claude copy is `index.html` with the outer `<!doctype>`, `<html>`, `<head>`, `<body>` and the charset and viewport `<meta>` tags removed, because the Claude host adds its own. Every update in this project was published with that `sed` strip, then the result was republished to the same Claude URL. If you only push to GitHub, the Claude copy falls behind.

## What works (checked 7 Oct 2026)

A headless Chromium test at 360px width found no console errors or warnings, no horizontal scrolling, no nodes without links, no duplicate links and no links pointing backward in time. Both maps were also checked visually at phone (390px) and desktop (1300px) widths. The owner has viewed the live site on an iPhone.

- **Both maps** draw a layered timeline. Within each era band, nodes are placed near the nodes they connect to, which reduces line crossings. The layout redraws when the window width changes.
- **Tap a node** to open its detail panel. It shows the kind of node, its era, dates, a summary, key texts, the threads it carries, and two lists ("Received from / Passed on to" or "Drew on / Fed into") with a note on every link. Tapping a list item jumps to that node on the map.
- **Direct links / Whole lineage**: Whole lineage highlights everything upstream and downstream of the selected node, skipping clash lines.
- **Thread chips** (10 ideas or 9 scripture streams) highlight one thread across a whole map. They also work together with a selected node.
- **Follow a verse** (scripture map only) compares two verses:
  - Deuteronomy 6:4 (the Shema), in 20 versions
  - Isaiah 7:14 ("virgin" or "young woman"?), in 25 versions

  Each version appears in its own language with the key word highlighted and an English gloss. The versions are listed oldest first and lit up on the map.
- **Cross-map buttons** ("Also on the scripture map…") connect 7 node pairs, for example the Septuagint and Origen.
- **Search** covers both maps and switches maps when needed.
- **Page links** use the part of the address after `#`, so you can link straight to a view: `#paul`, `#kjv`, `#scripture` or `#verse-isa`. The address updates as you select things.
- **Accessibility basics**: nodes can be reached and opened with the keyboard (Tab, then Enter or Space), focus is visible, Escape closes the panel, and the page respects the "reduce motion" setting.

## What's broken, risky or unfinished

### Content accuracy (most important)
1. **The verse quotations were written from memory, not copied from the published editions.** Uncertain versions were left out, but these entries are the shakiest: the Geneva Bible (shown in modern spelling), Wycliffe (only the key word "virgyn" is shown), Luther 1545, Reina-Valera 1960, the NABRE and NASB 1995 wording, and the Dead Sea Scroll note on Isaiah 7:14. **Check every `v:` entry in `S_NODES` against a real edition before promoting the app widely.**
2. **No scholar has reviewed the content.** The dates, summaries and links follow mainstream scholarship and the texts themselves, but they are compressed. Contested claims include Jethro and the Kenite hypothesis, Philo's influence on John, 1 Enoch's influence on Jesus, and Jerome's statement that Aquila studied under Akiva. Those links are marked "debated", but other judgment calls are not flagged.
3. **The voice is mixed.** At the owner's request, the Jesus summary now states a faith claim ("Galilean Jew who is the Messiah"). The rest of the app is written descriptively ("his followers proclaim…"). Decide whether that mix is intended.

### Leftover wording
4. The search box placeholder still says "Find someone… (Moses, Pharisees, Paul)" on the scripture map too.
5. Instructions still say "Pick an idea". The 10 thread chips are still called ideas in the code (`IDEAS`) and in the interface. The owner was asked whether to rename them and hasn't answered yet.
6. The `<nav>` has `aria-label="Filter by idea"` on both maps.

### Usability
7. **Lines cross labels** on busy eras. A few long lines run through other nodes, for example Moses → Nicaea and the many Biblia Hebraica and Nestle-Aland → modern Bible lines.
8. **The phone bottom sheet covers about 62% of the screen.** It has no drag-to-resize or minimize, only a close button. Opening a verse comparison covers most of the map right away.
9. **The browser Back button doesn't step through selections**, because the address is updated without adding history entries.
10. **Phones can show an old version.** The owner's phone did this once after an update. A full reload fixes it, but nothing in the app handles cache-busting.
11. **Sharing previews are plain.** There are no Open Graph or Twitter tags and no preview image, so a link sent in iMessage or WhatsApp shows only the title and description.
12. **There is no light theme** (this was deliberate) and no install-to-home-screen support (manifest or icon).
13. **Screen reader users have no alternative to the graph.** The graph is SVG, with an accessible label on each node, but there is no plain list or table view of all the links. Threads in the panel are shown only by colored dots (the colors have hover titles), which is weak for color-blind users.

### Engineering
14. **There are no tests and no linter.** The only check on the data is the console warning described under "How it's built".
15. **Everything is in one file of about 1,500 lines.** That's fine at this size, but if the content keeps growing, move the data into separate `.json` or `.js` files.
16. **The deploy setup is fragile.** Pages publishes from a `claude/…` feature branch, and nothing has been merged into `main`.

## What should come next (suggested order)

1. **Verify the verse texts** (item 1) and correct any wording. This matters most for a page meant for sharing.
2. **Make `main` the real home.** Merge the feature branch into `main`, switch Pages to deploy from `main` (Settings → Pages), and update the README.
3. **Finish the wording cleanup** (items 4–6), and decide on the voice question (item 3).
4. **Add sharing previews** (item 11): Open Graph and Twitter tags plus a 1200×630 preview image, so links look good when shared by text message.
5. **Improve the phone experience:** a bottom sheet that can be dragged or minimized (item 8), Back-button support (item 9), and a "List view" of all links for screen readers and for people who prefer reading (item 13).
6. **Add more content:**
   - More verses for Follow a verse, for example John 1:1, Psalm 23:1, Exodus 3:14, Genesis 1:1 or Isaiah 53.
   - Extend the Israel's God map past Nicaea (Augustine, the creeds, medieval Jewish thinkers such as Maimonides), or add a parallel rabbinic thread.
   - A "Sources" section with full citations.
7. **Add a small automated check** (Node or Playwright) that runs the data checks and loads both maps, so content edits can't silently break the page.
8. **Decide on the Claude copy.** Either keep publishing it with each change or drop it in favor of the public GitHub Pages link.

## Quick recipes

- **Run locally:** open `index.html` in any browser. No server is needed.
- **Add a person:** add a row to `NODES` (or `S_NODES`) with a unique id and the right era index, then add at least one row to `EDGES` (or `S_EDGES`). Open the page and check the console for warnings.
- **Add a verse comparison:** add an entry to `VERSES` (`label`, `chip`, `intro`), then add `newkey: [text, gloss]` to the `v` object of each scripture node that has it. The chip, map highlighting, timeline list and `#verse-newkey` link all appear automatically.
- **Add a thread:** add `{ id, label, color, desc }` to `IDEAS` or `S_THREADS` and use its id in edge rows. Keep colors readable on the dark blue background.

## Session log

- **7 Oct 2026:** Added `HANDOFF.md`, `CLAUDE.md` and `SPEC.md`. Audited the app with headless Chromium: both maps load with no console errors, no horizontal scrolling at 360px, and no link or id problems in the data. The Pages deploy for `3e61940` succeeded. No app code changed.
