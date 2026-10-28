# Is TurboFolk Faster? A Tempo Analysis of Yugoslav and Serbian Music

A permutation test (A/B test) of whether TurboFolk songs have a higher average tempo (BPM) than other genres of Serbian and Yugoslav music, paired with a research paper on TurboFolk, nationalism, and post-Yugoslav identity.

Originally written for **Music 108** (UC Berkeley, Fall 2025), using tools from **Data 8: Foundations of Data Science**.

---

## Overview

TurboFolk emerged in Serbia during the Milošević era, fusing synthesized, club-oriented pop with traditional Balkan folk melodies. It is closely tied to Serbian nationalism, and it is often described as a "techno-fied" version of folk music with fast tempos built for dancing.

This project asks a simple, testable piece of that description:

> **Is TurboFolk actually faster on average than other Serbian and Yugoslav genres, or is "fast tempo" just a stereotype?**

The repository contains:

- the **paper** that sets out the historical and cultural context (Yugoslav rock, the rise of TurboFolk, and why it resonated), and
- the **analysis** that tests the tempo claim with a permutation test.

## Hypotheses

- **Null (H₀):** TurboFolk songs and songs from other genres have the same BPM distribution, so any difference in average BPM is due to chance.
- **Alternative (H₁):** TurboFolk songs have a higher average BPM than other genres.

The test is one-sided. The test statistic is always **mean BPM (TurboFolk) − mean BPM (other)**.

## Data

BPM values were collected by hand from Spotify playlists using Spotify's in-app "mix" feature.

| Group | n | Contents |
|---|---|---|
| TurboFolk | 81 | A "Serbian Turbo-Folk" playlist, plus songs referenced in the paper's sources |
| Other | 135 | Yugoslav rock 'n' roll, Narodna muzika, 80s pop, folklore (kolo dance music), and two newer sevdalinka albums |

> **Note:** Only BPM values and group labels are stored here. No audio is included.

## Method

1. Build a table with two columns: `Label` (T or O) and `BPM`.
2. Compute the observed statistic: mean TurboFolk BPM minus mean other BPM.
3. Shuffle the labels (without replacement, which keeps group sizes fixed), recompute the difference, and repeat to simulate the null hypothesis.
4. Compute the p-value as the share of simulated differences that are at least as large as the observed one.

## Results

| | TurboFolk | Other |
|---|---|---|
| n | 81 | 135 |
| Mean BPM | 136.38 | 124.41 |
| Min | 93 | 65 |
| Q1 | 120 | 106 |
| Median | 136 | 123 |
| Q3 | 150 | 139.5 |
| Max | 198 | 208 |
| IQR | 30 | 33.5 |

- **Observed difference:** ≈ 11.97 BPM
- **p-value:** ≈ 0.001 (the original notebook reported 0.002 from 1,000 shuffles; see Known Issues)

In this sample, TurboFolk is faster on average, and the difference is unlikely to be due to chance alone. The "other" group is more spread out, with both the slowest and the fastest songs in the sample.

## Limitations

This is a small, hand-built sample, so the result describes **these playlists**, not the genres as a whole.

- The songs were chosen by hand, not randomly sampled from a defined population.
- The "other" group mixes several very different genres, so it is not a single comparison genre.
- TurboFolk is partly defined by artist and ideology, not just sound, so labeling is subjective, and the playlist likely mixes 1990s TurboFolk with later PopFolk.
- BPM comes from Spotify's automatic detection, which can mislabel half-time or double-time tempos.
- Songs by the same artist or from the same album are not independent.

## Known Issues / To Do

- [ ] Re-run the permutation test with 10,000+ shuffles and a fixed random seed (the original ran 1,000).
- [ ] Rename "bootstrap" to "permutation test" in code and write-up (shuffling without replacement is a permutation test).
- [ ] Add song metadata (title, artist, release year, source playlist) so every BPM can be traced and audited.
- [ ] Add a confidence interval and effect size alongside the p-value.
- [ ] Check suspiciously fast or slow values for half/double-time errors.
- [ ] Break the "other" group into separate genres and compare each against TurboFolk.

## Roadmap

- Compare BPM across **release years** (for example, 1990s rock vs. earlier rock).
- Separate **TurboFolk (1990s)** from **PopFolk (post-2000)**.
- Explore whether a classifier can predict genre, and whether BPM is an important feature.

## Repository Structure

```
.
├── README.md
├── paper/
│   └── turbofolk_paper.pdf
├── notebooks/
│   └── TurboFolkAB.ipynb
├── data/
│   └── bpm_data.csv
├── requirements.txt
└── .gitignore
```

## Running the Analysis

```bash
git clone <your-repo-url>
cd <your-repo-name>
pip install -r requirements.txt
jupyter notebook notebooks/TurboFolkAB.ipynb
```

`requirements.txt` should include:

```
numpy
matplotlib
datascience
jupyter
```

## Sources

Key references from the paper:

- Čvoro, Uroš. *Turbo-Folk Music and Cultural Representations of National Identity in Former Yugoslavia.* Routledge, 2014.
- Misina, Dalibor. *Shake, Rattle and Roll: Yugoslav Rock Music and the Poetics of Social Critique.* Routledge, 2013.
- Slavková, Markéta. "Echoing the Beats of Turbo-Folk: Popular Music and Nationalism in Ex-Yugoslavia." *Lidé Města*, 2010.
- Halilovich, Hariz. "Songs after genocide: music of hatred and triumphalism." *The Routledge Handbook of Popular Music and Politics of the Balkans*, 2024.
- Momčilović, Aleksandar. "'Please, Mile, Don't Sing Anything Political': Turbo-folk, politics and the restoration of capitalism in Serbia." *The Routledge Handbook of Popular Music and Politics of the Balkans*, 2024.
- Kheterpal, Nishant, et al. *Data 8: Foundations of Data Science.* UC Berkeley, Fall 2025.

The full bibliography is in the paper.

## Author

**Your Name** · [GitHub profile](https://github.com/your-username)

## License

Choose a license for the code (for example MIT). The paper is your own writing, so consider "All rights reserved" for it or a Creative Commons license.
