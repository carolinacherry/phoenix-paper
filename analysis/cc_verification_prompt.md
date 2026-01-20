# Claude Code Verification Prompt

Use this prompt with Claude Code to independently verify claims in the Phoenix paper against the source repository.

## Prerequisites

Clone the X algorithm repository:
```bash
git clone https://github.com/xai-org/x-algorithm.git
cd x-algorithm
```

## Verification Prompt

Copy and paste the following prompt into Claude Code:

---

**Prompt:**

I need you to verify claims from a technical paper about X's Phoenix recommendation system against this repository. For each claim, please:

1. Search for the relevant code/documentation
2. Confirm whether the claim is accurate
3. Provide the specific file path and line numbers as evidence

**Claims to verify:**

### Architecture Claims

1. Phoenix uses a two-stage pipeline (retrieval + ranking)
2. The retrieval stage uses a two-tower model with ANN search
3. The transformer is based on Grok-1 architecture
4. The transformer config includes:
   - Grouped Query Attention (separate `num_q_heads` and `num_kv_heads`)
   - RoPE (Rotary Positional Embeddings)
   - RMSNorm (not LayerNorm)
   - Widening factor for FFN (default 4.0)

### Candidate Isolation Claims

5. A function `make_recsys_attn_mask` exists in `phoenix/grok.py`
6. The attention mask prevents candidates from attending to other candidates
7. Candidates can attend to user context (user embedding + engagement history)

### Engagement Signals

8. Phoenix predicts 19 engagement types
9. Verify these specific signals exist in `runners.py`:
   - Positive: favorite, reply, repost, photo_expand, click, profile_click, vqv, share, share_via_dm, share_via_copy_link, dwell, quote, quoted_click, follow_author
   - Negative: not_interested, block_author, mute_author, report
   - Continuous: dwell_time

### Candidate Sources

10. Thunder serves in-network posts using DashMap
11. Thunder has three timeline indices: original, secondary, video
12. Pre-ranking filters exist (count them)

### Post-Ranking

13. Author Diversity Scorer exists in `home-mixer/scorers/`
14. It uses a decay-based formula for repeated authors

### Transparency

15. `weighted_scorer.rs` exists but actual weight values are not disclosed
16. No model checkpoint/weight files are included in the repository

---

For each claim, respond with:
- **Claim #X**: [VERIFIED/NOT VERIFIED/PARTIALLY VERIFIED]
- **Evidence**: [File path and relevant code snippet or explanation]

---

## Expected Output

A comprehensive verification report confirming or refuting each claim with specific file references from the repository.

## Notes

- The paper references commit `aaa167b` from January 19, 2026
- Repository statistics cited: 6.1k stars, 1k forks, Apache 2.0 license
- Some details may have changed if the repository has been updated since the paper was written
