# Phoenix: Candidate-Isolated Transformer Ranking in X's Recommendation System

**A Technical Analysis of the 2026 Open-Source Release**

*Daniel An*
*January 2026*

## Overview

This repository contains a technical analysis of X's Phoenix recommendation system, released on January 19, 2026. Phoenix is a Grok-based transformer that replaced X's previous feature-engineered Heavy Ranker.

## Key Contributions

- **Comparative Analysis**: Detailed comparison of X's 2023 Heavy Ranker and 2026 Phoenix architectures
- **Candidate Isolation**: Technical examination of the novel attention pattern that ensures batch-independent scoring
- **Engagement Signals**: Enumeration and analysis of the 19 engagement signals predicted by Phoenix
- **Transparency Discussion**: Analysis of what remains undisclosed and implications for algorithmic auditing
- **Production System Comparison**: Phoenix contextualized against YouTube, TikTok/ByteDance Monolith, and Instagram architectures

## Repository Structure

```
phoenix-paper/
├── README.md
├── LICENSE
├── .gitignore
├── paper/
│   ├── phoenix_paper.tex       # LaTeX source
│   └── phoenix_paper.pdf       # Compiled paper
└── analysis/
    ├── verification_checklist.md    # Verified claims with source references
    └── cc_verification_prompt.md    # Prompt for re-verifying claims
```

## Verification

All code references in this paper have been verified against the public repository at [`github.com/xai-org/x-algorithm`](https://github.com/xai-org/x-algorithm) (commit `aaa167b`, January 19, 2026).

See [`analysis/verification_checklist.md`](analysis/verification_checklist.md) for a detailed breakdown of verified claims.

## Citation

```bibtex
@article{an2026phoenix,
  title={Phoenix: Candidate-Isolated Transformer Ranking in X's Recommendation System},
  author={An, Daniel},
  journal={GitHub Repository},
  year={2026},
  month={January},
  url={https://github.com/carolinacherry/phoenix-paper}
}
```

## License

This work is licensed under the [MIT License](LICENSE).
