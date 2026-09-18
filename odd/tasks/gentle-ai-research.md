# Feature: First-class generic research agent

## Objective

Add a package-owned global `gentle-ai-research` agent for generic non-SDD external research while preserving parent orchestration, strict read-only behavior, source provenance, and a thin parent context.

## Accepted scope

- Generic non-SDD role, installed and routed like the existing delegation agents.
- Local tools: `read`, `grep`, `find` only.
- External tools: `fetch_content`, `web_search`, `source_check`, `get_search_content`, narrowed by the existing provenance-bound `research_selection` pipeline.
- Excluded: Bash, writes, memory, delegation, generic/dynamic MCP, installs, auth, credentials, publication, and `codegraph`.
- Preserve existing `sdd-research` output-only behavior.
- No push, pull request, release, or publication.

## Tasks

- [x] T1. Add RED contract tests for asset installation, exact tool allowlists, generic research selection/guards, continuation behavior, and ODD routing. Commit: `1d5b0bbd`.
- [x] T2. Implement the delegation-owned agent asset and runtime capability enforcement; make focused runtime tests GREEN.
- [ ] T3. Update ODD routing and public documentation, run focused and full verification, and record residual risks.

## Progress and evidence

- Source checkout: `/home/ramage/code/gentle-shell`
- Branch: `feat/gentle-ai-research`
- Handoff checkpoint: `infra-clean-slate-research/2026-09-18/v13`
- User authorized implementation, cloning the source repository, dependency installation, and local work-unit commits; push/publication remain unauthorized.
- T1 RED: `sdd-research-capabilities` fails because generic local reads are stripped; `sdd-preflight` fails because the new asset is absent; `odd-routing-contract` fails because no dedicated route exists; focused `gentle-agents` cases fail because generic launches are not narrowed and SDK local reads are blocked.
- T2 GREEN: research capabilities 9/9; preflight 33/33; focused launch/child guard cases 5/5; runtime harness passed; package resource check passed (169 files).

## Acceptance criteria

- Package startup/install surfaces include `gentle-ai-research` as a delegation-owned global agent.
- Its effective child tools are exactly fixed local reads plus explicitly selected/provenanced approved web tools and `subagent_parent_message`.
- Missing/stale provenance, unselected external tools, Bash, writes, MCP, memory, and nesting fail closed.
- `sdd-research` retains its existing local-tool stripping behavior.
- Generic ODD external research routes to `gentle-ai-research`; SDD research remains SDD-only.
- Focused tests, typecheck, package checks, harness, and the full test suite pass or have explicitly recorded blockers.
