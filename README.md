# Battle of the OpenAI Models in Three.js

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Homepage](https://img.shields.io/badge/homepage-eval--forge.github.io-c4582f)](https://eval-forge.github.io)
[![Three.js](https://img.shields.io/badge/Three.js-r128-black)](https://cdnjs.com/libraries/three.js)
[![Entries](https://img.shields.io/badge/entries-8-2f5d62)](#the-entries)
[![Single file](https://img.shields.io/badge/build-single--file%20HTML-776e62)](#how-to-run-an-entry)
[![Last commit](https://img.shields.io/github/last-commit/eval-forge/battle-of-gpts-threejs)](https://github.com/eval-forge/battle-of-gpts-threejs/commits/main)

Same prompt, same single HTML file, same Three.js from cdnjs. Each OpenAI model was asked to build **Lighthouse Cove**, an interactive voxel island with a spinning lighthouse, a fishing village, boats, seagulls and a night mode. This repo holds every result, a homepage that ranks them, and the scoring used to rank them.

**Live:** [eval-forge.github.io](https://eval-forge.github.io)

## Contents

- [The prompt](#the-prompt)
- [The entries](#the-entries)
- [How the ranking works](#how-the-ranking-works)
- [How to run an entry](#how-to-run-an-entry)
- [Repository layout](#repository-layout)
- [Adding an entry](#adding-an-entry)
- [License](#license)

## The prompt

The full prompt is on the [homepage](https://eval-forge.github.io). In short, each entry had to:

- Build a floating island with sand, grassy cliffs, a rocky underside and waterfalls.
- Add a striped lighthouse with a rotating beam, a fishing village, a dock, two sailboats and a voxel water pool.
- Add palms, bushes, flowers, barrels, crates, an animated campfire, three islets and seagulls.
- Support drag to rotate, scroll to zoom, auto-rotate, a day/night toggle and a beam toggle.
- Use InstancedMesh, per-voxel colour variation, fog, soft shadows and animated water.
- Open with a top bar showing the model, date and total time, with an Eval Forge homepage link at the far right.
- Ship as one self-contained HTML file that loads Three.js from cdnjs.

## The entries

Ranked by the formula in [How the ranking works](#how-the-ranking-works). Time is the value each model reported in its own top bar.

| Rank | Model | Looks | Accuracy | Prompt | Time | Score | File |
|---|---|---|---|---|---|---|---|
| 1 | GPT-6 Astra | 92 | 88 | 80 | 13m 09s | 85.4 | [gpt-6-astra.html](gpt-6-astra.html) |
| 2 | GPT-6.1 Sol | 88 | 82 | 90 | 8m 40s | 84.1 | [gpt-6.1-sol.html](gpt-6.1-sol.html) |
| 3 | GPT-5.6 Sol | 80 | 76 | 80 | 7m 54s | 77.2 | [gpt-5.6-sol.html](gpt-5.6-sol.html) |
| 4 | GPT-6 Sol | 80 | 70 | 85 | 7m 46s | 75.9 | [gpt-6-sol.html](gpt-6-sol.html) |
| 5 | GPT-5.6 Luna | 72 | 72 | 95 | 2m 49s | 75.0 | [gpt-5.6-luna.html](gpt-5.6-luna.html) |
| 6 | GPT-6 Luna | 65 | 78 | 85 | 1m 00s | 72.7 | [gpt-6-luna.html](gpt-6-luna.html) |
| 7 | GPT-5.5 | 50 | 84 | 90 | 14m 04s | 61.7 | [gpt-5-5.html.html](gpt-5-5.html.html) |
| 8 | GPT-5.6 Terra | 45 | 58 | 80 | 3m 41s | 54.1 | [gpt-5.6-terra.html](gpt-5.6-terra.html) |

Looks, accuracy and prompt-following are 0 to 100 ratings. Time points are described below.

## How the ranking works

Each entry gets a score from 0 to 100:

$$
\text{Score} = 0.55\,V + 0.3\,A + 0.1\,H + 0.05\,T
$$

$$
T = 100 \cdot \frac{T_{\max} - t}{T_{\max} - T_{\min}}
$$

| Symbol | Meaning |
|---|---|
| **V** | Looks: lighting, materials, composition, UI polish, and whether the scene feels finished. |
| **A** | Accuracy: how much of the prompt's scene checklist is actually built and working. |
| **H** | Prompt-following: top bar format, the homepage link, one self-contained file, and cdnjs-hosted Three.js. |
| **T** | Time points: the fastest entry scores 100 and the slowest scores 0. |
| **t** | Seconds to finish, as reported by the model in its top bar. |
| **T_min, T_max** | Fastest and slowest times in the set (60 s and 844 s). |

Looks and accuracy carry most of the weight. Time is a tiebreaker, not the headline.

The ratings for looks, accuracy and prompt-following are judgment calls made from each file's source and rendered output. They are not measured.

## How to run an entry

No build step. Every entry is a single HTML file that loads Three.js from cdnjs.

1. Clone the repo, or download the file you want.
2. Open the `.html` file in a modern browser.
3. You need an internet connection, because Three.js loads from `cdnjs.cloudflare.com`.

To view entries without cloning, use the homepage at [eval-forge.github.io](https://eval-forge.github.io). Its cards load each scene on click.

## Repository layout

```
.
├── index.html            Homepage: ranking, scoring equation, entry cards
├── gpt-*.html            One file per model (the entries)
├── gpt-5-5.html.html    GPT-5.5 entry (file name kept as published)
├── LICENSE               MIT
└── README.md
```

## Adding an entry

1. Add the new `.html` file to the repo root. It should be one self-contained file that loads Three.js from cdnjs.
2. Add an entry to the `ENTRIES` array in `index.html` with its model name, file, title, date, time in seconds, and V, A and H ratings.
3. Open `index.html` locally to check the card, the ranking table and the score.
4. Open a pull request with the ratings and a short reason for each.

Scores depend on the whole set, because time is scaled between the fastest and slowest entries. Adding an entry that is slower or faster than the current extremes will shift everyone's time points.

## License

Released under the [MIT License](LICENSE).
