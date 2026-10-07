# Spec: Cloud of Witnesses

Status: working draft, written 7 October 2026 from the app as built. See `HANDOFF.md` for the current technical state.

## What it is meant to be

A beautiful, trustworthy map that lets an ordinary person **see** how faith in Israel's God and the scriptures that carry it were handed down. Each step is a real person, community or text, from Abraham to the early church, and from the first scribes to the Bible in your hand today.

It should feel like exploring, not like reading a textbook. You tap a name and see who shaped them and whom they shaped. You pick a thread, such as "Messiah" or "English", and watch it run through the centuries. You pick a verse and watch the words change. Every link is backed by a text you can look up.

## Who it's for

**Primary user: someone the owner shares it with.** A friend, a small-group or Bible-study member, or a curious churchgoer, usually opening a link on a phone. They have little time, no academic background, and are curious about where their faith and their Bible came from.

They need:
- To understand the page within 10 seconds without instructions.
- To be able to tap around one-handed on a phone.
- Short, plain-English summaries with Bible references they can check.
- To be able to send a link to a specific person or verse they found interesting.

**Secondary users:**
- **The owner:** shares the app, adds content and wants to trust it.
- **Group leaders and teachers:** use it in a session to show one thread or verse on a screen or a shared phone.
- **More knowledgeable readers:** pastors, seminarians and Jewish friends. They will notice errors and judge credibility by the sources.

**Not for (for now):** academic researchers needing full apparatus, or anyone wanting a theology debate tool. The app shows how things were handed down; it doesn't argue which reading is right.

## Principles

1. **Phone first.** Every feature must work at 360–400px with touch.
2. **Every link is earned.** Each connection names a text, a teacher-and-student relationship, or a documented argument. Contested links are labeled as debated.
3. **Respectful to both traditions.** Jewish and Christian streams are both shown as living traditions, not one as a mere prelude to the other.
4. **Opens ready to use.** The first screen shows the map, not an empty search box.
5. **Simple to maintain.** One static page, free hosting, no accounts and no costs. Content edits are one-line data changes.

## What exists today

- Two maps: **Israel's God** (68 nodes, 149 links, 10 idea threads) and **Scripture's journey** (57 nodes, 117 links, 9 streams).
- Tap-to-explore detail panel with link notes, Direct links / Whole lineage tracing, thread highlighting, cross-map links and search across both maps.
- **Follow a verse:** Deuteronomy 6:4 in 20 versions and Isaiah 7:14 in 25 versions.
- Links to a specific person or verse (for example `#kjv` or `#verse-isa`), a public GitHub Pages site and a private Claude copy.

## Features still needed, in priority order

### P0: Trust (before sharing widely)
1. **Verify every verse quotation** against a published edition, and record the edition and year next to each one. *Done when:* all 45 verse entries have a checked source.
2. **Content review pass.** Have someone knowledgeable read the summaries and links on both maps. Flag or fix overstatements, and settle whether summaries are written in a descriptive or a confessional voice. *Done when:* the reviewer signs off and the voice is consistent or deliberately mixed.
3. **Sources page or panel.** List the main references behind the dates and claims, so skeptical readers can check them. *Done when:* every node's key texts can be traced to a listed source.

### P1: Sharing and first impressions
4. **Link previews.** Add Open Graph and Twitter tags and a preview image, so a shared link looks inviting in iMessage, WhatsApp and Facebook.
5. **Share button.** Copy a link to the current view (person, thread or verse) with one tap.
6. **Tidy the wording.** Make the search placeholder fit the active map, settle the name for idea threads, and give screen readers labels that fit each map.
7. **Make `main` the home branch.** Merge the work into `main` and deploy Pages from there, so the site doesn't depend on a feature branch.

### P2: Phone experience
8. **Resizable bottom sheet.** Let the reader drag the panel between half-screen and full-screen, or minimize it to a peek bar so the map stays visible.
9. **Back button support.** Each selection becomes a browser history step, so Back returns to the previous person or view.
10. **Cleaner lines.** Route lines around labels and fade very long lines, so busy eras stay readable.
11. **Short guided tour.** A 3–4 step tour the first time someone visits (tap a node, pick a thread, follow a verse), which they can skip.

### P3: More content
12. **More verse comparisons:** Genesis 1:1, Exodus 3:14, Psalm 23:1, Isaiah 53:5, John 1:1 and Matthew 6:13 (the doxology).
13. **Extend Israel's God past Nicaea:** Augustine and the later creeds, plus a parallel Jewish thread (the Talmud, Saadia, Maimonides) so the Jewish story doesn't stop in 200 CE.
14. **More translations:** major non-English Bibles (Chinese Union Version, Louis Segond, Luther 2017) and audio or sign-language translation milestones.

### P4: Reach and robustness
15. **List view.** A readable list or table of every node and link, for screen readers, printing and people who prefer text.
16. **Color-blind safe threads.** Label or pattern threads, not just color them.
17. **Add to home screen** (app icon and manifest), so friends can keep it like an app. It should keep working offline if that stays free and simple.
18. **Automated check.** A small test that validates the data and loads both maps, run before each publish.
19. **Split the data out** of `index.html` into separate files once content grows.

## Out of scope unless the owner decides otherwise
- User accounts, comments or user-submitted content.
- Paid hosting, analytics services or anything that costs money or requires signing up for a service.
- Ranking or judging traditions, or making doctrinal claims beyond what the owner has written.

## Open questions for the owner
- Should the summaries describe what traditions believe, or state faith claims directly (as the Jesus summary now does)?
- Who should review the content (a pastor, a Bible teacher, a rabbi friend)?
- Is the private Claude copy still needed, or is the GitHub Pages link enough?
- Should the 10 idea chips keep the name "ideas", or be renamed (for example "threads" or "themes")?
