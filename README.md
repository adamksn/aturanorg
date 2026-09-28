<p align="center">
  <a href="https://aturan.org">
    <img src="logo/logo-aturanorg.png" alt="Aturan.org" height="80" />
  </a>
</p>

<h1 align="center">Aturan.org</h1>

<h3 align="center">Indonesia’s First Public Semantic Search for Laws and Regulations</h3>

<p align="center">
  <a href="https://aturan.org">Website</a> ·
  <a href="https://aturan.org/mcp">MCP Server</a> ·
  <a href="https://aturan.org/api">REST API</a> ·
  <a href="https://aturan.org/discover">Discover</a>
</p>

<p align="center">
  <a href="https://aturan.org"><img src="https://img.shields.io/badge/Legal_Knowledge-Aturan.org-184B3B?style=flat" alt="Legal Knowledge by Aturan.org" /></a>
  <a href="https://aturan.org/mcp"><img src="https://img.shields.io/badge/MCP-Server-2463EB?style=flat" alt="MCP Server" /></a>
  <img src="https://img.shields.io/badge/Search-Exact_Nearest_Neighbor-184B3B?style=flat" alt="Search using Exact Nearest Neighbor" />
</p>

---

Aturan.org helps people and AI systems retrieve Indonesian regulations and the provisions within them. It is AI-ready through a remote **Model Context Protocol (MCP)** server, and is available through a REST API and web app for legal research.

> Aturan.org is a retrieval system, not an automated legal-opinion service. Always read the full text and context of a provision before relying on it.

## Why Aturan.org

Legal research often begins with a document name, but legal questions usually begin with an issue: a right, obligation, prohibition, procedure, sanction, authority, or condition. Keyword search alone can make it difficult to find the relevant provision when the regulation is not yet known.

Aturan.org enables semantic retrieval at the **Pasal** level, so a legal question can be used to discover relevant provisions and the regulations that contain them. An AI agent can then read the complete text of selected provisions before producing analysis with grounded references.

## What you can do

| Capability | What it does |
| --- | --- |
| Semantic Pasal search | Finds provisions relevant to a legal concept, right, obligation, procedure, or sanction. |
| Regulation discovery | Maps regulations related to an issue, across regulation types and hierarchies. |
| Title and identity search | Finds a regulation when its title, type, number, or year is known. |
| Full provision reading | Retrieves the complete text of a selected Pasal before it is cited or analysed. |
| AI integration | Connects compatible AI clients and agents through remote MCP over Streamable HTTP. |
| REST API and web app | Makes the same legal-research workflow usable for applications and people. |
| Research exports | Exports search results to DOCX for sharing and further work. |
| Saved collections | Lets users bookmark relevant Pasal into personal collections. |

## Search from the landing page

The Aturan.org landing page is always ready for legal research. Users can start a search immediately in one of two modes:

| Mode | Best for | What it finds |
| --- | --- | --- |
| **Cari Peraturan Terkait** | Broad issues, policy research, and early-stage legal mapping. | Regulations related to an issue, with semantic Pasal hits to inspect next. |
| **Cari Pasal Terkait** | A specific right, obligation, prohibition, procedure, sanction, or legal concept. | Candidate Pasal that are semantically relevant to the query. |

Search results can be exported as a **DOCX** document and important provisions can be bookmarked into a **Pasal collection**, so research can continue beyond a single search session.

## Connect an AI client

