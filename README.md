# peekbank-items

Word-level analyses of the [Peekbank](https://peekbank.stanford.edu) database
(release **2026.1**). Where the [peekbank-development paper] analyzes word
recognition at the *child* level, this project works at the *word* level: how
does looking-while-listening (LWL) item difficulty link to children's knowledge
of individual words (CDI)?

## Notebooks (run in order)

| Notebook | Purpose |
|----------|---------|
| `0_load_data.qmd` | Load 2026.1, build caches, descriptives; load the item-level CDI subset. |
| `1_tidy_data.qmd` | Trial- and child-level frames (accuracy, RT, exclusions). |
| `2_lwl_item_difficulty.qmd` | LWL-side word difficulty (animacy-adjusted random effects). |
| `3_cdi_word_difficulty.qmd` | CDI-side word difficulty: lightweight 2PL IRT + AoA + ability bridge. |
| `4_linking_aggregate.qmd` | Aggregate item-level linking; reproduces the background failure and tests fixes. |
| `5_linking_evaluation.qmd` | Unified evaluation: linking hypotheses × data settings (aggregate / imputed / precise). |

## Data pathways for the CDI linkage

- **Large / noisy** — all children; CDI is only a summary score, so per-word
  knowledge is *imputed* (child ability × word IRT difficulty).
- **Small / precise** — `adams_marchman_2018` subset with true item-level CDI
  responses (from `../../standard_model_2`); we know whether each child produced
  each word.

## Reproducing

Requires R with `peekbankr`, `tidyverse`, `lme4`, `mirt`, `wordbankr`,
`fuzzyjoin`, `here`, and the `quarto` CLI. Render in order, e.g.
`quarto render 0_load_data.qmd`. Heavy database/Wordbank pulls are cached in
`cached_intermediates/` (gitignored) and guarded so re-renders are fast.
