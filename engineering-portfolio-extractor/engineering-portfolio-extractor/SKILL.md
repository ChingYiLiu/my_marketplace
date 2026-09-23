---
name: engineering-portfolio-extractor
description: Transform approved work-project concepts into independently reimplemented, public-safe engineering portfolio cases. Use when selecting, abstracting, rebuilding, or safety-reviewing a portfolio case; do not use to merely anonymize or publish company source.
metadata:
  short-description: Rebuild private work concepts as safe portfolio cases
---

# Engineering Portfolio Extractor

Create public, recruiter-readable portfolio cases inspired by engineering work without publishing company code, data, systems, or confidential business knowledge.

The portfolio repository root is always:

```text
engineering-portfolio/
```

## Non-negotiable principle

Use this transformation:

```text
Understand → Abstract → Reimplement
```

Never use this transformation:

```text
Copy → Rename → Remove secrets → Publish
```

Removing credentials, hostnames, or company names does not make source code safe to release. The deliverable must be an independently written demonstration of a general engineering pattern, using a new public-safe domain, interfaces, names, sample data, and documentation.

## Authorization and boundaries

- Treat the source project, its Git history, tickets, logs, documentation, datasets, screenshots, prompts, and generated artifacts as private by default.
- Do not copy source files, commit history, test fixtures, SQL, schemas, configuration, comments, proprietary vocabulary, or long code fragments into the portfolio repository.
- Do not make a repository public, push externally, or reuse an existing company repository's Git history unless the user explicitly authorizes that action and confirms they have the right to do so.
- Do not modify the original work project. Build the case in a new portfolio directory or provide a plan when the user has not authorized creating files.
- If the applicable NDA, employment agreement, IP assignment, open-source policy, or ownership of an idea is unclear, stop before implementing or publishing. Explain the uncertainty and request confirmation from the user or their employer's authorized guidance. A technical rewrite cannot resolve a legal/IP restriction.

## Select a candidate before writing code

First make a concise candidate assessment. Describe the source only at a high level; do not reproduce private code or business details. Evaluate these dimensions:

| Dimension | A strong candidate | Reject or defer when |
| --- | --- | --- |
| Engineering signal | Shows a clear algorithm, design decision, reliability pattern, performance trade-off, API design, pipeline, or test strategy | It is mostly company-specific configuration, CRUD, operational process, or secret-dependent glue |
| Generality | Can be expressed with a neutral domain and ordinary synthetic inputs | Its value depends on non-public rules, internal taxonomy, customer behavior, or proprietary models/data |
| Reimplementability | The behavior can be rebuilt from first principles without copying expressions or structure | The only practical result would be a near-copy of the original implementation |
| Explainability | A reviewer can run it and understand the trade-offs quickly | It needs private infrastructure or internal context to make sense |
| Safety | A new case would reveal no confidential capabilities, customers, metrics, schemas, or roadmap | The concept itself could expose a protected competitive advantage or contractual secret |

Label each candidate with exactly one disposition:

- **SAFE** — already public, personal, or independently created material that the user confirms they may use. It may be adapted, while still scanning for accidental secrets and provenance issues.
- **REIMPLEMENT** — a private-work-inspired idea that has enough general engineering value to rebuild independently. This is the normal disposition.
- **EXCLUDE** — too sensitive, too company-specific, insufficiently separable, or not clearly authorized. Do not attempt cosmetic anonymization.

For a REIMPLEMENT candidate, state: the neutral problem, the transferable engineering skills, the public-safe domain, the intended case boundary, and the information deliberately omitted.

## Inspect and abstract safely

When the user has authorization to inspect a private project locally, examine only what is needed to understand the general problem and decisions. Keep notes at the concept level. Never place raw source excerpts in the destination repository, README, issue, prompt artifact, or commit message.

Build an abstraction brief before implementation:

```text
Original context (private, high level):     [one neutral sentence]
Public portfolio problem:                   [independent problem statement]
Transferable capabilities:                  [3–5 skills or decisions]
New domain and vocabulary:                  [neutral / invented]
Inputs and outputs:                         [public-safe contract]
Excluded private elements:                  [data, systems, rules, names]
Success criteria:                           [observable behavior]
```

Change the domain substantially enough that it does not preserve identifying business semantics. For example, rebuild an internal product-text pipeline as a generic document tagging workflow with invented records, rather than retaining product categories, naming conventions, field layout, or proprietary decision rules.

## Sensitive-information scan

Before creating or importing material, scan the proposed files and any candidate inputs for:

- credentials, tokens, keys, certificates, connection strings, internal URLs, IP addresses, emails, usernames, and environment files;
- customer, employee, vendor, or partner data; identifiers; production metrics; support conversations; logs; screenshots; and real datasets;
- company names, product names, internal abbreviations, project names, ticket IDs, repository URLs, hostnames, schema/table/index/queue names, and deployment topology;
- exact SQL, proprietary prompts, model weights, business rules, thresholds, ranking logic, taxonomies, or roadmap information;
- copied implementation structure, comments, test cases, fixtures, commit messages, or code phrasing.

