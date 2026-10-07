<p align="center">
  <a href="https://aturan.org">
    <img src="logo/logo-aturanorg-192.png" alt="Aturan.org" />
  </a>
</p>

<h1 align="center">Aturan.org</h1>

<h3 align="center">Semantic Legal Retrieval for Indonesian Regulations</h3>

<p align="center">
  Find legal norms by meaning. Verify the source.<br />
  Grounded regulatory data for people, applications, and AI agents.
</p>

<p align="center">
  <a href="https://aturan.org">Website</a> ·
  <a href="https://aturan.org/mcp">MCP Server</a> ·
  <a href="https://aturan.org/api">REST API</a> ·
  <a href="https://aturan.org/discover">Discover</a>
</p>

<p align="center">
  <a href="https://aturan.org"><img src="https://img.shields.io/badge/Legal_Knowledge-Aturan.org-184B3B?style=flat" alt="Legal Knowledge by Aturan.org" /></a>
  <a href="https://aturan.org/mcp"><img src="https://img.shields.io/badge/MCP-Streamable_HTTP-2463EB?style=flat" alt="MCP Streamable HTTP" /></a>
  <img src="https://img.shields.io/badge/Retrieval-Pasal_Level-184B3B?style=flat" alt="Pasal-level retrieval" />
  <img src="https://img.shields.io/badge/Search-Exact_Nearest_Neighbor-184B3B?style=flat" alt="Exact Nearest Neighbor" />
  <a href="https://mcpservers.org/servers/adamksn/aturanorg"><img src="https://mcpservers.org/badge.svg" alt="Listed on mcpservers.org" />
</p>

---

## What is Aturan.org?

**Aturan.org** is a semantic legal retrieval system for Indonesian regulations.

It helps people, applications, and AI agents discover regulations and legal provisions based on **meaning and legal context**, rather than relying only on exact keywords or already knowing the title of a regulation.

Aturan.org performs semantic retrieval at the **Pasal level**. A legal issue can therefore be matched directly against candidate provisions, which can then be traced back to the regulations that contain them and read in full before being used in legal analysis.

The platform is available through:

- a public **web application** for legal research;
- a **REST API** for application and system integration; and
- a remote **Model Context Protocol (MCP) server** for AI clients and agentic workflows.

> **Aturan.org is a retrieval system, not an automated legal-opinion service.**
>
> Semantic retrieval identifies relevant legal material. Legal applicability and interpretation still require evaluation of the complete provision, regulatory context, amendments, hierarchy, and the facts being analysed.

---

## Why semantic legal retrieval?

Legal research does not always begin with the name of a regulation.

It often begins with an issue:

- What obligations apply?
- What activity is prohibited?
- What authority does an institution have?
- What procedure must be followed?
- What sanctions may apply?
- What regulations govern a particular activity?

Traditional title or keyword search works well when the researcher already knows what document or wording to search for.

But legal questions are often expressed differently from the language used by legislation.

Aturan.org addresses this by matching the **meaning of a query** against structured legal provisions.

```text
Legal question or concept
          │
          ▼
   Semantic retrieval
          │
          ▼
 Candidate Pasal
          │
          ▼
 Relevant regulations
          │
          ▼
 Read full provisions
          │
          ▼
       Analyze
```

This makes it possible to begin legal research from the **substance of the issue**, rather than from an assumed document.

---

## What you can do

| Capability | Purpose |
| --- | --- |
| **Regulation discovery** | Discover regulations connected to a legal issue across regulation types and hierarchies. |
| **Pasal-level semantic search** | Find candidate provisions related to a right, obligation, prohibition, authority, procedure, sanction, condition, or other legal concept. |
| **Regulation identity search** | Locate a regulation when its type, number, year, title, or title fragment is already known. |
| **Full-Pasal retrieval** | Read the complete wording of a selected provision before quoting or analysing it. |
| **Legal landscape research** | Explore an issue across multiple regulations and normative dimensions. |
| **AI grounding** | Give AI agents structured access to retrieved Indonesian legal material before reasoning. |
| **Application integration** | Integrate Indonesian regulatory retrieval into LegalTech, RegTech, RAG, research, and other applications. |
| **Research workflow** | Search, inspect, save, export, and continue working with retrieved legal material. |

---

## Built for people, applications, and AI

Aturan.org exposes the same legal-retrieval foundation through three different interfaces.

### Web

The web application is designed for people conducting legal and regulatory research.

Users can search by legal issue, inspect regulations and Pasal candidates, verify source material, save relevant provisions, and export research results.

