# Quantum India Registry

[![Data licence: CC BY 4.0](https://img.shields.io/badge/data%20licence-CC--BY--4.0-blue.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Code licence: Apache 2.0](https://img.shields.io/badge/code%20licence-Apache--2.0-green.svg)](LICENSE)
[![Live registry](https://img.shields.io/badge/live-rslquantum.com%2Fquantum--india-orange)](https://rslquantum.com/quantum-india/)

Open, machine-readable registry of Indian quantum-technology companies and a rolling 30-day feed of India-affiliated quantum papers.

Maintained by [RSL Quantum Private Limited](https://rslquantum.com), New Delhi (CIN U62010DL2026PTC466369).

## Why this exists

India's quantum-tech sector is fragmented across academia, public-sector units, and private companies. There is no consolidated public dataset listing which Indian companies operate in quantum computing, sensing, communications, materials, or post-quantum cryptography. This repository fills that gap.

The registry is **append-only and verifiable**. Every entry must cite at least one third-party public source (PlanetExim, Falconebiz, MCA disclosure, arXiv paper, news article from a reputable outlet, or government grant record). CIN-only entries are rejected.

## What's in here

| Path | Contents | Updated |
|---|---|---|
| `data/companies.json` | Verified company registry | On merge |
| `data/companies.csv` | Same, flat | On merge |
| `data/papers.json` | 30-day rolling India-affiliated arXiv window | Daily (GitHub Actions) |
| `data/meta.json` | Counts, source freshness, errors | Daily |
| `schema/company.schema.json` | JSON Schema 2020-12; PRs must validate | Versioned |
| `scripts/verify.mjs` | Entry verifier (MCA / PlanetExim / Falconebiz / arXiv / OpenAlex) | — |
| `.github/ISSUE_TEMPLATE/` | Add, fix, or remove an entry | — |
| `CITATION.cff` | Citation File Format metadata | Versioned |

Live mirror: <https://rslquantum.com/quantum-india/data/companies.json>

## Quickstart

```bash
git clone https://github.com/RSL-Quantum/quantum-india-registry
cd quantum-india-registry
npm install
# Verify an entry against MCA + at least one external source
node scripts/verify.mjs --cin U72200KA2016PTC094502
# Validate the registry against the schema
node scripts/validate.mjs
```

## How to add a company

1. Open an issue with the **"Add a company"** template.
2. Provide: CIN, official URL, primary quantum subdomain (computing / sensing / communications / materials / PQC / software), and ≥1 third-party source link.
3. A maintainer runs `node scripts/verify.mjs --cin <CIN>`.
4. On pass, the entry moves from `_verification_drafts[]` → `rows[]`, the schema validates, and CI publishes.

CIN-only entries with no public domain and no third-party citation are rejected. We do not chase rumours.

## How to add a paper

Papers are pulled automatically nightly by `.github/workflows/sync.yml` from OpenAlex with the query `concepts.id:C121332964 AND authorships.countries:IN AND from_publication_date:<today-30>`. Manual additions go through the same issue template.

## Citing this dataset

```bibtex
@misc{rslq_quantum_india_registry_2026,
  author       = {RSL Quantum Private Limited},
  title        = {Quantum India Registry},
  year         = {2026},
  version      = {0.1.0},
  url          = {https://rslquantum.com/quantum-india/},
  doi          = {10.5281/zenodo.PLACEHOLDER},
  note         = {Data CC-BY-4.0, code Apache-2.0}
}
```

## Licences

- **Data** (`data/**`): CC BY 4.0. You may copy, redistribute, remix, and build commercial products on this data, provided you attribute *"Quantum India Registry, RSL Quantum, https://rslquantum.com/quantum-india/"* and link to the licence.
- **Code** (everything else): Apache 2.0.

## Related

- [`quanta-rag`](https://github.com/RSL-Quantum/quanta-rag) — the RAG pipeline behind the Quanta chatbot on rslquantum.com.
- [`pqc-benchmarks`](https://github.com/RSL-Quantum/pqc-benchmarks) — open post-quantum cryptography benchmark suite (Kyber, Dilithium, Falcon, SPHINCS+).

## Contact

- Issues: <https://github.com/RSL-Quantum/quantum-india-registry/issues>
- Email: <research@rslquantum.com> (alias `quantum-india@rslquantum.com`)
- Bluesky: [@rslquantum.bsky.social](https://bsky.app/profile/rslquantum.bsky.social)
- Mastodon: [@rslquantum@mastodon.social](https://mastodon.social/@rslquantum)
