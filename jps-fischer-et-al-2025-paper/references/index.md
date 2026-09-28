# Paper navigation

Use exact headings to locate current line numbers. Read relevant passages, not both complete documents. This index locates evidence; it does not summarize findings.

## Main paper — [paper.md](paper.md)

| Exact heading | Look here for |
| --- | --- |
| Highlights | Five highlight statements of the article |
| Abstract | Article abstract |
| 1. Introduction | Motivation and regulatory context |
| 1.1. Aging: Definition, mechanisms, and impact on capacity and resistance | Definitions of SOH_C, R_incr. and EFC (Eqs. 1.1-1.3); degradation modes and mechanisms; Fig. 1 |
| 1.2. Overview of existing research on the linkage of capacity fade and resistance increase | Prior work, research gap, study aim and contribution statement |
| 2.1. Dataset overview | 14 datasets and 814 cells; Table 1 cell specifications; Table 2 aging and RPT conditions; DC-pulse (Eq. 2) and impedance feature definitions |
| 2.2. Data preparation and requirements | Hampel filter settings, exclusion criteria, normalization, preprocessing counts; Fig. 2 |
| 2.3. Correlation analysis, fitting and evaluation metrics | PCC and p-value (Eq. 3, Table 3); linear, exponential and power-law models (Eqs. 4.1-4.4); RMSE (Eq. 5); knee-point cells |
| 3.1. Overview of preprocessed dataset | BOL vs EOT capacity and resistance distributions (Fig. 3); CoV and PCC per dataset (Table 4) |
| 3.2. Correlation analysis of capacity fade and resistance increase | PCC histograms over aging trajectories (Fig. 4); discussion of weakly correlated cells |
| 3.3. Fitting evaluation and selection | Exemplary trajectories and fits (Fig. 5, Table 5); fit error distributions (Fig. 6) |
| 3.4. Identifying optimal candidates for capacity fade determination and possible real-world approaches | DC-pulse vs impedance features (Fig. 7); global power-law fit and cross-validation for VTC5A (Fig. 8) |
| 4. Conclusion | Summary and proposed BMS implementation |
| Acknowledgments | Funding and data providers |
| Appendix A. Hampel-filter | Outlier filter equations (A.1-A.3) |
| Appendix B. Adjusted coefficient of determination | SSE, SST, R² and adjusted R² (B.1-B.4) |
| Appendix C. Results of the global power-law fit for the other datasets investigated | Cross-validated RMSE per dataset and aging condition (Table C.6) |
| Data availability | Data availability statement |
| References | Numbered bibliography [1]-[74] |
| Conversion notes | Source, license and data notes for this package |

For long sections, search a narrower subsection or prompt. Headings inside fenced quotations are source content, not document section boundaries.

## Supplementary information — [supplement.md](supplement.md)

| Exact heading | Look here for |
| --- | --- |
| Document beginning | Source text or supplied-material notes |

For long sections, search a narrower subsection or prompt. Headings inside fenced quotations are source content, not document section boundaries.

## Assets

Figure and table captions in the documents link to the files below. Open only the needed image; for a table, read its header and relevant rows first.

- `assets/figure/`: main figures (JPEG).
- `assets/supp_figs/`: supplementary and extended-data figures (JPEG).
- `assets/table/`: main tables (CSV, or JPEG when transcription is unreliable).
- `assets/supp_table/`: supplementary tables (CSV, or JPEG fallback).

Asset paths are relative to the skill root. CSVs retain internal blank rows; captions and merged headers may also occupy rows. Consult the document notes before treating every row as data.
