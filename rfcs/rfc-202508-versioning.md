# Versioning Strategy for O3DE Engine and Gems

# Summary:

A versioning strategy is essential for maintaining the integrity and usability of software projects. This document outlines the versioning practices used in our repositories, highlights the problems with the current approach, and lists some ideas without giving a definitive solution.

## What is the relevance of this feature?

### Current Versioning Strategy

The current versioning strategy is described in details in [RFC #44](https://github.com/o3de/sig-core/issues/44). Most of the document focuses on the implementation. The summary of the procedures can be found below.

Versioning and dependency information is currently stored inside `engine.json`, `gem.json`, and `project.json` files. We use the [Semantic Versioning](https://semver.org/) scheme, which consists of three components: _MAJOR_, _MINOR_, and _PATCH_. 

- _MAJOR_ version changes indicate breaking changes.
- _MINOR_ version changes indicate new features that are backward-compatible.
- _PATCH_ version changes indicate backward-compatible bug fixes.

The versioning information is updated by the developers manually. It will be automated in the future. The _stabilization_ branch takes the version number from the HEAD of the _development_ branch at the branch cutoff, and the _development_ branch should get an immediate update of the _MINOR_ version.

It is important to note, that there is one more RFC that describes the versioning strategy for the Engine itself, which is [rfc-core-2022-05-31-engine-versioning](https://github.com/o3de/sig-core/blob/main/rfcs/rfc-core-2022-05-31-engine-versioning.md), which describes the versioning in the format of `YEAR.MONTH.RELEASE`, e.g. `25.05.1` for the first path (point-release) version of the Engine with the planned release date in May 2025.

### What went wrong

The proposed versioning strategy has not been fully implemented, with the following points failing:
- **Manual Updates**: the developers did not update the version numbers at all (only Engine version was updated prior to the release) or did not update them correctly, leading to inconsistencies in versioning across Gems.
- **Incorrect Versioning**: the version on the _stabilization_ branch was created based on the previous _main_ release instead of the latest _development_ version (see [PR #17903](https://github.com/o3de/o3de/pull/17903)) in which there was a regression in the versioning logic
- **No Update on the _development_ branch**: the version numbers were not updated on the _development_ branch right after the _stabilization_ branch cutoff.

### Problems with Current Versioning

The current versioning strategy has several issues:
- **No Automation**: The manual process is error-prone and does not scale well with the high number of Gems.
- **No Information**: The current versioning strategy is not well documented and not spread across the community.
- **No Clear Update Path**: There is no clear information who and when should update the version numbers; there is no clear information how we should update the version numbers. Do we bump a _PATCH_ version for every change in the Gem when working on the _development_ branch? Do we bump a _PATCH_ or _MINOR_ version if the _MAJOR_ version is changed on the _development_ branch already (compared with the _main_ branch)?
- **No Definition of Engine Version**: The Engine version meaning is not clearly defined. If API changes occur in one of the core Gems (e.g. `Atom`), should the _MAJOR_ Engine version be incremented?
- **No Changes Possibility**: It can happen that a particular Gem does not get any updates; hence changing the version number right after the _stabilization_ branch cutoff defined in the RFC makes no sense.

### Current status

The _development_ branch is currently in a state where the version numbers of the Gems are not updated. E.g., `Atom` Gem has the version `0.1.0`. It was updated only once since the initial commit. The engine is set to `4.2.0` on the _development_ branch and `2.4.0` on the _main_ branch. The previous two releases were `2.3.0` and `2.2.0`, with the _PATCH_ version used for point releases. This happened even though there were some breaking changes in the API of the core Gems (e.g. `Atom` Gem).

# Feature design description:

Although the versioning strategy was suggested in the RFC, it was not fully implemented in practice. The current versioning strategy is not well documented, and there is no clear information on how to update the version numbers. This leads to inconsistencies in versioning across Gems and makes it difficult to track changes in the Engine and Gems.

### Temporary Solution for the 2510 Release

Before we can implement a new versioning strategy, we need to ensure that the version number of the Engine is updated correctly for the next release. I suggest the following solution:
- Keep the Engine version `4.2.0` for the upcoming release (2510).
- Keep the versions of the core Gems (e.g. `Atom`) unchanged for the upcoming release (2510).
- Bump the Engine version to `4.3.0` on the _development_ branch.
- Apply the selected versioning strategy described in this document on the _development_ branch for the future release (in 2026).

#### Benefits
- It ensures the Engine version on the _development_ branch and on the _stabilization_ branch is consistent and that the _development_ branch has newer version than release (2510).
- It allows us to continue working on the _development_ branch without breaking the versioning scheme.
- It provides a clear path for the next release without introducing additional complexity.

#### Drawbacks
- It means a bump from `2.4.0` to `4.2.0` for the Engine version between the releases.
- It does not address the issues with the current versioning strategy for Gems.

### Remove the version number from the core Gems
Use the Engine version as the version number for all core Gems instead of a standalone versioning. This way much of the complexity of versioning is removed, making it easier to manage for the community. This could be automated, with a script that updates the version number of all core Gems to match the Engine version whenever the Engine version is updated.

#### Benefits
- It simplifies the versioning scheme by having a single version number for all core Gems.
- It reduces the complexity of managing version numbers for core Gems, as they will always follow the Engine version.

#### Drawbacks
- It removes the ability to track changes in core Gems between Engine releases.
- It is not clear to all developers which Gems are core Gems and which are not (there used to be a plan to move all Gems that are not core to the `o3de-extras` repository, but it was not implemented).

### Bump the version number of the Gem only when doing a release
For all Gems that are **NOT** core Gems, I propose to bump the version number only when doing a release. This means that the version number is updated only when creating a new _stabilization_ branch from the _development_ branch; only for Gems that have changes since the last release. The version number is updated based on the changes made in the Gem, following the Semantic Versioning scheme.

The developers can still bump the version of the Gem internally to any number while testing a new feature or fixing a bug, but this will not be reflected in the version number of the Gem on the _development_ branch.

#### Benefits
- This approach reduces the frequency of version number changes, leading to a more stable versioning scheme on the _main_ branch.
- It clearly defines the changes made in each release by incrementing the _MAJOR_, _MINOR_, or _PATCH_ version numbers based on the changes made in the Gem. 

#### Drawbacks
- No information about the changes made in the Gem when working on the _development_ branch.
- It requires a large effort to ensure that the version number of each Gem is updated correctly when creating a new _stabilization_ branch (in particular, it requires a decision for each Gem whether to bump the _MAJOR_, _MINOR_, or _PATCH_ version number).
- It requires porting back the version number changed to the _development_ branch after the _stabilization_ branch is created.

> Note: this approach is used for all Gems and Templates in the `o3de-extras` repository, as it was the most intuitive to me, while the number of Gems is much smaller than in the Engine repository.

# Are there any alternatives to this feature?

### Keep the current versioning scheme for all Gems (including core Gems)
One alternative is to continue using the current versioning scheme for all Gems, including core Gems. This would mean that each Gem has its own version number, and changes to the Gem are reflected in its version number regardless of the Engine version. However, this approach would generate too much effort for the developers when changing the version numbers of the Gems for the release and would require another approach for changing the version numbers of the Gems on the _development_ branch. Two other approaches are described below.

### Always bump the version number of the Gem
One possible solution is to always bump the version number for every change in the Gem (when working on the _development_ branch). This means that the version number is updated by a developer working on a Gem or some automation when merging the Gem to the _development_ branch.

#### Benefits
- It enables tracking changes when working on the _development_ branch.
- It is easy to implement and understand (especially if some automation is implemented).
- No need to change the versions of the Gems on the _stabilization_ branch, as the _development_ branch will always have the latest version number.

#### Drawbacks
- It can lead to excessive version number changes, causing discontinuity in the versioning numbers on the _main_ branch (due to multiple updates on the _development_ branch between the releases).
- It can create conflicts when multiple developers are working on the same Gem.

### Update the version number of the Gem when doing a change in the Gem
Another alternative approach is a combination of the previous two solutions. The version number is updated when doing a change in the Gem on the _development_ branch, but the version number is not updated when creating a new _stabilization_ branch. The version number is updated based on the changes made in the Gem, following the Semantic Versioning scheme and taking into account the changes made in the Gem since the last release.

#### Benefits
- It enables tracking changes when working on the _development_ branch.
- It reduces the frequency of version number changes, leading to a more stable versioning scheme on the _main_ branch.
- It clearly defines the changes made in each release by incrementing the _MAJOR_, _MINOR_, or _PATCH_ version numbers based on the changes made in the Gem.

#### Drawbacks
- It requires a large effort to ensure that the version number of each Gem is updated correctly when creating/reviewing a pull request to the _development_ branch (it requires a check whether the version number was updated after the last release, as, e.g., the _PATCH_ version number should not be changed if the _MAJOR_ version number was already changed).

# How will users learn this feature?
We will update the documentation and announce it in the community channels. The most important part is to ensure that the maintainers are aware of the new versioning strategy and how to apply it. This way the maintainers can ensure that the version numbers are updated correctly in the pull requests to the _development_ or _stabilization_ branches.
