# English Design Specification — The Little Book of Kaggle 1st Place Solutions

This specification and an ordered list of Kaggle competitions are the starting inputs for a new English viewing edition. The production workflow takes the reader from a single example to a usable baseline, the reported winning solution and an experiment that could have led to it. It includes a portable compositor, an auditor, a synthetic layout fixture and a cover prompt. A fresh edition requires research and original writing. A repeat build of the same edition uses the approved manuscript, source records, cover and fonts.

This is an English adaptation of [the Japanese design specification](https://github.com/espritmirai/little-book-kaggle/blob/main/%E8%A8%AD%E8%A8%88%E6%9B%B8.md) in [espritmirai/little-book-kaggle](https://github.com/espritmirai/little-book-kaggle). The project credits the cover design of Alexandre Torres-Leguet's [The Little Book of Reinforcement Learning](https://github.com/alxndrTL/little-book-rl). The repository's [license and credits](https://github.com/espritmirai/little-book-kaggle/blob/main/README.md) apply to the underlying material. The adaptation follows the project's CC BY-SA 4.0 convention for original editorial text and its MIT convention for the original bundled code. Third-party publications, competition materials and font files retain their own terms.

## 1. Commission an edition

Provide the competition names or Kaggle URLs in the intended chapter order. Use a request with the following structure.

> Using this design specification, create an English viewing edition of *The Little Book of Kaggle 1st Place Solutions* covering the competitions below in this order. Research each competition, write the complete book, generate a new cover illustration, build the PDFs and complete the acceptance tests. Return the viewing PDF and the source and verification files needed to reproduce it.
>
> Competitions
>
> 1. [First official URL]
> 2. [Second official URL]

Use the official title and distinguish the division, season and scoring track. Resolve a name that points to several years from the official pages. Ask the commissioning reader only when the intended event or the editorial treatment depends on a decision the sources cannot supply. Retain the specified order and source cutoff date.

A workflow needs access to competition and participant sources, a way to write and execute the appendix code, an image-generation capability and a way to inspect rendered pages. Save completed sections and the sources needed to resume. The compositor itself requires the files documented below and runs offline. The choice and ordering of competitions never require the five original chapters to be present.

## 2. Assemble the book

| Order | Element | Editorial purpose |
| --- | --- | --- |
| 1 | Front cover | Use the three-line title and a newly generated grayscale reading scene. |
| 2 | Interior title page | Repeat the title treatment. Credit solution authors where their methods are discussed. |
| 3 | Contents | Link to the prologue, each competition and its four numbered sections, the epilogue and appendix. Generate folios from the laid-out book. |
| 4 | Competitions in This Book | Give each task a compact introduction and explain How to Read This Book. Record the edition's source cutoff and scope. |
| 5 | On Beginning Again | In an original short scene, follow a participant rereading a winning solution and finding a question they can test. |
| 6 | Competition chapters | Use the four-part structure below in the requested order. |
| 7 | He Will Win the Next Competition | Return to the participant as they put an experimental decision into practice. |
| 8 | Appendix and references | Provide shared vocabulary, an experiment-record template, source links and a concise production note when useful. |

Write the framing scenes as fiction. Present the technical chapters as explanatory prose for readers with basic programming or machine learning knowledge. Open each chapter with concrete data and a prediction or action. Introduce concepts when they solve a problem in the story. Expand acronyms at first use, define units and distinguish training, validation, hidden evaluation and deployment. Use idiomatic American English. Retain official names, product labels and identifiers where their spelling matters.

A complete chapter can be read on its own. Its length follows the difficulty of the competition and the available evidence. A reference chapter commonly takes several thousand words. Assess explanation and experiment quality directly. Preserve 9-point text and give tables and code the space they need. Page counts vary across editions.

## 3. Write each competition chapter

### 1. The Task

Start with a worked row, turn or output. Explain what participants receive, what they submit and what information is visible at the relevant time. Name the files or fields that matter and give the shape of the submission. Cover the unit of prediction, how the scorer aggregates results and whether a larger or smaller score is better. Show how to get a score from an example with invented inputs. Include data access, runtime and evaluation constraints when they change what a participant can build.

### 2. A Baseline Solution

Specify the simplest plausible rule or model and give its inputs, output and validation split. Match the competition interface or explain the boundary of a simplified example. Work through one characteristic failure and use it to motivate the next experiment. Provide a short readable listing the reader can run on small invented inputs. Give expected output and carry the executable source along with the manuscript. A more capable comparison earns space when its effect can be diagnosed.

### 3. The First-Place Solution

Establish the final ranking and the name used by the winning team. Use the winner's write-up, pinned implementation or the organizers' published method notes. Explain the system from input through training and inference to the scored output. Describe the few decisions that changed what the system could do. Follow a concrete row through the key operations. Include an original diagram of the winning method. Where a measured comparison exists, give the split, metric and configuration. Qualify proposed mechanisms separately from the measured outcome.

Compare with another documented solution when it shows a meaningful choice. A leaderboard gap seldom isolates one design decision. If rankings are provisional, give the cutoff, identify what was available and label an interim designation consistently. For missing essential evidence, keep the chapter in review and document the precise gap.

### 4. How to Find the Winning Approach Yourself

Reconstruct a feasible investigation starting from observations available during the event. Present at least two hypotheses, a comparison that holds unrelated conditions fixed, diagnostic slices, a decision rule, a budget and where to return when the test fails. Use a second original diagram for this sequence. Distinguish the teaching investigation from the winner's recorded development history.

Close the section with a small reproduction exercise and review questions with answers. The exercise should state what to measure, how to make a failure visible and what extra resources a full replay would require. Retain uncertainty about the hidden set when discussing new results. For security competitions, keep explanations focused on what the benchmark tests, defensive interpretation, scoring and safeguards.

## 4. Research and document claims

Start with the official overview, data, rules, submission format and final or date-stamped leaderboard. Use the winners' own account or a pinned code revision for solution details. Organizer reports can establish facts about the field and published scoring results. Read the relevant passage or implementation and extract the substantive claim. A search title or generic snippet is a lead. A verified excerpt is evidence for what it actually says.

Assign stable, uppercase IDs such as EX-RULES and EX-WINNER. Use IDs consistently in the source list, content records and manuscript markers. Store the URL, access date, read status, exact section or code path and revision when available. Give the part of the text inspected if the source was partially accessible. For each important claim, name its manuscript block and reference IDs. Record essential claims about the task, metric, final rank and winning architecture for every chapter. Keep a source dispute visible in the record until the prose accounts for it.

Use separate provenance for organizers' results, participants' reported experiments, direct code observations, performed toy checks and editorial hypotheses. Report a score beside its metric and data scope. Keep quotations short and follow source terms. Draw your own diagrams and use invented examples. Document assets and training data terms when they materially constrain a replay.

## 5. Design the page

| Feature | English viewing profile |
| --- | --- |
| Trim and orientation | 108 × 175 mm, single column, left bound, white, no bleed |
| Measure | 85 mm with 13 mm inner and 10 mm outer margins |
| Vertical flow | Body starts 39 pt from the top; bottom measure ends 15 mm from the foot |
| Body | STIX General Regular, 9 pt, 12.6 pt leading. The first line of every prose paragraph has an 8 pt indent. |
| Main headings | STIX General Bold. Chapter label 13 pt and chapter title 17 pt on separate lines. Numbered sections 11 pt. |
| Subheads | DejaVu Sans Bold, 9 pt. Keep with the opening prose. |
| Figure captions | DejaVu Sans Bold, 7.2 pt, centered. Figure number followed by its title. |
| Table captions | DejaVu Sans Bold, 7.2 pt, aligned with the left edge. Repeat the caption and column headings when the table flows across pages. |
| Table cells and figure labels | Sans serif at 7.6–8 pt. Main rules and arrows at least 0.75 pt. |
| Citations | Serif, 5.8 pt, raised 2.4 pt. Keep trailing citations with the preceding word. |
| Code | DejaVu Sans Mono, 7.2 pt, 9.6 pt leading. Preserve line order and indentation. |
| Running heads and folios | 7 pt. Running head at the top right of odd chapter continuation pages. Folio at the outer edge of the measure, 9 mm from the foot. |
| Part starts | Prologue, chapters, epilogue and appendix start on odd-numbered interior pages. A framing blank has no running head or folio. |
| Cover and title page | The Little Book / of / Kaggle 1st Place Solutions in three 17 pt lines, no byline. |
| Binding | The number of interior pages is even. The viewing PDF prepends the front cover. |

The 9-point body size, compact portrait trim, section order, facing margins and three-line title carry over from the approved English edition. This implementation pins and embeds an open serif, sans serif and monospaced font set. Different font metrics and new content affect line and page breaks. Its page-count ceiling is 300 interior pages at these margins. A longer or print edition needs its own validated gutter and print profile. Confirm a printer's current submission template separately when print files are requested.

## 6. Prepare illustrations and listings

Use one purpose per figure. Put each figure near the prose that explains it. Diagram the winning mechanism and the discovery path with labels that make sense on the printed page. The bundled renderer makes vector flow diagrams with two to six steps. If the inference depends on branches, feedback loops, charts or a more complex topology, extend the drawing schema and audit the resulting paths. The prose should still explain the exact data movement.

Use tables to make comparisons or look up specific values. Keep the caption free of final punctuation, repeat headers for long tables and put qualification text immediately below the table when space allows. Preserve every cell. Keep code as a complete short listing. Wrap at syntactic boundaries before relying on the compositor's continuation marker. If a listing cannot fit on a single page, prepare self-contained excerpts at meaningful boundaries and retain the full executable source in the edition files. Typeset scalar formulas or simple fractions or radicals through the formula block. For more complex math, prepare and inspect a dedicated renderer extension or a verified vector figure.

Generate the cover art for each new edition with the appendix prompt. Select an illustrated reading scene with a clean white perimeter and comfortable margins. Review the book's orientation, believable anatomy and objects, ink weight, empty background and distance between the title and illustration. Typeset the title in the compositor. Preserve the illustration's aspect ratio. Record the actual prompt, generator, known settings or seed, accepted PNG hash, dimensions and reason for selection. The bundled image pipeline supports 8-bit noninterlaced PNG, converts it to grayscale, and places it within a 75 mm square at 200 ppi or higher for viewing. Re-export the image when the format or effective resolution is outside that profile.

A fixed seed can make a supported image-generation process easier to repeat. Different generator versions can give different artwork. Use the adopted PNG as the immutable input for a repeat build of a particular edition.

## 7. Extract the assets and build

Save this document as UTF-8. Put the following cross-platform extractor into `extract.py` in the same directory. The embed delimiters use four backticks. Each asset's SHA-256 and UTF-8 byte count are checked before it is written. Use a fresh directory.

```python
from pathlib import Path
import hashlib
import re
import sys

if len(sys.argv) != 2:
    raise SystemExit("Usage: python3 extract.py Design_Specification_EN.md")
source = Path(sys.argv[1]).read_text(encoding="utf-8")
expected = {"portable_book.mjs", "layout-fixture.json", "cover-prompt.txt"}
pattern = r"^<!-- asset:([a-zA-Z0-9_.-]+) -->\n````[a-z]*\n(.*?)\n````$"
found = re.findall(pattern, source, re.M | re.S)
if len(found) != len(expected) or {name for name, _ in found} != expected:
    raise SystemExit("An appendix asset is missing or duplicated.")

checked = []
for name, body in found:
    row = re.search(r"\| `" + re.escape(name) + r"` \| (\d+) \| `([0-9a-f]{64})` \|", source)
    contents = (body + "\n").encode("utf-8")
    if row is None or int(row[1]) != len(contents) or row[2] != hashlib.sha256(contents).hexdigest():
        raise SystemExit("Appendix checksum mismatch for " + name)
    path = Path(name)
    if path.exists():
        raise SystemExit("Refusing to overwrite " + str(path))
    checked.append((path, contents))

for path, contents in checked:
    with path.open("xb") as stream:
        stream.write(contents)
    print("Verified and wrote", path)
```

```bash
python3 extract.py Design_Specification_EN.md
```

The compositor runs on a modern Node.js runtime with built-in filesystem, path and cryptographic modules. Use Node.js 22 for a fresh setup, record the exact runtime used, and compare two runs on that runtime. Python is used only for the extraction command. There are no package-manager dependencies. The production code creates no network connections.

Download the five static TTF files from Matplotlib's immutable v3.10.8 release tree. Keep the names intact. The compositor checks their hashes against the values in the appendix. [Font files and notices](https://github.com/matplotlib/matplotlib/tree/v3.10.8/lib/matplotlib/mpl-data/fonts/ttf)

| Static font | SHA-256 |
| --- | --- |
| `STIXGeneral.ttf` | `167378031e2dddc6216d67819c9260e9a06ffc4c478e4e23cb98a6fd44b183c2` |
| `STIXGeneralBol.ttf` | `e8533dc7083fa346bda1933d60ea4a83b67d0945bceaf1b3541f82b4a0e2c6a0` |
| `DejaVuSans.ttf` | `3fdf69cabf06049ea70a00b5919340e2ce1e6d02b0cc3c4b44fb6801bd1e0d22` |
| `DejaVuSans-Bold.ttf` | `b184b89e3c1075f22f6b71575b6fc20d4972b3cfd3b23322ca6fd596dcaef167` |
| `DejaVuSansMono.ttf` | `602ec86b8948cfcd956482fe64f94c36c867770149ef2f791d4613f443bcecb3` |

The following command downloads the same pinned files on a Bash-compatible system.

```bash
mkdir -p fonts
font_base='https://raw.githubusercontent.com/matplotlib/matplotlib/v3.10.8/lib/matplotlib/mpl-data/fonts/ttf'
for font_file in STIXGeneral.ttf STIXGeneralBol.ttf DejaVuSans.ttf DejaVuSans-Bold.ttf DejaVuSansMono.ttf
do
  curl -fL "${font_base}/${font_file}" -o "fonts/${font_file}" || exit 1
done
```

Write your new manuscript to book.json and place the adopted cover at the relative path in coverImage. The included layout-fixture.json is a quick technical test with a fictional chapter and no researched source claims. Pair it with a compatible generated cover for a build test. It has the same schema as the finished manuscript.

| Field | Value |
| --- | --- |
| `schema`, `title`, `language` | `1`, `The Little Book of Kaggle 1st Place Solutions`, `en` |
| `asOf`, `profile`, `coverImage` | YYYY-MM-DD source cutoff, `public` for a reviewed edition or `fixture` during layout tests, project-relative PNG path |
| `guide`, `prologue`, `epilogue`, `appendix` | An object with a `title` and ordered `blocks` array |
| `chapters` | Ordered array of objects with unique `id`, official `title` and exactly four arrays under `sections` |
| `sources` | Global `{id, title, url}` entries. Use HTTPS with ASCII percent encoding in URLs. |

| Block | Fields |
| --- | --- |
| `p` | `text` with optional `[[SOURCE-ID]]` markers. Spaces are normalized for layout. |
| `h` | `text` for a subheading followed by a paragraph. |
| `table` | `title, columns, rows` and optional positive `weights` and `note`. Two to five string columns. |
| `figure` | `title, steps` with two to six string labels. |
| `formula` | `text` for a scalar expression or `lhs, numerator, denominator` and optional `root: true`. |
| `code` | String `code` with LF and spaces, `language` of `javascript`, `python` or `text`, optional `title` and exact `expected` standard output for runnable examples. |

Set `type` to the listed block name. Begin every section with prose or a subheading and its paragraph. Keep figures and tables in competition chapters. The embedded fonts cover the viewing profile's Latin English text and supported WinAnsi characters. Check accented spellings and mathematical glyphs as you write. For a name or equation outside this character set, preserve the exact original in the source ledger and use an accepted English transliteration or extend and validate the font and math profile. The compositor reports unsupported characters.

The commands below use an empty release-a and release-b. A build directory becomes complete when its manifest is written. A second build runs the compositor again. It has a different build ID even when every PDF byte is the same.

```bash
node portable_book.mjs build book.json release-a fonts
node portable_book.mjs build book.json release-b fonts
node portable_book.mjs audit book.json release-a fonts
node portable_book.mjs compare release-a release-b
node portable_book.mjs render release-a/book.pdf review-a fonts
```

The viewing PDF is `book.pdf`. `interior.pdf` and `front-cover.pdf` provide separate components for inspection. Preserve the source JSON, artwork and source records with the exact code and font hashes. Save the links and identifiers that disclose the versions of any original auxiliary materials. Package the finished edition's source and verification records together.

## 8. Run the checks and repeat after fixes

Use a second editorial pass with source passages and manuscript side by side. A second reviewer or independent review session is preferred. Identify the reviewer and the actual scope. Record one specific observation for each of these eight fields in content-review.json.

| Field | Check |
| --- | --- |
| competition_identity | Official title, track, date, rank and attribution agree with source records. |
| task_metric_constraints | Required input and output, score direction and aggregation, constraints and hidden information are correct. |
| winner_solution_sources | Each material winning component is attributed and supported. |
| examples_and_math | Hand calculations, scales, examples and comparisons agree with the text and the actual printed formula. |
| figures_and_text | Both figures per chapter match the prose and carry usable labels. |
| code_execution_scope | Each executable teaching listing was run, with its exact bytes, runtime, expected value and actual output recorded. |
| reconstructed_path_labeling | The proposed investigation is clearly an editorial reconstruction with tests and decision points. |
| chapter_structure_and_endmatter | Chapters have four full sections, exercise and review, and all front and back matter is present. |

Run the technical audit and examine all pages at a readable size, including the cover and deliberate blanks. Look for clipped glyphs, broken words, sparse spill pages, isolated headings or citations, unclear table continuations, visual math, missing code, mismatched captions, stale page numbers and loss of figure detail. Check the original cover image and the composed cover. Record every physical PDF page and its raster hash, using the raster-index.json generated by render. The viewing PDF counts the cover as PDF page 1, before interior folio 1.

Inspect the main edition and at least one reordered or extended fixture. Include a long official name, table continuation and long code line. Challenge the auditor with damaged copies that move or resize body text, change a code character or omit a figure stroke. Correct the cause of each issue. A layout change can alter subsequent pages, chapter folios and the contents. Render the changed pages again. An existing approval can carry over to a page whose raster hash remains identical at the same settings. Archive the review notes and repeat until the edition files have no unresolved findings.

## 9. Confirm the release conditions

Keep the following five acceptance conditions together in the production record.

1. The input has public review status, essential competition claims and source locators, exact teaching runs, and a new cover's generation record.
2. The eight editorial checks pass for the same manuscript and evidence ledger.
3. The technical audit passes for the full viewing PDF and separate components.
4. Every page has a visual review record for the exact final viewing PDF, with no outstanding issues.
5. Independent builds use identical accepted inputs and produce matching PDF hashes.

Use these record shapes. Values in the verification package show one filled example for each role.

| File | Fields |
| --- | --- |
| `evidence.json` | `sources` entries with `id, date, access, locator`; `claims` entries with `id, location, category, text, sources, essential, status`; `examples` with listing `id, source_sha256, runtime, exit_code, stdout`; `cover` with `prompt, generator, selection, date, generated_for, png_sha256` and known dimensions and settings |
| `content-review.json` | `input_sha256, evidence_sha256, reviewer, open_issues, checks`. Under `checks`, each of the eight fields contains `{status: 'pass', note: '<observed check>'}`. |
| `visual-review.json` | `pdf_sha256, dpi, reviewer, open_issues, pages`. Per-page objects contain `pdf_page, raster_sha256, pass, note`. Use physical viewing PDF page numbers. |
| `manifest.json` | Generated build identifier, hashes, page counts and technical audit. |
| Release report | Return value from the release command. Keep the output with the input, evidence and manifests. |

For chapter blocks, use `chapter-id-section/block`, for example `river-forecast-1/3`. Sections and blocks count from one. The essential claim categories are `task`, `metric`, `rank` and `method`. Use access values `direct`, `pinned-code` or `verified-excerpt` for inspected records, and `supported` or `limited` for a claim in review. Essential claims must be supported. The manifest supplies the exact manuscript and cover digests. Compute `evidence_sha256` over the parsed evidence object serialized using JavaScript's `JSON.stringify(evidence, null, 2) + "\n"`. Hash each teaching listing's exact source string as UTF-8. Match its recorded stdout to the `expected` field, allowing the archived record to trim a single terminal newline consistently.

```bash
node portable_book.mjs release book.json release-a release-b fonts evidence.json content-review.json visual-review.json
```

A completed review returns `pass: true` and `public_release_ready: true`. A build by itself marks its manifest `public_release_ready: false`. When you edit content, art, source records or layout, rerun the affected checks for the new files and produce a new report.

The release command checks record integrity and pixel hashes. It cannot certify that a source says what a reviewer recorded or that someone actually inspected the page. Use honest editorial and visual attestations. Do not train contestants' full solutions solely to populate release reports. A full winning-score replay is its own experiment. When you distribute a new edition, include method attribution and the source links readers need to verify it. Follow the commissioning reader's publication instructions.


## 10. Verification edition

In November 2026 the English specification was used to write and build two new chapters on time-series forecasting and image-and-text retrieval. It exercised the full chapter sequence and the same design features on fresh source material.

| Test | Observed result |
| --- | --- |
| M5 Forecasting - Accuracy | Interior folios 7–21, with four sections, RMSSE example and two new diagrams |
| Shopee - Price Match Guarantee | Interior folios 23–36, with four sections, mean F1 example and two new diagrams |
| Viewing edition | 41 PDF pages, including 40 interior pages and a newly generated front cover |
| Content and paper geometry | 10 source entries, 18 essential claims, four diagrams, four tables, two runnable listings and 49 links audited. All 41 page proofs reviewed with the embedded outline fonts. |
| Executed teaching listings | RMSSE 0.707107; mean row F1 0.828571. Both used invented data. |
| Independent build | All three PDF hashes identical with accepted inputs, two independent build IDs and separate input/output paths in the filesystem test adapter. |
| Changed chapter order | Both real chapters remained on odd openings and contents and references resolved after reversal. |
| Layout stress edition | Seven synthetic chapters and 53 viewing pages tested a two-page contents sequence, repeated table headings, long titles, long code and the formula renderer. |
| Deliberate damage | Rejected a changed body size, changed citation size, out-of-frame line, altered code character and missing vector stroke. |
| Review guardrails | Missing teaching runs, missing visual coverage, fixture input and comparison with the same directory were rejected. |

Successive passes corrected an isolated citation, shortened code lines at syntactic boundaries, removed thin spill pages and verified the distance exception and final single-view union in the Shopee write-up. The final PDF was regenerated and inspected. The test ran the bundled compositor and auditor in a V8 runtime, with the Node CLI file flow exercised through an isolated filesystem adapter. A system-installed Node command and external PDF-viewer compatibility were outside this run. Training and submitting either winner's full solution were outside the verification scope.

| Fixed artifact | SHA-256 |
| --- | --- |
| Viewing PDF | `b0367e9dd631c7f03ac56e7a0256d4b11e56b82274806a74e8d438535b0b2ed7` |
| Interior PDF | `c94d39753f86125d55803066c1ab212da056f6bfa37a4979b10830e78559a479` |
| Front cover PDF | `6238060be37fd1ceaf583f3aaa2ecaf46cd2b642fbdc698821a98a87903bd7f2` |
| Adopted cover PNG | `890d96ec5c13a63c0f5f06b01ddc1e8ff568a35a84b0c7c1cf2d5e72cd56ffe2` |
| Exact manuscript JSON | `2e0601593f6dc8acf67f0e03ca01d9c06709b763c1ba90b93b3ba1d4e1adba7a` |

The source package contains the manuscript, the adopted image, review records and output manifests for this test edition. Combine those with the code and pinned fonts in the specification to repeat the build. For a fresh edition, start from a new competition list and generate cover art for that edition.


## 11. Portable source and assets

The appendix contains UTF-8 text assets. Save generated illustration files in the individual edition's source package. Each row below describes the file produced by the extraction command, including its final LF.

| Asset | Bytes | SHA-256 |
| --- | ---: | --- |
| `portable_book.mjs` | 74612 | `18b472fe808557b5e3d9bc5f17a2fd56bc442b20f0b2ddd351524fbfac1a39e0` |
| `layout-fixture.json` | 15259 | `cabc37986b2d204878d39b2f3f3043b0da5e5b7325ff0bde9cea1f3dbfefa807` |
| `cover-prompt.txt` | 1074 | `d251bc3367ae63e45b10cff02f4b9c3ff6a2e19edca518e174116c5de6cec637` |

### portable_book.mjs

<!-- asset:portable_book.mjs -->
````javascript
import { readFile, writeFile, mkdir, rm } from "node:fs/promises";
import { dirname, isAbsolute, resolve, join } from "node:path";
import { fileURLToPath } from "node:url";
import { createHash, randomUUID } from "node:crypto";

function imageKernel(){
  function requireThat(condition, message) { if (!condition) throw Error(message); }
  function concat(parts) {
    const out = new Uint8Array(parts.reduce((n, p) => n + p.length, 0));
    let offset = 0;
    for (const part of parts) { out.set(part, offset); offset += part.length; }
    return out;
  }
  function uint32(bytes, i) { return (bytes[i] * 0x1000000 + (bytes[i + 1] << 16) + (bytes[i + 2] << 8) + bytes[i + 3]) >>> 0; }
  function byteString(bytes) {
    let out = "";
    for (let i=0; i<bytes.length; i+=16384) out += String.fromCharCode(...bytes.subarray(i,i+16384));
    return out;
  }
  function latinBytes(str) { return Uint8Array.from(str, c => c.charCodeAt(0)); }
  function adler32(data) {
    let a=1, b=0;
    for (const value of data) { a=(a+value)%65521; b=(b+a)%65521; }
    return ((b << 16) | a) >>> 0;
  }
  function reverse(v,n) {
    let r=0;
    while(n-- > 0) { r=(r << 1) | (v & 1); v >>>= 1; }
    return r;
  }
  function huffman(lens) {
    const counts=Array(16).fill(0), first=Array(16).fill(0), codes=[], symbols=new Map();
    for (const n of lens) if(n) counts[n]++;
    for(let n=1;n<16;n++) first[n]=(first[n-1]+counts[n-1])<<1;
    lens.forEach((n,i)=>{
      if(n) {
        const bits = reverse(first[n]++,n);
        codes[i] = [bits,n];
        symbols.set((1<<n)+bits,i);
      }
    });
    return {codes,symbols};
  }
  const lens=Array.from({length:288},(_,i)=>i<144?8:i<256?9:i<280?7:8);
  const fixedA=huffman(lens), fixedB=huffman(Array(32).fill(5));
  const lengths=[3,4,5,6,7,8,9,10,11,13,15,17,19,23,27,31,35,43,51,59,67,83,99,115,131,163,195,227,258];
  const lengthBits=[0,0,0,0,0,0,0,0,1,1,1,1,2,2,2,2,3,3,3,3,4,4,4,4,5,5,5,5,0];
  const distances=[1,2,3,4,5,7,9,13,17,25,33,49,65,97,129,193,257,385,513,769,1025,1537,2049,3073,4097,6145,8193,12289,16385,24577];
  const distanceBits=[0,0,0,0,1,1,2,2,3,3,4,4,5,5,6,6,7,7,8,8,9,9,10,10,11,11,12,12,13,13];
  function inflate(bytes, size) {
    requireThat(size>=0 && size<=120000000,"Invalid inflated size");
    const out=new Uint8Array(size);
    requireThat(bytes.length>=6 && (bytes[0]&15)===8 && ((bytes[0]<<8)+bytes[1])%31===0 && !(bytes[1]&32),"Unsupported zlib header");
    let p=16,i=0;
    function get(n) {
      requireThat(p+n <= (bytes.length-4)*8,"Truncated deflate stream");
      let value=0;
      for(let j=0;j<n;j++,p++) value|=((bytes[p>>>3] >>> (p&7))&1)<<j;
      return value;
    }
    function symbol(tree) {
      let value=0;
      for(let n=1;n<=15;n++) {
        value|=get(1)<<(n-1);
        const id=tree.symbols.get((1<<n)+value);
        if(id!==undefined) return id;
      }
      throw Error("Invalid Huffman code");
    }
    function put(v) { requireThat(i<size,"Inflated data exceeds expected size"); out[i++]=v; }
    let last;
    do{
      last=get(1);
      const kind=get(2);
      if(kind===0) {
        p=Math.ceil(p/8)*8;
        const n=get(16);
        requireThat((n^get(16))===65535,"Invalid stored block");
        for(let k=0;k<n;k++) put(get(8));
        continue;
      }
      requireThat(kind!==3,"Reserved deflate block type");
      let a=fixedA,b=fixedB;
      if(kind===2) {
        const n=get(5)+257,m=get(5)+1,k=get(4)+4;
        const order=[16,17,18,0,8,7,9,6,10,5,11,4,12,3,13,2,14,1,15];
        const cl=Array(19).fill(0), codings=[];
        for(let l=0;l<k;l++) cl[order[l]]=get(3);
        const t=huffman(cl);
        while(codings.length<n+m) {
          const s=symbol(t);
          if(s<16) codings.push(s);
          else {
            requireThat(s!==16||codings.length>0,"Missing repeated code");
            const repeats=s===16?get(2)+3:s===17?get(3)+3:get(7)+11;
            const value=s===16?codings.at(-1):0;
            for(let l=0;l<repeats;l++) codings.push(value);
          }
        }
        requireThat(codings.length===n+m,"Invalid code count");
        a=huffman(codings.slice(0,n)); b=huffman(codings.slice(n));
      }
      for(;;) {
        const s=symbol(a);
        if(s<256) put(s);
        else if(s===256) break;
        else {
          const j=s-257;
          requireThat(j<lengths.length,"Invalid match length");
          const count=lengths[j]+get(lengthBits[j]), d=symbol(b);
          requireThat(d<distances.length,"Invalid match distance");
          const dist=distances[d]+get(distanceBits[d]);
          requireThat(dist<=i,"Match precedes data");
          for(let q=0;q<count;q++) put(out[i-dist]);
        }
      }
    }while(!last);
    requireThat(i===size && adler32(out)===uint32(bytes,bytes.length-4),"Decoded byte count or checksum differs");
    return out;
  }
  function deflate(raw) {
    const out=[0x78,0x01], previous=new Int32Array(raw.length), heads=new Int32Array(65536);
    heads.fill(-1);
    let pending=0,nBits=0;
    function put(v,n) {
      pending|=v<<nBits; nBits+=n;
      while(nBits>=8) { out.push(pending&255); pending>>>=8; nBits-=8; }
    }
    function code(tree,n){ put(...tree.codes[n]); }
    function hash(i) { return ((raw[i]*251+raw[i+1])*251+raw[i+2])&65535; }
    function track(i) {
      if(i+2>=raw.length) return;
      const h=hash(i); previous[i]=heads[h]; heads[h]=i;
    }
    function bucket(arr, x) {
      let first=0, end=arr.length;
      while(first+1<end) {
        const mid=(first+end)>>>1;
        if(arr[mid]<=x) first=mid; else end=mid;
      }
      return first;
    }
    put(3,3);
    for(let i=0;i<raw.length;){
      let length=2,distance=0;
      if(i+2<raw.length) {
        const limit=Math.min(258,raw.length-i);
        for(let j=heads[hash(i)], n=0;j>=0&&i-j<=32768&&n<32&&length<limit;j=previous[j],n++){
          if(raw[j+length]!==raw[i+length]) continue;
          let k=0;
          while(k<limit && raw[j+k]===raw[i+k]) k++;
          if(k>length) { length=k; distance=i-j; }
        }
      }
      if(length>=3) {
        const v=bucket(lengths,length),d=bucket(distances,distance);
        code(fixedA,257+v); put(length-lengths[v],lengthBits[v]);
        code(fixedB,d); put(distance-distances[d],distanceBits[d]);
        for(let j=0;j<length;j++) track(i++);
      } else {
        code(fixedA,raw[i]); track(i++);
      }
    }
    code(fixedA,256);
    if(nBits) out.push(pending);
    const adler=adler32(raw);
    for(let n=24;n>=0;n-=8) out.push((adler>>>n)&255);
    return Uint8Array.from(out);
  }
  function decodePng(bytes) {
    requireThat(uint32(bytes,0)===0x89504e47&&uint32(bytes,4)===0x0d0a1a0a,"PNG signature required");
    let w=0,h=0,s=0;
    const data=[];
    for(let i=8;i+12<=bytes.length;) {
      const length=uint32(bytes,i), type=byteString(bytes.subarray(i+4,i+8));
      requireThat(i+12+length<=bytes.length,"Truncated PNG chunk");
      if(type==="IHDR") {
        w=uint32(bytes,i+8); h=uint32(bytes,i+12);
        s=({0:1,2:3,4:2,6:4})[bytes[i+17]];
        requireThat(w>0&&h>0&&w<=4500&&h<=4500&&bytes[i+16]===8&&s&&bytes[i+18]===0&&bytes[i+19]===0&&bytes[i+20]===0,"Use noninterlaced 8-bit RGB, RGBA, grayscale, or grayscale-alpha PNG");
      } else if(type==="IDAT") data.push(bytes.subarray(i+8,i+8+length));
      else if(type==="IEND") break;
      i+=length+12;
    }
    requireThat(w&&h&&data.length,"PNG header or image data missing");
    const row=w*s, decoded=inflate(concat(data),(row+1)*h), pixels=new Uint8Array(w*h);
    let prior=new Uint8Array(row);
    function paeth(a,b,c) {
      const p=a+b-c, da=Math.abs(p-a), db=Math.abs(p-b), dc=Math.abs(p-c);
      return da<=db&&da<=dc?a:db<=dc?b:c;
    }
    for(let y=0;y<h;y++) {
      const i=y*(row+1), f=decoded[i], line=decoded.subarray(i+1,i+1+row);
      requireThat(f<=4,"Unsupported PNG filter");
      for(let j=0;j<row;j++) {
        const a=j>=s?line[j-s]:0,b=prior[j],c=j>=s?prior[j-s]:0;
        const prediction=f===0?0:f===1?a:f===2?b:f===3?((a+b)>>1):paeth(a,b,c);
        line[j]=(line[j]+prediction)&255;
      }
      for(let x=0;x<w;x++){
        const j=x*s, alpha=s%2===0?line[j+s-1]:255;
        const gray=s<3?line[j]:Math.round(.2126*line[j]+.7152*line[j+1]+.0722*line[j+2]);
        pixels[y*w+x]=255-Math.round((255-gray)*alpha/255);
      }
      prior=line;
    }
    return {width:w,height:h,pixels};
  }
  function coverFromPng(bytes){
    const {width:w,height:h,pixels}=decodePng(bytes);
    requireThat(Math.min(w,h)>=350,"Cover must have at least 350 pixels on its short side");
    const scale=Math.min(1,600/Math.max(w,h)), width=Math.round(w*scale), height=Math.round(h*scale);
    const out=new Uint8Array(width*height);
    for(let y=0;y<height;y++) for(let x=0;x<width;x++) {
      let t=0,n=0;
      const top=Math.floor(y*h/height),bottom=Math.floor((y+1)*h/height);
      const left=Math.floor(x*w/width),right=Math.floor((x+1)*w/width);
      for(let yy=top;yy<bottom;yy++) for(let xx=left;xx<right;xx++) {
        t+=pixels[yy*w+xx]; n++;
      }
      const value=t/n;
      out[y*width+x]=value>=244?255:Math.min(240,Math.round(value/4)*4);
    }
    for(let x=0;x<width;x++) if(out[x]<235||out[(height-1)*width+x]<235) throw Error("Cover has marks at the top or bottom edge");
    for(let y=0;y<height;y++) if(out[y*width]<235||out[y*width+width-1]<235) throw Error("Cover has marks at the side edge");
    for(let x=0;x<width;x++){out[x]=255;out[(height-1)*width+x]=255;}
    for(let y=0;y<height;y++){out[y*width]=255;out[y*width+width-1]=255;}
    requireThat(out.some(x=>x<100),"Cover illustration is missing");
    return {width,height,pixels:out};
  }
  return {requireThat,concat,uint32,byteString,latinBytes,inflate,deflate,decodePng,coverFromPng};
}

function fontKernel(){
  const {requireThat:assert,concat,latinBytes,byteString}=imageKernel();
  const ext="€\u0081‚ƒ„…†‡ˆ‰Š‹Œ\u008dŽ\u008f\u0090‘’“”•–—˜™š›œ\u009džŸ";
  const decode=c=>c>=128&&c<160?ext[c-128]:String.fromCharCode(c);
  const cp1252=Array.from({length:224},(_,i)=>decode(i+32));
  const wrapView=data=>new DataView(data.buffer,data.byteOffset,data.byteLength);
  const align4=n=>Math.ceil(n/4)*4;
  function sum(data){
    let s=0;const v=wrapView(data);
    for(let i=0;i+4<=data.length;i+=4)s=(s+v.getUint32(i))>>>0;
    let last=0;
    for(let i=data.length-data.length%4,d=24;i<data.length;i++,d-=8)last|=data[i]<<d;
    return (s+last)>>>0;
  }
  function sfnt(tables,payload){
    const sorted=[...tables.keys()].sort(), header=new Uint8Array(12+16*sorted.length), v=wrapView(header);
    v.setUint32(0,0x00010000);v.setUint16(4,sorted.length);
    const lr=Math.floor(Math.log2(sorted.length)),sr=16*(2**lr);
    v.setUint16(6,sr);v.setUint16(8,lr);v.setUint16(10,16*sorted.length-sr);
    const parts=[header];let offset=header.length, h;
    for(const [i,tag] of sorted.entries()){
      const data=tables.get(tag), record=12+16*i;
      header.set(latinBytes(tag),record);v.setUint32(record+4,sum(data));
      v.setUint32(record+8,offset);v.setUint32(record+12,data.length);
      if(tag==="head")h=offset;
      parts.push(data); const extra=align4(data.length)-data.length;
      if(extra)parts.push(new Uint8Array(extra));
      offset+=align4(data.length);
    }
    const out=concat(parts);
    wrapView(out).setUint32(h+8,(0xb1b0afba-sum(out))>>>0);
    return out;
  }
  function read(bytes){
    const v=wrapView(bytes), tables=new Map();
    assert(v.getUint32(0)===65536,"A static TrueType font with glyf outlines is required");
    const n=v.getUint16(4);
    for(let i=0;i<n;i++){
      const r=12+16*i,tag=byteString(bytes.slice(r,r+4));
      const a=v.getUint32(r+8),b=v.getUint32(r+12);
      tables.set(tag,bytes.subarray(a,a+b));
    }
    const d=x=>wrapView(tables.get(x));
    const head=d("head"),hhea=d("hhea"),hmtx=d("hmtx"),cm=d("cmap");
    const em=head.getUint16(18), num=d("maxp").getUint16(4), metrics=hhea.getUint16(34), long=head.getInt16(50)===1;
    const off=d("loca");
    const loca=Array.from({length:num+1},(_,i)=>long?off.getUint32(i*4):off.getUint16(i*2)*2);
    const glyphs=tables.get("glyf"),glyf=i=>glyphs.subarray(loca[i],loca[i+1]);
    const os=d("OS/2"),rights=os.getUint16(8);
    assert((rights&2)===0&&(rights&256)===0&&(rights&512)===0,"This TrueType font bars the required outline embedding or subsetting");
    const tab=Array.from({length:cm.getUint16(2)},(_,i)=>{
      const r=4+8*i, off=cm.getUint32(r+4);
      return {platform:cm.getUint16(r),enc:cm.getUint16(r+2),off,fmt:cm.getUint16(off)};
    });
    const cmap=tab.find(x=>x.platform===3&&x.enc===10&&x.fmt===12)??tab.find(x=>x.platform===3&&x.enc===1&&x.fmt===4)??tab.find(x=>x.fmt===4);
    assert(cmap,"No usable Unicode cmap");
    function gid(code){
      const base=cmap.off;
      if(cmap.fmt===12){
        let lo=0,hi=cm.getUint32(base+12);
        while(lo<hi){
          const m=(lo+hi)>>>1,r=base+16+12*m;
          const min=cm.getUint32(r),max=cm.getUint32(r+4);
          if(code<min)hi=m;else if(code>max)lo=m+1;else return cm.getUint32(r+8)+code-min;
        }
        return 0;
      }
      if(code>65535)return 0;
      const sg=cm.getUint16(base+6)/2, end=base+14,start=end+sg*2+2,delta=start+sg*2,ofs=delta+sg*2;
      for(let i=0;i<sg;i++){
        if(cm.getUint16(end+2*i)<code)continue;
        const first=cm.getUint16(start+2*i);
        if(first>code)return 0;
        const fix=cm.getInt16(delta+2*i), seek=cm.getUint16(ofs+2*i);
        if(seek===0)return (code+fix)&65535;
        const g=cm.getUint16(ofs+2*i+seek+2*(code-first));
        return g?(g+fix)&65535:0;
      }
      return 0;
    }
    function components(g){
      const data=glyf(g), out=[];
      if(data.length<10||wrapView(data).getInt16(0)>=0)return out;
      const q=wrapView(data);let p=10,f;
      do{
        f=q.getUint16(p);
        const j=q.getUint16(p+2);
        let dx=0,dy=0;
        if(f&2){dx=f&1?q.getInt16(p+4):q.getInt8(p+4);dy=f&1?q.getInt16(p+6):q.getInt8(p+5);}
        p+=4+(f&1?4:2);
        let a=1,b=0,c=0,d=1;
        if(f&8){a=d=q.getInt16(p)/16384;p+=2;}
        if(f&64){a=q.getInt16(p)/16384;d=q.getInt16(p+2)/16384;p+=4;}
        if(f&128){a=q.getInt16(p)/16384;b=q.getInt16(p+2)/16384;c=q.getInt16(p+4)/16384;d=q.getInt16(p+6)/16384;p+=8;}
        out.push({j,dx,dy,a,b,c,d,hasOffsets:Boolean(f&2)});
      }while(f&32);
      return out;
    }
    const glyphMap=new Map(cp1252.map(c=>[c,gid(c.codePointAt(0))]));
    const advance=g=>hmtx.getUint16(Math.min(g,metrics-1)*4);
    function measure(c){
      const g=glyphMap.get(c);
      assert(g,"Unsupported font character "+JSON.stringify(c));
      return Math.round(advance(g)*1000/em);
    }
    function subset(){
      const use=new Set([0]);
      function add(g){
        if(use.has(g))return;
        use.add(g);
        for(const sub of components(g))add(sub.j);
      }
      for(const g of glyphMap.values())add(g);
      const zeroHead=tables.get("head").slice(), b=wrapView(zeroHead);
      b.setUint32(8,0);b.setInt16(50,1);
      const loc=new Uint8Array((num+1)*4), u=wrapView(loc), chunks=[];
      let pos=0;
      for(let j=0;j<=num;j++){
        u.setUint32(4*j,pos);
        if(j===num||!use.has(j))continue;
        const g=glyf(j);
        chunks.push(g);
        const extra=align4(g.length)-g.length;
        if(extra)chunks.push(new Uint8Array(extra));
        pos+=align4(g.length);
      }
      const out=new Map([...tables].filter(([k])=>["OS/2","cmap","cvt ","fpgm","gasp","hhea","hmtx","maxp","name","post","prep"].includes(k)));
      const ps=out.get("post");
      if(ps){
        const v=ps.slice(0,32);wrapView(v).setUint32(0,0x00030000);out.set("post",v);
      }
      out.set("head",zeroHead);out.set("loca",loc);out.set("glyf",concat(chunks));
      return sfnt(out);
    }
    const outlineCache=new Map();
    function contours(g){
      if(outlineCache.has(g))return outlineCache.get(g);
      const b=glyf(g);
      if(b.length<10)return [];
      const x=wrapView(b),num=x.getInt16(0),ret=[];
      if(num<0){
        for(const c of components(g)){
          assert(c.hasOffsets,"Preview requires positioned composite glyphs");
          for(const r of contours(c.j)) ret.push(r.map(p=>({...p,x:p.x*c.a+p.y*c.c+c.dx,y:p.x*c.b+p.y*c.d+c.dy})));
        }
      }else if(num>0){
        const ends=Array.from({length:num},(_,i)=>x.getUint16(10+2*i));
        const count=ends.at(-1)+1;
        let k=10+num*2;k+=2+x.getUint16(k);
        const flags=[];
        while(flags.length<count){const f=b[k++];flags.push(f);if(f&8){let rep=b[k++];while(rep-->0)flags.push(f);}}
        const coord=(short,same)=>{
          let a=0;
          return flags.map(f=>{if(f&short)a+=(f&same?1:-1)*b[k++];else if(!(f&same)){a+=x.getInt16(k);k+=2;}return a;});
        };
        const xs=coord(2,16),ys=coord(4,32);
        for(let s=0,i=0;i<ends.length;i++){
          const r=[];
          for(;s<=ends[i];s++)r.push({x:xs[s],y:ys[s],on:Boolean(flags[s]&1)});
          ret.push(r);
        }
      }
      outlineCache.set(g,ret);return ret;
    }
    const post=d("post"), scale=x=>Math.round(x*1000/em);
    const box=[36,38,40,42].map(i=>scale(head.getInt16(i)));
    return {metric:measure,glyphMap,cp1252,em,subset,contours,desc:{box,ascent:scale(hhea.getInt16(4)),descent:scale(hhea.getInt16(6)),cap:os.byteLength>=90?scale(os.getInt16(88)):scale(hhea.getInt16(4)),angle:post.getInt32(4)/65536}};
  }
  return {read,decode,cp1252};
}

function bookKernel(fontSources) {
  const {requireThat,byteString,latinBytes,deflate}=imageKernel();
  const mm=72/25.4, W=108*mm, H=175*mm, TOP=39, END=H-15*mm, LEFT=13*mm, OUT=10*mm, BW=W-LEFT-OUT;
  const TITLE=["The Little Book","of","Kaggle 1st Place Solutions"];
  const HEADS=["The Task","A Baseline Solution","The First-Place Solution","How to Find the Winning Approach Yourself"];
  const fonts=["STIXGeneral-Regular","STIXGeneral-Bold","DejaVuSans","DejaVuSans-Bold","DejaVuSansMono"];
  const fontUtil=fontKernel();
  requireThat(Array.isArray(fontSources)&&fontSources.length===fonts.length,"Provide all five pinned TrueType fonts");
  const faces=fontSources.map(fontUtil.read);
  const winExt="€\u0081‚ƒ„…†‡ˆ‰Š‹Œ\u008dŽ\u008f\u0090‘’“”•–—˜™š›œ\u009džŸ";
  function faceCode(c) {
    const cp=c.codePointAt(0);
    if(cp>=32&&cp<=126||cp>=160&&cp<=255) return cp;
    const i=winExt.indexOf(c);
    if(i!==-1&&cp>=256) return 128+i;
    throw Error("No WinAnsi glyph for "+JSON.stringify(c)+". Keep the source spelling in the ledger and use an accepted English display form or extend the font profile.");
  }
  function width(s,font,size){
    const face=faces[font-1];
    return Array.from(s).reduce((sum,c)=>{ faceCode(c);return sum+face.metric(c); },0)*size/1000;
  }
  function pdfText(s){
    return "("+Array.from(s,c=>{
      const byte=faceCode(c);
      if(byte>126) return "\\"+byte.toString(8).padStart(3,"0");
      return /[()\\]/.test(c)?"\\"+c:c;
    }).join("")+")";
  }
  function rawLiteral(s) {
    requireThat(/^[\x20-\x7e]*$/.test(s),"Use an ASCII percent-encoded URI");
    return "("+s.replace(/[()\\]/g,"\\$&")+")";
  }
  function words(s) { return s.trim().split(/\s+/).filter(Boolean); }
  function wrap(s,font,size,room,{split=false}={}) {
    const lines=[], current=[];
    function push(){ if(current.length) lines.push(current.join(" "));current.length=0; }
    for(const word of words(s)){
      let w=word;
      if(width(current.concat(w).join(" "),font,size)>room) push();
      if(width(w,font,size)>room){
        requireThat(split,"Unbreakable text exceeds the frame: "+w);
        while(width(w,font,size)>room) {
          const chars=Array.from(w);
          let j=1;
          while(j<chars.length&&width(chars.slice(0,j+1).join(""),font,size)<=room) j++;
          lines.push(chars.slice(0,j).join(""));w=chars.slice(j).join("");
        }
      }
      if(w) current.push(w);
    }
    push();
    return lines;
  }
  function ellipsis(value,font,size,room){
    if(width(value,font,size)<=room) return value;
    const chars=Array.from(value);
    while(chars.length && width(chars.join("")+"…",font,size)>room) chars.pop();
    return chars.join("").trimEnd()+"…";
  }
  function checkBook(book){
    requireThat(book?.schema===1&&book.title===TITLE.join(" "),"Unsupported book schema or title");
    requireThat(/^\d{4}-\d{2}-\d{2}$/.test(book.asOf),"Set the source cutoff as YYYY-MM-DD");
    requireThat(book.chapters?.length>=1&&book.chapters.length<=25,"Include 1 to 25 chapters; extend and test larger configurations");
    requireThat(new Set(book.chapters.map(c=>c.id)).size===book.chapters.length,"Repeated chapter ID");
    const given=new Set((book.sources??[]).map(s=>s.id));
    requireThat(given.size===(book.sources??[]).length,"Repeated source ID");
    for(const s of book.sources??[]) requireThat(/^[A-Z0-9-]+$/.test(s.id)&&/^https:\/\/[!-~]+$/.test(s.url)&&typeof s.title==="string","Invalid source");
    for(const c of book.chapters) {
      requireThat(/^[a-z0-9][a-z0-9-]+$/.test(c.id)&&c.title&&c.sections?.length===4,"Invalid chapter ID, title or section count");
      requireThat(c.sections.every(s=>Array.isArray(s)&&s.length>0),"Empty chapter section");
    }
    for(const unit of [book.guide,book.prologue,book.epilogue,book.appendix]) requireThat(unit?.title&&unit.blocks?.length,"Required English front or back matter is missing");
    for(const unit of [book.prologue,book.epilogue,book.appendix]) requireThat(unit.title.length<140,"Front or back matter title length");
  }
  function layout(book,cover,previous={},titleOnly=false) {
    checkBook(book);
    requireThat(cover.width*cover.height===cover.pixels.length&&Math.min(cover.width,cover.height)>=320,"Invalid grayscale cover");
    const pages=[],anchors={},checkpoints=[],expectedText=[];
    let pg, y, active=null, label="", tocPage=0, seq={figure:0,table:0}, id="";
    const references=new Map((book.sources??[]).map(s=>[s.id,s]));
    function emit(command){pg.ink.push(command);}
    function text(s,x,base,font,size,role,cid="",align="left") {
      if(!s) return;
      const w=width(s,font,size);
      const left=x-(align==="right"?w:align==="center"?w/2:0);
      requireThat(Number.isFinite(w)&&left>=-.01&&left+w<=W+.01&&base>=size&&base<=H,"Text leaves the page: "+s);
      emit({kind:"text",s,x:left,y:base,font,size,role,id:cid,w});
    }
    function ln(x1,y1,x2,y2,w=.75,g=.2){ emit({kind:"line",x1,y1,x2,y2,w,g}); }
    function rect(x,y,w,h,{fill=null,stroke=null,weight=.75}={}){emit({kind:"rect",x,y,w,h,fill,stroke,weight});}
    function link(x,y,w,h,to,url=false){emit({kind:"link",x,y,w,h,to,url});}
    function newPage(role) {
      const n=pages.length,e=role==="cover"?LEFT:n%2?LEFT:OUT;
      pg={number:n,role,chapter:active?.n??null,x:e,ink:[]};
      pages.push(pg);
      y=TOP;
      if(n>0&&role!=="blank"&&role!=="title") {
        text(String(n),n%2?e+BW:e,H-9*mm,3,7,"folio","",n%2?"right":"left");
        if(n%2&&active&&role==="chapter") text(ellipsis(active.heading,3,7,BW),e+BW,25,3,7,"running head","","right");
      }
      return pg;
    }
    function pageBreak() { newPage(label); }
    function recto(role) {
      if(pages.length%2===0) newPage("blank");
      newPage(role);
    }
    function need(height) {
      requireThat(height<=END-TOP+.001,"Block is taller than the page");
      if(y+height>END+.001) pageBreak();
    }
    function anchor(key) {requireThat(anchors[key]===undefined,"Duplicate anchor "+key);anchors[key]=pg.number;}
    function heading(s,font,size,gap,role,key="",keep=27,topGap=0) {
      const lines=wrap(s,font,size,BW), lead=size*1.26;
      need(topGap+lines.length*lead+gap+keep);
      if(y>TOP+.01)y+=topGap;
      if(key) anchor(key);
      for(const line of lines){text(line,pg.x,y+size,font,size,role);y+=lead;}
      y+=gap;
    }
    function bookTitle() {
      let base=107;
      for(const line of TITLE){text(line,W/2,base,2,17,"title","","center");base+=22;}
    }
    newPage("cover");bookTitle();
    const maxW=75*mm,maxH=75*mm,scale=Math.min(maxW/cover.width,maxH/cover.height), iw=scale*cover.width,ih=scale*cover.height;
    requireThat(72/scale>=200,"Cover falls below 200 pixels per inch");
    emit({kind:"image",x:(W-iw)/2,y:235+(maxH-ih)/2,w:iw,h:ih});
    if(titleOnly) return {pages,anchors,checkpoints,expectedText};
    newPage("title");bookTitle();
    const contentsGroups=[
      [{key:"prologue",title:book.prologue.title}],
      ...book.chapters.map((c,i)=>[{key:c.id,title:"Chapter "+(i+1)+"   "+c.title},
        ...HEADS.map((h,j)=>({key:c.id+"-"+(j+1),title:(j+1)+". "+h,inset:true}))]),
      [{key:"epilogue",title:book.epilogue.title}],[{key:"appendix",title:book.appendix.title}]
    ];
    label="contents";newPage(label);tocPage=pg.number;
    function contentsHeading(){ heading(pg.number===tocPage?"Contents":"Contents (continued)",2,16,13,"contents title","",0); }
    contentsHeading();
    for(const group of contentsGroups) {
      const rows=group.map(row=>{
        const font=row.inset?1:2,indent=row.inset?9:0,size=row.inset?9:10;
        const isChapter=/^Chapter [0-9]+ /u.test(row.title);
        const lines=wrap(row.title,font,size,BW-indent-23-(isChapter?8:0));
        if(isChapter)lines[0]=lines[0].replace(/^(Chapter [0-9]+) /u,"$1   ");
        return {...row,font,indent,size,lines};
      });
      const height=rows.reduce((n,r)=>n+r.lines.length*(r.size+3),0)+8;
      if(y+height>END){pageBreak();contentsHeading();}
      requireThat(y+height<=END,"A contents group is too tall");
      for(const r of rows){
        const base=y+r.size;
        for(const [i,line] of r.lines.entries())text(line,pg.x+r.indent,base+i*(r.size+3),r.font,r.size,"contents entry",r.key);
        const last=base+(r.lines.length-1)*(r.size+3);
        text(String(previous[r.key]??0),pg.x+BW,last,3,8.5,"contents page",r.key,"right");
        link(pg.x+r.indent,y,BW-r.indent,last-y+3,r.key);
        y+=r.lines.length*(r.size+3);
      }
      y+=8;
    }
    function paragraph(s,bid) {
      requireThat(typeof s==="string"&&s.trim(),"Empty paragraph");
      const wordsAndCitations=words(s).map(w=>{
        const runs=[];
        for(const part of w.split(/(\[\[[A-Z0-9-]+\]\])/).filter(Boolean)){
          const match=/^\[\[([A-Z0-9-]+)\]\]$/.exec(part);
          if(match){requireThat(references.has(match[1]),"Unknown source "+match[1]);runs.push({s:"["+match[1]+"]",size:5.8,ref:match[1]});}
          else runs.push({s:part,size:9});
        }
        return runs;
      });
      const tokens=[];
      for(const run of wordsAndCitations){
        if(tokens.length&&run.every(t=>t.ref)) tokens.at(-1).push({s:" ",size:9},...run);
        else tokens.push(run);
      }
      const printed=tokens.map(r=>r.map(t=>t.s).join("")).join(" ");
      expectedText.push({id:bid,value:printed,type:"body"});
      const lines=[];let used=0,line=[],room=BW-8;
      for(const token of tokens) {
        const measure=token.reduce((n,t)=>n+width(t.s,1,t.size),0);
        if(used+measure+(line.length?width(" ",1,9):0)>room+.001&&line.length){
          lines.push(line);line=[];used=0;room=BW;
        }
        requireThat(measure<=room+.001,"Paragraph token exceeds the text frame: "+token.map(t=>t.s).join(""));
        if(line.length){line.push({s:" ",size:9});used+=width(" ",1,9);}
        line.push(...token);used+=measure;
      }
      if(line.length) lines.push(line);
      const lead=12.6;
      if(lines.length>=2) need(Math.min(3,lines.length)*lead);
      let start=0;
      while(start<lines.length){
        let capacity=Math.floor((END-y+.001)/lead);
        if(capacity===0){pageBreak();capacity=Math.floor((END-y+.001)/lead);}
        let count=Math.min(lines.length-start,capacity);
        if(lines.length-start-count===1&&count>2)count--;
        for(let k=0;k<count;k++){
          const i=start+k;let x=pg.x+(i===0?8:0);
          const base=y+9;
          const runs=[];
          for(const r of lines[i]) {
            const prior = runs.at(-1);
            if(prior && !prior.ref && !r.ref) prior.s += r.s;
            else runs.push({...r});
          }
          for(const r of runs){
            text(r.s,x,base-(r.ref?2.4:0),1,r.size,r.ref?"citation":"body",bid);
            const rw=width(r.s,1,r.size);
            if(r.ref)link(x,base-8,rw,9,"source-"+r.ref);
            x+=rw;
          }
          y+=lead;
        }
        start+=count;
        if(start<lines.length)pageBreak();
      }
      y+=3.4;
    }
    function caption(prefix,s,note,align) {
      requireThat(typeof s==="string"&&s.trim()&&!s.endsWith("."),"Use a nonempty caption without a final period");
      const lines=wrap(prefix+s+(note??""),4,7.2,BW);
      return {h:lines.length*10,
        paint(base,x){ for(const [i,t] of lines.entries())text(t,x,base+7.2+i*10,4,7.2,"caption",id,align); }};
    }
    function figure(b) {
      requireThat(Array.isArray(b.steps)&&b.steps.length>=2&&b.steps.length<=6,"A flow figure takes two to six steps");
      const n=++seq.figure, cap=caption("Figure "+active.n+"."+n+"  ",b.title,"","center");
      const boxes=b.steps.map(s=>wrap(s,3,8,BW-29));
      const shape=boxes.map(lines=>Math.max(25,lines.length*10+12));
      const gap=13, boxW=BW-16;
      const h=shape.reduce((a,v)=>a+v,0)+(boxes.length-1)*gap+cap.h+20;
      need(h);y+=5;
      const x=pg.x+8,cx=x+boxW/2;
      for(const [j,lines] of boxes.entries()){
        const rh=shape[j];
        rect(x,y,boxW,rh,{fill:j===0?.97:.99,stroke:.24,weight:.8});
        const base=y+(rh-(lines.length-1)*10)/2+2.6;
        for(const [k,l] of lines.entries()) text(l,cx,base+k*10,3,8,"figure label",id,"center");
        y+=rh;
        if(j<boxes.length-1){
          ln(cx,y,cx,y+gap-2,.8);ln(cx-2.5,y+gap-5,cx,y+gap-2,.8);ln(cx+2.5,y+gap-5,cx,y+gap-2,.8);
          y+=gap;
        }
      }
      y+=5;cap.paint(y,pg.x+BW/2);y+=cap.h+10;
    }
    function table(b) {
      requireThat(b.columns?.length>=2&&b.columns.length<=5&&b.rows?.length>0,"Invalid table dimensions");
      requireThat(b.rows.every(r=>r.length===b.columns.length),"Missing table cell");
      const n=++seq.table;
      const weights=b.weights??b.columns.map(()=>1);
      requireThat(weights.length===b.columns.length&&weights.every(w=>Number.isFinite(w)&&w>0),"Invalid column weights");
      const widths=weights.map(v=>BW*v/weights.reduce((a,x)=>a+x,0));
      const cellFont=7.6, cellLead=10.5;
      const patt=(r,header)=>r.map((v,i)=>wrap(v,header?4:3,cellFont,widths[i]-9,{split:true}));
      const rowH=r=>Math.max(1,...r.map(c=>c.length))*cellLead+8;
      const head=patt(b.columns,true), hHead=rowH(head);
      const rows=b.rows.map(r=>patt(r,false));
      function paintRow(row,header){
        const h=rowH(row);
        if(header) rect(pg.x,y,BW,h,{fill:.93});
        let x=pg.x;
        for(const [k,cell] of row.entries()){
          for(const [i,l] of cell.entries())text(l,x+4.5,y+4+cellFont+i*cellLead,header?4:3,cellFont,"table cell",id);
          x+=widths[k];
        }
        y+=h;
        ln(pg.x,y,pg.x+BW,y,.75,.5);
      }
      const prefix="Table "+active.n+"."+n+"  ";
      for(let index=0;index<rows.length;){
        let cap=caption(prefix,b.title,index?" (continued)":"","left");
        const total=rows.slice(index).reduce((sum,r)=>sum+rowH(r),0);
        const short=index===0&&rows.length<=5&&cap.h+hHead+total+13<=END-TOP;
        need(cap.h+hHead+(short?total:rowH(rows[index]))+13);
        y+=5;cap.paint(y,pg.x);y+=cap.h+3;paintRow(head,true);
        do{paintRow(rows[index]);index++;}
        while(index<rows.length&&y+rowH(rows[index])+5<=END);
        y+=5;
        if(index<rows.length)pageBreak();
      }
      if(b.note){
        const note=wrap(b.note,3,7.6,BW,{split:true});
        need(note.length*10.5+4);
        for(const l of note){text(l,pg.x,y+7.6,3,7.6,"table note",id);y+=10.5;}
        y+=4;
      }
    }
    function code(b) {
      requireThat(typeof b.code==="string"&&b.code.length>0&&!/[\r\t]/.test(b.code),"Use LF and spaces in code");
      requireThat(b.language==="javascript"||b.language==="python"||b.language==="text","Identify the code language");
      const chunks=b.code.split("\n");
      const max=Math.floor((BW-19)/width("M",5,7.2));
      const vis=[];
      for(const l of chunks) {
        if(!l)vis.push({s:"",continuation:false});
        for(let i=0;i<l.length;i+=max)vis.push({s:l.slice(i,i+max),continuation:i>0});
      }
      expectedText.push({id,value:b.code,type:"code"});
      const head=b.title?wrap(b.title,4,7.2,BW):[], h=head.length*10+vis.length*9.6+15;
      need(h);y+=4;
      for(const s of head){text(s,pg.x,y+7.2,4,7.2,"code title",id);y+=10;}
      rect(pg.x,y,BW,vis.length*9.6+6,{fill:.96});
      y+=3;
      for(const line of vis){
        if(line.continuation)text(">",pg.x+4,y+7.2,3,7,"continuation",id);
        text(line.s,pg.x+11,y+7.2,5,7.2,"code",id);
        checkpoints.push({id,line:line.s,continuation:line.continuation,page:pg.number});
        y+=9.6;
      }
      y+=8;
    }
    function formula(b) {
      const parts=b.numerator!==undefined?[b.lhs??"",b.numerator,b.denominator]:[b.text];
      requireThat(parts.every(s=>typeof s==="string"),"Formula text is missing");
      const size=9;
      const largest=parts.length===3?Math.max(width(parts[1],1,size),width(parts[2],1,size))+6:0;
      const radical=b.root&&parts.length===3 ? 13 : 0;
      const span=width(parts[0],1,size)+largest+radical;
      requireThat(span<=BW-10,"Formula exceeds measure");
      need(parts.length===3?37:21);y+=2;
      const x=pg.x+(BW-span)/2;
      if(parts.length===1){text(parts[0],x,y+9,1,size,"formula",id);y+=19;return;}
      const x2=x+width(parts[0],1,size)+radical, center=x2+largest/2;
      text(parts[0],x,y+17,1,size,"formula",id);
      if(radical){
        ln(x2-13,y+19,x2-10,y+16,.8);ln(x2-10,y+16,x2-6,y+26,.8);
        ln(x2-6,y+26,x2-2,y-2,.8);ln(x2-2,y-2,x2+largest,y-2,.8);
      }
      text(parts[1],center,y+9,1,size,"formula",id,"center");ln(x2,y+13,x2+largest,y+13,.8);
      text(parts[2],center,y+25,1,size,"formula",id,"center");y+=35;
    }
    function blocks(items,base) {
      for(const [i,node] of items.entries()){
        id=base+"/"+(i+1);
        switch(node.type){
          case "p": paragraph(node.text,id);break;
          case "h":
            requireThat(items[i+1]?.type==="p","A subhead requires a following paragraph");
            heading(node.text,4,9,3,"subhead","",38,6);break;
          case "table": requireThat(active,"Tables must be in chapters");table(node);break;
          case "figure": requireThat(active,"Figures must be in chapters");figure(node);break;
          case "code": code(node);break;
          case "formula": formula(node);break;
          default: throw Error("Unknown block type "+node.type);
        }
      }
    }
    function part(unit,key,odd){
      active=null;label=key;
      if(odd)recto(label);else newPage(label);
      y=odd?67:TOP;
      heading(unit.title,2,15,12,"part title",key);
      blocks(unit.blocks,key);
    }
    part(book.guide,"guide",false);
    part(book.prologue,"prologue",true);
    for(const [j,c] of book.chapters.entries()) {
      const n=j+1;active={n,heading:"Chapter "+n+"   "+c.title};label="chapter";
      seq={figure:0,table:0};recto("chapter opener");anchor(c.id);y=64;
      heading("Chapter "+n,2,13,5,"chapter number","",50);
      heading(c.title,2,17,15,"chapter title","",41);
      for(const [k,arr] of c.sections.entries()){
        label="chapter";
        const key=c.id+"-"+(k+1);
        requireThat(["h","p"].includes(arr[0]?.type),"Start each chapter section with prose or a subhead followed by prose");
        const opening=arr[0].type==="h"?wrap(arr[0].text,4,9,BW).length*11.34+9:0;
        heading((k+1)+". "+HEADS[k],2,11,5,"section",key,38+opening,k===0?0:9);
        blocks(arr,key);
      }
    }
    part(book.epilogue,"epilogue",true);
    part(book.appendix,"appendix",true);
    if(references.size) {
      label="references"; newPage(label); anchor("references");
      heading("References",2,15,9,"part title");
      const sourceGutter=Math.max(...[...references.keys()].map(k=>width("["+k+"]",4,8.1)))+11;
      requireThat(sourceGutter<BW/2,"Use shorter source IDs in the reference column");
      for(const s of references.values()){
        const rows=wrap(s.title,3,8.5,BW-sourceGutter);
        need(rows.length*11.3+8);
        anchor("source-"+s.id);
        text("["+s.id+"]",pg.x,y+8.5,4,8.1,"source ID");
        const start=y;
        for(const row of rows){text(row,pg.x+sourceGutter,y+8.5,3,8.5,"source title");y+=11.3;}
        link(pg.x+sourceGutter,start,BW-sourceGutter,y-start,s.url,true);
        y+=8;
      }
    }
    if((pages.length-1)%2) newPage("blank");
    requireThat(pages.length-1<=300,"Extend and verify a wider-gutter profile beyond 300 interior pages");
    return {pages,anchors,checkpoints,expectedText};
  }
  const fmt=n=>Number(n.toFixed(4)).toString();
  function commands(page) {
    return page.ink.map(e=>{
      const f=fmt;
      switch(e.kind){
        case "text":return `BT 0 g /F${e.font} ${f(e.size)} Tf 1 0 0 1 ${f(e.x)} ${f(H-e.y)} Tm ${pdfText(e.s)} Tj ET\n`;
        case "line":return `${f(e.w)} w ${f(e.g)} G ${f(e.x1)} ${f(H-e.y1)} m ${f(e.x2)} ${f(H-e.y2)} l S\n`;
        case "rect":{
          const r=`${f(e.x)} ${f(H-e.y-e.h)} ${f(e.w)} ${f(e.h)} re`;
          const fill=e.fill===null?"":`${f(e.fill)} g ${r} f\n`;
          const stroke=e.stroke===null?"":`${f(e.weight)} w ${f(e.stroke)} G ${r} S\n`;
          return fill+stroke;
        }
        case "image":return `q ${f(e.w)} 0 0 ${f(e.h)} ${f(e.x)} ${f(H-e.y-e.h)} cm /Cover Do Q\n`;
        case "link":return "";
        default:throw Error("Unexpected command "+e.kind);
      }
    }).join("");
  }
  function pdf(doc,cover,selection="viewing") {
    const objects=[];
    const reserve=()=>objects.push(null);
    const set=(i,s)=>{objects[i-1]=s;return i;};
    const add=s=>set(reserve(),s);
    const stream=(attrs,raw)=>`<< ${attrs} /Length ${raw.length} >>\nstream\n${raw}\nendstream`;
    const catalog=reserve(), tree=reserve(), outline=reserve();
    const fontIds=fonts.map((name,i)=>{
      const face=faces[i], pars=face.desc, sub=face.subset();
      const encoded=byteString(deflate(sub)), data=add(stream(`/Filter /FlateDecode /Length1 ${sub.length}`,encoded));
      const desc=add(`<< /Type /FontDescriptor /FontName /${name} /FontFile2 ${data} 0 R /Flags ${32+(i<=1?2:0)+(i===4?1:0)} /FontBBox [${pars.box.join(" ")}] /ItalicAngle ${pars.angle} /Ascent ${pars.ascent} /Descent ${pars.descent} /CapHeight ${pars.cap} /StemV ${i===1||i===3?120:80} >>`);
      const mapped=face.cp1252.map((c,k)=>face.glyphMap.get(c)?[k+32,c]:null).filter(Boolean);
      const hex=(n,w)=>n.toString(16).toUpperCase().padStart(w,"0");
      const unicode=[];
      for(let k=0;k<mapped.length;k+=100){
        const p=mapped.slice(k,k+100);
        unicode.push(`${p.length} beginbfchar\n${p.map(([b,c])=>`<${hex(b,2)}> <${hex(c.codePointAt(0),4)}>`).join("\n")}\nendbfchar`);
      }
      const cmap=`/CIDInit /ProcSet findresource begin\n12 dict begin\nbegincmap\n/CIDSystemInfo << /Registry (Adobe) /Ordering (UCS) /Supplement 0 >> def\n/CMapName /BookText def\n/CMapType 2 def\n1 begincodespacerange\n<00> <FF>\nendcodespacerange\n${unicode.join("\n")}\nendcmap\nCMapName currentdict /CMap defineresource pop\nend\nend`;
      const uni=add(stream("/Filter /FlateDecode",byteString(deflate(latinBytes(cmap)))));
      const ws=face.cp1252.map(c=>face.glyphMap.get(c)?face.metric(c):0).join(" ");
      return add(`<< /Type /Font /Subtype /TrueType /BaseFont /${name} /Encoding /WinAnsiEncoding /FirstChar 32 /LastChar 255 /Widths [${ws}] /FontDescriptor ${desc} 0 R /ToUnicode ${uni} 0 R >>`);
    });
    const use=doc.pages.filter(p=>selection==="cover"?p.number===0:selection==="interior"?p.number>0:true);
    const coverId=use.some(p=>p.number===0)?add(stream(`/Type /XObject /Subtype /Image /Width ${cover.width} /Height ${cover.height} /ColorSpace /DeviceGray /BitsPerComponent 8 /Interpolate true /Filter /FlateDecode`,byteString(deflate(cover.pixels)))):null;
    const pageIds=new Map(use.map(p=>[p.number,reserve()]));
    const fid=fontIds.map((v,i)=>`/F${i+1} ${v} 0 R`).join(" ");
    for(const p of use){
      const content=commands(p);
      const all=p.ink.filter(e=>e.kind==="link");
      const annotations=[];
      for(const link of all){
        const f=fmt,r=`[${f(link.x)} ${f(H-link.y-link.h)} ${f(link.x+link.w)} ${f(H-link.y)}]`;
        const dest=pageIds.get(doc.anchors[link.to]);
        const target=link.url?`/A << /S /URI /URI ${rawLiteral(link.to)} >>`:dest?`/Dest [${dest} 0 R /Fit]`:"";
        if(target)annotations.push(add(`<< /Type /Annot /Subtype /Link /Rect ${r} /Border [0 0 0] ${target} >>`));
      }
      const cid=add(stream(`/Filter /FlateDecode /DL ${content.length}`,byteString(deflate(latinBytes(content)))));
      const res=`/Resources << /Font << ${fid} >> ${p.number===0?`/XObject << /Cover ${coverId} 0 R >>`:""} >>`;
      set(pageIds.get(p.number),`<< /Type /Page /Parent ${tree} 0 R /MediaBox [0 0 ${fmt(W)} ${fmt(H)}] ${res} /Contents ${cid} 0 R ${annotations.length?`/Annots [${annotations.map(a=>`${a} 0 R`).join(" ")}]`:""} >>`);
    }
    const outlines=[];
    for(const p of use) {
      const match=p.ink.filter(e=>e.kind==="text"&&["part title","chapter title","contents title"].includes(e.role));
      if(!match.length||p.role==="contents"&&p.ink.some(e=>e.s==="Contents (continued)"))continue;
      outlines.push({obj:reserve(),n:p.number,title:match.map(e=>e.s).join(" ")});
    }
    for(const [i,e] of outlines.entries()) set(e.obj,`<< /Title ${pdfText(e.title)} /Parent ${outline} 0 R /Dest [${pageIds.get(e.n)} 0 R /Fit] ${i?`/Prev ${outlines[i-1].obj} 0 R`:""} ${i+1<outlines.length?`/Next ${outlines[i+1].obj} 0 R`:""} >>`);
    set(outline,`<< /Type /Outlines /Count ${outlines.length} ${outlines.length?`/First ${outlines[0].obj} 0 R /Last ${outlines.at(-1).obj} 0 R`:""} >>`);
    set(tree,`<< /Type /Pages /Count ${use.length} /Kids [${[...pageIds.values()].map(x=>`${x} 0 R`).join(" ")}] >>`);
    const labels=selection==="viewing"?" /PageLabels << /Nums [0 << /P (Cover) >> 1 << /S /D /St 1 >>] >>":"";
    set(catalog,`<< /Type /Catalog /Pages ${tree} 0 R /Lang (en) /Outlines ${outline} 0 R${labels} /ViewerPreferences << /DisplayDocTitle true >> >>`);
    const info=add(`<< /Title ${pdfText(TITLE.join(" "))} /Creator (Portable Book) /Producer (Portable Book PDF 1.4) >>`);
    let start="%PDF-1.4\n%\xE2\xE3\xCF\xD3\n";const offsets=[];
    for(const [i,o] of objects.entries()){offsets.push(start.length);start+=`${i+1} 0 obj\n${o}\nendobj\n`;}
    const xref=start.length;
    start+=`xref\n0 ${objects.length+1}\n0000000000 65535 f \n${offsets.map(o=>String(o).padStart(10,"0")+" 00000 n \n").join("")}trailer\n<< /Size ${objects.length+1} /Root ${catalog} 0 R /Info ${info} 0 R >>\nstartxref\n${xref}\n%%EOF\n`;
    return latinBytes(start);
  }
  function build(book,cover) {
    const first=layout(book,cover);
    const full=layout(book,cover,first.anchors);
    requireThat(JSON.stringify(full.anchors)===JSON.stringify(first.anchors),"Contents pagination changed");
    return {layout:full,viewing:pdf(full,cover,"viewing"),interior:pdf(full,cover,"interior"),cover:pdf(full,cover,"cover")};
  }
  return {build,layout,pdf,commands,width,HEADS,W,H,TOP,END,BW,LEFT,OUT,fonts,faces};
}

function auditKernel(fontSources){
  const {requireThat:assert,byteString,inflate}=imageKernel();
  const E=bookKernel(fontSources), {W,H,TOP,END,BW,LEFT,OUT,width}=E;
  const near=(a,b,tolerance=.002)=>Math.abs(a-b)<=tolerance;
  const clean=s=>s.trim().replace(/\s+/g," ");
  function parsePdf(bytes){
    const raw=byteString(bytes);
    assert(raw.startsWith("%PDF-1.4\n%"),"PDF header missing");
    const anchor=/\nstartxref\n(\d+)\n%%EOF\n$/.exec(raw);
    assert(anchor,"Missing xref trailer");
    const start=Number(anchor[1]);
    const xref=raw.slice(start).split("\n");
    assert(xref[0]==="xref","Invalid xref offset");
    const count=Number(xref[1].split(" ")[1]);
    const offsets=xref.slice(3,count+2).map(x=>Number(x.slice(0,10)));
    assert(offsets.length===count-1,"Missing xref offsets");
    assert(xref[count+2]==="trailer","Malformed xref records");
    const objects=offsets.map((offset,i)=>{
      const header=(i+1)+" 0 obj\n", end=(offsets[i+1]??start);
      assert(raw.slice(offset,offset+header.length)===header&&raw.slice(end-8,end)==="\nendobj\n","Invalid PDF object boundary");
      return raw.slice(offset+header.length,end-8);
    });
    const get=n=>objects[n-1];
    const ff=objects.filter(o=>o.startsWith("<< /Type /Font /Subtype /TrueType "));
    assert(ff.length===5,"Missing embedded font objects");
    for(const o of ff){
      const descriptor=get(Number(/\/FontDescriptor (\d+) 0 R/.exec(o)?.[1]));
      const embedded=descriptor&&get(Number(/\/FontFile2 (\d+) 0 R/.exec(descriptor)?.[1]));
      assert(embedded&&embedded.includes("/Length1")&&o.includes("/ToUnicode"),"Font embedding or character map missing");
    }
    const tree=objects.find(s=>s.startsWith("<< /Type /Pages "));
    assert(tree,"Missing page tree");
    const kids=/\/Kids \[([0-9 R]+)\]/.exec(tree)[1].match(/\d+ 0 R/g).map(x=>parseInt(x));
    assert(kids.length===Number(/\/Count (\d+)/.exec(tree)[1]),"Page tree count mismatch");
    const ext="€\u0081‚ƒ„…†‡ˆ‰Š‹Œ\u008dŽ\u008f\u0090‘’“”•–—˜™š›œ\u009džŸ";
    function unlock(s){
      return s.replace(/\\([0-7]{3}|.)/g,(_,x)=>{
        if(!/^[0-7]{3}$/.test(x)) return x;
        const k=parseInt(x,8);return k>=128&&k<160?ext[k-128]:String.fromCharCode(k);
      });
    }
    return kids.map(ref=>{
      const obj=get(ref), size=/\/MediaBox \[0 0 ([\d.]+) ([\d.]+)\]/.exec(obj);
      assert(size&&near(W,Number(size[1]))&&near(H,Number(size[2])),"Wrong trim size");
      const stream=get(Number(/\/Contents (\d+) 0 R/.exec(obj)[1]));
      const i=stream.indexOf("\nstream\n")+8, n=Number(/\/Length (\d+)/.exec(stream)[1]);
      assert(i>7&&stream.slice(i+n)==="\nendstream","Malformed page stream length");
      const dec=inflate(Uint8Array.from(stream.slice(i,i+n),c=>c.charCodeAt(0)),Number(/\/DL (\d+)/.exec(stream)[1]));
      const rows=byteString(dec).split("\n").filter(Boolean);
      const ts=/^BT 0 g \/F([1-5]) ([\d.]+) Tf 1 0 0 1 ([\d.-]+) ([\d.-]+) Tm \((.*)\) Tj ET$/;
      const text=rows.filter(x=>x.startsWith("BT")).map(line=>{
        const m=ts.exec(line);
        assert(m,"Unparseable text operator");
        return {font:Number(m[1]),size:Number(m[2]),x:Number(m[3]),y:H-Number(m[4]),s:unlock(m[5])};
      });
      const ann=(/\/Annots \[([0-9 R]+)\]/.exec(obj)?.[1]??"").match(/\d+ 0 R/g)??[];
      return {text,rows,
        cover:get(Number(/\/Cover (\d+) 0 R/.exec(obj)?.[1]??0)),
        annotations:ann.map(a=>get(parseInt(a))),
        ref};
    });
  }
  function check(book,doc,viewing,interior=null,coverOnly=null) {
    const a=parsePdf(viewing), errors=[], counts={pages:a.length,ordinaryText:0,citations:0,figures:0,codeLines:0,tables:0,links:0,refs:0,headings:0};
    function ok(value,label){if(!value)errors.push(label);}
    ok(a.length===doc.pages.length&&a.length%2===1,"Even interior and correct viewing length required");
    if(interior&&coverOnly){
      const m=parsePdf(interior),c=parsePdf(coverOnly); 
      ok(m.length+1===a.length&&c.length===1&&c[0].cover===a[0].cover,"Cover/interior concatenation mismatch");
      m.forEach((p,i)=>ok(JSON.stringify(p.text)===JSON.stringify(a[i+1].text)&&JSON.stringify(p.rows)===JSON.stringify(a[i+1].rows),"Interior differs at p. "+(i+1)));
      ok(JSON.stringify(c[0].text)===JSON.stringify(a[0].text),"Cover text differs");
    }
    const body=new Map(), code=new Map(), starts=new Set(), figures=new Set(), tables=new Set(), coverText=[];
    const physical=new Map(doc.pages.map(p=>[p.number,a[p.number].ref]));
    for(const p of doc.pages) {
      const actual=a[p.number], roles=p.ink.filter(e=>e.kind==="text"), where="p. "+p.number+" ";
      ok(actual.text.length===roles.length,where+"text operator count mismatch");
      if(p.role==="cover") {
        ok(Boolean(actual.cover)&&actual.rows.filter(x=>x.endsWith("/Cover Do Q")).length===1,where+"cover image is missing");
        for(const e of actual.text)coverText.push(e.s);
        const img=actual.cover??"";
        const bits=/\/Width (\d+) \/Height (\d+)/.exec(img);
        const m=/\/Length (\d+)/.exec(img);
        const first=img.indexOf("\nstream\n")+8;
        const body=img.slice(first,first+Number(m?.[1]??0));
        if(bits&&m){
          const pix=inflate(Uint8Array.from(body,c=>c.charCodeAt(0)),Number(bits[1])*Number(bits[2]));
          ok(pix.some(x=>x<100),where+"front image is blank");
        } else ok(false,where+"cover stream is missing");
      }else ok(!actual.cover,where+"cover raster in interior");
      const folio=roles.filter(x=>x.role==="folio"), head=roles.filter(x=>x.role==="running head");
      const x=p.number%2?LEFT:OUT, plain=!["cover","title","blank"].includes(p.role);
      ok(folio.length===Number(plain),where+"incorrect folio");
      if(plain){
        ok(folio[0].s===String(p.number)&&near(folio[0].y,H-9*72/25.4),where+"incorrect folio number or height");
        ok(p.number%2?near(folio[0].x+folio[0].w,x+BW):near(folio[0].x,x),where+"folio is on the wrong side");
      }
      ok(head.length===Number(p.role==="chapter"&&p.number%2===1),where+"unexpected chapter running head");
      if(head.length)ok(near(head[0].x+head[0].w,x+BW),where+"chapter head must be right-aligned");
      if(["prologue","chapter opener","epilogue","appendix"].includes(p.role))ok(p.number%2===1,where+"section opener is not on recto");
      if(p.role==="blank")ok(!actual.rows.length&&!actual.annotations.length,where+"intentional blank has content");
      const marks=[];
      for(const [i,role] of roles.entries()){
        const seen=actual.text[i];
        if(!seen){ok(false,where+"missing "+role.role);continue;}
        ok(seen.s===role.s&&seen.font===role.font&&near(seen.x,role.x)&&near(seen.y,role.y),where+"emitted text does not match source placement");
        ok(near(seen.size,role.size),where+"emitted font size mismatch");
        const w=width(seen.s,seen.font,seen.size);
        const bound=!("title|folio|running head".split("|").includes(role.role));
        if(bound)ok(seen.x>=x-.002&&seen.x+w<=x+BW+.002&&seen.y>=TOP&&seen.y<=END+.002,where+role.role+" outside measure: "+seen.s.slice(0,36));
        if(w>0)marks.push({...seen,right:seen.x+w,top:seen.y-seen.size*.74,bottom:seen.y+seen.size*.22});
        if(role.role==="body"||role.role==="citation"){
          const bodySize=role.role==="body";
          ok(near(seen.size,bodySize?9:5.8)&&seen.font===1,where+"wrong body/citation size");
          if(bodySize)counts.ordinaryText+=seen.s.replace(/\s/g,"").length;
          else counts.citations++;
          const base=seen.y+(bodySize?0:2.4);
          if(!body.has(role.id))body.set(role.id,[]);
          const a=body.get(role.id), last=a.at(-1);
          if(last&&last.p===p.number&&near(base,last.y)) last.s+=seen.s;
          else {
            a.push({p:p.number,y:base,s:seen.s});
            const first=!starts.has(role.id);
            ok(near(seen.x,x+(first?8:0)),where+"paragraph start or wrap indented incorrectly");
            if(last&&last.p===p.number)ok(near(base-last.y,12.6),where+"wrong body leading");
            if(first)starts.add(role.id);
          }
        }
        if(role.role==="code"){
          counts.codeLines++;
          if(!code.has(role.id))code.set(role.id,[]);
          code.get(role.id).push(seen.s);
          ok(seen.font===5&&near(seen.size,7.2),where+"code type style");
        }
        if(role.role==="figure label"){
          ok(seen.size>=7,where+"diagram label too small");
          figures.add(role.id);
        }
        if(role.role==="table cell"){ok(seen.size>=7,where+"table text too small");tables.add(role.id);}
        if(role.role==="caption"){
          ok(seen.size>=7&&seen.font===4,where+"incorrect caption style");
          if(seen.s.startsWith("Figure ")){
            ok(near(seen.x+w/2,x+BW/2),where+"figure caption not centered");
            ok(roles.some(t=>t.role==="figure label"&&t.id===role.id),where+"figure and caption are split");
          }
          if(seen.s.startsWith("Table ")){
            ok(near(seen.x,x),where+"table caption not left-aligned");
            ok(roles.some(t=>t.role==="table cell"&&t.id===role.id),where+"table and caption are split");
          }
        }
        if(role.role==="formula")ok(seen.font===1&&near(seen.size,9),where+"math type style");
        if(["section","subhead"].includes(role.role)){
          const prose=roles.slice(i+1).find(t=>t.role==="body");
          ok(Boolean(prose),where+"orphan heading");counts.headings++;
        }
        if(role.role==="contents page")ok(seen.s===String(doc.anchors[role.id]),where+"stale contents page label");
        if(role.role==="source ID")counts.refs++;
      }
      for(let i=0;i<marks.length;i++) for(let j=i+1;j<marks.length;j++){
        const m=marks[i],n=marks[j];
        ok(Math.min(m.right,n.right)-Math.max(m.x,n.x)<.025||
           Math.min(m.bottom,n.bottom)-Math.max(m.top,n.top)<.025,where+"overlapping text: "+m.s.slice(0,19)+" / "+n.s.slice(0,19));
      }
      const expectedLinks=p.ink.filter(e=>e.kind==="link"), visibleVector=p.ink.filter(e=>e.kind==="rect"||e.kind==="line");
      const nVector=visibleVector.reduce((n,e)=>n+(e.kind==="line"?1:Number(e.fill!==null)+Number(e.stroke!==null)),0);
      const printedVectors=actual.rows.filter(x=>/( re [fS]| l S)$/.test(x));
      ok(printedVectors.length===nVector,where+"vector caption/figure/table stroke is missing");
      for(const e of visibleVector)if(e.kind==="line")ok(e.w>=.75,where+"vector stroke is too thin");
      for(const e of printedVectors){
        const inside=e.match(/^([\d.]+) w/);
        if(inside)ok(Number(inside[1])>=.75,where+"emitted vector stroke too thin");
      }
      ok(actual.annotations.length===expectedLinks.length,where+"link count mismatch");
      expectedLinks.forEach((e,i)=>{
        const printed=actual.annotations[i]??"";
        const destination=physical.get(doc.anchors[e.to]);
        ok(e.url?printed.includes("/A << /S /URI /URI"):printed.includes(`/Dest [${destination} 0 R /Fit]`),where+"link destination differs");
        counts.links++;
      });
    }
    ok(JSON.stringify(coverText)===JSON.stringify(["The Little Book","of","Kaggle 1st Place Solutions"]),"Three-line front title differs");
    for(const x of doc.expectedText){
      if(x.type==="body")ok(clean((body.get(x.id)??[]).map(l=>l.s).join(" "))===clean(x.value),"Paragraph text differs: "+x.id);
      else {
        const physicalCode=(code.get(x.id)??[]).slice();
        const logical=[];
        for(const l of doc.checkpoints.filter(s=>s.id===x.id)){
          const value=l.line?physicalCode.shift():"";
          ok(value===l.line,"Code is changed or missing: "+x.id);
          if(l.continuation)logical[logical.length-1]+=value;else logical.push(value);
        }
        ok(logical.join("\n")===x.value&&!physicalCode.length,"Code whitespace or line order differs: "+x.id);
      }
    }
    const startsInOrder=book.chapters.map(c=>doc.anchors[c.id]);
    ok(startsInOrder.every((p,i)=>p%2===1&&(i===0||p>startsInOrder[i-1])),"Chapter order or parity changed");
    counts.figures=figures.size;counts.tables=tables.size;
    return {pass:errors.length===0,counts,errors};
  }
  function sha256(bytes) {
    const words=new Uint32Array(64);
    const ks=[], start=[];
    for(let k=2;ks.length<64;k++){
      let isPrime=true;
      for(let d=2;d*d<=k;d++) if(k%d===0){isPrime=false;break;}
      if(!isPrime)continue;
      if(start.length<8) start.push((4294967296*Math.sqrt(k))>>>0);
      ks.push((4294967296*Math.cbrt(k))>>>0);
    }
    const length=bytes.length,padded=new Uint8Array((Math.floor((length+8)/64)+1)*64);
    padded.set(bytes);padded[length]=128;
    const dv=new DataView(padded.buffer);dv.setUint32(padded.length-8,Math.floor(length/536870912));dv.setUint32(padded.length-4,(length*8)>>>0);
    const rot=(a,b)=>(a>>>b)|(a<<(32-b));
    for(let offset=0;offset<padded.length;offset+=64){
      for(let i=0;i<16;i++)words[i]=dv.getUint32(offset+i*4);
      for(let i=16;i<64;i++){
        const a=words[i-15], b=words[i-2];
        words[i]=(words[i-16]+(rot(a,7)^rot(a,18)^(a>>>3))+words[i-7]+(rot(b,17)^rot(b,19)^(b>>>10)))>>>0;
      }
      let [a,b,c,d,e,f,g,h]=start;
      for(let i=0;i<64;i++){
        const t1=(h+(rot(e,6)^rot(e,11)^rot(e,25))+((e&f)^((~e)&g))+ks[i]+words[i])>>>0;
        const t2=((rot(a,2)^rot(a,13)^rot(a,22))+((a&b)^(a&c)^(b&c)))>>>0;
        h=g;g=f;f=e;e=(d+t1)>>>0;d=c;c=b;b=a;a=(t1+t2)>>>0;
      }
      [a,b,c,d,e,f,g,h].forEach((v,i)=>start[i]=(start[i]+v)>>>0);
    }
    return start.map(x=>x.toString(16).padStart(8,"0")).join("");
  }
  return {parsePdf,check,sha256};
}

function proofRaster(fontSources){
  const I=imageKernel(), A=auditKernel(fontSources), E=bookKernel(fontSources);
  const {concat,latinBytes,deflate,inflate}=I, {W,H,faces}=E;
  const crcTable=Array.from({length:256},(_,i)=>{let x=i;for(let j=0;j<8;j++)x=(x>>>1)^((x&1)?0xedb88320:0);return x>>>0;});
  const be=n=>Uint8Array.of(n>>>24,(n>>>16)&255,(n>>>8)&255,n&255);
  function png(width,height,pixels){
    function chunk(name,data){
      const bytes=concat([latinBytes(name),data]);
      let crc=0xffffffff;
      for(const b of bytes)crc=(crc>>>8)^crcTable[(crc^b)&255];
      return concat([be(data.length),bytes,be((crc^0xffffffff)>>>0)]);
    }
    const raw=new Uint8Array((width+1)*height);
    for(let i=0;i<height;i++)raw.set(pixels.subarray(i*width,(i+1)*width),i*(width+1)+1);
    return concat([Uint8Array.of(137,80,78,71,13,10,26,10),chunk("IHDR",concat([be(width),be(height),Uint8Array.of(8,0,0,0,0)])),chunk("IDAT",deflate(raw)),chunk("IEND",new Uint8Array())]);
  }
  function cover(data){
    const dims=/\/Width (\d+) \/Height (\d+)/.exec(data);
    const n=Number(/\/Length (\d+)/.exec(data)[1]),begin=data.indexOf("\nstream\n")+8;
    const w=Number(dims[1]),h=Number(dims[2]);
    return {w,h,pixels:inflate(latinBytes(data.slice(begin,begin+n)),w*h)};
  }
  function glyphPoints(contour){
    if(!contour.length)return [];
    const mid=(a,b)=>({x:(a.x+b.x)/2,y:(a.y+b.y)/2,on:true});
    const all=[];
    for(let i=0;i<contour.length;i++){
      const p=contour[i], next=contour[(i+1)%contour.length];
      all.push(p);if(!p.on&&!next.on)all.push(mid(p,next));
    }
    const i=all.findIndex(p=>p.on), pts=all.slice(i).concat(all.slice(0,i));pts.push(pts[0]);
    let out=[pts[0]];
    for(let j=1;j<pts.length;j++){
      const b=pts[j];
      if(b.on)out.push(b);
      else {
        const a=out.at(-1),c=pts[++j];
        for(let k=1;k<=6;k++){
          const t=k/6,t1=1-t;
          out.push({x:t1*t1*a.x+2*t*t1*b.x+t*t*c.x,y:t1*t1*a.y+2*t*t1*b.y+t*t*c.y});
        }
      }
    }
    return out;
  }
  const glyphCache=new Map();
  function raster(page,scale=1.45) {
    const w=Math.ceil(W*scale), h=Math.ceil(H*scale), aa=2, ss=scale*aa,wide=w*aa,hi=h*aa, pixels=new Uint8Array(wide*hi).fill(255);
    function pixel(x,y,g){if(x>=0&&y>=0&&x<wide&&y<hi)pixels[y*wide+x]=g;}
    function fill(x,y,x2,y2,g){
      const from=Math.max(0,Math.round(x)),to=Math.min(wide,Math.round(x2));
      for(let row=Math.max(0,Math.round(y));row<Math.min(hi,Math.round(y2));row++) pixels.fill(g,row*wide+from,row*wide+to);
    }
    function line(x0,y0,x1,y1,width,gray){
      const r=width/2,dx=x1-x0,dy=y1-y0,sq=dx*dx+dy*dy;
      if(!sq)return;
      for(let y=Math.floor(Math.min(y0,y1)-r);y<=Math.ceil(Math.max(y0,y1)+r);y++)
       for(let x=Math.floor(Math.min(x0,x1)-r);x<=Math.ceil(Math.max(x0,x1)+r);x++){
        const p=Math.min(1,Math.max(0,((x+.5-x0)*dx+(y+.5-y0)*dy)/sq));
        if((x+.5-x0-p*dx)**2+(y+.5-y0-p*dy)**2<=r*r)pixel(x,y,gray);
       }
    }
    function glyph(font,ch,x,base,size) {
      const f=faces[font-1],gid=f.glyphMap.get(ch);
      const key=font+"|"+ch;
      if(!glyphCache.has(key))glyphCache.set(key,f.contours(gid).map(glyphPoints));
      const c=glyphCache.get(key);
      if(!c.length)return;
      const ratio=size*ss/f.em;
      const pols=c.map(p=>p.map(q=>[x+q.x*ratio,base-q.y*ratio])), vectors=pols.flat();
      const yLow=Math.min(...vectors.map(q=>q[1])),yHigh=Math.max(...vectors.map(q=>q[1]));
      const aStart=Math.max(0,Math.floor(yLow)),aEnd=Math.min(hi,Math.ceil(yHigh));
      for(let yy=aStart;yy<aEnd;yy++){
        const scan=yy+.5,dots=[];
        for(const p of pols)for(let j=1;j<p.length;j++){
          const [x1,y1]=p[j-1],[x2,y2]=p[j];
          if(y1<=scan&&y2>scan||y2<=scan&&y1>scan)dots.push([x1+(x2-x1)*(scan-y1)/(y2-y1),y2>y1?1:-1]);
        }
        dots.sort((a,b)=>a[0]-b[0]);
        let winding=0,next=0;
        for(const [x,s] of dots){
          if(winding!==0)for(let xx=Math.ceil(next-.5);xx<Math.ceil(x-.5);xx++)pixel(xx,yy,0);
          winding+=s;next=x;
        }
      }
    }
    let t=0;
    for(const cmd of page.rows){
      const parts=cmd.split(" ");
      if(parts[0]==="BT"){
        const {font,size,s,x,y}=page.text[t++];let X=x*ss;
        for(const ch of s){glyph(font,ch,X,y*ss,size);X+=faces[font-1].metric(ch)*size*ss/1000;}
      }else if(parts.at(-1)==="f"){
        const [g,_,x,y,ww,hh]=parts;
        fill(+x*ss,(H-y-hh)*ss,(+x+ +ww)*ss,(H-y)*ss,Math.round(+g*255));
      }else if(parts.at(-1)==="S"&&parts.at(-2)==="re"){
        const [lw,_,g,__,x,y,ww,hh]=parts;
        const xs=+x*ss,ys=(H-y-hh)*ss,xe=(+x+ +ww)*ss,ye=(H-y)*ss,c=Math.round(+g*255),tw=+lw*ss;
        for(const [a,b,c1,d] of [[xs,ys,xe,ys],[xs,ye,xe,ye],[xs,ys,xs,ye],[xe,ys,xe,ye]])line(a,b,c1,d,tw,c);
      }else if(parts.at(-1)==="S"&&parts.at(-2)==="l"){
        const [lw,_,g,__,x,y,___,x2,y2]=parts;
        line(+x*ss,(H-y)*ss,+x2*ss,(H-y2)*ss,+lw*ss,Math.round(g*255));
      }else if(parts.at(-2)==="Do"){
        const img=cover(page.cover),ww=Number(parts[1])*ss,hh=Number(parts[4])*ss;
        const x=Math.round(Number(parts[5])*ss),y=Math.round((H-Number(parts[6])-Number(parts[4]))*ss);
        for(let iy=0;iy<Math.round(hh);iy++){
          for(let ix=0;ix<Math.round(ww);ix++)pixel(x+ix,y+iy,img.pixels[Math.floor(iy*img.h/Math.round(hh))*img.w+Math.floor(ix*img.w/Math.round(ww))]);
        }
      }else throw Error("Preview does not handle a PDF drawing command");
    }
    const final=new Uint8Array(w*h);
    for(let y=0;y<h;y++)for(let x=0;x<w;x++){
      const i=y*2*wide+x*2;
      final[y*w+x]=(pixels[i]+pixels[i+1]+pixels[i+wide]+pixels[i+wide+1]+2)>>>2;
    }
    return {width:w,height:h,pixels:final};
  }
  function sheet(images,columns=3){
    const pad=10,w=images[0].width,h=images[0].height, width=(w+pad)*columns+pad,height=(h+pad)*Math.ceil(images.length/columns)+pad;
    const out=new Uint8Array(width*height).fill(198);
    for(const [i,img] of images.entries()){
      const x=pad+i%columns*(w+pad),y=pad+Math.floor(i/columns)*(h+pad);
      for(let j=0;j<h;j++)out.set(img.pixels.subarray(j*w,(j+1)*w),(y+j)*width+x);
    }
    return png(width,height,out);
  }
  return {raster,parsePdf:A.parsePdf,png,sheet};
}

const peers = {
  "STIXGeneral.ttf": "167378031e2dddc6216d67819c9260e9a06ffc4c478e4e23cb98a6fd44b183c2",
  "STIXGeneralBol.ttf": "e8533dc7083fa346bda1933d60ea4a83b67d0945bceaf1b3541f82b4a0e2c6a0",
  "DejaVuSans.ttf": "3fdf69cabf06049ea70a00b5919340e2ce1e6d02b0cc3c4b44fb6801bd1e0d22",
  "DejaVuSans-Bold.ttf": "b184b89e3c1075f22f6b71575b6fc20d4972b3cfd3b23322ca6fd596dcaef167",
  "DejaVuSansMono.ttf": "602ec86b8948cfcd956482fe64f94c36c867770149ef2f791d4613f443bcecb3"
};
const files = ["book.pdf", "interior.pdf", "front-cover.pdf"];
const checks = [
  "competition_identity", "task_metric_constraints", "winner_solution_sources",
  "examples_and_math", "figures_and_text", "code_execution_scope",
  "reconstructed_path_labeling", "chapter_structure_and_endmatter"
];
const fingerprint = bytes => createHash("sha256").update(bytes).digest("hex");
const json = x => JSON.stringify(x, null, 2) + "\n";
const readJSON = async p => JSON.parse(await readFile(p, "utf8"));
const rule = (valid, msg) => { if (!valid) throw Error(msg); };

async function fontsFrom(root) {
  return Promise.all(Object.entries(peers).map(async ([name, sha]) => {
    const bytes = await readFile(join(root, name));
    rule(fingerprint(bytes) === sha, "Wrong static font bytes for " + name);
    return bytes;
  }));
}

async function inputs(source, fontRoot) {
  const data = await readFile(source);
  const book = JSON.parse(data.toString("utf8"));
  const rel = book.coverImage;
  rule(typeof rel === "string" && rel.length > 0 && !isAbsolute(rel) &&
       !rel.split(/[\\/]/).includes("..") && !rel.includes("\\") && !rel.includes(":"),
       "Use a project-relative POSIX path to the generated cover PNG");
  const png = await readFile(resolve(dirname(source), rel));
  const cover = imageKernel().coverFromPng(png);
  const fonts = await fontsFrom(fontRoot);
  const build = bookKernel(fonts).build(book, cover);
  const hashes = Object.fromEntries(files.map((s,i) =>
    [s, fingerprint([build.viewing,build.interior,build.cover][i])]));
  return {book, data, cover, png, fonts, build, hashes, coverHash:fingerprint(png), inputHash:fingerprint(data)};
}

async function temporaryOutput(path, write) {
  const directory=resolve(path);
  const parent=dirname(directory);
  await mkdir(parent,{recursive:true});
  await mkdir(directory);
  try { await write(directory); }
  catch(err) {
    await rm(directory,{recursive:true,force:true});
    throw err;
  }
}

async function produce(source, dest, fontRoot){
  const q=await inputs(source,fontRoot);
  const summary=auditKernel(q.fonts).check(q.book,q.build.layout,q.build.viewing,q.build.interior,q.build.cover);
  rule(summary.pass,"Technical checks failed: "+summary.errors.slice(0,5).join(" | "));
  const manifest={
    schema:1,profile:q.book.profile,build_id:randomUUID(),runtime:process.version,
    input_sha256:q.inputHash,cover_sha256:q.coverHash,script_sha256:fingerprint(await readFile(fileURLToPath(import.meta.url))),
    fonts:peers,viewing_pages:q.build.layout.pages.length,body_pages:q.build.layout.pages.length-1,
    folios:q.build.layout.anchors,sha256:q.hashes,technical:summary,public_release_ready:false
  };
  await temporaryOutput(dest,async dir=>{
    const payload=[q.build.viewing,q.build.interior,q.build.cover];
    await Promise.all(files.map((s,i)=>writeFile(join(dir,s),payload[i])));
    await writeFile(join(dir,"manifest.json"),json(manifest));
  });
  return manifest;
}

async function audit(source, dest, fontRoot){
  const q=await inputs(source,fontRoot);
  const [a,b,c]=await Promise.all(files.map(s=>readFile(join(dest,s))));
  const technical=auditKernel(q.fonts).check(q.book,q.build.layout,a,b,c);
  const hashes=Object.fromEntries(files.map((s,i)=>[s,fingerprint([a,b,c][i])]));
  const exact=files.every(s=>hashes[s]===q.hashes[s]);
  return {pass:technical.pass&&exact,technical,exact_fixed_inputs:exact,sha256:hashes};
}

async function compare(a,b){
  rule(resolve(a)!==resolve(b),"Independent builds require separate output directories");
  const [p,q]=await Promise.all([readJSON(join(a,"manifest.json")),readJSON(join(b,"manifest.json"))]);
  rule(p.build_id&&q.build_id&&p.build_id!==q.build_id,"Use two separate builds, not a copied manifest");
  rule(["input_sha256","cover_sha256","script_sha256","runtime","body_pages","viewing_pages"].every(k=>p[k]===q[k]) &&
       JSON.stringify(p.fonts)===JSON.stringify(q.fonts),"Build inputs or runtime differ");
  const result={};
  for(const s of files){
    const [first,second]=await Promise.all([readFile(join(a,s)),readFile(join(b,s))]);
    result[s]=fingerprint(first)===fingerprint(second)&&fingerprint(first)===p.sha256[s]&&p.sha256[s]===q.sha256[s];
  }
  return {pass:Object.values(result).every(Boolean),same_bytes:result,builds:[p.build_id,q.build_id]};
}

async function render(pdfPath,out,fontRoot){
  const bytes=await readFile(pdfPath), sha=fingerprint(bytes), p=proofRaster(await fontsFrom(fontRoot));
  const pages=p.parsePdf(bytes);
  await temporaryOutput(out,async dir=>{
    const report=[];
    for(const [i,page] of pages.entries()){
      const raster=p.raster(page,2.1),name="page-"+String(i+1).padStart(3,"0")+".png";
      const png=p.png(raster.width,raster.height,raster.pixels);
      await writeFile(join(dir,name),png);
      report.push({pdf_page:i+1,name,raster_sha256:fingerprint(raster.pixels),width:raster.width,height:raster.height});
    }
    await writeFile(join(dir,"raster-index.json"),json({pdf_sha256:sha,dpi:151.2,pages:report}));
  });
  return {pdf_sha256:sha,pages:pages.length};
}

function reviewStatus(q, evidence, content, visual, compareReport, technical) {
  const reasons=[];
  const gate=(valid,s)=>{if(!valid)reasons.push(s);};
  const blockIds=q.book.chapters.flatMap(c=>c.sections.flatMap((arr,k)=>arr.map((_,i)=>c.id+"-"+(k+1)+"/"+(i+1))));
  const srcs=new Set(q.book.sources.map(s=>s.id));
  const cited=new Set(q.book.chapters.flatMap(c=>c.sections.flatMap(arr=>arr.flatMap(b=>
    b.type==="p"?[...b.text.matchAll(/\[\[([A-Z0-9-]+)\]\]/g)].map(m=>m[1]):[]))));
  const log=new Map((evidence.sources??[]).map(s=>[s.id,s]));
  const verified=s=>["direct","pinned-code","verified-excerpt"].includes(s?.access)&&
     /^\d{4}-\d{2}-\d{2}$/.test(s.date)&&typeof s.locator==="string"&&s.locator.trim();
  gate(q.book.profile==="public","Input has not been marked for public review");
  gate(srcs.size>0&&log.size===srcs.size&&[...srcs].every(id=>verified(log.get(id))),"Missing source access records");
  const claims=evidence.claims??[];
  gate(claims.length>0&&claims.every(c=>c.id&&c.text&&blockIds.includes(c.location)&&
    c.sources?.length&&c.sources.every(s=>cited.has(s)&&verified(log.get(s)))&&
    (!c.essential||c.status==="supported")&&["supported","limited"].includes(c.status)),
    "Unverified or unlocated essential claim");
  gate(q.book.chapters.every(c=>{
    const ids=claims.filter(x=>x.location?.startsWith(c.id+"-"));
    return ["task","metric","rank","method"].every(type=>ids.some(x=>x.category===type&&x.status==="supported"));
  }),"Each competition needs supported task, metric, rank and method claims");
  const cover=evidence.cover??{};
  gate(cover.png_sha256===q.coverHash&&typeof cover.prompt==="string"&&cover.prompt.length>=40&&
    typeof cover.generator==="string"&&cover.generator.length>1&&typeof cover.selection==="string"&&cover.selection.length>=20&&
    cover.generated_for===q.inputHash&&/^\d{4}-\d{2}-\d{2}$/.test(cover.date),"New cover record missing or stale");
  const code=[];
  for(const c of q.book.chapters) for(const [k,s] of c.sections.entries())
    for(const [i,p] of s.entries()) if(p.type==="code"&&p.language!=="text")
      code.push({id:c.id+"-"+(k+1)+"/"+(i+1),sha:fingerprint(p.code),output:p.expected});
  const runs=new Map((evidence.examples??[]).map(x=>[x.id,x]));
  gate(code.every(x=>{
    const s=runs.get(x.id);
    return s&&typeof x.output==="string"&&s.source_sha256===x.sha&&s.exit_code===0&&s.stdout===x.output&&
      typeof s.runtime==="string"&&s.runtime.length>1;
  }),"Executable listing evidence missing or stale");
  const evidenceDigest=fingerprint(json(evidence));
  gate(content?.input_sha256===q.inputHash&&content?.evidence_sha256===evidenceDigest&&
     typeof content.reviewer==="string"&&content.reviewer.trim()&&Array.isArray(content.open_issues)&&
     content.open_issues.length===0&&checks.every(k=>{
       const s=content.checks?.[k];return s?.status==="pass"&&typeof s.note==="string"&&s.note.trim().length>=25;
     }),"Complete the eight content checks for these exact inputs");
  const pdfPages=q.build.layout.pages.length;
  gate(visual?.pdf_sha256===q.hashes["book.pdf"]&&visual?.dpi>=120&&
    typeof visual.reviewer==="string"&&visual.reviewer.trim()&&Array.isArray(visual.open_issues)&&visual.open_issues.length===0&&
    visual.pages?.length===pdfPages&&visual.pages.every((p,i)=>p.pdf_page===i+1&&p.pass===true&&
       /^[0-9a-f]{64}$/.test(p.raster_sha256)&&typeof p.note==="string"&&p.note.trim().length>=10),
    "Complete the full-size visual review for this viewing PDF");
  gate(compareReport.pass&&technical.pass,"Technical audit or independent build comparison failed");
  return {pass:reasons.length===0,public_release_ready:reasons.length===0,problems:reasons,
    review_statement:"Human or second-pass editorial observations are accepted as attestations."};
}

async function release(source,a,b,fontRoot,evidencePath,contentPath,visualPath){
  const [q,technical,comparison,evidence,content,visual]=await Promise.all([
    inputs(source,fontRoot),audit(source,a,fontRoot),compare(a,b),
    readJSON(evidencePath),readJSON(contentPath),readJSON(visualPath)
  ]);
  const report=reviewStatus(q,evidence,content,visual,comparison,technical);
  if(report.pass) {
    const painter=proofRaster(q.fonts), actual=painter.parsePdf(q.build.viewing);
    for(const [i,p] of actual.entries()){
      const test=painter.raster(p,visual.dpi/72);
      if(fingerprint(test.pixels)!==visual.pages[i].raster_sha256)report.problems.push("Visual review pixel hash differs on PDF page "+(i+1));
    }
    report.pass=report.public_release_ready=report.problems.length===0;
  }
  return {...report,technical,comparison};
}

async function main(args){
  const [command,...a]=args;
  switch(command){
    case "build":return produce(a[0],a[1],a[2]);
    case "audit":return audit(a[0],a[1],a[2]);
    case "compare":return compare(a[0],a[1]);
    case "render":return render(a[0],a[1],a[2]);
    case "release":return release(...a);
    default:throw Error("Choose build, audit, compare, render or release. See the specification for arguments.");
  }
}

if (process.argv[1] && resolve(process.argv[1]) === fileURLToPath(import.meta.url)) {
  main(process.argv.slice(2)).then(x => {
    console.log(json(x));
    if(x.pass===false) process.exitCode=1;
  }).catch(err=>{
    process.stderr.write(String(err.message??err)+"\n");
    process.exitCode=1;
  });
}
````

### layout-fixture.json

<!-- asset:layout-fixture.json -->
````json
{
  "schema": 1,
  "title": "The Little Book of Kaggle 1st Place Solutions",
  "language": "en",
  "asOf": "2026-11-20",
  "profile": "fixture",
  "coverImage": "assets/cover.png",
  "guide": {
    "title": "Competitions in This Book",
    "blocks": [
      {
        "type": "p",
        "text": "Kaggle competitions give participants a shared problem and a scoring rule. A leaderboard tracks the results. In these chapters, the result depends on more than fitting a model. A forecaster supplies twenty-eight future days from one cutoff. A product matcher determines which similar listings belong in each answer."
      },
      {
        "type": "p",
        "text": "M5 Forecasting - Accuracy starts with one product at a store and follows the forecast upward through the retail hierarchy. Shopee - Price Match Guarantee follows a posting through a search for similar items, then asks whether the search improves when those neighbors inform a new representation."
      },
      {
        "type": "h",
        "text": "How to Read This Book"
      },
      {
        "type": "p",
        "text": "Each chapter starts with one input, output and score. Run the baseline example before looking for its failures. Read the reported winning system from data to submission. The final section proposes tests based on information competitors could have seen at the time."
      },
      {
        "type": "p",
        "text": "References identify organizer and participant reports. Each toy example tests a method on invented data. A leaderboard score comes from the corresponding competition process."
      },
      {
        "type": "p",
        "text": "This English viewing edition tests a reusable book specification. Sources were checked through November 20, 2026."
      }
    ]
  },
  "prologue": {
    "title": "On Beginning Again",
    "blocks": [
      {
        "type": "p",
        "text": "Late in the evening, the competition page stopped changing. A participant saved his notebook, closed the leaderboard and went to make tea. When he came back he opened the winning write-up again. Earlier that day he had tried to copy a table of settings. Now the question he wrote in the margin was smaller: what would have shown that his current approach was wrong?"
      },
      {
        "type": "p",
        "text": "He picked an example he had scored badly and recreated the prediction on paper. There were enough numbers to keep track of, but few enough to finish. The prediction looked reasonable until he compared it with the rule used to score it. On the second reading, one paragraph of the winning write-up became more legible. He could see what a comparison between the two approaches might reveal."
      },
      {
        "type": "p",
        "text": "This book starts in that interval, when the pressure to submit has passed and there is time to understand a decision. You will meet two problems with different data. One grows outward from a row of unit sales. The other begins with the gap between two photographs. Each chapter gives you a baseline and a path toward a better experiment. The path is reconstructed from published evidence and from questions a reader can test."
      },
      {
        "type": "p",
        "text": "Keep a short record beside the examples. Which information has already arrived? What is counted as a mistake? Where does an apparently safe shortcut pay for its speed? A record like that is a companion to the solution write-ups. You will have something to reach for the next time a promising score appears."
      }
    ]
  },
  "chapters": [
    {
      "id": "river-forecast-stress",
      "title": "Regional River Forecasting — Daily Origin and Multi-Region Calibration Fixture",
      "sections": [
        [
          {
            "type": "p",
            "text": "This fictional layout fixture exercises long contents entries, multipage tables and technical notation. Forecast a weekly sequence from records available at the origin. The examples use invented data."
          },
          {
            "type": "table",
            "title": "Repeated headings for a long table",
            "weights": [
              0.7,
              1.2,
              1.6
            ],
            "columns": [
              "Slice",
              "Diagnostic",
              "Observation"
            ],
            "rows": [
              [
                "1",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "2",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "3",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "4",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "5",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "6",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "7",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "8",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "9",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "10",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "11",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "12",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "13",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "14",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "15",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "16",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "17",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "18",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "19",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "20",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "21",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "22",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "23",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "24",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "25",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "26",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "27",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "28",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "29",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "30",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ],
              [
                "31",
                "A controlled comparison",
                "This exercise keeps the scoring denominator fixed while the group changes."
              ]
            ]
          },
          {
            "type": "formula",
            "lhs": "Scaled error = ",
            "numerator": "validation squared error",
            "denominator": "historical squared change",
            "root": true
          }
        ],
        [
          {
            "type": "p",
            "text": "Keeping the same time cutoff makes two sample predictions comparable across all rows."
          },
          {
            "type": "code",
            "language": "text",
            "title": "Continuation marker for one intentionally long line",
            "code": "function intentionallyLongIdentifierForPageMeasure(aValue, anotherValue, aThirdValue) {\n  return (aValue + anotherValue + aThirdValue);\n}"
          }
        ],
        [
          {
            "type": "p",
            "text": "The repeated synthetic chapter describes a staged baseline for exercising the artwork engine."
          },
          {
            "type": "figure",
            "title": "The test sequence",
            "steps": [
              "Choose the input cutoff",
              "Calculate the baseline",
              "Keep the same metric when comparing alternatives"
            ]
          }
        ],
        [
          {
            "type": "p",
            "text": "First compare predictions by region. Then vary the pooling strategy on the same split and measure the change."
          },
          {
            "type": "figure",
            "title": "A second figure for chapter numbering",
            "steps": [
              "Compare regions",
              "Pin the scorer",
              "Check for an improvement on held-aside records"
            ]
          }
        ]
      ]
    }
  ],
  "epilogue": {
    "title": "He Will Win the Next Competition",
    "blocks": [
      {
        "type": "p",
        "text": "The following spring he opened a fresh competition page. A value in the data table looked odd, and his first instinct was to look for a notebook that would remove it. Instead, he wrote down how the organizer would count an error on that row. He tried the simplest prediction he could compute by hand and drew a map of the remaining mistakes."
      },
      {
        "type": "p",
        "text": "By the weekend two small experiments disagreed. A new feature helped on one split and hurt on the other. He checked what information each split permitted and found a join that slipped a few days into the future. After repairing the join he kept the weaker score in his notes. It marked the moment when the experiment began to measure what he meant to predict."
      },
      {
        "type": "p",
        "text": "He still read the public discussions carefully. This time he could tell which ideas he could compare and which required a different test. He scheduled one night for the search and left time in the morning to look at the examples it lost. Winning remained uncertain, but his procedure for deciding what to try next was concrete. When the first group result arrived, he already knew which predictions to open."
      }
    ]
  },
  "appendix": {
    "title": "Appendix",
    "blocks": [
      {
        "type": "h",
        "text": "Shared vocabulary"
      },
      {
        "type": "p",
        "text": "A baseline is a fixed point of comparison. It can be a repeat-of-last-week forecast or a rule based on identical image hashes. A model earns a useful improvement when it passes a comparison with the same inputs, splits and primary metric."
      },
      {
        "type": "p",
        "text": "A validation split is a simulation of the data and conditions the system will see later. M5 uses a cutoff in time. Product matching keeps whole label groups together in a fold. Leakage occurs when the experiment grants information that would be unavailable for the intended prediction."
      },
      {
        "type": "p",
        "text": "An ablation changes a part of an approach and measures the effect while holding other relevant conditions fixed. An ensemble uses several models or predictions together. Their errors matter as much as their individual headline scores."
      },
      {
        "type": "h",
        "text": "A record for the next experiment"
      },
      {
        "type": "p",
        "text": "Write the prediction you expect to change, the hypothesis behind it, the one change being tested, the fixed data split, the metric, two diagnostic slices and a time or memory budget. Record whether the result supported the hypothesis. Save a failed run if it can distinguish between the two competing explanations."
      },
      {
        "type": "p",
        "text": "Preserve the exact source snapshot, model or scoring code, identifiers and parameters needed to replay the result. If you work with simulated data, say so beside the reported number. A fitted leaderboard solution and a teaching calculation answer different questions."
      }
    ]
  },
  "sources": []
}
````

### cover-prompt.txt

<!-- asset:cover-prompt.txt -->
````text
Create only the illustration for the front cover of an original technical little book with a quiet black-on-white print aesthetic. No letters, title, labels, numbers, graphic frame, or margins drawn into the artwork. Pure solid white #ffffff background from all four edges. Simple original pen and ink, black plus restrained cross-hatching. A light gray large cartoon ostrich with a black outline and gently curved long neck, beak angled down, is looking into an open unmarked book laid on a small garden table. A potted twig stands at the back of the table. The book faces the bird. A few tiny bits of grass at the feet. Front three-quarter view. Charming, anatomically convincing, vintage natural history engraving technique in a restrained original scene, graceful linework silhouette and generous negative space. No people or logos. The complete isolated drawing fits in an approximately square bounding shape and has at least 8% empty white space all around. Center composition. Keep the middle fairly light and the outline clear, suited to reproduction at 75 mm wide.
````

### Code license

The original code in the appendix follows the repository's MIT license convention. [Repository credits and licenses](https://github.com/espritmirai/little-book-kaggle/blob/main/README.md)
