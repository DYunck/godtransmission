# Cloud of Witnesses

An interactive network map of how Israel's God moved from person to person: from Abraham through Moses, the prophets, the exile and the Jewish sects of the Second Temple period, to Jesus, the apostles and the church fathers who wrote the Nicene Creed.

- **Tap anyone** to see who shaped them and whom they shaped, with the texts behind each link.
- **Pick an idea** (One God, Covenant, the Divine Name, Messiah, Son of Man, Wisdom & Word, Spirit, Resurrection, Kingdom of God, Presence & Priesthood) to trace its thread through the centuries.
- **Whole lineage** shows everyone upstream and downstream of a person.
- **Scripture's journey** is a second map: how the Bible was copied, translated and argued over, from the Temple scribes and early rabbis (Akiva, Aquila, the Masoretes, Rashi) through the Septuagint, Vulgate, Luther, Tyndale and the King James to modern translations (NIV, ESV, NRSV, JPS and others). Pick any Bible and choose *Whole lineage* to see its family tree.
- **Follow a verse** shows Deuteronomy 6:4 (the Shema) and Isaiah 7:14 ("virgin" or "young woman"?) in each version, oldest first, in the original language with an English gloss.
- Deep links work: `index.html#paul` opens with Paul selected, `#scripture` opens the scripture map, `#kjv` selects the King James, and `#verse-isa` opens the Isaiah 7:14 comparison.

It is one self-contained file (`index.html`) with no build step. Open it in a browser, or turn on GitHub Pages (Settings → Pages → deploy from the default branch) to get a link that works on phones.

The data (people, eras and links) lives at the top of the `<script>` block in `index.html`, so adding a person or a link is a one-line change.
