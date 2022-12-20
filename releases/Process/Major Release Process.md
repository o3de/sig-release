> Written with [StackEdit](https://stackedit.io/).
> <![endif]-->

# Draft - O3DE Major Release Process
V1.0 Updated December 5, 2022. 
The release process is managed by sig-release. To request an update to this document, please open an issue at https://github.com/o3de/sig-release/issues

## Key Details
*Intent: Outlines the high-level information about O3DE releases.*

* Releases are owned and managed by sig-release.
* Sig-release relies on the help of others in the O3DE community (outside of SIG-Release). See "Roles and Responsibilities" below
* O3DE Major Releases occur twice each year: approximately in April and October. These dates are discussed in SIG-Release meetings.
* O3DE Minor Releases occur as needed, as decided by sig-release.
* Releases are named  according to recommendations from the marketing committee as outlined at https://github.com/o3de/sig-release/issues/39
* Each release managed using a a Github project board with the set of release process tasks.
* Releases will update the following Repositories:
	* o3de
	* o3de-multiplayersample
	* o3de-netsoaktest


## Roles and Responsibilities
*Intent: Outlines the minimum set of roles and their responsibilities in order to complete all of the necessary release tasks.*

|SIG|Title|Count|Description
|--|--|--|--
|sig-release|Release Manager (and optional Co-Release Manager)|1 to 2|Project manager for a given release responsible for coordinating the release and ensuring processes are followed and tasks are completed. A release manager will also have some tasks they need to complete themselves. Coordination and communication with other SIGs and the marketing committee are essential skills in being a successful release manager. Co-Release manager is second project manager for a given release. They work side-by-side with the release manager on the project management of a release and they take on some of the project management tasks. Co-Release Manager may also be used as a “training role” for someone eventually wanting to serve as release manager.
|sig-build|Release Deployment Engineer|1|Responsible for creating the stabilization branch, uploading the release, tagging Release, and publishing the version number update to o3debinaries.org
|sig-docs-community|Documentation Project Manager|1|Responsible for managing the documentation repository for a release. This includes managing release notes, publishing the documentation for a release, and applying release tags to the docs site. The Documentation Project Manager works closely with the Release manager.
|any sig|Mainline Integrator|1|Requires privilege https://github.com/orgs/o3de/teams/integrators/members . Engineer responsible for merging code from the stabilization branch to mainline.
|any sig|Stabilization Integrator|(up to 12 people)|During the stabilization phase, these community members are responsible for performing "branch maintenance" by merging code from the stabilization branch to the development branch according to a schedule. This branch maintenance is ensures that all of the code submitted into the stabilization branch is also applied back to the development branch.
|any sig|Release Verifier|1|Responsible for verifying release actions such as confirming the merge to the mainline branch, installer verification, and binary verification.
|Marketing Committee|Marketing Coordinator|1|The marketing committee representative responsible for all of the marketing efforts around a release. They will use the feature list to develop their materials for launch such as blog posts and social media. 
|Marketing Committee|Website Manager|1|Responsible for updates to O3DE.org. 


## Terminology
*Intent: Define terms used throughout the release process* 

**Emergency Release:**  also known as a “hotfix”, an emergency updates to fix a specific set of bugs deemed as either critical security issues or blocking basic utilization of the project. Emergency releases result in an incremental update of the version number (i.e. 22.05.0 would become 25.05.1).

**Exception/Exception Process:** The process by which a SIG requests that a particular pull request be introduced into the Stabilization branch during the "soft lock" phase of the stabilization process.

**Feature List:** A list of all of the features in a release. For O3DE, feature lists consist of a summary section at the top with a summary of the main purpose of the release and feature highlights. Then, below this section, the features are listed, grouped by SIG. The Feature list has 2 purposes. 1) it provides the community and marketing with a summary of what to expect in the release 2) it is used by the Documentation Program Manager to create the release notes.

**Major Release:** A planned, scheduled release of O3DE. These usually include efforts by the marketing committee, blog, posts, and generally contain large, significant features. Major releases result in a full update of the version number (e.g. 22.05.0 -> 22.10.0).

