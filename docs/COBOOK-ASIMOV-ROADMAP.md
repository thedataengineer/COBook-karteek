# COBook to ASIMOV Roadmap

## Strategic position

Build COBook as the **ASIMOV COBOL Analyst Workbench**, not as a standalone modernization platform.

COBook should handle program review, SME annotation, source-linked explanations, and evidence capture. ASIMOV should remain the system of record for graphs, specifications, migration planning, validation evidence, and delivery governance.

This roadmap assumes a 16 to 20 week pilot with one bounded COBOL application. [ASSUMPTION]

## Roadmap structure

| Term | Meaning |
|---|---|
| Feature | User-visible capability |
| Feat | Small demonstrable slice of a feature |
| Enabler | Technical or operational foundation required by features |
| Gate | Evidence-based checkpoint that permits the next phase |
| Outcome | Business or delivery result expected from the phase |

## Phase 0: Security and delivery control

**Timeline:** Weeks 0 to 2
**Objective:** Make the prototype safe for controlled AccionLabs use.

### Features

- **F0.1 Credential protection:** Revoke exposed keys, remove environment files from Git history, keep provider credentials server-side, and add secret scanning.
- **F0.2 Workspace access:** Add identity-provider login, project boundaries, and reviewer and administrator roles.
- **F0.3 Safe COBOL execution:** Run compilation and execution in isolated workers with filesystem, network, CPU, memory, process, and time limits.
- **F0.4 Audit trail:** Record user, project, source commit, AI request, generated artifact, reviewer action, approval state, and execution result.

### Feats

- `FEAT-0.1`: No active secret remains in the repository.
- `FEAT-0.2`: Unauthenticated requests cannot execute code.
- `FEAT-0.3`: A runaway COBOL process can be stopped without restarting the service.
- `FEAT-0.4`: Every AI response has a request ID and user ID.
- `FEAT-0.5`: A reviewer can approve or reject an AI-generated explanation.

### Enablers

- Identity provider integration.
- Secrets manager.
- Isolated execution service.
- Project and workspace data model.
- Audit event schema.
- CI secret and dependency scanning.

### Gate G0: Controlled-use approval

Pass only when no credential appears in the current repository, code execution runs outside the application process, protected routes require authorization, audit events are queryable, and a security reviewer approves the execution boundary.

**So what?** If this gate fails, COBook remains a developer demo with unacceptable credential, code-execution, and client-data exposure. No client source should enter the system.

**Now what?** If it passes, authorize a bounded internal pilot and begin source-ingestion work. If it fails, stop feature expansion and assign owners to each failed control with a dated remediation plan.

## Phase 1: Source ingestion and evidence graph

**Timeline:** Weeks 2 to 5
**Objective:** Move from single-file analysis to ASIMOV-compatible source evidence.

### Features

- **F1.1 Multi-file ingestion:** Ingest COBOL programs, copybooks, job definitions, data definitions, documentation, and tests.
- **F1.2 Source provenance:** Retain repository, branch, commit, file path, line range, program, paragraph, and source hash.
- **F1.3 COBOL relationship graph:** Capture programs, paragraphs, sections, variables, copybooks, calls, performs, file operations, data movement, conditions, and interfaces.
- **F1.4 Coverage reporting:** Report file inventory, parsed files, unsupported constructs, graph objects, relationships, and parse errors.

### Feats

- `FEAT-1.1`: Import a repository and display all COBOL source files.
- `FEAT-1.2`: Open any graph node and jump to its source location.
- `FEAT-1.3`: Display unresolved copybooks, calls, and external references.
- `FEAT-1.4`: Generate a coverage report for a bounded application.
- `FEAT-1.5`: Re-ingest a new commit and show changed nodes.
- `FEAT-1.6`: Export source-to-node mappings as CSV and JSON.

### Enablers

- Canonical graph schema.
- Parser adapter interface.
- Source location model.
- Graph database or ASIMOV graph API.
- Incremental ingestion queue.
- Parser error taxonomy.

### Gate G1: Source coverage accepted

Pass only when every input file has a status, supported constructs map to graph objects, unsupported constructs appear in an exception report, users can navigate from graph objects to source lines, and ASIMOV accepts the graph schema.

**So what?** Without this gate, later AI explanations and migration plans can omit source logic while appearing complete. That creates rework and weakens the ASIMOV evidence chain.

**Now what?** If it passes, use the graph as the source for analyst review. If it fails, restrict the pilot scope to supported constructs and publish the uncovered inventory before making delivery claims.

## Phase 2: COBOL analyst workbench

