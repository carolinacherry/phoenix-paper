# Phoenix Paper Verification Checklist

All claims in this paper have been verified against the public repository at [github.com/xai-org/x-algorithm](https://github.com/xai-org/x-algorithm) (commit `aaa167b`, January 19, 2026).

## Repository Metadata

| Claim | Verified | Source |
|-------|----------|--------|
| Repository URL: `github.com/xai-org/x-algorithm` | Yes | Direct observation |
| Commit hash: `aaa167b` | Yes | Repository inspection |
| Release date: January 19, 2026 | Yes | Commit history |
| Stars: 6.1k | Yes | Repository page |
| Forks: 1k | Yes | Repository page |
| License: Apache 2.0 | Yes | LICENSE file |

## Architectural Claims

| Claim | Verified | Source File |
|-------|----------|-------------|
| Two-stage pipeline (retrieval + ranking) | Yes | `phoenix/README.md`, system docs |
| Retrieval uses two-tower model | Yes | `phoenix/retrieval/two_tower.py` |
| Transformer based on Grok-1 | Yes | `phoenix/grok.py` header comments |
| Grouped Query Attention (GQA) | Yes | `phoenix/grok.py:TransformerConfig` |
| RoPE positional embeddings | Yes | `phoenix/grok.py:TransformerConfig` |
| RMSNorm (not LayerNorm) | Yes | `phoenix/grok.py:TransformerConfig` |
| Widening factor default 4.0 | Yes | `phoenix/grok.py:TransformerConfig` |

## Candidate Isolation

| Claim | Verified | Source File |
|-------|----------|-------------|
| `make_recsys_attn_mask` function exists | Yes | `phoenix/grok.py` |
| Candidates cannot attend to other candidates | Yes | `phoenix/grok.py` mask implementation |
| Candidates can attend to user context | Yes | `phoenix/grok.py` mask implementation |
| Enables batch-independent scoring | Yes | Function docstring |

## Engagement Signals (19 total)

| Index | Signal Name | Verified | Source |
|-------|-------------|----------|--------|
| 0 | `p_favorite_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 1 | `p_reply_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 2 | `p_repost_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 3 | `p_photo_expand_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 4 | `p_click_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 5 | `p_profile_click_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 6 | `p_vqv_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 7 | `p_share_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 8 | `p_share_via_dm_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 9 | `p_share_via_copy_link_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 10 | `p_dwell_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 11 | `p_quote_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 12 | `p_quoted_click_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 13 | `p_follow_author_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 14 | `p_not_interested_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 15 | `p_block_author_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 16 | `p_mute_author_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 17 | `p_report_score` | Yes | `phoenix/runners.py:RankingOutput` |
| 18 | `p_dwell_time` (continuous) | Yes | `phoenix/runners.py:RankingOutput` |

## Candidate Sources

| Claim | Verified | Source File |
|-------|----------|-------------|
| Thunder serves in-network posts | Yes | `thunder/README.md` |
| Thunder uses DashMap (concurrent hashmap) | Yes | `thunder/src/timeline_store.rs` |
| Three timeline indices (original, secondary, video) | Yes | `thunder/src/timeline_store.rs` |
| Phoenix Retrieval for out-of-network posts | Yes | `phoenix/retrieval/` directory |
| L2-normalized embeddings | Yes | `phoenix/retrieval/two_tower.py` |
| 13 pre-ranking filters | Yes | `home-mixer/filters/` directory |

## Post-Ranking Diversity

| Claim | Verified | Source File |
|-------|----------|-------------|
| Author Diversity Scorer exists | Yes | `home-mixer/scorers/author_diversity_scorer.rs` |
| Uses decay-based multiplier | Yes | `author_diversity_scorer.rs` implementation |
| Formula: `(1.0 - floor) * decay^position + floor` | Yes | `author_diversity_scorer.rs` |

## Transparency Limitations

| Claim | Verified | Source |
|-------|----------|--------|
| `weighted_scorer.rs` exists | Yes | `home-mixer/scorers/weighted_scorer.rs` |
| Actual weight values not disclosed | Yes | File inspection (values redacted/absent) |
| Model weights not released | Yes | No checkpoint files in repository |
| Documentation states weights have positive/negative signs | Yes | `docs/scoring.md` |

---

*Verification performed: January 2026*
*Verifier: Claude Code (Anthropic)*
