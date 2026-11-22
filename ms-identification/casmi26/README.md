# CASMI 2026 method graph (ChemField · mass-spectrometry identification)

A signed [Knitweb](https://github.com/Knitweb) fabric of the **methods used in the public notebooks of the
[CASMI 2026 molecule-identification competition](https://www.kaggle.com/competitions/enveda-CASMI26-molecule-id-mass-spectra)**
(MS/MS spectrum → molecular structure). It shows the method components, which ones go together, how the notebooks
descend from each other (forks), and the score claims the notebooks state publicly.

**Viewer:** [`web/casmi26/`](../../web/casmi26/), also served at knitweb.art/chemfield/casmi26/ once deployed.

## Files

| File | What |
|---|---|
| `records.jsonl` | 2,285 signed records (`record`, `sig`, `author_pub`): 46 method components (43 occur), 8 method families, 2,046 notebooks, 169 dataset slugs, 6 leaderboard groups, 5 background categories, 5 Kaggle tiers |
| `edges.jsonl` | 49,955 edges: `usesMethod`, `usesDataset`, `forkOf`, `coOccurs` (weight = notebooks), `inFamily`, `authorTeamIn` (notebook → leaderboard group), `groupUsesMethod`, `groupBackground`, `groupKaggleTier` (aggregate team counts) |
| `summary.json` | component usage, median score claim per component (≥ 5 claims), co-occurrence counts, fabric author, Merkle root |

## Record kinds

- `casmi-kg-component`: `name` (for example *DreaMS*, *ICEBERG*, *RRF*, *documentation prior*).
- `casmi-kg-notebook`: `kernel_id`, `slug`, `title`, `url` (the original public notebook), `votes`,
  `score_claim_milli` (highest MRR@25 the notebook states, ×1000; 0 = none), `n_components`, `has_code`.
- `casmi-kg-dataset`: `slug` of an attached public dataset (owner omitted).
- `casmi-kg-family`: one of 8 method families (spectral similarity & library, candidate sources & generation, forward models,
  inverse models & embeddings, priors, learning to rank, fusion & assignment, data hygiene).
- `casmi-kg-lbgroup`: a public-leaderboard rank band (`gid`, `rank_from`, `rank_to`, `teams`, `median_score_milli`,
  `median_submissions`, `notebooks`, `snapshot_lb`). A notebook links to a group when its author is a member of a team in
  that band (public notebook author + public leaderboard membership, coarsened to bands).
- `casmi-kg-background`, `casmi-kg-kaggle-tier`: categories that only carry **aggregate** team counts per group (from the
  public Meta Kaggle dataset); no per-person data.

Integers only (Knitweb convention). Components are detected in the public notebook text with fixed regular expressions,
so a component counts as "used" when the notebook names it. That is a mention, not proof of use.

## Provenance and scope

- **Source:** public Kaggle notebooks of the competition. The record holds their metadata and detected components, plus
  a link to each original. Nothing is re-hosted.
- **Not included:** author profiles, per-person background or rankings, research notes, inferences about people, full notebook texts.
- **Score claims** are what notebooks state, not verified leaderboard results.

## Verify

Each record is signed with secp256k1-ECDSA by the fabric author `pls1ad4s4mkw63nvis3evsyranwgjq7m75mfhq`. The Merkle
root over `sha256(json.dumps(line, sort_keys=True))` of all signed record lines is in `summary.json`.

```python
import json
from knitweb.core import crypto
from knitweb.fabric.attest import verify_record
recs = [json.loads(l) for l in open('records.jsonl')]
print(all(verify_record(r['record'], r['author_pub'], r['sig']) for r in recs))   # True: every signature valid
root = crypto.merkle_root([crypto.sha256(json.dumps(r, sort_keys=True).encode()) for r in recs]).hex()
print(root == json.load(open('summary.json'))['records_merkle_root'])
```

Built by Claude (Opus 5.5) for VEther / Knitweb, 22 November 2026. Data derived from public sources; code and page Apache-2.0.
