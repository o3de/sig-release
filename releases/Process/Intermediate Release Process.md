
# O3DE Intermediate Release Process for Canonical Repositories
V1.0 
The release process is managed by SIG-Release. To request an update to this document, please open an issue at [https://github.com/o3de/sig-release/issues](https://github.com/o3de/sig-release/issues)

This document describes how **canonical repositories** — repositories that ship Gems and Templates consumable through the O3DE Project Manager, such as `o3de-extras` — can be released *between* scheduled O3DE engine releases. It builds on the backporting strategy proposed in [backporting strategy RFC](https://github.com/o3de/sig-release/pull/356) and reuses terminology and roles already established in the [O3DE Major Release Process](./Major%20Release%20Process.md) and the [O3DE Stabilization Process](./Stabilization%20Process.md).

## Key Details
*Intent: Outline when and how an intermediate release of a canonical repository happens, independent of the main O3DE engine release cadence.*

* Canonical repositories, such as `o3de-extras`, normally release in lockstep with the O3DE engine (see the "Current Release Process" section of the backport RFC). This document describes the exception to that: releasing Gems/Templates from a canonical repository without waiting for the next scheduled engine release.
* There are two independent paths, chosen based on urgency and scope:
  1. **Emergency Release Path** — for a single blocker/critical bug that cannot wait for the next scheduled release.
  2. **Feature Addition Path** — for bundling one or more non-urgent features or backports into a planned, time-boxed intermediate release.
* An intermediate release always targets one of two branches:
  * `main` — if the release applies to the **latest** O3DE engine release.
  * `backports/<o3de-version>` — if the release applies to an **older, previously-released** O3DE engine version, following the branch naming convention defined in the backport RFC (for example `backports/25051` for O3DE 25.05.1).
* This process does **not** change how the repository is tagged. Tags continue to be added only to the release commits that correspond to an official O3DE **engine** release (see [Major Release Process](./Major%20Release%20Process.md#key-details)). Intermediate releases produced by either path are identified through `gem.json`/`template.json` version bumps and the published `repo.json`, not through new git tags.
* Compatibility between a backported release and the O3DE engine version(s) it supports is resolved through existing `gem.json`/`template.json` tooling, which allows a Gem or Template to declare which engine versions it is compatible with. This is not a new mechanism introduced by this document — it's the same metadata already used by the O3DE Project Manager to filter available Gems and Templates.

## Roles and Responsibilities
*Intent: Outlines the minimum set of roles and their responsibilities to complete an intermediate release.*

|Role|Count|Description
|--|--|--
|Maintainer (Requester)|1|A maintainer of the canonical repository who identifies the need for an intermediate release — either a critical bug (Emergency Release Path) or a set of features/backports (Feature Addition Path) — and drives the release to completion.
|Approving Maintainers/Reviewers|2+|Maintainers or reviewers with merge privileges on the canonical repository who review and approve the change before it is merged. See approval requirements per path below.
|SIG-Release Approver (Release Manager or co-Release Manager)|1|Reviews and approves the release before merge, on behalf of SIG-Release, for **both** paths. Required so that SIG-Release keeps the [Key Information](./Major%20Release%20Process.md) for the affected engine version(s) accurate, and can flag any conflict with the engine's own release/stabilization schedule.

---

## Path 1: Emergency Release
*Intent: Get a fix for a blocker/critical bug in front of the community as fast as possible, without waiting for the next scheduled engine or intermediate release.*
*Entry Criteria: A blocker or critical bug is found in a canonical repository, affecting a released O3DE engine version.*

### Steps
1. **Maintainer** raises the need for an emergency release by opening an issue (or commenting on the existing bug issue) in the canonical repository, clearly stating: the affected Gem/Template, the affected O3DE engine version(s), the severity/impact, and the target branch (`main` or `backports/<o3de-version>`); and posts a notice to `#sig-release` and the owning SIG's Discord channel announcing the intent to create an emergency release.
2. **Maintainer** (or the reporting contributor) opens a PR with the fix against the target branch. The PR also bumps the patch version in the affected `gem.json`/`template.json` file(s) and confirms the engine-compatibility metadata is still correct for the target branch.
3. **Approving Maintainers/Reviewers** review the PR. The PR requires approval from **at least two maintainers with merge privileges on the repository**, with **at least one of those approvals from a maintainer of the affected Gem/Template**. This mirrors the two-party sign-off already used for exceptions during engine stabilization (see [O3DE Exception Checklist](./O3DE%20Exception%20Checklist.md)), scaled down for a single-repository fix.
4. **SIG-Release Approver** reviews and approves the PR, in addition to the maintainer approvals from step 3.
5. Once both maintainer approvals and the SIG-Release approval are in place, the PR is merged **immediately** — there is no stabilization period or exception board for this path, since the whole point is to react quickly to a blocking issue.
6. **Maintainer** generates the release package(s) for the merged fix.
7. **Maintainer** regenerates and publishes the updated `repo.json` to `canonical.o3de.org` so the fix is available through the O3DE Project Manager.
8. **Maintainer** posts a notice to `#sig-all` and the owning SIG's Discord channel describing the fix and affected version(s), for visibility.

*Exit Criteria: The fix is merged to the target branch, the release package and `repo.json` are published, and the community has been notified.*

---

## Path 2: Feature Addition Release
*Intent: Bundle one or more non-urgent features or backports into a planned intermediate release, using a short stabilization window scaled down from the full [Stabilization Process](./Stabilization%20Process.md).*
*Entry Criteria: A maintainer identifies enough pending features or backport requests to justify a scheduled intermediate release, rather than waiting for the next scheduled engine release.*

### Steps
1. **Maintainer** announces the need for an intermediate release on the `#sig-release` Discord channel, identifying:
   * Whether the release targets the **latest** release (merging into `main`) or an **older, backported** engine version (merging into an existing or new `backports/<o3de-version>` branch).
   * The set of features/backports intended to be included.

   The **SIG-Release Approver** confirms the request on that channel before the maintainer proceeds.
2. **Maintainer** creates a stabilization branch off the **release branch being targeted** — `main` if the intermediate release targets the latest O3DE release, or the corresponding `backports/<o3de-version>` branch if it targets an older, backported engine version — the same way a point release branches off the released version rather than off `development` (naming convention: `stabilization/<target>`, for example `stabilization/25051`). If the target is an older engine version and its `backports/<o3de-version>` branch does not yet exist, the **Maintainer** creates it first.
3. **Maintainer** posts a notice to `#sig-all` and the owning SIG's Discord channel, as in [Path 1](#path-1-emergency-release), announcing the start of a **two-week stabilization period**, stating the branch name, target (`main` or `backports/<o3de-version>`), and the planned end date.
4. During the two-week window, only fixes for bugs found in the stabilization branch are accepted; new, unrelated features are not added once the branch is created (same principle as the full Stabilization Process, scoped to this single repository).
5. At the end of the two weeks, the **Maintainer** confirms the stabilization branch has no outstanding blocker/critical bugs, and bumps the relevant `gem.json`/`template.json` version(s) and engine-compatibility metadata on the stabilization branch.
6. **SIG-Release Approver** reviews and approves the release before it is merged.
7. Once approved, the **Maintainer** merges the stabilization branch:
   * Into `main`, if the intermediate release targets the latest O3DE release.
   * Into the corresponding `backports/<o3de-version>` branch, if the intermediate release targets an older, backported engine version.
8. **Maintainer** generates the release package(s), and regenerates and publishes `repo.json` to `canonical.o3de.org`.
9. **Maintainer** posts a notice to the relevant Discord channel(s) announcing the completed intermediate release and its contents.

*Exit Criteria: The stabilization branch is merged to its target branch, the release package(s) and `repo.json` are published, and the community has been notified.*

---

## Post-Intermediate-Release
*Intent: Describe the housekeeping that follows the publication of an intermediate release, for either path.*

1. If a stabilization branch was created (Feature Addition Path), the **Maintainer** deletes it once it has been merged into its target branch, consistent with how the engine's stabilization branch is removed after being merged to `main` (see [Stabilization Process](./Stabilization%20Process.md)).
2. The **Maintainer** ports the changes released via the updated `repo.json` (the underlying code changes on `main` or the `backports/<o3de-version>` branch) back to the `development` branch, so that ongoing development does not diverge from what was just released. This mirrors the role of the Stabilization Integrator in the full engine release process, who ensures fixes made in the stabilization branch are also applied back to `development`.