Aturan.org provides a remote MCP server via **Streamable HTTP**. It can be used with MCP-capable clients such as [Cherry Studio](https://cherryai.com/), [Agora](https://play.google.com/store/apps/details?id=com.newoether.agora), and other compatible agents or frameworks.

### Public test connection

MCP endpoint:

```text
https://mcp.aturan.org/mcp
```

Use this header:

```http
Authorization: Bearer aturanorg-mcp-ujicoba-1234567890abcdef
```

The public token is only for evaluation. It may be rotated, rate-limited, or disabled at any time. Do not use it as a production credential or embed it in a public application. It is different from an Aturan.org REST API key.

### Cherry Studio configuration

Add the following server configuration, then refresh or reconnect the MCP client so it loads the available tools.

```json
{
  "mcpServers": {
    "aturanorg": {
      "url": "https://mcp.aturan.org/mcp",
      "headers": {
        "Authorization": "Bearer aturanorg-mcp-ujicoba-1234567890abcdef"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## MCP tools

| Tool | Use it when | Returns |
| --- | --- | --- |
| `cari_judul_peraturan` | The regulation’s title, type, number, or year is known. | Matching regulation records and `regulation_id`. |
| `cari_pasal_terkait` | You need a relevant norm or Pasal, but do not yet know the regulation. | Semantically relevant candidate provisions. |
| `cari_peraturan_terkait` | You need to map regulations related to an issue. | Grouped regulations with semantic Pasal hits. |
| `baca_isi_pasal` | A candidate provision must be read in full. | The full text of one selected Pasal. |

## From retrieval to agentic legal research

Each tool returns a different kind of evidence. Used once, a tool helps answer one retrieval need. Used together by an agentic LLM, the four tools form a research loop: the model can map an issue, find candidate norms, resolve an exact regulation, read the complete provision, and refine the next retrieval from what it learned.

This makes analysis easier to ground because the agent is not forced to answer from a single search result or its internal knowledge. It can collect the relevant primary material first, then separate what the regulation says from its own interpretation.

| Tool | Distinct contribution in an agentic workflow |
| --- | --- |
| `cari_peraturan_terkait` | The **wide-angle lens**: discovers the legal landscape and groups related regulations from semantic Pasal hits. |
| `cari_pasal_terkait` | The **norm finder**: surfaces provisions that are semantically close to a focused legal issue. |
| `cari_judul_peraturan` | The **identity resolver**: finds the precise regulation when its name, type, number, year, or title fragment is known. |
| `baca_isi_pasal` | The **source check**: obtains the full text of a selected provision before it is quoted or relied on. |

An agent should use only the tools that add information. The results are complementary, not interchangeable: regulation discovery answers *which documents may matter*; Pasal search answers *which norms may matter*; title search answers *which exact document is meant*; and full-text reading answers *what the provision actually says*.

### Agentic workflow

```text
question or legal issue
        ↓
plan one or more focused queries
        ↓
cari_peraturan_terkait ──→ map candidate regulations
        ↓                         │
cari_pasal_terkait ──────→ find candidate norms
        ↓                         │
cari_judul_peraturan ────→ resolve a known document and regulation_id
        ↓
baca_isi_pasal ──────────→ verify full wording of selected provisions
        ↓
compare, refine, retrieve again if needed, then analyse
```

The final analysis is still an analysis, not an automated legal conclusion. It should state the retrieved text and sources separately from any interpretation, and flag where further verification is needed.

## Four complementary scenarios

### 1. Broad issue: build the legal landscape first

**Question:** “What regulations relate to administrative sanctions in mining business activities?”

1. Start with `cari_peraturan_terkait("sanksi administratif dalam kegiatan usaha pertambangan")` to discover a broad set of related regulations and their `semantic_hits`.
2. Inspect the resulting groups: regulation type, year, status, and the candidate Pasal numbers in `semantic_hit_pasals`.
3. Run narrower follow-up queries where necessary, for example `kewajiban pemegang izin usaha pertambangan` or `prosedur pengenaan sanksi administratif pertambangan`.
4. Use `baca_isi_pasal` only for selected candidate provisions before describing the sanctions or procedure.

**Why all results matter:** regulation discovery prevents the research from starting with a single assumed document; focused Pasal search narrows the question; full-text reading prevents a semantic preview from being mistaken for the rule itself.

### 2. Specific norm: find the relevant Pasal, then widen the check

**Question:** “What are the rights of an heir receiving BPJS Ketenagakerjaan death benefits?”

1. Start with `cari_pasal_terkait("hak ahli waris penerima manfaat jaminan kematian BPJS Ketenagakerjaan")` to find candidate norms directly.
2. Read the strongest candidates with `baca_isi_pasal`, using only their returned `regulation_id` and Pasal numbers.
3. Use `cari_peraturan_terkait` with the same or a refined query to check whether the issue is also addressed in other related regulations.
4. If the agent needs to verify a regulation mentioned in the results by its formal identity, use `cari_judul_peraturan` before reading further provisions.

**Why the results differ:** Pasal search is optimized to surface a concrete norm. Regulation discovery may reveal related documents that a single norm-level search does not make obvious. The agent can use both without treating either as a conclusion.

### 3. Known document: resolve the identity, then read the exact rule

**Question:** “What does PP 45 Tahun 2009 say about a particular requirement?”

1. Run `cari_judul_peraturan("PP 45 Tahun 2009")` to resolve the regulation and obtain its actual `regulation_id`.
2. If a Pasal number is already known, call `baca_isi_pasal(regulation_id, pasal)` to read the full text.
3. If the relevant Pasal number is not known, use `cari_pasal_terkait` with the substantive requirement as the query, then read the candidate Pasal returned for that regulation.
4. When the question may have implications outside that document, use `cari_peraturan_terkait` to discover related regulations before forming an analysis.

**Why the results differ:** title search establishes *which document* is being discussed; Pasal search helps find *where inside the legal material* the requirement is discussed; the reading tool verifies *the actual wording*.

### 4. Complex issue: split one question into several retrieval paths

**Question:** “How is PLTS atap regulated, and what are the obligations of an electricity provider?”

An agent should avoid one oversized semantic query. Instead, it can work through focused paths:

```text
cari_peraturan_terkait("pengaturan PLTS atap")
cari_pasal_terkait("perizinan PLTS atap")
cari_pasal_terkait("kewajiban pemegang izin usaha penyediaan tenaga listrik terkait PLTS atap")
cari_pasal_terkait("ekspor impor energi listrik PLTS atap")
cari_pasal_terkait("kapasitas pemasangan PLTS atap")
```

The agent compares the resulting regulations and candidate provisions, uses `cari_judul_peraturan` to resolve any document it needs to identify exactly, and calls `baca_isi_pasal` for every provision that will support its explanation.

**Result:** instead of one shallow answer, the agent can produce a structured research trail: the relevant regulatory landscape, each issue-specific norm, the full wording that supports each point, and a clearly marked interpretation.

### Example prompts

After connecting the MCP server, ask an AI client questions such as:

```text
Temukan ketentuan tentang kewajiban pemberi kerja mendaftarkan pekerja
ke program jaminan sosial.
```

```text
Regulasi apa saja yang berkaitan dengan sanksi administratif
dalam kegiatan usaha pertambangan?
```

```text
Cari PP 45 Tahun 2009, lalu bacakan Pasal yang mengatur topik terkait.
```

## Retrieval workflow

```text
DISCOVER → IDENTIFY → READ → ANALYZE
```

1. **Discover** — use title search, Pasal search, or regulation discovery to retrieve candidates.
2. **Identify** — evaluate the title, type, year, status, metadata, and semantic hits.
3. **Read** — retrieve the full text of the relevant Pasal using `baca_isi_pasal`.
4. **Analyze** — distinguish the text of the norm, relations between regulations, interpretation, and your conclusion.

Choose the tool based on what is known:

```text
Known regulation identity
cari_judul_peraturan → regulation_id → baca_isi_pasal

Known legal issue or norm
cari_pasal_terkait → evaluate candidates → baca_isi_pasal → analyze

Need to map the legal landscape
cari_peraturan_terkait → evaluate groups → semantic_hit_pasals → baca_isi_pasal → analyze
```

## Using semantic retrieval well

Write queries as the legal substance you need, rather than as a conversational instruction.

| Prefer | Instead of |
| --- | --- |
| `hak ahli waris penerima manfaat program jaminan kematian BPJS Ketenagakerjaan` | `bagaimana jaminan kematian BPJS Ketenagakerjaan untuk ahli waris pekerja yang meninggal` |
| `jenis alat bukti yang sah dalam hukum acara pidana` | `apa saja alat bukti yang sah?` |

For a complex issue, break it into several focused retrievals. For example, research on PLTS atap may need separate queries on licensing, an electricity provider’s obligations, electricity export and import, and installation capacity.

## Principles for AI agents

- **Retrieve before reasoning.** Use retrieval when an analysis depends on a regulation or Pasal.
- **Read before citing.** A semantic hit is a candidate, not a substitute for the full wording of a provision.
- **Do not fabricate references.** Only present regulation identities, Pasal numbers, and text returned by Aturan.org as retrieval results.
- **Use `regulation_id` only from tool results.** Do not invent or guess it.
- **Iterate when necessary.** Inspect results, refine the query, retrieve again, then read the selected provisions.

## Limitations

Semantic search ranks candidates by relevance. It does not by itself establish that a provision applies to every fact pattern, is the controlling legal basis, remains in force without amendment, or supports a particular interpretation.

Before drawing a legal conclusion, evaluate the complete text and context of the Pasal, the regulation’s status and amendments, the relationship and hierarchy of relevant regulations, and the facts at issue.

## Public architecture

The diagram below describes the public Aturan.org retrieval architecture. It intentionally focuses on the product interfaces and retrieval flow—not private infrastructure or implementation details.

```text
                         ┌───────────────────────────────────┐
                         │  Indonesian regulation corpus     │
                         │  288,826 regulations              │
                         │  5,339,903 structured Pasal       │
                         └─────────────────┬─────────────────┘
                                           │
                                           ▼
                    ┌──────────────────────────────────────────────┐
                    │            Aturan.org Retrieval Core         │
                    │                                              │
                    │  · title / identity retrieval                │
                    │  · Exact Nearest Neighbor semantic search    │
                    │  · Pasal-level candidate retrieval           │
                    │  · regulation grouping and full Pasal read   │
                    └───────────────┬─────────────┬────────────────┘
                                    │             │
                ┌───────────────────┘             └──────────────────┐
                ▼                                                    ▼
┌─────────────────────────────────┐                 ┌────────────────────────────────────┐
│  MCP Server · Streamable HTTP   │                 │  Aturan.org web app and REST API   │
│                                 │                 │                                    │
│  · cari_judul_peraturan         │                 │  · issue and regulation discovery  │
│  · cari_pasal_terkait           │                 │  · legal research workflows        │
│  · cari_peraturan_terkait       │                 │  · application integration         │
│  · baca_isi_pasal               │                 │                                    │
└───────────────┬─────────────────┘                 └────────────────┬───────────────────┘
                │                                                    │
                ▼                                                    ▼
┌─────────────────────────────────┐                 ┌────────────────────────────────────┐
│  AI clients and agentic LLMs    │                 │  Researchers and applications      │
│                                 │                 │                                    │
│  retrieve → read → analyse      │                 │  search · inspect · integrate      │
│  with grounded source material  │                 │                                    │
└─────────────────────────────────┘                 └────────────────────────────────────┘
```

## Retrieval design

Aturan.org is designed as a legal-research system in which each retrieval mode has a different job. Rather than asking one search endpoint to answer every question, the system separates document identity, norm discovery, regulatory landscape discovery, and source verification.

| Retrieval layer | Method | Purpose |
| --- | --- | --- |
| Regulation identity | Literal/full-text title search | Resolves a known title, type, number, year, or title phrase. |
| Norm discovery | Exact Nearest Neighbor semantic retrieval at Pasal level | Finds candidate provisions relevant to a legal concept. |
| Landscape discovery | Aggregated Pasal-level semantic retrieval | Maps regulations connected to an issue, with candidate Pasal hits. |
| Source verification | Full Pasal retrieval | Reads the complete wording of one provision before citation or analysis. |

### Built for grounded, multi-step research

- **Exact Nearest Neighbor, not ANN/HNSW.** Semantic retrieval uses an exact nearest-neighbor approach rather than approximating the nearest retrieved candidates through an ANN index.
- **GPU-sharded exact search.** The candidate space is searched across GPU shards and the resulting candidates are merged globally. This makes exact retrieval practical at corpus scale while avoiding the recall trade-off of approximate ANN/HNSW indexes, where relevant near-neighbours can be missed.
- **Pasal-first retrieval.** A legal issue is matched to candidate norms at the provision level, then connected back to the regulations that contain them.
- **Separate discovery from verification.** A semantic hit helps select what to inspect; `baca_isi_pasal` retrieves the complete provision that supports any later explanation.
- **Agentic by design.** An LLM can run several focused retrievals, compare their outputs, read selected provisions, and refine its next query before drafting analysis.
- **Stable retrieval references.** The gateway returns `regulation_id` values for use in subsequent provision reads. Agents must obtain them from results rather than constructing them.
- **Bounded, focused queries.** MCP tools accept a substantive query and constrained `top_k` results, making it practical to iterate from broad landscape mapping to a particular Pasal.

### Deployment and operating principles

- **Institution-ready by design.** Aturan.org is engineered with on-premise deployment in mind, so institutions and enterprises can adopt the retrieval architecture within their own infrastructure, governance, and data-boundary requirements.
- **Practical tool calling.** Tool-calling workflows are deliberately tested with models in the 4B class. This establishes a demanding efficiency baseline: if a smaller model can execute a useful retrieval workflow, larger models have additional headroom for planning and analysis.
- **Coverage at the time of writing.** The corpus contains **288,826 regulations** and **5,339,903 structured Pasal**. Coverage and counts will evolve as the corpus is expanded and maintained.

## Interfaces

| Surface | Address | Role |
| --- | --- | --- |
| Web app | [aturan.org](https://aturan.org) | Human-facing legal discovery and research. |
| MCP Server | [aturan.org/mcp](https://aturan.org/mcp) | Remote MCP connection for AI clients and agents. |
| REST API | [aturan.org/api](https://aturan.org/api) | Application integration. |
| Discover | [aturan.org/discover](https://aturan.org/discover) | Entry point for exploring Aturan.org. |

## Service access

Aturan.org offers free and paid access tiers. Access to the hosted web app, MCP server, and REST API is governed by the applicable service terms, credentials, quotas, and plan limits.

The logo and the Aturan.org name are proprietary brand assets. A future repository license will apply only to the source code and documentation that are actually published in this repository; it will not govern the private backend or replace the service terms.