**Minor Release:** also known as a “point release”, primarily focused on bug fixes. Point releases usually address a specific need or problem in a previous release. For example, if a major release is occurring and there's a feature that is not yet complete, there could be a decision to ship the major release and follow it with a point release that includes the additional feature. Point releases result in an incremental update of the version number (e.g. 22.05.0 -> 25.05.1).

**Release Stabilization:** The process by which we stabilize the codebase for release. Stabilization is only used for Major Releases and Minor Releases.

**Stabilization Branch:** The code branch where release stabilization occurs.



# Major Release Process Runbook
*Intent: Outline the main steps necessary to complete a major release.* 
Each of the below phases is represented on the Github Issues project board for the release. 

## Phase (1 of 4): Planning
*Intent: Identify all stakeholders and their requirements for the release. Confirm stakeholder responsibilities.* 
Begins 3 months prior to estimated release.
Entry Criteria: sig-release has has discussed the need for a release, per current schedule. 

### 1.1 General Steps
 1. **sig-release** coordinates with the Technical Steering Committee, the O3DE Foundation, and the sigs to determine a release date. This may be done by the SIG chair, co-chair, or the release manager is one has been chosen.
 2. **Release Manager** begins the feature list (see below)
 3. . **Release Manager** Creates Milestones for each of the repositories involved in the release. //TODO 
 4.  **Release Manager** creates the Key Information Github Issue similar to https://github.com/o3de/sig-release/issues/64. The releaser manager should maintain the Key Information as more information about the release is known, or when details change. The release manager should also communicate this issue in sig-all Discord channel to inform the community of the upcoming release and remind them of the Key Information if details change.
 5. **Release Manager** creates a project board for the release with all tasks. Refer to the project board and tasks from the previous release, and manually create tasks 1-by-1 based on the previous release's tasks. Previous project boards are located at https://github.com/o3de/o3de/projects?type=classic
 6. **Release Manager** ensures all Planning tasks on the project board are completed, either by completing them or assigning them to others.
 7. **Release Manager**  has a Planning task on the project board to identify all Release Roles . These release roles should be updated in the Key Information once known.

### 1.2 Beginning work on the Feature List 
The feature list usually begins 6-8 weeks prior to release.  See Terminology (above) for description of the Feature List
Entry Criteria: Pre Release task exists to generate the Feature List, similar to https://github.com/o3de/o3de/issues/11100

Note: This is a highly manual process. There is an opportunity to improve. See Appendix A,

1. Refer to all O3DE Roadmaps to understand which features have been delivered to the codebase. You will use a combination of the SIG-Roadmaps and any other roadmaps (such as those published by corporate development teams working on O3DE).
2. For each roadmap item delivered, enter a summary into the feature list.
3. If you need assistance, comment under the GHI or reach out to the SIG owning that area of the engine
4. (Optional) Review the submitted pull requests or closed Github Issues. The reason to do this would be to discover any features that were not on the Roadmap, potentially features that were accidentally missed. 
5. Save the feature list to https://github.com/o3de/sig-release/tree/main/releases under the appropriate release, for example [22100 feature list.md](https://github.com/o3de/sig-release/blob/main/releases/22.10.0/22100%20feature%20list.md "22100 feature list.md")
6. Once you have created the feature list, post a note to sig-all in discord requesting the sigs to review and update if needed via Pull Request.
7. Notify the marketing committee one the feature list is mostly (80%) done. They may ask for a summary of the release and key features. It is up to the release manager to provide this guidance to the marketing committee. The release manager may discuss with sig-release or any other sig to figure this out.

### 1.3 Using Milestones
//TODO potentially document this. We have not been using milestones consistently, so before doing this we need to speak with QA and Docs to verify usage. 

Exit Criteria: Ideally, all of the planning tasks are complete on the project board. If not all tasks are complete, it is up to the release manager and co-release manager to understand and accept any risk before moving onto Phase 2. 


