# CLAUDE.md

## Working rules

- **Before saying something works, actually test it.** Open the page in a browser (headless Chromium/Playwright is available), check the console for errors and warnings, and look at it at phone width (about 390px) as well as desktop width. If you could not test something, say so plainly.
- **Don't spend money or sign up for services without asking me.**
- **Update HANDOFF.md at the end of every session.** Record what changed, what you tested, what's still broken, and what should come next.

## Project at a glance

- The whole app is `index.html`, with no build step and no dependencies apart from Google Fonts. Read `HANDOFF.md` for the full state of the project and `SPEC.md` for where it's going.
- The live site is GitHub Pages at https://dyunck.github.io/godtransmission/, deployed from branch `claude/biblical-theology-network-2p6dzf`. Pushing to that branch redeploys it.
- A private copy is also published at https://claude.ai/artifact/7fqfoh143WtH5vFdMfLup3. It doesn't update itself: republish it after changes, as described in HANDOFF.md.
- Node ids must be unique across both maps. After any data edit, load the page and check the console for "bad edge" or "duplicate id" warnings.
- Content is historical and religious, and the owner reviews the wording. Don't invent quotations. Mark uncertain links as debated (`"d"`) and say in your reply when a claim needs checking.
