# DREAD scoring review

Sources reviewed: 2026-10-28.

The CSV contains all 19 assigned CWEs, sorted by descending weighted risk. Its first 11 columns follow the assignment sample; two final columns provide the CWE URL and review notes.

## Counting choices

- Damage Potential counts Common Consequences data rows, following the written rule. Semicolon-separated items within a row are not additional rows. Affected Users equals Damage Potential.
- The CWE-73 sample gives Damage=6, while its current page contains 3 rows with 6 listed entries (5 distinct individual impacts). This is an assignment ambiguity, not a hidden change to the scoring method.
- Reproducibility counts CVE references listed in Selected Observed Examples. Scores are raw counts and are not capped at 10. CWE-502 lists CVE-2012-0911 twice: 13 listed references, 12 distinct IDs.
- Exploitability uses Low=1, Medium=5, High=9. CWE-918 has no Likelihood Of Exploit section, so it uses the required missing-score default of 10.
- Discoverability counts distinct Detection Methods labels. CWE-20 and CWE-798 each have 10 actual methods; those values are not defaults.
- Weights count Table 3 columns in the supplied PDF. Independent check-mark coordinate counts agree with table extraction: 117 checks total. CWE-20 has 11 mapped threats, despite the rubric example saying 7.
- Probability = Reproducibility + Exploitability + Discoverability. Impact = Damage Potential + Affected Users. Overall Risk = Weight × Probability × Impact.
- Equal risk scores share a competition rank (1,2,2,4). CSV stores calculated values; it has no live formulas.

## Source counts

| CWE | Weight | Consequence rows | Listed impact entries | CVE references | Likelihood | Distinct methods | Source |
|---|---:|---:|---:|---:|---|---:|---|
| CWE-20 | 11 | 3 | 7 | 43 | High | 10 | [MITRE](https://cwe.mitre.org/data/definitions/20.html) |
| CWE-22 | 5 | 4 | 4 | 23 | High | 9 | [MITRE](https://cwe.mitre.org/data/definitions/22.html) |
| CWE-77 | 4 | 1 | 1 | 9 | High | 1 | [MITRE](https://cwe.mitre.org/data/definitions/77.html) |
| CWE-78 | 4 | 1 | 7 | 19 | High | 9 | [MITRE](https://cwe.mitre.org/data/definitions/78.html) |
| CWE-79 | 10 | 3 | 6 | 20 | High | 2 | [MITRE](https://cwe.mitre.org/data/definitions/79.html) |
| CWE-89 | 15 | 5 | 6 | 15 | High | 9 | [MITRE](https://cwe.mitre.org/data/definitions/89.html) |
| CWE-94 | 3 | 4 | 4 | 22 | Medium | 1 | [MITRE](https://cwe.mitre.org/data/definitions/94.html) |
| CWE-200 | 4 | 1 | 1 | 19 | High | 6 | [MITRE](https://cwe.mitre.org/data/definitions/200.html) |
| CWE-269 | 11 | 1 | 1 | 15 | Medium | 1 | [MITRE](https://cwe.mitre.org/data/definitions/269.html) |
| CWE-287 | 4 | 1 | 3 | 33 | High | 8 | [MITRE](https://cwe.mitre.org/data/definitions/287.html) |
| CWE-306 | 4 | 1 | 2 | 17 | High | 8 | [MITRE](https://cwe.mitre.org/data/definitions/306.html) |
| CWE-352 | 3 | 1 | 5 | 10 | Medium | 9 | [MITRE](https://cwe.mitre.org/data/definitions/352.html) |
| CWE-400 | 2 | 2 | 6 | 17 | High | 3 | [MITRE](https://cwe.mitre.org/data/definitions/400.html) |
| CWE-434 | 3 | 1 | 1 | 11 | Medium | 5 | [MITRE](https://cwe.mitre.org/data/definitions/434.html) |
| CWE-502 | 3 | 3 | 4 | 13 | Medium | 1 | [MITRE](https://cwe.mitre.org/data/definitions/502.html) |
| CWE-798 | 3 | 2 | 5 | 20 | High | 10 | [MITRE](https://cwe.mitre.org/data/definitions/798.html) |
| CWE-862 | 13 | 4 | 10 | 25 | High | 9 | [MITRE](https://cwe.mitre.org/data/definitions/862.html) |
| CWE-863 | 11 | 5 | 11 | 13 | High | 9 | [MITRE](https://cwe.mitre.org/data/definitions/863.html) |
| CWE-918 | 4 | 3 | 3 | 10 | Missing; score 10 | 1 | [MITRE](https://cwe.mitre.org/data/definitions/918.html) |

All other source data was available. The single missing-data default is CWE-918 Exploitability.
