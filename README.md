# Verba

*Verba* — Latin for "words," which is what William Whitaker called the original program. A complete Latin dictionary and morphological parser that runs entirely in the browser. Type any Latin word, inflected or not, and get the dictionary entry, the meanings, and every grammatical reading of the form.

**[Launch Verba →](https://rjedtech.github.io/Verba/)**

Built for the Regis Jesuit Latin department after the online dictionary they had used for years went offline. This one can't go offline the same way — there is no server to go down.

Two tabs: **Look up a word**, and **Practice**.

## Look up a word

Type `amaverunt` and it tells you the word is `amo, amare, amavi, amatus` — "love, like" — in the perfect active indicative, 3rd person plural, with a plain-English note underneath saying what that actually means in a sentence.

- **Inflected forms work.** You don't need the dictionary form; that's the whole point.
- **Every reading is listed.** `senatus` is nominative, vocative, *and* genitive singular, plus three plural cases. Students see all of them.
- **Enclitics are split.** `senatusque` finds `senatus` + `-que`.
- **Macrons are fine.** Paste `amāvērunt` from a textbook and it works.
- **`j`/`v` or `i`/`u`** spellings both match, so `iulius` and `Julius` land in the same place.
- **Paste a whole line** and every word in it gets parsed — useful for prepping a passage.
- **English → Latin** too. Ask for "river" and get *flumen*, *fluvius*, *amnis*. Ranked so the word a Latin I student wants comes first, not the rarest word whose gloss happens to match.
- **Misspellings are caught.** Type `ameverunt` and it offers `amaverunt`.
- **Plain English: on** explains every grammar label — "genitive" also says *shows belonging — "of"*. Teachers can switch it off.
- **Whitaker view** shows the classic fixed-width output for anyone who misses it.
- **Link to a word:** `...Verba/#amaverunt` opens with that word already parsed, which is handy for assignments and Canvas pages.

## Practice

A teacher pastes a list of Latin words — one per line, bare words are enough, since meanings and principal parts fill in from the dictionary. `porto = to carry` overrides the meaning if you want your own wording.

**Share this list** copies a link with the whole list encoded inside it. Paste that into Canvas and students open it straight into the practice tab. No accounts, no server, nothing to expire.

Five modes, each with an optional 60-second timed round and a running streak:

- **Review what's due** — the words the student is closest to forgetting. The default place to start.
- **Mixed practice** — meanings and forms jumbled together.
- **Flashcards** — recall the meaning, then click the card to flip. Keyboard: space to flip, 1 and 2 to grade.
- **Write the form** — "*corpus, corporis* — ablative plural" and the student types `corporibus`. Generated and graded from the dictionary's own inflection tables, so it works on any word in the list.
- **Name the form** — the reverse, multiple choice. Closest to what a test asks.

### Sharing a list

**Share this list** opens a panel with two things: the link, and a ready-to-paste Canvas post containing the link *and* the instructions students need. A 20-word list makes a ~250-character URL. No accounts, no server, nothing to expire.

A student opening that link lands on a banner explaining what it is and what to do, with a button to keep the list on their device so they don't need the link again. A teacher can also paste a colleague's link into the words box to import their list.

### Why it's built this way

The practice design follows the learning research rather than what feels productive:

- **Retrieval before checking.** Attempting recall — and failing — beats re-reading (Roediger & Karpicke).
- **Spacing across days.** Correct words return on a widening schedule; missed words come back soon (Cepeda et al.).
- **Even spacing within a session.** Missed words reappear about five questions later rather than at the end of the round: Karpicke & Roediger (2007) found expanding intervals help short-term recall but *equal* intervals produce better long-term retention.
- **Interleaving.** Mixed practice is harder in the moment and stronger later than blocked drilling (Rohrer & Taylor).
- **High-frequency words first.** Core vocabulary is badged throughout, and a list can be filtered to it. The DCC core 1000 covers roughly 78% of Caesar's *Gallic War* and 70% of the *Aeneid*.
- **Elaboration.** The back of each card shows the Latin stem and asks what English words come from it — making the connection yourself is what fixes it.

The page says all of this to students where it matters, especially that clicking "Didn't know it" honestly is what makes the scheduling work.

None of this replaces reading a lot of Latin, which is where fluency actually comes from. It handles the vocabulary and forms that make the reading possible.

## How it works

**The entire site is one file: `index.html` (2.2 MB).** No server, no build step, no database, no API key, no dependencies. The complete dictionary — 38,091 entries and 48,508 stems — ships gzipped inside the page and is unpacked by the browser on load.

Consequences worth knowing:

- Nothing a student types leaves their device.
- It works **offline**. Once the page has loaded, students can lose wifi and keep going, and the file can be saved to a Chromebook or handed out on a flash drive.
- Deploying it is copying one file.

## Accuracy

The parser is a JavaScript port of [blagae/whitakers_words](https://github.com/blagae/whitakers_words), a maintained Python reimplementation of William Whitaker's original Ada program.

The port was checked against the Python implementation across 16,845 words and **17,792 grammatical analyses, with zero differences in output** — including a final run of this exact `index.html` in a headless browser after every UI change, so what was verified is what ships.

The practice drills are generated from the same inflection tables the parser uses, so a form the drill asks for is a form the dictionary can confirm.

Two deliberate departures from the Python package's defaults:

- **The whole dictionary is included.** That package defaults to a frequency filter that drops 63,000 of 94,000 stems. Fine for a demo, useless for a classroom, so rare, late, and inscriptional vocabulary is all here.
- **Principal parts display correctly.** The package folds `v`→`u` internally for matching, which renders *portavi* as "portaui". This build re-reads the original dictionary file for display spelling.

## Known limits

Inherited from the Python implementation, not introduced by the port:

- Prefix and suffix decomposition is not applied.
- Interrogative pronouns are analyzed unreliably.
- Latin → English only; there is no English → Latin lookup.

If exact fidelity to the original Ada program ever matters more than these, the fallback is to run Whitaker's actual binary behind a small API and point this same front end at it.

## Also worth your time

[Magistrula](https://www.magistrula.com/) — a separate site built by a Latin teacher, linked from the footer of this one. Nothing in Verba is derived from it.

## Credits

Dictionary and morphological data by **William Whitaker (1936–2010)**, released for free and unrestricted use. Original Ada program: [mk270/whitakers-words](https://github.com/mk270/whitakers-words).

---

Regis Jesuit High School · Educational Technology
