# Fiction

[Vale](https://vale.sh) styles for fiction: a core of the checks most
editors agree on, the rules of four writers who wrote theirs down, and
the checks of the [Hemingway Editor](https://hemingwayapp.com/).
[Elmore Leonard](https://www.theguardian.com/books/2010/feb/20/ten-rules-for-writing-fiction-part-one)'s
ten rules, [Chuck Palahniuk](https://litreactor.com/essays/chuck-palahniuk/nuts-and-bolts-“thought”-verbs)'s
thought verbs,
[William Strunk Jr.](https://www.gutenberg.org/ebooks/37134)'s 1918
*Elements of Style*, and
[George Orwell](https://www.orwellfoundation.com/the-orwell-foundation/orwell/essays-and-other-works/politics-and-the-english-language/)'s
six rules from "Politics and the English Language". `Hemingway` is the
editor's highlights as Vale rules: adverbs, passive voice, qualifiers,
words with simpler alternatives, hard sentences, and the reading grade.

Works on [Markdown](https://docs.vale.sh/formats/markdown),
[plain text](https://docs.vale.sh/formats/text),
[Org](https://docs.vale.sh/formats/org),
[reStructuredText](https://docs.vale.sh/formats/restructuredtext), and
[AsciiDoc](https://docs.vale.sh/formats/asciidoc).

## Install

Requires Vale 3.23.0 or later. The rules that grade a sentence or measure
a chapter, `Hemingway.HardSentence`, `Hemingway.VeryHardSentence`,
`Hemingway.ChapterGrade`, and `ChapterLength`, need a Vale built from the
`v3` branch until the next release.

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
`https://github.com/jdkato/fiction/releases/download/v0.2.0/Fiction.zip`.

`Fiction` is also the core style and is always on. Add an author next to
it, and `Narration` for a manuscript in the third person or the past
tense.

| Style | What it checks |
| ----- | -------------- |
| `Fiction` | Filter words, `began to`, told emotions, intensifiers, stock phrases, dialogue punctuation, stiff and expository dialogue, action tags, participial openers, adjective stacks, mixed spellings and marks, and chapter openings and endings. See below. |
| `Narration` | Slips in narration: a present-tense verb in a past-tense manuscript, a first-person pronoun in a third-person one. Turn off the rule that doesn't apply. |
| `Leonard` | Six of the ten rules: no weather in the opening, no prologue, only `said`, no adverb on a tag, exclamation points capped, no `suddenly`, and dialect kept sparse. |
| `Palahniuk` | Thought verbs: `thinks`, `knows`, `realizes`, `wants`, `remembers`, `loves`, `hates`, and the rest of the list. |
| `Strunk` | Rules 10, 11, and 13 of *The Elements of Style*, and the Chapter V entries that name a replacement. |
| `Orwell` | Four of the six rules: dying metaphors, pretentious diction, verbal false limbs and the `not un-` formation, and foreign phrases. |
| `Hemingway` | The Hemingway Editor's highlights: adverbs, passive voice, qualifiers, words with simpler alternatives, sentences that are hard and very hard to read, and a reading grade for the file. |

### Core rules

| Rule | Examples flagged |
| ---- | ---------------- |
| `FilterWords` | `she saw`, `he heard`, `it seemed`, `could feel` |
| `BeganTo` | `began to run`, `started to follow` |
| `TellingEmotion` | `felt sad`, `was so angry`, `looked nervous` |
| `Intensifiers` | `very`, `really`, `quite`, `literally` |
| `Cliches` | `heart pounded`, `a breath she didn't know she was holding`, `a chill ran down` |
| `Participle` | `Walking to the door, she opened it` |
| `Adjectives` | `a tall, dark, handsome stranger` |
| `Beats` | more than 10 nods, shrugs, sighs, and smiles in a file |
| `DialoguePunctuation` | `"I know", she said` |
| `TagCase` | `"Run!" She said` |
| `ActionTag` | `"Hello," she smiled`, `He nodded, "Fine."` |
| `StiffDialogue` | `"I do not know"`, `"I am not going"` |
| `AsYouKnow` | `"As you know, Bob,"`, `"As I told you,"` |
| `Monologue` | one speech over 80 words |
| `Variants` | `toward` and `towards` in the same file |
| `Marks` | `"` and `“`, `'` and `’`, `...` and `…`, `--` and `—` in the same file |
| `Waking` | `woke up`, `the alarm went off` in the paragraph after a heading |
| `Cliffhanger` | a chapter whose last paragraph ends on `?` |
| `ChapterLength` | a chapter under 1,000 words or over 6,000 |
| `Redundancy` | `nodded his head`, `shrugged her shoulders`, `thought to himself` |

The rules about speech, `StiffDialogue`, `AsYouKnow`, and `Monologue`,
read only the text between quotation marks. The rules about narration,
`FilterWords`, `TellingEmotion`, `Intensifiers`, `Palahniuk.ThoughtVerbs`,
and the four Hemingway word rules, read everything but.

### Narration

| Rule | Examples flagged |
| ---- | ---------------- |
| `PresentTense` | `she walks`, `he is` in narration |
| `FirstPerson` | `I`, `my`, `we` in narration |

Both read narration only, and `PresentTense` reads it by part of speech. A
first-person manuscript turns off `FirstPerson`, and a present-tense one
turns off `PresentTense`.

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

### Orwell

| Rule | Orwell's rule | Examples flagged |
| ---- | ------------- | ---------------- |
| `Metaphors` | 1. Never use a metaphor, simile, or other figure of speech which you are used to seeing in print. | `no axe to grind`, `swan song`, `toe the line` |
| `Pretentious` | 2. Never use a long word where a short one will do. | `utilize`, `phenomenon`, `veritable`, `expedite` |
| `FalseLimbs` | 3. If it is possible to cut a word out, always cut it out. | `give rise to`, `in view of`, `the fact that` |
| `NotUn` | 3, from the essay's footnote. | `not unsmall` |
| `Foreign` | 5. Never use a foreign phrase, a scientific word, or a jargon word if you can think of an everyday English equivalent. | `cul-de-sac`, `deus ex machina`, `status quo` |

Each list is the essay's own. Rule 4, never use the passive where you can
use the active, is `Hemingway.PassiveVoice` below, or
`Std.Grammar.PassiveVoice` in [Std](https://github.com/vale-cli/Std). Rule
6, break any of these rules sooner than say anything outright barbarous, is
yours.

### Hemingway

| Rule | The editor's highlight | Examples flagged |
| ---- | ---------------------- | ---------------- |
| `Adverbs` | Blue: adverbs | `walked slowly`, `quietly opened` |
| `PassiveVoice` | Blue: passive voice | `was opened by`, `were being followed` |
| `Qualifiers` | Blue: qualifiers | `perhaps`, `sort of`, `I think`, `it seemed` |
| `Simpler` | Purple: words with simpler alternatives | `utilize`, `commence`, `in order to`, `subsequently` |
| `HardSentence` | Yellow: hard to read | a sentence of 14 words or more at grade 10 to 13 |
| `VeryHardSentence` | Red: very hard to read | a sentence of 14 words or more at grade 14 or higher |
| `Grade` | Readability | a file that reads above grade 9 |
| `ChapterGrade` | Readability | a chapter that reads above grade 9 |

The grade is the editor's: the Automated Readability Index, from letters
per word and words per sentence. The two sentence rules take it one
sentence at a time, with the editor's floor of fourteen words, and `Grade`
takes it over the whole file, against the editor's default target of grade
9, and `ChapterGrade` takes it over each level-two section. The word lists
are the package's own, except `Simpler`, which takes its pairs from the
United States government's plain-language guidelines.

Every rule file starts with a comment quoting or paraphrasing the passage it
comes from and links to the source.

## Configuration

```ini
# A novel, one chapter per file, in the first person
[*.md]
BasedOnStyles = Fiction, Leonard, Palahniuk, Narration
Narration.FirstPerson = NO

# Essays and everything else
[*.txt]
BasedOnStyles = Fiction, Strunk, Orwell, Hemingway
```

Limits are parameters, so you can change them without editing the rule:

```ini
Leonard.Exclamations[max] = 30
Leonard.Dialect[max] = 50
Fiction.Beats[max] = 40
Fiction.Monologue[max] = 120
Fiction.DialoguePunctuation = NO
```

A measured rule's `condition` is one too, and `result` in it is the
measurement, so both ends of a band can move:

```ini
Fiction.ChapterLength[condition] = "< 500 || result > 8000"
Hemingway.Grade[condition] = "> 7"
```

So is a scope. `Cliffhanger` reads the last paragraph of each level-two
section; for a manuscript with one chapter per file, point it at the last
paragraph of the file:

```ini
Fiction.Cliffhanger[scope] = text & doc(p:last-of-type)
```

### Names

Invented names trip the spell checker. If the built-in `Vale` style is on,
list the characters and places in a
[vocabulary](https://docs.vale.sh/topics/vocab) and `Vale.Spelling` accepts
them:

```
styles/config/vocabularies/Names/accept.txt
```

```ini
Vocab = Names
```

## Notes

**Speech.** The text between quotation marks, curly, straight, or single,
is speech. The rules about speech read only that, and the rules about
narration leave it out, so a character may say "I know" and "very" without
a note. An opening mark with no closing mark runs to the end of its
paragraph, which is the convention for speech that continues into the next
one. The rules that read a tag beside the mark, `Leonard.Said`,
`Leonard.Adverb`, `ActionTag`, `TagCase`, and `DialoguePunctuation`, read
both sides.

**Openings and endings.** `Leonard.Weather` reads the paragraph after the
level-one heading, and `Waking` the paragraph after any heading.
`Cliffhanger` reads the last paragraph of each level-two section, and
`ChapterLength` and `Hemingway.ChapterGrade` the whole of it. A file with
no heading, and any plain-text file, has no opening or chapter to check.

**Counts.** `Leonard.Exclamations`, `Leonard.Dialect`, and `Beats` count
per file. Leonard's budget is two or three exclamation points per 100,000
words, so raise `max` for a whole novel in one file.

**Consistency.** `Variants` and `Marks` don't prefer a form. Once a file
has both, each paragraph that uses either is flagged, once, at its last
use.

**Sentences.** `HardSentence` and `VeryHardSentence` read every sentence,
speech included, and a sentence gets one note or the other, never both.
The grades are the editor's, and are not parameters; `Grade` reads the
whole file and fires once.

**British punctuation.** `DialoguePunctuation` wants the comma and period
inside the closing quotation mark, which is the American convention. Turn
it off for the other.

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
