
# O3DE Stabilization Process
V1.1 Updated Mar 10, 2023. The release process is managed by sig-release. To request an update to this document, please open an issue at [https://github.com/o3de/sig-release/issues](https://github.com/o3de/sig-release/issues)
																												

O3DE Stabilization is the process we use to prepare the codebase for a release. During Stabilization we create a branch off of the development branch to create a “stabilization branch”, limit any new feature introduced into the branch, and the community fixes bugs. This helps to ensure O3DE releases do not ship with bugs that will block a user’s ability to utilize O3DE. Note that stabilization is not mean to catch every issue, and instead works in conjunction with unit tests, nightly automated test runs, functional automated testing, manually running test passes, and issues filed by the community.  
  

## Key Details

-   The Stabilization Process typically takes place as part of the Release Process. Please refer to the [O3DE Major Release Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Major%20Release%20Process.md) for more information about O3DE releases.
-   As of Release 22.10.0, stabilization takes approximately 5 weeks from beginning stabilization to declaring the stabilization branch as "stable"
-   Stabilization involves the following O3DE Repositories:
    -   o3de
    -   o3de-multiplayersample
    -   o3de-test
    -   o3de-extras

## Roles and Responsibilities
*Intent: Outlines the minimum set of roles and their responsibilities in order to complete all of the necessary release tasks.*

The following outlines roles and responsibilities related to the Stabilization process. This list represents a subset of the roles involved in the O3DE Release. The other roles involved in the release are identified in the [O3DE Major Release Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Major%20Release%20Process.md) 

|SIG or Group|Title|Count|Description
|--|--|--|--
Build SIG| Release Deployment Engineer|1|Responsible for creating the stabilization branch, uploading the release, tagging Release, and publishing the version number update to o3debinaries.org . Must have maintainer privileges.
|*All Code-Contributing SIG|Stabilization Integrator|up to 12|During the stabilization phase, these community members are responsible for performing "branch maintenance" by merging code from the stabilization branch to the development branch according to a schedule. This branch maintenance is ensures that all of the code submitted into the stabilization branch is also applied back to the development branch. Integrators must have maintainer privileges.
|Release SIG|Release Manager|1 to 2|Release Manager (and Co-Release Manager) act on behalf of sig-release as Project manager for a given release. They responsible for coordinating the release and ensuring processes are followed and tasks are completed.
|*All Code-Contributing SIG|Mainline Integrator|1|Requires specific privilege [https://github.com/orgs/o3de/teams/integrators/members](https://github.com/orgs/o3de/teams/integrators/members) . Responsible for merging code from the stabilization branch to mainline.

***All Code-Contributing SIG** refers to engineering/feature SIGs. These include: Build SIG, Content SIG, Core SIG, Network SIG, Platform SIG, Graphics-Audio SIG, Security SIG, Simulation SIG, Testing SIG     


## Terminology
*Intent: Define terms used throughout the release process* 
-   **Development Branch:** The branch where day-to-day development occurs. Submissions to this branch are not restricted during stabilization. Since this branch always contains work that is ‘in development’, it will occasionally have blocking bugs. This branch always exists. Stabilization work is not performed in this branch.
-   **Main Branch:** This branch only contains final releases and is the last integration performed at the end of a stabilization effort. This branch always exists and is a mirror of the latest release installer for Windows and Linux. This branch has restricted access and requires special permissions to be able to commit to.
-   **Stabilization branch:** This branch is where release stabilization efforts occur. This branch is created at the start of the stabilization process, and the branch is removed within 24 hours after the stabilization branch is integrated into the Main Branch.  
    ***Regarding Features In the Stabilization Branch*** When the stabilization branch is created, the Features that exist in the branch represent the features that will appear in the final release. After we create the stabilization branch, it is uncommon for new features to be added to the stabilization branch. Any new features added to the stabilization branch require an exception (see exception request).
-   **Exception Request:** This is a formal request to sig-release and the sig owning the suggested change, to either:
    -   Allow a feature into the stabilization branch at any time.
    -   Allow a bug fix into the branch during the ‘soft lock’ phase of stabilization.
    -   See [Exception Process](#exception-process)
-   **Soft Lock Phase:** This is a period of time, towards the end of the stabilization period, when no changes are allowed to the stabilization branch, unless an exception is granted (see  [Exception Process](#exception-process)). The Soft Lock Phase is similar to the traditional Beta phase of a project.
-   **Hardening Process:** The process of allowing the stabilization branch to be tested with zero changes over a period of time, giving confidence that the code base is of high enough quality to release. This occurs at the end of the stabilization process.


## Exception Process  
The Exception process is managed in a Github project - the process is currently documented in the description of the project [https://github.com/o3de/o3de/projects?type=classic](https://github.com/o3de/o3de/projects?type=classic) .  
There is an open discussion regarding streamlining the exception process: [https://github.com/o3de/sig-release/discussions/106](https://github.com/o3de/sig-release/discussions/106)    


## Goals of the Stabilization process

1.  **Stabilize the Release:** Ensure we ship the most stable version of O3DE we can.
2.  **Separate Release preparation from day-to-day development:** We permit bug fixing and stabilization to occur without hindering developers that are working on new features.
3.  **Stabilize the O3DE project overall:** Our process ensures that bug fixes made for stabilization are reflected in the development branch.
  
## Stabilization Process:

*Note: during this process, development still continues as normal in the development branch. The development branch is never locked and never requires exceptions.*  
  
### Precondition:  

1.  (Release Manager) coordinates with the Technical Steering Committee, the Open 3D Foundation Marketing Committee, and the SIGs to determine a release date.

### Phase 1 - Setup

1.  (Release Deployment Engineer) Currently, 6 weeks before a planned release, a stabilization branch is created. This branch is named Stabilization/<version number>. Example; for the 22.10 release we would create a Stabilization/2210 branch.
2.  (Release Deployment Engineer) The development branch, in its current state, is integrated to the newly created stabilization branch, preferably on the same day the stabilization branch is created.
3.  (Release Manager) publishes a note in sig-all indicating that we have begun release stabilization. Encourage the community to test, report bugs, and fix them in the stabilization branch.
4.  (Release Manager) Coordinates with sigs to create a schedule of stabilization → development integrations and maintainers responsible for those integrations.

### Phase 2 - Stabilization

1.  When fixing bugs for stabilization and/or a release, please fix these bugs in stabilization and let the stabilization integrators handle getting these fixes to development branch. “Cherry picking” of changes between development and stabilization branches should not be done because it can lead to problematic integrations.
2.  (Stabilization Integrator) Twice a week, during the entire stabilization period, a contributor (Stabilization Integrator) will integrate from the stabilization branch to the development branch. These integrations require 2 reviewers and a maintainer to submit the integration. <link to integration process here>

1.  The frequent cadence ensures that the commit rate per integration is low, making for an easier and quicker integration.
2.  The frequent cadence makes it easier to identify and remove any stabilization changes that we do NOT want integrated into development. Better signal to noise ratio.
3.  If a major conflict is encountered, the stall in the integration is not holding up a large chain of commits
4.  It is easier to handle Developer Certificate of Origin (DCO) issues with smaller integrations.
5.  Integrations usually occur on Mondays and Thursdays. Never Fridays to reduce the chance the development branch is broken over a weekend.

### Phase 3 - Soft Lock
 
1. (Release Manager) Once sig-release determines the stabilization branch is potentially releasable, the branch is “soft locked”. This means no changes are allowed into the branch unless the change receives an exception from sig release and the owning sig. "Soft Lock" is not a physical lock - it is something that is communicated and understood across the project. The Release Manager should communicate in Discord #sig-all, #sig-release that the stabilization branch is soft locked. 

### Phase 4 - Release

1.  (Mainline Integrator) This step occurs on release day during the release call. Once sig-release determines the stabilization branch has been locked and hardened for enough time (usually 2 weeks) and no critical issues are outstanding, the stabilization branch is integrated to development, then integrated to main, and tagged with the release version.
