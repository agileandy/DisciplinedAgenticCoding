# Disciplined Agentic Coding (DAC) Framework – 
*A Principles-Driven Operating Model for Multi‑Agent AI Software Development*

## Table of Contents
1. Introduction
2. Rationale & Problem Space
3. Principles-First Approach (Why Principles, Not Tools)
4. Core Canon of Principles
5. Role System (Prompts & Behavioural Contracts)
   - 5.1 Orchestrator Agent
   - 5.2 Architect Agent
   - 5.3 Software Tester Agent
   - 5.4 Coder Agent
6. Canonical Artefacts (Purpose, Templates, Validation)
   - 6.1 projectContext.md
   - 6.2 systemDesign.md
   - 6.3 activeDevelopment.md
7. Interaction & Governance Workflows
   - 7.1 Initial Project Setup
   - 7.2 Feature Development (TDD Loop Embedded)
   - 7.3 Continuous Integration & Quality Gates
   - 7.4 Conflict / Decision Resolution & Consensus
   - 7.5 Rollback & Recovery Procedure
8. Quality Gates, Validation & Metrics
9. Decision Architecture & Operational Safety Nets
10. Scaling Context & Large Project Strategies
11. Continuous Improvement & Feedback Loops
12. Adoption Roadmap (Phased Evolution)
13. Future Directions (Short, Medium, Long Term)
14. Appendix: Checklists & Quick Reference

---
## 1. Introduction
The Disciplined Agentic Coding (DAC) Framework is an operating model for coordinating multiple specialised AI (and optionally human) agents to produce reliable, maintainable, and auditable software. It embeds timeless engineering principles, enforces explicit quality gates, and applies constraint‑based prompting to reduce non‑determinism while retaining creative problem solving.

DAC is not a tooling bundle or a set of scripts—it is a principled architecture for *how* autonomous and semi‑autonomous contributors collaborate, make decisions, and maintain shared context without drifting into chaos.

---
## 2. Rationale & Problem Space
Uncoordinated multi‑agent development typically suffers from:
- Context fragmentation across isolated LLM sessions
- Role ambiguity → duplicated effort & orphaned responsibilities
- Inconsistent quality due to prompt variance & missing gates
- Poor decision traceability → lost rationale & rework
- Escalating coordination overhead as scope & team grow

The DAC framework addresses these via:
- Explicit role contracts with imperative behavioural constraints
- Three canonical, living artefacts as single sources of truth
- Structured interaction workflows with enforced gates
- Formal decision & conflict resolution pathways
- Embedded validation & feedback metrics for adaptive improvement

---
## 3. Principles-First Approach (Why Principles, Not Tools)
Technology stacks evolve; foundational quality practices endure. DAC emphasises:
- Longevity: Practices transcending languages & frameworks
- Predictability: Reducing LLM randomness through structured constraints
- Transferability: Teams can adopt with minimal tooling assumptions
- Scalability: Principles compose; ad‑hoc tactics do not

Principles anchor agent behaviour so upgrades (models, infra, languages) do not break the operational fabric.

---
## 4. Core Principles
**Development Process**: Agile iteration, Trunk-Based Development, Test-Driven Development, Continuous Integration/Delivery.
**Code Quality**: SOLID, DRY, YAGNI, Clean Code, Refactoring discipline.
**Architecture**: Separation of Concerns, C4 modelling, purposeful pattern selection, defensive & observable design.
**AI Collaboration**: Imperative / constraint prompting, explicit error & uncertainty handling, structured context surfaces.
**Governance & Safety**: Quality gates, consensus & escalation protocols, auditability, rollback readiness.
**Learning & Evolution**: Metrics-driven adaptation, retrospectives, artefact hygiene, capability-aware role adjustment.

---
## 5. Role System (Prompts & Behavioural Contracts)
Each role prompt is written as an executable governance contract. *Capitalise MUST / NEVER / BEFORE / IF / WHEN / ONLY for enforceable constraints.*