**Timeline:** Weeks 5 to 8
**Objective:** Reduce SME review time and turn informal knowledge into structured evidence.

### Features

- **F2.1 Source and graph exploration:** Provide code, paragraph, control-flow, data-flow, dependency, external-call, and documentation views.
- **F2.2 Source-grounded AI explanation:** Generate summaries, business-rule candidates, lineage explanations, risk flags, and SME questions with source references, confidence, model, prompt version, and review status.
- **F2.3 SME annotation:** Classify findings as confirmed, rejected, uncertain, obsolete, missing context, requires test, or requires client decision.
- **F2.4 Delta capture:** Record differences between observed behavior, confirmed behavior, and desired future behavior.

### Feats

- `FEAT-2.1`: Select a paragraph and request an explanation with source citations.
- `FEAT-2.2`: Accept, reject, or edit the generated explanation.
- `FEAT-2.3`: Mark a business rule as confirmed by a named SME.
- `FEAT-2.4`: Create a delta against current behavior.
- `FEAT-2.5`: Export a review pack for one module.
- `FEAT-2.6`: Show unresolved questions by program and business process.

### Enablers

- Annotation schema.
- Review-state model.
- Source-linked prompt context.
- Model gateway with request logging.
- Human approval workflow.
- Graph and document search.

### Gate G2: SME evidence accepted

Pass only when every accepted rule has a source reference, reviewer identity and timestamp are retained, rejected AI content remains in audit history, SMEs can complete a module review in the workbench, and review time is measured against the current process.

**Pilot target:** 30% reduction in SME review time. [ASSUMPTION]

**So what?** This gate tests whether COBook removes a real delivery bottleneck, rather than producing attractive diagrams or unverified AI summaries.

**Now what?** If it passes, make the workbench the standard review path for the pilot module. If it fails, identify whether the cause is parser coverage, poor prompt context, weak UX, or SME workflow mismatch before adding more AI features.

## Phase 3: ASIMOV specification and migration readiness

**Timeline:** Weeks 8 to 11
**Objective:** Convert reviewed COBOL understanding into migration-ready artifacts.

### Features

- **F3.1 ASIMOV Specification Format export:** Export requirements, rules, entities, interfaces, dependencies, tests, exceptions, decisions, and open questions.
- **F3.2 Module scope management:** Classify modules as retain, modify, replace, retire, or investigate.
- **F3.3 Target mapping:** Map source components to target languages, services, data models, APIs, complexity, risk, and decisions.
- **F3.4 Traceability matrix:** Link source files to programs, rules, requirements, target components, tests, and validation results.

### Feats

- `FEAT-3.1`: Select a migration boundary at module level.
- `FEAT-3.2`: Classify every selected module.
- `FEAT-3.3`: Generate an ASF package from approved evidence.
- `FEAT-3.4`: Map COBOL modules to target Java or .NET components.
- `FEAT-3.5`: Produce a requirement-to-source traceability matrix.
- `FEAT-3.6`: Generate a migration-readiness report.

### Enablers

- ASF schema.
- Target blueprint schema.
- Module classification model.
- Complexity and risk scoring.
- Traceability service.
- COBook to ASIMOV export and import APIs.

### Gate G3: Migration scope approved

Pass only when the migration boundary is explicit, retain/modify/replace/retire decisions are recorded, target mappings have owners, open questions have disposition dates, and the client SME and technical lead approve the ASF package.

**So what?** This gate converts system understanding into an executable modernization decision. Without it, ASIMOV has documentation but no controlled migration scope.

**Now what?** If it passes, release the ASF package to migration planning and estimate the selected work. If it fails, do not generate target code for the affected scope; resolve ownership, business-rule, or target-architecture gaps first.

## Phase 4: Migration and validation integration

**Timeline:** Weeks 11 to 15
**Objective:** Connect COBook evidence to ASIMOV transformation and validation.

COBook should supply verified source evidence and consume validation results. It should not become the migration engine.

### Features

- **F4.1 Migration work packages:** Generate source scope, rules, dependencies, target mapping, tests, exceptions, decisions, and acceptance criteria.
- **F4.2 Functional test generation:** Generate unit, integration, boundary, negative, reconciliation, and business-rule tests.
- **F4.3 Source-to-target comparison:** Compare input, output, error, data transformation, boundary, external-call, and performance behavior.
- **F4.4 Validation evidence:** Store test input, source result, target result, difference, classification, reviewer decision, and retest result.

### Feats