**Website:**  
https://aturan.org

### REST API

The REST API provides programmatic access to Aturan.org retrieval services.

It is intended for applications, LegalTech, RegTech, RAG pipelines, enterprise systems, and developers who need explicit control over requests and responses.

**Documentation:**  
https://aturan.org/api

### MCP Server

The Aturan.org MCP Server exposes legal retrieval as tools that AI models and agents can call directly.

Instead of placing an entire legal corpus into a model context, an agent can retrieve only the regulatory material needed for the current question, inspect the results, read selected provisions, and continue its reasoning from grounded source material.

**Documentation:**  
https://aturan.org/mcp

---

## Connect your AI

Aturan.org provides a remote MCP server using **Streamable HTTP**.

```text
https://mcp.aturan.org/mcp
```

### Quick install

Connect Aturan.org to supported AI development environments using a single command:

```bash
npx add-mcp 'https://mcp.aturan.org/mcp'
```

The `add-mcp` CLI simplifies MCP server configuration for compatible AI clients and development tools.
After installation, complete authentication using OAuth or an API Key, depending on the client's capabilities.
Alternatively, configure the MCP endpoint manually in any compatible client supporting remote MCP over Streamable HTTP.
For client-specific instructions, see the [MCP documentation](https://aturan.org/mcp).

### Authentication

Aturan.org supports two authentication paths:

```text
                         Aturan.org Account
                                │
                 ┌──────────────┴──────────────┐
                 │                             │
              OAuth                        API Key
                 │                             │
        interactive access            programmatic access
                 │                             │
                 └──────────────┬──────────────┘
                                │
                                ▼
                         Aturan.org services
```

### OAuth

OAuth provides an interactive connection between a compatible client and an Aturan.org account.

The client can open the Aturan.org authorization flow in a browser, where the user signs in and grants access. The client can then manage the resulting OAuth credentials according to its own implementation.

OAuth is particularly convenient for AI services and MCP clients with native OAuth support.

### API Key

Users can create dedicated API keys directly from the **Aturan.org Dashboard**.

API keys are suitable for:

- MCP clients using bearer authentication;
- REST API integration;
- backend applications;
- automation and agent services;
- development environments; and
- server-to-server workflows.

Separate keys can be created for different clients or environments and revoked independently when no longer needed.

API keys are transmitted using the HTTP `Authorization` header:

```http
Authorization: Bearer YOUR_API_KEY
```

Do not embed API keys in public source code or expose them in client-side applications.

For current authentication details, supported clients, connection instructions, and configuration examples, see:

**https://aturan.org/mcp**

For REST API integration, see:

**https://aturan.org/api**

> Operational connection details may evolve independently from this repository. The MCP and REST API documentation are the source of truth for their respective interfaces.

---

## MCP tools

The MCP server exposes five complementary legal retrieval tools.

| Tool | Purpose |
| --- | --- |
| `cari_peraturan_terkait` | Discover regulations related to a legal issue through aggregated Pasal-level semantic retrieval. |
| `cari_pasal_terkait` | Find candidate Pasal directly by semantic similarity to a legal concept or normative issue. |
| `cari_judul_peraturan` | Resolve a known regulation from its title, type, number, year, or title fragment. |
| `baca_isi_pasal` | Retrieve the complete wording of one selected Pasal from a regulation already identified by Aturan.org. |
| `baca_isi_pasal_batch` | Retrieve multiple already-identified Pasal in one call, including across different regulations. |

Each tool answers a different retrieval question.

```text
Which regulations may matter?
        │
        └── cari_peraturan_terkait

Which norms may matter?
        │
        └── cari_pasal_terkait

Which exact regulation is this?
        │
        └── cari_judul_peraturan

What does one provision actually say?
        │
        └── baca_isi_pasal

What do several identified provisions say?
        │
        └── baca_isi_pasal_batch
```

The tools are complementary rather than interchangeable. An agent does not need to call every tool for every question. It should select the tools that add information needed for the research task.

When several relevant Pasal have already been identified, baca_isi_pasal_batch can retrieve up to 20 provisions in a single call, including provisions from different regulations.

---

## Retrieval workflow

A useful mental model for legal research with Aturan.org is:

```text
DISCOVER → IDENTIFY → READ → ANALYZE
```

### 1. Discover

Find candidate regulations or provisions.

Depending on what is already known, this may begin with:

```text
cari_peraturan_terkait
cari_pasal_terkait
cari_judul_peraturan
```

### 2. Identify

Evaluate the retrieved candidates.

Relevant signals may include:

- regulation title;
- regulation type;
- year;
- status;
- metadata;
- semantic hits;
- candidate Pasal numbers; and
- relationships with other retrieved regulations.

### 3. Read

Retrieve the complete wording of provisions that will support the analysis.

For a single provision:

```text
baca_isi_pasal
```

When several relevant Pasal have already been identified:

```text
baca_isi_pasal_batch
```

The batch tool can read up to 20 identified Pasal in one call, including Pasal from different regulations.

A semantic hit is a **candidate**, not a substitute for reading the legal provision itself.

### 4. Analyze

Only after retrieving the relevant material should the model or researcher build the substantive analysis.

The analysis should distinguish between:

```text
retrieved legal text
        ↓
relationship between regulations
        ↓
interpretation
        ↓
analytical conclusion
```

---

## Three retrieval paths

The appropriate workflow depends on what is already known.

### Known regulation

If the regulation is already identified:

```text
Known regulation
      ↓
cari_judul_peraturan
      ↓
 regulation_id
      ↓
baca_isi_pasal
      ↓
    analyze
```

### Known legal issue

If the issue or norm is known but the regulation is not:

```text
Known legal issue
      ↓
cari_pasal_terkait
      ↓
evaluate candidates
      ↓
baca_isi_pasal
or baca_isi_pasal_batch
      ↓
    analyze
```

### Regulatory landscape

If the objective is to identify the broader regulatory framework:

```text
Regulatory landscape
      ↓
cari_peraturan_terkait
      ↓
evaluate regulation groups
      ↓
inspect candidate Pasal
      ↓
baca_isi_pasal_batch
when multiple Pasal are identified
      ↓
    analyze
```

Complex legal issues can combine these paths and run several focused retrievals before analysis.

---

## Semantic retrieval

Aturan.org semantic search is designed around the **substance of legal norms**.

A useful query describes the legal concept being sought.

For example:

```text
hak ahli waris penerima manfaat program jaminan kematian BPJS Ketenagakerjaan
```

rather than:

```text
bagaimana jaminan kematian BPJS Ketenagakerjaan untuk ahli waris?
```

Or:

```text
kewajiban pemberi kerja mendaftarkan pekerja dalam program jaminan sosial
```

rather than:

```text
apa kewajiban perusahaan soal BPJS?
```

Semantic retrieval benefits from sufficient context. Queries for semantic retrieval should therefore contain enough substantive information to represent the intended legal meaning.

For complex issues, several focused queries are usually more useful than one oversized query containing every aspect of the problem.

Current query requirements and retrieval parameters are documented in the relevant API and MCP specifications.

---

## Multilingual semantic retrieval

Semantic retrieval is based on meaning rather than literal word matching.

This allows queries to be expressed differently from the wording found in Indonesian regulations, including queries written in other languages supported by the underlying multilingual embedding model.

For example:

```text
foreign investor land ownership restrictions
```

can be used as a semantic query against Indonesian regulatory provisions even though the source legislation itself is written in Indonesian.

```text
English or multilingual query
             │
             ▼
     semantic embedding
             │
             ▼
 Indonesian legal corpus
             │
             ▼
      candidate Pasal
```

This is useful for international users, cross-border research, and AI agents that may reason in a language different from the language of the underlying legal source.

Semantic similarity, however, is not legal interpretation. Retrieved candidates must still be evaluated in their complete regulatory context.

---

## Agentic legal research

Aturan.org is designed for **multi-step retrieval**, not only one-shot search.

An AI agent can use its own reasoning to formulate queries, inspect retrieval results, identify missing dimensions, retrieve again, and read selected provisions before producing an answer.

For example, a question about rooftop solar regulation may lead an agent to investigate several dimensions:

```text
pengaturan PLTS atap

perizinan PLTS atap

kewajiban pemegang izin usaha penyediaan tenaga listrik terkait PLTS atap

ekspor impor energi listrik PLTS atap

kapasitas pemasangan PLTS atap
```

The agent can then compare the regulations and Pasal candidates returned from those retrievals and read the provisions that materially support the analysis.

The workflow becomes:

```text
question
   │
   ▼
understand the issue
   │
   ▼
formulate focused queries
   │
   ▼
retrieve
   │
   ▼
inspect results
   │
   ├──────── insufficient coverage ────────┐
   │                                       │
   ▼                                       │
refine query                               │
   │                                       │
   └──────────── retrieve again ◄──────────┘
   │
   ▼
read selected provisions
   │
   ▼
compare legal material
   │
   ▼
analyze
```

This allows the model's reasoning capability and Aturan.org's retrieval capability to perform separate jobs:

> **The model reasons about what to investigate; Aturan.org retrieves the regulatory evidence.**

---

## Principles for AI agents

### Retrieve before reasoning

When an analysis depends on Indonesian regulations, retrieve the relevant legal material before relying on the model's internal knowledge.

Internal model knowledge can help formulate queries, decompose an issue, recognize legal concepts, and reason about the retrieved material.

It should not replace retrieval when a regulation, Pasal, or legal wording is being presented as the basis of the analysis.

### Read before citing

Semantic search identifies candidates.

Before quoting a provision or relying on its wording, retrieve the complete Pasal.

```text
semantic hit ≠ full legal provision
```

### Do not fabricate references

Regulation identities, Pasal numbers, `regulation_id` values, and legal text presented as Aturan.org retrieval results must come from actual retrieval results.

In particular:

```text
Never guess regulation_id.
```

### Iterate when necessary

Legal retrieval is not necessarily a one-query process.

```text
query
  ↓
inspect
  ↓
refine
  ↓
retrieve again
  ↓
read
  ↓
analyze
```

The number of retrievals should depend on the complexity of the issue and whether each additional call contributes useful evidence.

---

## Retrieval architecture

Aturan.org separates several retrieval problems that are often incorrectly treated as a single search problem.

| Retrieval layer | Method | Purpose |
| --- | --- | --- |
| **Regulation identity** | Literal/full-text title retrieval | Resolve a known regulation from its title, type, number, year, or title phrase. |
| **Norm discovery** | Pasal-level semantic retrieval | Find candidate provisions relevant to a legal concept. |
| **Landscape discovery** | Aggregated Pasal-level semantic retrieval | Map regulations connected to an issue through their relevant provisions. |
| **Source verification** | Full-Pasal retrieval | Read the complete provision before citation or analysis. |

The public architecture can be represented as:

```text
                   ┌──────────────────────────────────┐
                   │ Indonesian regulation corpus     │
                   │                                  │
                   │ structured regulations & Pasal   │
                   └────────────────┬─────────────────┘
                                    │
                                    ▼
              ┌────────────────────────────────────────────┐
              │         Aturan.org Retrieval Core          │
              │                                            │
              │  · regulation identity retrieval           │
              │  · Pasal-level semantic retrieval          │
              │  · regulation-level aggregation            │
              │  · full-Pasal retrieval                    │
              └──────────────┬──────────────┬──────────────┘
                             │              │
                 ┌───────────┘              └───────────┐
                 ▼                                      ▼
      ┌───────────────────────┐              ┌───────────────────────┐
      │      MCP Server       │              │   Web & REST API      │
      │                       │              │                       │
      │  AI tool interface    │              │ humans & applications │
      └───────────┬───────────┘              └───────────┬───────────┘
                  │                                      │
                  ▼                                      ▼
      ┌───────────────────────┐              ┌───────────────────────┐
      │ AI clients & agents   │              │ researchers, systems  │
      │                       │              │ and applications      │
      │ retrieve              │              │                       │
      │ read                  │              │ search                │
      │ reason                │              │ inspect               │
      │ analyze               │              │ integrate             │
      └───────────────────────┘              └───────────────────────┘
```

---

## Retrieval engine

Aturan.org is designed around high-recall legal discovery at the provision level.

### Pasal-first retrieval

The fundamental semantic retrieval unit is the **Pasal**.

This preserves the legal provision as a meaningful normative unit while allowing a legal concept to be matched directly against candidate norms.

Retrieved Pasal can then be connected back to the regulations that contain them.

### Exact Nearest Neighbor

Semantic retrieval uses **Exact Nearest Neighbor (ENN)** rather than an approximate nearest-neighbor index such as ANN/HNSW.

```text
query embedding
      │
      ▼
exact candidate search
      │
      ▼
global nearest candidates
      │
      ▼
candidate Pasal
```

The objective is to search the available candidate space directly rather than accepting an approximation at the retrieval layer.

For legal discovery, this design prioritizes retrieval recall: a potentially relevant neighbouring provision should not be excluded merely because an approximate index did not traverse that candidate.

### GPU-sharded exact search

The semantic candidate space can be searched across GPU shards and the results merged globally.

```text
                 query
                   │
                   ▼
            query embedding
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
    shard 1     shard 2     shard N
       │           │           │
       └───────────┼───────────┘
                   ▼
             global merge
                   │
                   ▼
          nearest Pasal
```

This architecture makes exact semantic retrieval practical at corpus scale while keeping the retrieval model conceptually simple.

### Discovery and verification are separate

Semantic retrieval answers:

> **What legal material should I inspect?**

Full-Pasal retrieval answers:

> **What does the selected provision actually say?**

Keeping those operations separate prevents a similarity result or snippet from being treated as though it were the complete legal rule.

---

## Designed for efficient agentic use

Aturan.org does not assume that legal retrieval requires the largest possible language model.

The MCP workflow is deliberately structured so that retrieval tools have clear roles, bounded inputs, and machine-readable outputs.

This makes the system suitable for tool-calling agents ranging from lightweight local models to larger frontier models.

A capable agent needs to understand a relatively small set of operations:

```text
discover regulations
find norms
resolve regulation identity
read provisions
```

The legal corpus and retrieval workload remain outside the LLM itself.

This separation allows the language model to concentrate on planning and reasoning while Aturan.org performs legal evidence retrieval.

---

## Institution and enterprise use

The retrieval architecture is designed so that the same general pattern can be used beyond the public Aturan.org service.

```text
structured legal corpus
        +
semantic retrieval
        +
legal source reading
        +
tool interface
        +
agentic LLM
```

This architecture is suitable for LegalTech, RegTech, institutional legal knowledge systems, private RAG environments, and on-premise AI deployments where organizations require greater control over infrastructure, governance, or data boundaries.

The public Aturan.org service demonstrates this retrieval model using Indonesian regulations.

---

## Interfaces

| Interface | Address | Primary role |
| --- | --- | --- |
| **Web** | https://aturan.org | Human-facing semantic legal research. |
| **MCP Server** | https://aturan.org/mcp | AI clients and agentic legal retrieval. |
| **REST API** | https://aturan.org/api | Application and system integration. |
| **Discover** | https://aturan.org/discover | Overview of available integration methods and use cases. |

The interfaces serve different users but share the same core principle:

```text
find relevant legal material
        ↓
inspect the source
        ↓
read the norm
        ↓
then analyze
```

---

## Source verification

Aturan.org is designed to support **grounded legal research**, not to replace authoritative legal sources.

Where source verification is required, users and AI systems should inspect the official source document associated with the retrieved regulation.

A retrieval result helps locate relevant legal material.

It does not transform Aturan.org into the official publisher of that material.

---

## Limitations

Semantic similarity is evidence of **retrieval relevance**, not evidence of legal applicability.

A highly similar provision does not by itself establish that the provision:

- applies to every factual situation;
- is the primary or controlling legal basis;
- remains effective without amendment;
- overrides another regulation;
- has no relevant implementing regulation;
- supports a particular interpretation; or
- leads to a particular legal conclusion.

Before drawing a legal conclusion, evaluate:

- the complete wording of the Pasal;
- the context of the provision within the regulation;
- definitions and related provisions;
- the regulation's status;
- amendments and revocations;
- implementing regulations;
- relationships between regulations;
- regulatory hierarchy; and
- the facts being analysed.

Aturan.org helps retrieve the evidence needed for that work.

The interpretation remains a separate analytical step.

---

## Documentation

Detailed and current specifications are maintained outside this README.

### MCP Server

Connection methods, OAuth, API Key authentication, MCP tools, parameters, retrieval strategy, and AI usage guidance:

**https://aturan.org/mcp**

### REST API

Authentication, endpoints, request parameters, response structures, and integration guidance:

**https://aturan.org/api**

### Discover

Comparison of the available interfaces and guidance on choosing between Web, REST API, and MCP:

**https://aturan.org/discover**

These documentation pages are the source of truth for operational specifications that may change over time.

---

## Service access

Aturan.org provides free and paid access to its hosted services.

Access conditions, authentication methods, credits, quotas, usage limits, and available plans may differ between the Web application, REST API, and MCP Server.

Users can manage their account and create or revoke API keys through the Aturan.org Dashboard.

Refer to the relevant Aturan.org documentation for current service specifications.

---

## About this repository

This repository represents the public-facing Aturan.org project and its published resources.

The hosted Aturan.org service includes infrastructure, datasets, retrieval systems, and backend components that are not necessarily part of this repository.

The **Aturan.org** name and logo are proprietary brand assets.

Any repository license applies only to source code and documentation explicitly published under that license. It does not grant rights to private backend systems, hosted services, datasets, trademarks, or brand assets unless expressly stated otherwise.

---

<p align="center">
  <strong>Find the norm by meaning. Verify the source.</strong>
</p>

<p align="center">
  <a href="https://aturan.org">aturan.org</a>
</p>