### 5.1 Orchestrator Agent
**Mission**: Align project execution with goals; manage flow, prioritisation, and review cadence.
**Behavioural Contract**:
```
You are the ORCHESTRATOR AGENT.

MANDATORY BEHAVIOURS:
- BEFORE approving any task: VERIFY (1) requirement linkage to projectContext.md, (2) tests pass, (3) peer review logged. IF any missing → SET status NEEDS_REVIEW + LOG action.
- BEFORE sprint closure: CONFIRM all sprint acceptance criteria satisfied; IF not, EXTEND or REPLAN explicitly.
- WHEN creating tasks: LINK to requirement IDs + DEFINE acceptance criteria or REQUEST Tester to supply.
- IF agent conflict arises: INITIATE conflict workflow; DOCUMENT positions, decision, rationale.
- ALWAYS maintain a current sprint goal summary in activeDevelopment.md dashboard.
- NEVER approve integration without quality gate checklist fulfilment.

ERROR HANDLING:
- IF ambiguity in requirements → REQUEST clarification; BLOCK downstream work.
- IF deadline risk predicted → LOG risk, PROPOSE mitigations, SEEK consensus.
- IF artefact inconsistency detected → OPEN issue entry + ASSIGN responsible role.

SUCCESS CRITERIA: 100% tasks traceable; zero unreviewed merges; sprint commitments met or replanned with documented rationale.
```

### 5.2 Architect Agent
**Mission**: Provide coherent, scalable architectural blueprint & technical trade-off governance.
**Behavioural Contract**:
```
You are the ARCHITECT AGENT.

MANDATORY BEHAVIOURS:
- BEFORE drafting or modifying architecture: MAP every functional & non-functional requirement from projectContext.md to design elements.
- ALWAYS document C4 layers (Context → Containers → Components) before recommending deep implementation tactics.
- NEVER approve designs violating SOLID or explicit constraints; IF violation emerges, REJECT + PROPOSE alternative.
- WHEN choosing technologies: JUSTIFY with constraints, trade-offs, and alignment; LOG as ADR entry.
- ALWAYS specify observability: logging structure, metrics, trace points.

ERROR HANDLING:
- IF requirement infeasible: PRESENT at least 2 alternatives with trade-off matrix.
- IF performance/SLA unspecified: REQUEST concrete targets prior to final design.
- IF external dependency unclear: FLAG risk + create ISSUE entry.

SUCCESS CRITERIA: Complete C4 + ADR coverage; zero major re-architecture within sprint window; observability plan actionable.
```

### 5.3 Software Tester Agent
**Mission**: Safeguard reliability, correctness, and measurable quality.
**Behavioural Contract**:
```
You are the SOFTWARE TESTER AGENT.

MANDATORY BEHAVIOURS:
- BEFORE implementation starts for a task: DEFINE acceptance criteria + unit/integration/e2e scenario list.
- NEVER approve code lacking (a) failing pre-implementation test history (Red), (b) passing suite post-change (Green), (c) refactor verification.
- ALWAYS track coverage drift; IF coverage dips below threshold → BLOCK merge.
- WHEN requirements unclear or untestable: RETURN for clarification with concrete deficiency notes.

ERROR HANDLING:
- IF flaky tests detected: ISOLATE, TAG as FLAKY, PRIORITISE fix before new feature approval.
- IF critical bug found post-merge: INITIATE rollback procedure; LOG root cause entry.
- IF performance regression > defined tolerance: RAISE performance incident.

SUCCESS CRITERIA: High coverage (threshold configurable), zero critical defects escaping to release gate, stable & reliable test suite.
```

### 5.4 Coder Agent
**Mission**: Deliver maintainable, well‑tested, principle-aligned implementation.
**Behavioural Contract**:
```
You are the CODER AGENT.

MANDATORY BEHAVIOURS:
- BEFORE writing production code: ENSURE a failing (Red) test exists illustrating intended behaviour.
- FOLLOW TDD cycle strictly: Red → Green (minimal) → Refactor (improve structure without changing behaviour).
- ALWAYS produce atomic commits: single responsibility, descriptive message, link to Task ID + Requirement ID.
- NEVER bypass architectural guidance; IF unclear → REQUEST clarification.
- WHEN complexity increases unexpectedly: UPDATE estimate + LOG rationale.

ERROR HANDLING:
- IF merge conflict: RESOLVE then RE-RUN full test suite; IF failure → FIX before push.
- IF design constraint blocks implementation: ESCALATE to Architect with context + proposed options.
- IF repetitive pattern detected: PROPOSE refactor ticket.

SUCCESS CRITERIA: All code covered by tests; no lint/style gate failures; minimal rework due to design misalignment.
```

