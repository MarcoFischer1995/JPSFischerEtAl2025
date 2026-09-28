# Paper agent: capacity fade vs. resistance increase in 814 Li-ion cells

An AI-readable version of our open-access article, packaged as an agent skill with [Paper2Agent](https://github.com/jmiao24/Paper2Agent) ([Miao et al., *Nature* 2026](https://doi.org/10.1038/s41586-026-11044-y)). Ask it about the dataset, methods, equations, figures and tables. Every answer can be traced back to a section, figure or table of the paper.

> M. Fischer, M.J. Brand, A. Karger, M. Rubio Gomez, M. Rehm, J. Natterer, A. Jossen,
> **How degradation of lithium-ion batteries impacts capacity fade and resistance increase: A systematic, correlative analysis**,
> *Journal of Power Sources* 656 (2025) 237921. https://doi.org/10.1016/j.jpowsour.2025.237921

## What is inside

| Folder / file | Content |
| --- | --- |
| `jps2025-capacity-resistance-paper/SKILL.md` | Entry point for the agent |
| `.../references/paper.md` | Full article text, including equations as searchable transcriptions |
| `.../references/index.md` | Section navigation |
| `.../assets/figure/` | Figures 1 to 8, graphical abstract, equation images |
| `.../assets/table/` | Tables 1 to 5 and C.6 as CSV |

The package contains only the published article. It contains no raw data and no code. As stated in the article, data are available on request.

## Install

**Claude apps (web and desktop):** download `jps2025-capacity-resistance-paper.zip` from the [latest release](https://github.com/DerBOY1995/jps2025-capacity-resistance-agent/releases/latest). In Claude, open **Customize > Skills** and upload the zip. Code execution must be enabled.

**Claude Code:** clone this repository and copy the folder `jps2025-capacity-resistance-paper` to `~/.claude/skills/` (all projects) or to `.claude/skills/` inside one project. Restart Claude Code.

```bash
git clone https://github.com/DerBOY1995/jps2025-capacity-resistance-agent.git
```

**Codex:** copy the same folder to `~/.agents/skills/`.

Then ask, for example:

- "Which cells and chemistries are in the dataset, and how many cells per dataset?"
- "Which expression links SOH_C and resistance increase best, and how accurate is it?"
- "Why do some FTC1 cells show a weak correlation?"
- "Compare the DC-pulse resistance with the EIS features R_zc and R_pl."

## Limitations

- The agent answers from the article only. It can still misread or over-generalize. Check important numbers against the paper.
- Values printed inside figures, such as the per-subset fit parameters in Fig. 8, exist only as images. Agents without image input cannot read them.
- The global-fit parameters are specific to the cell types and aging conditions in the paper. They are not universal constants.
- Conversion status: `reviewed_with_limitations`. Every page was checked against the PDF. The remaining limitations are documented parser differences (subscripted dataset IDs, superscript exponents, rejoined URLs). No content was changed. The only difference from the verified build is a shorter `description` in `SKILL.md`, because the Claude apps accept at most 200 characters.

## License and attribution

The article is published open access under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This repository is an adaptation of that article. Text, figures and tables were converted to Markdown, JPEG and CSV. Layout artefacts were repaired, and equations were additionally transcribed as text. The scientific content was not modified. This repository is released under CC BY 4.0 as well, see `LICENSE`. Please cite the original article, see `CITATION.cff`.

Conversion tool: Paper2Agent, J. Miao, J.R. Davis, Y. Zhang, J.K. Pritchard, J. Zou, *Reimagining research papers as interactive and reliable AI agents*, Nature (2026). https://doi.org/10.1038/s41586-026-11044-y

## Contact

Marco Fischer, Chair of Electrical Energy Storage Technology (EES), Technical University of Munich, marco.fischer@tum.de