## Phase (2 of 4): Pre Release (includes Code Stabilization)
*Intent: Accomplish all tasks needed to prepare the codebase for release. Complete all documentation and marketing materials.* 

Begins 6-8 weeks prior to release. This Phase may begin before previous phases are completed, at the discretion of the Release Manager.
Entry Criteria: Project board exists and Pre-Release tasks were created during the Release Planning Phase. 

### 2.1 Communication during Stabilization
It is crucial to maintain strong communication with the community and throughout stabilization. This includes but not limited to:
 - **Release Manager** At least 1 week before stabilization, posting a notification to sig-all and sig-release giving them a heads up.  For example: https://discord.com/channels/805939474655346758/816043864858951710/1011404890364444712
 - **Release Manager** When the stabilization branch is created, post a notification to sig-all and sig-release. This is already listed as a step in the stabilization process
 - **Release Manager** Midway through the stabilization, posting a notification informing the community of the remaining time.
 -  **Release Manager** work with QA/sig-testing to ensure we have regular updates in Discord as to the number of outstanding bugs and how we are doing in terms of stabilizing the release.
 - **Release Manager** communicate with the Documentation Program Manager to ensure that the release notes are kept up to date. This is important because during stabilization there will be bugs that do not get fixed and in some cases these bugs will need to be documented as known issues. 

### 2.2 Steps
 1. **Release Manager** is responsible for ensuring all Github issues in the "Pre Release" phase of the project board are completed.
 2.  **Release Manager** is responsible for overall maintenance and accuracy of the project board.
 3. **Release Manager** is responsible for all tasks assigned to them  identified in the Stabilization Process (link here), which includes periodic community duties. For example, communicating to the community via Discord sig-all, to inform the community that stabilization phase has begun.
 4. On the day we end stabilization (according to plan) it is up to the **Release Manager** to make a determination on whether the stabilization branch is stable enough to be releases.  A release is considered stable when (1) there are no more blocker or critical bugs in the Stabilization branch (2)  and there is agreement from the parties involved in the release

 Then the stabilization branch is merged back to O3DE/main to create the release. After the release is published and all of the code has been merged back to development, the stabilization branch is deleted. During the Stabilization Phase the development branch is used in the same way that it is always used – code submissions to the development branch are not restricted in any way.

### 2.3 Stabilization
//TODO Link to the Stabilization process. It's coming soon and it's large enough to be a separate process. 


### 2.4 Feature Grid 
//TODO - document the process for updating the feature grid

Exit Criteria: All Pre-Release Steps are complete

## Phase (3 of 4): Release Day
*Intent: Accomplish all tasks needed to deploy the release so that it is available for download.* 
Begins day of release
Entry Criteria: All pre-release steps are complete.

### 3.1 Steps
//TODO - document the process for Release day and running the call

Exit Criteria: All Release Day Tasks are complete.

## Phase (4 of 4): Post-Release
*Intent: Perform activities that typically occur after release day.* 
Begins immediately after the release. 

//TODO outline the things that take place post-release

Creating the stabilization branch



## Appendix A: Opportunities and Potential Improvements
1. **Feature List Process:** The ideal way to generate a feature list would be to run a query against pull requests, since the O3DE codebase itself is the source of truth for what has been added since the last release. Although running a query against Github would be ideal, this is not yet possible for O3DE. To achieve this ideal state, you would need to introduce and some standardization for pull requests so that the feature descriptions and details are always present for significant features. More here on simplifying the process https://github.com/o3de/sig-release/discussions/107
2. **Lack of clear overall metrics on Release Readiness:** Through discussions we realized that release readiness likely requires project-wide input (performance, ux, quality, security). Today we mainly look at bug count. We need to get project-wide input and figure out which metrics we should monitor.
3. **We don't have a link on the downloads page for the stabilization build.** We should work with sig-build to make sure they get a link up the day we create the stabilization branch, so the community can more easily get and test the build. It's listed here https://github.com/o3de/o3de/issues/13208 so that it will be done for future releases. We may want to also get it on the downloads page on the website.