---
## 6. Canonical Artefacts (Purpose, Templates, Validation)
Each artefact is a single source of truth for a dimension of shared context. Validation rules mitigate drift.

### 6.1 projectContext.md (Vision & Requirements)
**Purpose**: Defines *what & why*—business goals, personas, scope, constraints.
**Validation Rules**:
- Every Epic has ≥1 measurable success metric.
- Each User Story has: persona, action, value clause.
- Constraints cross‑referenced in systemDesign.md.
- Out‑of‑scope items explicitly enumerated.

**Template (Abbreviated)**:
```
# Project Context: <Name>
1. Executive Summary
2. Business Goals & Metrics (Goal → Metric)
3. Personas (Name, Description, Needs)
4. User Journeys (Narratives)
5. Epics & User Stories (ID, Story, Rationale)
6. Constraints & Assumptions (Business, Technical)
7. Out of Scope
8. Requirement → Design Trace Table (auto/maintained)
```

### 6.2 systemDesign.md (Technical Blueprint)
**Purpose**: Translates requirements into architecture & operational design.
**Validation Rules**:
- All requirements mapped in a traceability table.
- All ADRs include decision, rationale, alternatives, consequences.
- C4 diagrams present for current abstraction level.
- Observability strategy covers logs, metrics, traces.

**Template (Abbreviated)**:
```
# System Design: <Name>
1. ADR Index (ID, Title, Status)
2. Technology Stack & Rationale
3. C4 Diagrams (Context, Containers, Components [+ optional Code])
4. Data Flows (Key Use Cases)
5. Design Patterns (Pattern → Context → Rationale)
6. Non-Functional Requirements (Performance, Security, Reliability, Compliance)
7. Observability (Logging Schema, Metrics, Alerts, Traces)
8. Risk & Dependency Register
9. Requirement Trace Matrix (Req ID → Component / Pattern / ADR)
```

### 6.3 activeDevelopment.md (Operational Log)
**Purpose**: Reverse‑chronological operational intelligence (tasks, decisions, incidents, test status).
**Validation Rules**:
- New entries prepend (latest first).
- Every Task ID links to Requirement ID(s).
- Decision entries include alternatives & chosen rationale.
- Incident entries include root cause + preventive action.

**Template (Abbreviated)**:
```
# Active Development Log: <Name>
1. Current State Dashboard (Sprint Goal, In Progress, Next Up, Blocked)
2. Metrics Snapshot (Coverage %, Open Defects, Lead Time, MTTR)
3. Development Log (Newest First)
   - LOG ENTRY YYYY-MM-DD
     Type: Task|Decision|Issue|Incident|Review
     IDs: TASK-### / REQ-### / ADR-###
     Status Transition (OLD → NEW)
     Summary
     Linked Requirements
     Commits / References
     Acceptance Criteria / Test Scenarios
     Outcome / Follow-Ups
4. Open Risks & Mitigations
5. Pending Reviews
```

---
## 7. Interaction & Governance Workflows
Mermaid diagrams optional; enforceable gate checklists mandatory.

### 7.1 Initial Project Setup
Steps:
1. Orchestrator drafts projectContext.md (Goals, Personas, Epics).
2. Architect produces initial systemDesign.md (C4 L1–L2 + initial ADRs).
3. Tester derives test strategy outline & acceptance criteria template.
4. All roles review → Gate: unanimous approval required.
5. Active development may begin; backlog seeded.

### 7.2 Feature Development (TDD Embedded)
1. Orchestrator creates Task (links Requirement ID + preliminary acceptance criteria).
2. Tester finalises acceptance criteria + enumerates test scenarios.
3. Architect adds any design guidance (patterns, constraints, interfaces).
4. Coder: Red → Green → Refactor; atomic commits referencing Task & Requirement.
5. Tester validates full suite + non-functional checks.
6. Peer review (Architect or Orchestrator + Tester mandatory for critical paths).
7. Orchestrator runs quality gate checklist → Merge / Integrate.

### 7.3 Continuous Integration & Quality Gates
Pipeline gates (example):
- Gate A: Lint + Static Analysis
- Gate B: Unit Tests (≥ coverage threshold)
- Gate C: Integration Tests + Contract Tests
- Gate D: Security Scan (SAST/Dependency)
- Gate E: Performance Smoke (thresholds)
- Manual Approval: Orchestrator verifies artefact sync (context/design/log).

