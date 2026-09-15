# Siegler, Thompson, & Schneider (2011) Fraction Arithmetic Dataset

This repository contains children's fraction arithmetic performance data
originally collected for:

> Siegler, R. S., Thompson, C. A., & Schneider, M. (2011). An integrated
> theory of whole number and fractions development. *Cognitive Psychology,
> 62*, 273–296. https://doi.org/10.1016/j.cogpsych.2011.03.001

The data were later reanalyzed, and are described in detail (as "Study 2"),
in:

> Braithwaite, D. W., Pyke, A. A., & Siegler, R. S. (2017). A computational
> model of fraction arithmetic. *Psychological Review, 124*(5), 603–625.
> https://doi.org/10.1037/rev0000072

If you use this dataset, please cite both papers above.

## Overview

Forty-eight U.S. middle school students (24 sixth graders, 24 eighth
graders) each solved 8 fraction arithmetic problems: one addition, one
subtraction, one multiplication, and one division problem with equal
denominators, and one of each with unequal denominators. All problems used
the operand pair 3/5 and 2/5 (equal-denominator problems) or 3/5 and 1/2
(unequal-denominator problems). After each problem, children reported the
strategy they had used to solve it, which was later coded into one of
several categories.

This yields 48 participants × 8 trials = 384 rows.

## Files

- `siegler_thompson_schneider_2011.RData` — an R data file containing a
  single data frame, `sts.data`, with one row per trial (384 rows, 19
  columns).

## Data dictionary

| Column | Type | Description |
|---|---|---|
| `grade` | integer | Participant's grade in school: 6 or 8. |
| `subjid` | integer | Anonymous participant identifier assigned during data collection (620–643 for sixth graders, 809–832 for eighth graders). Arbitrary lab codes; not linked to any identifying information. |
| `seq_idx` | integer | Trial code from the original study, encoding the problem: 401/402 = addition, 501/502 = division, 601/602 = multiplication, 701/702 = subtraction; the final digit (1 or 2) distinguishes the equal- vs. unequal-denominator problem for that operation. |
| `prob` | character | The problem as presented, formatted `operand1<op>operand2`, e.g. `"3/5+2/5"`. Operators: `+` addition, `-` subtraction, `*` multiplication, `:` division. |
| `oper` | factor | Arithmetic operation: `add`, `sub`, `mult`, `div`. |
| `group` | factor | Operation grouping used in analysis: `add_sub`, `mult`, `div` (addition and subtraction problems used identical operand pairs and are grouped together). |
| `denom` | factor | Whether the two operands had the same or different denominators: `same-denom`, `diff-denom`. |
| `operands` | factor | Type of operands in the problem. Always `fraction` in this dataset (the factor also has unused `mixed`/`whole` levels, retained for compatibility with the broader analysis codebase used across multiple datasets). |
| `key` | character | The correct answer, in the same `a/b` format as `prob`. |
| `resp` | character | The participant's answer, in `a/b` format. |
| `acc` | integer (0/1) | 1 if `resp` exactly matches `key`, else 0. |
| `strat` | factor | The child's self-reported strategy, collapsed into 4 categories (see below): `OpNumKeepDen`, `IndepComp`, `InvertOper`, `Other/None`. |
| `strat_orig` | integer | The original, fine-grained strategy code underlying `strat` (see mapping below). |
| `strat_corr` | numeric (0/1) | 1 if the reported strategy, executed correctly, would produce the correct answer for that specific problem; 0 otherwise. (Correctness depends on the combination of strategy and operation — e.g., independently operating on numerators and denominators is correct for multiplication but not for addition/subtraction.) |
| `strat_err` | numeric (0/1) | Complement of `strat_corr` (1 = strategy was inherently flawed for this problem). |
| `strat_overgen` | numeric (0/1) | 1 if the strategy reflects overgeneralizing a procedure from a different arithmetic operation (e.g., applying the addition procedure to a multiplication problem). |
| `OpNumKeepDen`, `IndepComp`, `InvertOper` | numeric (0/1) | Dummy-coded indicators for 3 of the 4 `strat` categories, used directly as predictors in the regression models reported in Braithwaite et al. (2017). `Other/None` is the omitted reference category. |

### Strategy codes (`strat` / `strat_orig`)

| `strat_orig` | `strat` | Description |
|---|---|---|
| 1 | `OpNumKeepDen` | Operate on numerators, keep denominator. E.g., 3/5 + 2/5 = (3+2)/5 = 5/5. |
| 2 | `OpNumKeepDen` | Convert to a common denominator, then operate on numerators, keeping the denominator. E.g., 3/5 + 1/2 = 6/10 + 5/10 = 11/10. |
| 3 | `IndepComp` | Operate independently on numerators and on denominators. E.g., 3/5 + 1/2 = (3+1)/(5+2) = 4/7. |
| 4 | `IndepComp` | Convert to a common denominator, then operate independently on numerators and denominators. |
| 5 | `InvertOper` | Invert one operand, then operate independently on numerators and denominators (division only). E.g., 3/5 ÷ 1/2 = 3/5 × 2/1 = 6/5. |
| 6 | `InvertOper` | Cross-operate: combine the numerator of one operand with the denominator of the other, and vice versa. E.g., 3/5 ÷ 1/2 = (3×2)/(5×1) = 6/5. |
| 10 | `Other/None` | Guessed. |
| 20 | `Other/None` | Any other strategy. |

## Data quality

No missing values. Every participant contributed exactly 8 trials
(48 × 8 = 384 rows). No personally identifying information is included:
`subjid` values are arbitrary codes assigned during data collection, and no
names, dates, school identifiers, or free-text responses are present in
this file.

## License

Released under the MIT License — see [LICENSE](LICENSE).

## Contact

David W. Braithwaite (braithwaite@psy.fsu.edu), Florida State University.