- `FEAT-4.1`: Generate test scenarios from approved rules.
- `FEAT-4.2`: Execute source and target tests through controlled runners.
- `FEAT-4.3`: Compare source and target outputs.
- `FEAT-4.4`: Classify differences as defect, approved delta, data issue, or test issue.
- `FEAT-4.5`: Produce an exception report.
- `FEAT-4.6`: Export validation evidence to ASIMOV.

### Enablers

- Test runner abstraction.
- COBOL runtime adapter.
- Java and .NET runtime adapters.
- Data fixture management.
- Result normalization.
- Difference classifier.
- Validation evidence store.

### Gate G4: Functional equivalence review

Pass only when the agreed test set runs repeatably, every difference has a classification, approved deltas are separated from defects, no unresolved critical difference remains, and the client SME signs off on accepted behavior.

**So what?** This gate protects the client from a technically successful rewrite that changes business behavior. It is the point where modernization evidence becomes release confidence.

**Now what?** If it passes, approve the module for UAT or deployment planning. If it fails, route each difference to defect repair, data correction, test correction, or an approved business delta. Do not collapse those categories into one pass rate.

## Phase 5: Pilot deployment and operating model

**Timeline:** Weeks 15 to 20
**Objective:** Prove the combined workflow on a real modernization stream.

### Features

- **F5.1 Pilot workspace:** Provide project status, coverage, SME review queues, open questions, migration decisions, validation exceptions, and approvals.
- **F5.2 Delivery reporting:** Measure files ingested, parser issues, confirmed rules, SME hours, module decisions, generated tests, validation pass rate, and rework.
- **F5.3 Handover package:** Produce graph export, ASF, annotations, work packages, test scenarios, validation evidence, limitations, and runbook.

### Feats

- `FEAT-5.1`: Run one bounded client application from ingestion through review.
- `FEAT-5.2`: Produce an approved ASF package.
- `FEAT-5.3`: Generate migration work packages from approved evidence.
- `FEAT-5.4`: Complete source-to-target validation for one representative module.
- `FEAT-5.5`: Produce an executive delivery report.
- `FEAT-5.6`: Hand the evidence package to the ASIMOV delivery team.

### Enablers

- Pilot governance.
- Named product owner.
- Named ASIMOV technical lead.
- Named client SME.
- Data handling agreement.
- Deployment environment.
- Support and incident process.
- Measurement baseline.

### Gate G5: Scale decision

Scale only when the pilot demonstrates measurable reduction in SME review effort, higher source coverage, source-to-requirement traceability, repeatable validation evidence, no unresolved critical security issue, and a clear operating cost per application or million lines of code.

**So what?** This gate separates a repeatable AccionLabs capability from a one-off client demo. It must show delivery economics, evidence quality, and client control at the same time.

**Now what?** If it passes, define the next application cohort, platform funding, and product ownership model. If it fails, keep the work at pilot scope and fix the failed measure before expanding the platform.

## Priority order

### P0

- Revoke exposed Groq keys.
- Remove tracked environment files.
- Isolate COBOL execution.
- Add authentication.
- Bind local demos to loopback.
- Establish audit events.

### P1

- Build source provenance.
- Add multi-file ingestion.
- Create graph-backed navigation.
- Add source-cited AI explanations.
- Add SME review and approval states.

### P2

- Export ASF.
- Add module classification.
- Add target mapping.
- Generate migration work packages.
- Generate test scenarios.

### P3

- Add source-to-target execution comparison.
- Add validation evidence.
- Add delivery dashboards.
- Run a bounded client pilot.

## Measures that matter

| Measure | Baseline | Pilot target |
|---|---:|---:|
| Source files mapped to graph nodes | Unknown | 100% status assigned |
| Files with unresolved parser issues | Unknown | Reported by file and construct |
| AI outputs with source citations | 0% | 100% |
| SME decisions captured structurally | Unknown | 100% of reviewed findings |
| SME review time | Establish baseline | 30% reduction [ASSUMPTION] |
| Migration modules with approved scope | Unknown | 100% of pilot scope |
| Test scenarios linked to rules | Unknown | 100% of accepted rules |
| Validation differences classified | Unknown | 100% |
| Critical unresolved validation issues | Unknown | 0 at gate |
| Secrets in repository | Confirmed | 0 |

## Product decision

COBook should become a front-end and evidence-capture layer for ASIMOV.

The first product increment should prove four capabilities:

1. Source-grounded COBOL understanding.
2. SME review captured as structured evidence.
3. ASF and traceability export.
4. Validation evidence returned to the modernization workflow.

Everything else remains secondary until that evidence chain works end to end.
