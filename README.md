# Cloud of Witnesses

An interactive network map of how Israel's ideas about God moved from person to person: from Abraham through Moses, the prophets, the exile and the Jewish sects of the Second Temple period, to Jesus, the apostles and the church fathers who wrote the Nicene Creed.

- **Tap anyone** to see who shaped them and whom they shaped, with the texts behind each link.
- **Pick an idea** (One God, Covenant, the Divine Name, Messiah, Son of Man, Wisdom & Word, Spirit, Resurrection, Kingdom of God, Presence & Priesthood) to trace its thread through the centuries.
- **Whole lineage** shows everyone upstream and downstream of a person.
- Deep links work: `index.html#paul` opens with Paul selected.

It is one self-contained file (`index.html`) with no build step. Open it in a browser, or turn on GitHub Pages (Settings → Pages → deploy from the default branch) to get a link that works on phones.

The data (people, eras and links) lives at the top of the `<script>` block in `index.html`, so adding a person or a link is a one-line change.
