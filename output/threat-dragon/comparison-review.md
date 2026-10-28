# DFD completeness and correctness comparison

Audit date: 2026-10-28 (Asia/Manila).

**Verdict:** The pasted model passes threat identification and severity checks, but needs workflow corrections. Our model is more faithful to the four source workflows. Neither source JSON was modified.

## Compared files

- Pasted: `STRIDE-Data-Flow-Diagram-Threat-Identification-Almin-Del-Rosario-Gan.json`
- Ours: `output/threat-dragon/brew-and-bloom-pe1.json`
- Authority: `Threat Model Document - Coffee Ordering Web App.pdf`, sections 5.1 and 5.2, Tables 2 and 3; and `Practical Exercise 1 - Threat Modeling.pdf`.

## Results

| Check | Pasted | Ours |
|---|---|---|
| Four workflows in one project | PASS | PASS |
| Native Threat Dragon import | PASS | PASS (previously verified) |
| Schema with declared nullable semantics | PASS | PASS |
| Titles, descriptions, STRIDE meanings | PASS: all 128 attachments | PASS: all 128 attachments |
| Affected-component mappings | PASS: 32 per diagram | PASS: 32 per diagram |
| Severity from source matrix row counts | PASS: all 128 attachments | PASS: all 128 attachments |
| Graph endpoints and referenced ports | PASS | PASS |
| Required data-transfer semantics | PARTIAL: Manager report response missing | PASS |
| Server operations versus data transfers | Needs corrections | PASS |
| Payment-success condition and channel metadata | Needs corrections | Explicitly represented |

Per-diagram severity distribution is identical: 24 Medium, 6 High, and 2 Low attachments. There are 18 distinct source threats, repeated on affected components; 128 attachments does not mean 128 distinct vulnerabilities.

## Workflow comparison

| Workflow | Pasted arrows | Ours | Assessment |
|---|---:|---:|---|
| Customer order | 5 | 5 | Same required directions; pasted write condition and payment encryption metadata need clarification. |
| Barista update | 7 | 6 | Required transfer directions exist, plus an authentication/authorization action arrow; update step reference is incorrect. |
| Manager report | 4 | 4 | Equal arrow counts conceal a missing processed-report response; authentication action occupies the only server-to-client arrow. |
| Administrator menu addition | 6 | 3 | New-item submission, database write, and confirmation are present. Extra login request can be reasonable, but authenticate/authorize action arrows do not name transferred data. |

Arrow counts are evidence, not the grading rule. Different legitimate levels of decomposition are possible.

## Findings

### F1 — High — Manager Accesses Basic Sales Reports

No backend-to-Manager transfer carries the processed basic sales report. The sole backend-to-frontend flow is labeled authentication/authorization (3.2).

Correction: Represent 3.4 as the returned basic sales report and show totals/formatting as backend processing. Frontend displays it in 3.5.

Our version: The 3.4 processed report response and 3.5 display note are present.

### F2 — Medium — Barista, Manager, Administrator

Authentication and authorization are drawn as backend-to-frontend arrows named after server actions, without a data payload. The source places those decisions at the backend.

Correction: Use process descriptions/notes for these checks. If a distinct login response is intentional, identify its actual data (such as authentication result/session) and keep authorization decisions at the backend.

Our version: These operations are backend notes/descriptions rather than invented response transfers.

### F3 — Medium — Customer Places an Order

Order write has no explicit payment-success guard in its name or description. Sequence numbering alone does not state the condition.

Correction: Annotate the write as conditional on successful payment. Do not imply the source defines a detailed failure-handling path.

Our version: The database-write label and description explicitly state payment must succeed.

### F4 — Medium — Customer Places an Order

Both payment flows have isEncrypted=false while the source and the boundary description state secured communication channels. This is a model-metadata inconsistency, not evidence about a running implementation.

Correction: Make the payment-flow security metadata consistent with the stated secured channel.

Our version: Both payment directions have isEncrypted=true; unspecified transports are not asserted.

### F5 — Low — Barista and Manager

Barista sending the update is labeled 2.5, but sending is 2.6; 2.5 is local selection/change. Manager sales-data query is labeled 3.3a, but the backend query belongs to 3.2; 3.3 is the database retrieval/response.

Correction: Correct the step references; use suffixes only within the corresponding source step.

Our version: The sending/query flows reference 2.6 and 3.2 respectively.

### F6 — Advisory — All workflows

The pasted model describes the backend generically and omits workflow-specific business checks and processing details. Its boundary does mention input validation, so validation is not wholly absent.

Correction: Document item availability/customization checks, status validation, report calculation/formatting, and new-menu-item input validation in process descriptions or notes. No extra arrows are needed.

Our version: Workflow-specific processing is documented in notes and descriptions.

## Boundaries and nonissues

Both models include Client/Server, Server/Database, and Server/Payment boundaries at the corresponding trust transitions. The pasted model repeats an unused payment service and payment boundary in the three staff workflows. That adds context/clutter but is not a missing requirement. Our staff diagrams contain only the two boundaries crossed by their flows; the customer diagram supplies the payment boundary.

The pasted version has useful owner/reviewer metadata absent from ours. Keep that metadata when finalizing a project.

Nonconsecutive diagram numbers, identifiers reused in separate graphs, blank custom threat-score fields, and missing custom `sourceId` fields are not correctness defects here. All required threat metadata is still present. The schema declares nullable style fields; a generic strict Draft 7 validator reports null warnings, but the native app imports successfully and nullable-aware validation passes.

## Submission completeness

The exercise requires a PDF report generated by Threat Dragon and matching JPG/PNG diagram backups. Neither JSON alone fulfills that requirement. Our existing native PNG exports match our model. The pasted version will need matching final exports after its corrections. The review screenshots are inspection evidence, not a replacement for those exports. Part 2 DREAD scoring is outside this DFD audit.

## Verification scope

- Re-read the reference PDF tables and independently recounted Table 3 checks.
- Compared every required threat field and affected-component pair in both models.
- Checked graph references, port references, numbering, file schemas, and workflow transfer directions.
- Imported and visually inspected all four pasted diagrams in Threat Dragon 2.6.2.
- Confirmed both model files retained their original SHA-256 hashes throughout the audit.

Machine-readable results: `comparison-audit.json`.