Remove unsafe material by designing an alternative, not by redacting it in place. Replace data with synthetic data and rebuild code from the abstraction brief. If a scanner finding cannot be confidently classified as safe, treat it as **EXCLUDE** until the user confirms it is public and reusable.

## Public examples and attribution

Apply the same disclosure rules to prose, diagrams, screenshots, sample requests, HTML, bundled JavaScript, and files that are not linked from the homepage. Readers can inspect source files as well as the visible page.

- Never use a real service route as a demonstration route. Invent a distinct route and interface for the new case; also invent request parameter names, response fields, error behavior, module/class/function names, and internal resource names. Check them against the source project before publishing. Changing only a prefix or a few characters is insufficient. If the interface is not central to the case, describe its purpose without a contract example.
- Explain decision stages and trade-offs without reproducing exact production triggers, thresholds, ranking weights, fallback order, special treatment for suppliers or products, or other business rules. Any runnable demo logic must be independently designed and clearly labeled as illustrative, not a disguised version of production logic.
- Omit real system scale, latency, conversion figures, dataset sizes, and similar measurements by default. Include a real figure only when the user confirms it is approved for public use and can substantiate it; otherwise use a clearly labeled synthetic demonstration measurement that is not derived from a production value.
- Describe only the user's verified contribution. Do not identify an employer, manager, colleague, customer, patent title or number, or the source of a business idea unless the user explicitly confirms that specific attribution is public and approved. Avoid wording that implies sole ownership of team work or company IP.
- Call invented data **synthetic**, not merely anonymized or de-identified. State that demo routes, scores, rules, and assets are independent examples when a reader might mistake them for the real service.

## Reimplement the case

Create a small, runnable case under a clear engineering-domain folder, for example:

```text
engineering-portfolio/
├── README.md
└── data-engineering/
    └── resilient-record-normalizer/
        ├── README.md
        ├── src/
        ├── sample_data/
        └── tests/
```

Choose a structure appropriate to the case; do not add framework or cloud dependencies just to imitate the work system. The implementation should:

- be newly written from the public portfolio problem, not transcribed from the source project;
- keep all runtime dependencies local or publicly accessible;
- use invented/neutral identifiers and a distinct interface and module design;
- demonstrate the selected decisions clearly, including relevant validation, failure handling, observability, performance considerations, or extensibility;
- expose a simple command or test command that a reviewer can run without private access.

Use deterministic **synthetic data** that is representative enough to exercise normal, edge, and failure paths but contains no real-world records, reconstructed records, or disguised production values. Label it as synthetic. Do not use a private dataset merely after masking names or IDs.

## Tests and documentation

Add focused automated tests for the core behavior and important edge cases. Tests must use only synthetic/public-safe inputs. Run the relevant test suite and fix failures before presenting the case as complete.

Each case README should include:

1. **Problem** — the neutral engineering problem, without company context.
2. **Approach** — the key algorithm, components, and data flow.
3. **Architecture** — a compact diagram or component description when it clarifies relationships.
4. **Key decisions and trade-offs** — why this design was chosen and what it does not optimize for.
5. **How to run** — minimal setup, example command, and expected output.
6. **Testing** — test command and coverage of important cases.
7. **Scope note** — state that it is an independently reimplemented, synthetic demonstration inspired by general production engineering patterns; do not identify an employer or project.

Update the root `engineering-portfolio/README.md` with a short index entry for each finished case: its neutral title, one-sentence problem, technology tags, and link. Do not add a case that is still unsafe, incomplete, or unverified.

Use [references/portfolio-case-template.md](references/portfolio-case-template.md) only when drafting a case README or its root index entry.

## Final safety and provenance gate

Before committing, packaging, publishing, or calling a case finished:

1. Re-scan every tracked file, including documentation, samples, hidden files, generated outputs, and test fixtures.
2. Review the diff for copied text, recognizable naming, private URLs, data shapes, credentials, and business semantics.
   Compare all published routes, parameter and response names, function names, example rules, metrics, and attribution against the source; confirm that examples are invented and that any approved real figure is accurately labeled.
3. Inspect Git history and staged changes. A clean current tree is insufficient if sensitive content appeared in an earlier portfolio commit.
4. Ensure the portfolio is a fresh repository or has an independently created history. Never carry over the company repository's commits, authorship, remotes, branches, tags, or ignored files.
5. Run the documented test command and any local static/safety checks that are appropriate to the language.
6. Confirm the user has reviewed any remaining ownership/NDA concern before external publication.

If unsafe content is found in unpushed local portfolio history, pause and explain the scope before proposing a history rewrite. If it was pushed or made public, treat it as an exposure incident: stop normal publishing work, preserve evidence as appropriate, and direct the user to their organization’s security/legal reporting process. Do not promise that deleting a file or repository removes it from all copies.

## Completion report

Report the candidate disposition, the general skills demonstrated, files created or changed, validation performed, synthetic-data status, and any NDA/IP confirmation still needed. Do not reveal private source details in the report.
