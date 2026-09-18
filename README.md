# Fiction

[Vale](https://vale.sh) styles for fiction: a core of the checks most
editors agree on, and the rules of three writers who wrote theirs down.
[Elmore Leonard](https://www.theguardian.com/books/2010/feb/20/ten-rules-for-writing-fiction-part-one)'s
ten rules, [Chuck Palahniuk](https://litreactor.com/essays/chuck-palahniuk/nuts-and-bolts-“thought”-verbs)'s
thought verbs, and
[William Strunk Jr.](https://www.gutenberg.org/ebooks/37134)'s 1918
*Elements of Style*.

Works on [Markdown](https://docs.vale.sh/formats/markdown),
[plain text](https://docs.vale.sh/formats/text),
[Org](https://docs.vale.sh/formats/org),
[reStructuredText](https://docs.vale.sh/formats/restructuredtext), and
[AsciiDoc](https://docs.vale.sh/formats/asciidoc).

## Install

Requires Vale 3.22.0 or later.

```ini
StylesPath = styles
Packages = Fiction

[*.md]
BasedOnStyles = Fiction, Leonard, Palahniuk
```

```console
$ vale sync
```

`Fiction` is in the [package library](https://vale.sh/explorer), so the
name is enough. To pin a version, give a release URL instead:
`https://github.com/jdkato/fiction/releases/download/v0.1.0/Fiction.zip`.

`Fiction` is also the core style and is always on. Add an author next to
it.

| Style | What it checks |
| ----- | -------------- |
| `Fiction` | Filter words, `began to`, told emotions, intensifiers, stock phrases, and dialogue punctuation. See below. |
| `Leonard` | Six of the ten rules: no weather in the opening, no prologue, only `said`, no adverb on a tag, exclamation points capped, no `suddenly`, and dialect kept sparse. |
| `Palahniuk` | Thought verbs: `thinks`, `knows`, `realizes`, `wants`, `remembers`, `loves`, `hates`, and the rest of the list. |
| `Strunk` | Rules 10, 11, and 13 of *The Elements of Style*, and the Chapter V entries that name a replacement. |

### Core rules

| Rule | Examples flagged |
| ---- | ---------------- |
| `FilterWords` | `she saw`, `he heard`, `it seemed`, `could feel` |
| `BeganTo` | `began to run`, `started to follow` |
| `TellingEmotion` | `felt sad`, `was so angry`, `looked nervous` |
| `Intensifiers` | `very`, `really`, `quite`, `literally` |
| `Cliches` | `heart pounded`, `a breath she didn't know she was holding`, `a chill ran down` |
| `DialoguePunctuation` | `"I know", she said` |
| `TagCase` | `"Run!" She said` |

### Leonard

| Rule | Leonard's rule | Examples flagged |
| ---- | -------------- | ---------------- |
| `Weather` | 1. Never open a book with weather. | `raining` in the paragraph after the title |
| `Prologue` | 2. Avoid prologues. | a heading that says `Prologue` |
| `Said` | 3. Never use a verb other than "said" to carry dialogue. | `she hissed`, `he grumbled,` |
| `Adverb` | 4. Never use an adverb to modify the verb "said". | `he said gravely` |
| `Exclamations` | 5. Keep your exclamation points under control. | more than 3 in a file |
| `Suddenly` | 6. Never use the words "suddenly" or "all hell broke loose". | both |
| `Dialect` | 7. Use regional dialect, patois, sparingly. | more than 5 dropped g's in a file |

Rules 8 through 10, on describing characters and places and on leaving out
the parts readers skip, are not things a regex can find.

`Said` only reads a verb beside a quotation mark, so `she laughed` in
narration is fine, and `asked` is allowed.

### Strunk

| Rule | Source | Examples flagged |
| ---- | ------ | ---------------- |
| `ActiveVoice` | Rule 10 | `There were a great number of`, `could be heard` |
| `Positive` | Rule 11 | `not honest`, `did not remember` |
| `Needless` | Rule 13 | `the question as to whether`, `he is a man who`, `owing to the fact that` |
| `FactThat` | Rule 13 | `the fact that` |
| `Misused` | Chapter V | `different than`, `most everybody`, `have got`, `like I did` |
| `Hackneyed` | Chapter V | `certainly`, `factor`, `interesting`, `very`, `one of the most` |
| `However` | Chapter V | `However,` first in its sentence |
| `SplitInfinitive` | Chapter V | `to diligently inquire` |
| `LikeAs` | Chapter V | `like in the old days` |

Every rule file starts with a comment quoting or paraphrasing the passage it
comes from and links to the source.

## Configuration

```ini
# A novel, one chapter per file
[*.md]
BasedOnStyles = Fiction, Leonard, Palahniuk

# Essays and everything else
[*.txt]
BasedOnStyles = Fiction, Strunk
```

Limits are parameters, so you can change them without editing the rule:

```ini
Leonard.Exclamations[max] = 30
Leonard.Dialect[max] = 50
Fiction.DialoguePunctuation = NO
```

## Notes

**Dialogue.** A rule cannot yet tell a quotation from narration, so
`Palahniuk.ThoughtVerbs` and `Fiction.FilterWords` read a character's
speech too. A dialogue scope is on Vale's roadmap; until then, expect a
"she knew" inside quotation marks to be flagged.

**Openings.** `Leonard.Weather` reads the paragraph after the level-one
heading. A file with no title heading, and any plain-text file, has no
opening to check.

**Counts.** `Leonard.Exclamations` and `Leonard.Dialect` count per file.
Leonard's budget is two or three exclamation points per 100,000 words, so
raise `max` for a whole novel in one file.

**British punctuation.** `Fiction.DialoguePunctuation` wants the comma and
period inside the closing quotation mark, which is the American convention.
Turn it off for the other.

## Tests

```console
$ ./test.sh
```

Each rule has test cases in a `tests:` block, run by `vale test`. Each
format also has a fixture in `fixtures/` with a golden file in `testdata/`,
and a clean version in `fixtures/clean/` that must produce no alerts. A
rule with no test that expects an alert fails the run. Use `./test.sh -u`
to regenerate goldens.

## License

MIT. Sources for the transcribed rules are listed in [NOTICE](NOTICE).