### 7.4 Conflict / Decision Resolution & Consensus
Trigger: Disagreement on design / test sufficiency / requirement.
Protocol:
1. Log conflict entry (positions, impacted artefacts).
2. Orchestrator facilitates structured debate (max 2 iterations).
3. Attempt consensus (≥2 roles concurrence, no hard veto). If deadlock → apply Decision Arbitration Hierarchy: Requirement Scope → Orchestrator; Architecture Integrity → Architect; Quality Standard → Tester; Implementation Feasibility → Coder.
4. Record decision in activeDevelopment.md + (if architectural) ADR entry.
5. Update impacted artefacts; link Decision ID.

### 7.5 Rollback & Recovery Procedure
Used when critical regression escapes or gating failure discovered post-integration.
1. Detect (monitoring alert / failing canary / incident report).
2. Freeze new merges.
3. Identify offending change (bisect / commit trace).
4. Execute rollback (revert commit / redeploy prior artefact).
5. Log Incident Entry (root cause, detection latency, impact, preventive action).
6. Add regression test (Tester) + potential architectural safeguard (Architect).
7. Resume pipeline after all gates green.

---
## 8. Quality Gates, Validation & Metrics
**Pre-Implementation Gate** (Task may start only if checked):
- [ ] Requirement linkage present
- [ ] Acceptance criteria defined & test scenarios enumerated
- [ ] Architectural guidance assessed (or explicitly N/A)
- [ ] Dependencies resolved / mocked strategy defined

**Pre-Integration Gate**:
- [ ] All tests pass (unit/integration/e2e)
- [ ] Coverage ≥ threshold (e.g., 85% lines, 70% branches) OR justified waiver logged
- [ ] Peer review completed (min 2 roles for critical modules)
- [ ] activeDevelopment.md updated (log entry + commits)
- [ ] systemDesign.md adjustments (if any) merged & traced

**Pre-Release Gate**:
- [ ] End-to-end regression suite green
- [ ] Performance SLAs met (document metrics snapshot)
- [ ] Security & dependency scans clean (critical Vilna = block)
- [ ] Observability instrumentation verified
- [ ] Rollback plan validated

**Cross-Artefact Consistency Automated Checks (Recommended)**:
- 100% Tasks map to ≥1 Requirement ID
- 100% Requirements map to ≥1 Design Component (trace matrix)
- All ADRs referenced by ≥1 component or marked DEPRECATED

**Core Metrics**:
- Flow: Lead Time, Cycle Time, WIP Count
- Quality: Defect Escape Rate, Flaky Test Ratio, Mean Time To Repair (MTTR)
- Coverage: Test Coverage %, Requirements Trace Coverage %
- Stability: Change Failure Rate, Rollback Frequency
- Predictability: Sprint Commitment Reliability %

Each metric should have: definition, measurement method, owner role, and review cadence.

---
## 9. Decision Architecture & Operational Safety Nets
**Decision Types**:
- Strategic (Goals / Scope) → Orchestrator primary
- Architectural (Patterns / Structure) → Architect primary
- Quality (Test depth / Acceptance) → Tester primary
- Implementation (Refactor approach / Technique) → Coder primary

**Consensus Pattern**: Default mode; accept when no primary role veto + at least two supportive roles.
**Fallback Arbitration**: Primary role decides; must log rationale & dissent summary.
**Leader Election (Optional Extension)**: For long-running refactors or spikes, temporary "Task Lead" elected (criteria: expertise, complexity). Logged with scope & expiry.
**Audit Trail**: Every architectural or disputed decision → ADR or Decision Log entry (immutable index ID).

---
## 10. Scaling Context & Large Project Strategies
Challenges: Artefact bloat, cognitive overload, divergent subdomain evolution.
Strategies:
- **Artefact Partitioning**: Split systemDesign.md by bounded context modules; maintain root index.
- **Context Summarisation Layers**: Generate automated digests (weekly) with delta focus.
- **Selective Context Loading**: Role prompts feed only relevant artefact segments using tag indexing (Requirement IDs, Component Tags).
- **Versioning & Branching**: Introduce artefact branches for exploratory design; merge via formal review.
- **Context TTL & Pruning**: Archive stale log sections beyond retention window (e.g., > 90 days) with summarised incident ledger.

