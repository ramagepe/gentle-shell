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
- [x] T2. Implement the delegation-owned agent asset and runtime capability enforcement; make focused runtime tests GREEN. Commit: `2520db3c`.
- [x] T3. Update ODD routing and public documentation, run focused and full verification, and record residual risks. Commit: `d6fb6233`.
- [x] T4. Add regression coverage proving a parent can select research tools by semantic name without supplying hidden extension paths. Route: delegated writer; trigger: multi-file TDD correction. RED evidence unavailable because the writer changed implementation before returning a blocked result; regression coverage passes against the correction. Commit: `93d180da`.
- [x] T5. Reuse the existing inventory, model-profile, and child guard pipeline while deriving trusted extension provenance inside the host. Route: delegated writer; trigger: multi-file runtime and contract update. Commit: `93d180da`.
- [x] T6. Verify focused tests, typecheck, runtime/package checks, and a live `gentle-ai-research` web invocation; record any host-reload limitation. Route: delegated verifier after native high-risk assessment. Commit: `93d180da`.

## Progress and evidence

- Source checkout: `/home/ramage/code/gentle-shell`
- Branch: `feat/gentle-ai-research`
- Handoff checkpoint: `infra-clean-slate-research/2026-09-18/v13`
- User authorized implementation, cloning the source repository, dependency installation, and local work-unit commits; push/publication remain unauthorized.
- T1 RED: `sdd-research-capabilities` fails because generic local reads are stripped; `sdd-preflight` fails because the new asset is absent; `odd-routing-contract` fails because no dedicated route exists; focused `gentle-agents` cases fail because generic launches are not narrowed and SDK local reads are blocked.
- T2 GREEN: research capabilities 9/9; preflight 33/33; focused launch/child guard cases 5/5; runtime harness passed; package resource check passed (169 files).
- T3 GREEN: routing 12/12; SDD/ODD integration 2/2; orchestrator budget 38/38; focused package-manifest 5/5; runtime metrics 8/8; typecheck passed; generated runtime check passed; package resource check passed; full `pnpm test` passed with 2720 passing and 38 platform/live skips, followed by provider-contract and runtime-harness success.
- Independent verification: PASS for every authorized command and inspected contract; final verdict PARTIAL only because 38 live/provider/platform-specific tests were skipped. No findings at any severity.
- Earlier native review was unavailable because the then-active package-local binary was missing; that historical attempt created no lineage.
- Independent re-investigation reopened this feature after reproducing a live generic launch where `web_search` was unavailable and the injected capability block reported `open-web: blocked; tools=[]`.
- Diagnosis under test: the public `research_selection` schema requires caller-authored `sourceInfo.path` values, while the parent-facing capability block exposes only semantic tool names. Existing tests bypass this boundary with fixture paths.
- TDD mode: enabled by explicit user instruction. Focused runner: `node --experimental-strip-types --test tests/sdd-research-capabilities.test.ts tests/gentle-agents.test.ts`; broader runner: `pnpm test`.
- Delivery strategy: `ask-on-risk`; the correction added 52 and removed 24 lines across eight files, including this progress document.
- Focused verification: 110 passed, 0 failed, 0 skipped. Package-file verification: 169 package files and 69 byte-pinned artifacts passed.
- Direct package-script equivalents passed because `pnpm` was unavailable: typecheck baseline check, generated runtime-module check, 2,720/2,758 tests with 38 platform/live skips, provider-contract check, and runtime harness.
- Native review: approved and acknowledged for target `sha256:6801801a54953d8673c3463cbf018443728f91f20d426374f6b404dc3077d1f6`; one informational resilience warning noted possible duplicate tool provenance and opened no correction.
- Live pre-fix reproduction confirmed `gentle-ai-research` had `open-web: blocked; tools=[]`. A live post-fix invocation is unavailable in the current process because its loaded extension and tool schema predate the uninstalled worktree correction; tests cover the corrected launch boundary.
- Residual constraints: opt-in live research, producer integration, and Windows-native behavior remain unverified on this host; no PR, release, publication, or active-package installation was performed. The correction was committed locally as `93d180da` for branch persistence.

## Acceptance criteria

- Package startup/install surfaces include `gentle-ai-research` as a delegation-owned global agent.
- Its effective child tools are exactly fixed local reads plus explicitly selected/provenanced approved web tools and `subagent_parent_message`.
- The parent selects source classes and tool names only; trusted extension provenance is derived from the host's active registered inventory and revalidated by the child.
- Missing/stale provenance, unselected external tools, Bash, writes, MCP, memory, and nesting fail closed.
- `sdd-research` retains its existing local-tool stripping behavior.
- Generic ODD external research routes to `gentle-ai-research`; SDD research remains SDD-only.
- Focused tests, typecheck, package checks, harness, and the full test suite pass or have explicitly recorded blockers.