---
## 11. Continuous Improvement & Feedback Loops
Mechanisms:
- Weekly Retrospective Entry: What worked / friction / action items (assigned owners).
- Monthly Metrics Review: Trend analysis → improvement experiment backlog.
- Quarterly Evolution Assessment: Consider dynamic role adjustments & automation opportunities.
- Post‑Incident Reviews: 5 Whys root cause + preventive actions integrated into gates/automation.
- Prompt Refinement Cycle: Log prompt failure modes → update behavioural contracts (versioned).

---
## 12. Adoption Roadmap (Phased Evolution)
**Phase 1 – Foundation (Weeks 0–2)**: Implement role prompts, artefact templates, baseline gates.
**Phase 2 – Discipline (Weeks 3–6)**: Enforce traceability, introduce metrics dashboard, refine review cadence.
**Phase 3 – Automation**: Add consistency scripts, coverage enforcement, flaky test quarantine automation.
**Phase 4 – Adaptation**: Dynamic role delegation, context summarisation services, meta‑agent suggestions.
**Phase 5 – Optimisation**: Predictive risk modelling, self‑tuning gates, capability-aware task allocation.

---
## 13. Future Directions
### Short Term
- Strengthen automated cross-artefact validators (trace completeness, stale decisions).
- Introduce structured uncertainty handling (agents tag CONFIDENCE scores).
- Build real-time dashboards (flow + quality + risk heat-map).

### Medium Term
- Dynamic Role Recomposition: Skill matrix drives task routing vs. static roles.
- Meta-Orchestrator Agent: Optimises WIP limits, sequencing, and throughput predictions.
- Human-AI Hybrid Controls: Seamless human code review injection & override gating.
- Advanced Context Compression: Embedding-based retrieval aligned with task intent.

### Long Term
- Self-Optimising Governance: Gates adapt thresholds automatically from historical success/failure patterns.
- Multi-Modal Architecture Collaboration: Diagram synthesis & validation from natural language + code base diffing.
- Autonomous Refactoring Waves: Scheduled improvement sprints initiated by metric lag detection.
- Industry-Specific Profiles: Pre-tuned principle weightings (e.g., safety-critical vs. consumer SaaS).

### Keeping Relevance
- Preserve principle minimalism—resist procedural bloat.
- Regularly prune obsolete metrics & rituals.
- Evolve prompts responsively to observed failure classes.
- Maintain portability: avoid coupling to proprietary tool dialects.

---
## 14. Appendix: Checklists & Quick Reference
**Daily Sync (Async) Checklist**:
- [ ] Dashboard updated (In Progress / Blocked accurate)
- [ ] New risks logged
- [ ] Metrics drift noted (if threshold breach)

**Incident Review Template**:
```
INCIDENT ID: <ID>
Detection Time / Resolution Time
Severity / Impact Scope
Root Cause (5 Whys Summary)
Mitigations Implemented
Follow-Up Actions (IDs)
Regression Tests Added
Owner / Review Date
```

**Traceability Mini-Matrix Example**:
```
REQ-004 → ADR-002, Component: PaymentService, Tasks: TASK-019, TASK-021, Tests: T-API-17,T-E2E-05
```

**Commit Message Format**:
```
<type>(<scope>): <concise change>

Refs: TASK-012 REQ-003
Rationale: <if non-trivial>
```

---
## Conclusion
The DAC Framework operationalises disciplined multi-agent software engineering by fusing principle-based structure, enforceable behavioural contracts, and adaptive governance. Its durability comes from clarity of responsibility, artefact rigour, and evolving quality gates—not from any transient tooling fad.

Adopt incrementally, measure relentlessly, and refine continuously. Let principles be stable, processes be inspectable, and automation be additive—not ornamental.

**Next Step**: Instantiate the three artefacts with your project’s seed context and begin Phase 1. Discipline first; sophistication later.

*This guide represents the current state of the DAC framework based on extensive analysis, critique, and refinement. It will continue to evolve as teams gain experience with multi-agent development and as AI capabilities advance. Your feedback and experiences are valuable contributions to this evolution.*
