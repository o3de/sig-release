
# O3DE Major Release Process
V1.2 Updated Mar 10, 2023. 
The release process is managed by the Release Special Interest Group (SIG). To request an update to this document, please open an issue at https://github.com/o3de/sig-release/issues

## Key Details
*Intent: Outlines the high-level information about O3DE releases.*

* Releases are owned and managed by the Release SIG.
* The Release SIG relies on the help of others in the O3DE community (outside of SIG-Release). See "Roles and Responsibilities" below
* O3DE Major Releases occur twice each year: approximately in April and October. These dates are discussed in Release SIG meetings.
* O3DE Minor Releases occur as needed, as decided by the Release SIG.
* Releases are named  according to recommendations from the O3DE marketing committee as outlined at https://github.com/o3de/sig-release/issues/39
* Each release managed using a a Github project board with the set of release process tasks.
* Releases will update the following Repositories:
	* o3de
	* o3de-multiplayersample
	* o3de-netsoaktest
	* o3de-extras
	* o3de.org


## Roles and Responsibilities
*Intent: Outlines the minimum set of roles and their responsibilities in order to complete all of the necessary release tasks.*

|SIG or Group|Title|Count|Description
|--|--|--|--
|Release SIG|Release Manager (and optional Co-Release Manager)|1 to 2|Project manager for a given release responsible for coordinating the release and ensuring processes are followed and tasks are completed. A release manager will also have some tasks they need to complete themselves. Coordination and communication with other SIGs and the marketing committee are essential skills in being a successful release manager. Co-Release manager is second project manager for a given release. They work side-by-side with the release manager on the project management of a release and they take on some of the project management tasks. Co-Release Manager may also be used as a “training role” for someone eventually wanting to serve as release manager.
|Build SIG|Release Deployment Engineer|1|Responsible for creating the stabilization branch, uploading the release, tagging Release, and publishing the version number update to o3debinaries.org. Must have maintainer privileges . 
|Docs-Community SIG|Documentation Project Manager|1|Responsible for managing the documentation repository for a release. This includes managing release notes, publishing the documentation for a release, and applying release tags to the docs site. The Documentation Project Manager works closely with the Release manager, completing the steps detailed in the [Docs Release Process](./Docs%20Release%20Process.md).
|*All Code-Contributing SIG|Mainline Integrator|1|Requires privilege https://github.com/orgs/o3de/teams/integrators/members . Engineer responsible for merging code from the stabilization branch to mainline.
|*All Code-Contributing SIG|Stabilization Integrator|up to 12|During the stabilization phase, these community members are responsible for performing "branch maintenance" by merging code from the stabilization branch to the development branch according to a schedule. This branch maintenance is ensures that all of the code submitted into the stabilization branch is also applied back to the development branch. Integrators must have maintainer privileges.
|All SIG|Release Verifier|1|Responsible for verifying release actions such as confirming the merge to the mainline branch, installer verification, and binary verification.
|Marketing Committee|Marketing Coordinator|1|The marketing committee representative responsible for all of the marketing efforts around a release. They will use the feature list to develop their materials for launch such as blog posts and social media. 
|Marketing Committee|Website Manager|1|Responsible for updates to O3DE.org. 

***All Code-Contributing SIG** refers to engineering/feature SIGs. These include: Build SIG, Content SIG, Core SIG, Network SIG, Platform SIG, Graphics-Audio SIG, Security SIG, Simulation SIG, Testing SIG

## Terminology
*Intent: Define terms used throughout the release process* 

**Emergency Release:**  also known as a “hotfix”, an emergency updates to fix a specific set of bugs deemed as either critical security issues or blocking basic utilization of the project. Emergency releases result in an incremental update of the version number (i.e. 22.05.0 would become 25.05.1).

**Exception/Exception Process:** The process by which a SIG requests that a particular pull request be introduced into the Stabilization branch during the "soft lock" phase of the stabilization process.

**Feature List:** A list of all of the features in a release. For O3DE, feature lists consist of a summary section at the top with a summary of the main purpose of the release and feature highlights. Then, below this section, the features are listed, grouped by SIG. The Feature list has 2 purposes. 1) it provides the community and marketing with a summary of what to expect in the release 2) it is used by the Documentation Program Manager to create the release notes.

**Major Release:** A planned, scheduled release of O3DE. These usually include efforts by the marketing committee, blog, posts, and generally contain large, significant features. Major releases result in a full update of the version number (e.g. 22.05.0 -> 22.10.0).

**Minor Release:** also known as a “point release”, primarily focused on bug fixes. Point releases usually address a specific need or problem in a previous release. For example, if a major release is occurring and there's a feature that is not yet complete, there could be a decision to ship the major release and follow it with a point release that includes the additional feature. Point releases result in an incremental update of the version number (e.g. 22.05.0 -> 25.05.1).

**Release Notes:** A document that list of all of the notable features, bug fixes, deprecations, and known issues in a release. See  https://www.o3de.org/docs/release-notes/archive/ for previous Release Notes. Release notes are generated by sig-docs-community Documentation Program Manager for the release using the Feature List as an input. 

**Release Stabilization:** The process by which we stabilize the codebase for release. Stabilization is only used for Major Releases and Minor Releases.

**Stabilization Branch:** The code branch where release stabilization occurs.



# Major Release Process Runbook
*Intent: Outline the main steps necessary to complete a major release.* 
Each of the below phases is represented on the Github Issues project board for the release. 

## Phase (1 of 4): Planning
*Intent: Identify all stakeholders and their requirements for the release. Confirm stakeholder responsibilities.
Begins: 3 months prior to estimated release.
Entry Criteria: Release SIG has has indicated the need for a release and has a general idea of the release date. See [key details.](#key-details) for the current release cadence. See previous release dates at https://www.o3de.org/docs/release-notes/archive/*

### 1.1 General Steps
1. **Release SIG** coordinates with the Technical Steering Committee, the Open 3D Foundation Marketing Committee, and the SIGs to determine a release date. This may be done by the SIG chair, co-chair, or the release manager if one has been chosen.
 2. **Release Manager** begins the feature list (see below)
 3. **Release Manager** Creates Milestones for each of the repositories outlined in [Key Details](#key-details). Here is an example from the 22.10.0 Release. https://github.com/o3de/o3de/milestone/11 - follow a similar naming convention.
 4.  **Release Manager** creates the Key Information Github Issue similar to https://github.com/o3de/sig-release/issues/64. The releaser manager should maintain the Key Information throughout the release. It should be updated as more information about the release is known, or when details change. The release manager should also post a link to the Key Information in #sig-all Discord channel to inform the community of the upcoming release, If the Key Information changes, the Release Manager should post a new message to #sig-all noting that release information has changed.
 5. **Release Manager** creates a project board for the release with all tasks in the O3DE Repository. Refer to the project board and tasks from the previous release, then manually create tasks in your new release  1-by-1 based on the previous release's tasks. Previous project boards are located at https://github.com/o3de/o3de/projects?type=classic
 6. **Release Manager** ensures all Planning tasks on the project board are completed, either by completing them or assigning them to others.
 7. **Release Manager**  has a Planning task on the project board to identify all Release Roles. These release roles should be updated in the Key Information once known.

### 1.2 Create the Feature List 
The Feature List usually begins 6-8 weeks prior to release and ends 1-2 weeks after stabilization begins.  See [Terminology](#terminology) for description of the Feature List.
Entry Criteria: A Pre Release task exists to generate the Feature List, similar to https://github.com/o3de/o3de/issues/11100

Note: This is a highly manual process. There is an opportunity to improve. See Appendix A,

1. Follow the steps outlined for the pre-release task. In the pre-release task step (1) Create a feature list file at [https://github.com/o3de/sig-release/tree/main/releases](https://github.com/o3de/sig-release/tree/main/releases)  under the appropriate release, for example  [22100 feature list.md](https://github.com/o3de/sig-release/blob/main/releases/22.10.0/22100%20feature%20list.md "22100 feature list.md") . The initial feature list file that you create should have a heading for each SIG.  
For pre-release step (4) "Review closed issues to see if anything else should be added."  
	* You will need to Refer to all O3DE Roadmaps to understand which features have been delivered to the codebase.
	  * SIG Roadmaps, for example [the O3DE UI/UX Roadmap.](https://github.com/orgs/o3de/projects/9)
	  * Other roadmaps,  including those published by foundation members. For example [the Roadmap of AWS Contributions to O3DE.](https://github.com/orgs/o3de/projects/11)
	* For each roadmap item delivered to the o3de codebase since the last release, enter a summary into the feature list.
	* If you need assistance, comment under the GHI or reach out to the SIG owning that area of the engine
	* (Optional) Review the submitted pull requests or closed Github Issues. The reason to do this would be to discover any features that were not on the Roadmap, potentially features that were accidentally missed. 
3. Once you have created the feature list, post a note to #sig-all in discord requesting the SIGs to review and update if needed via Pull Request. Allow Pull Requests to the Feature List until 1-2 weeks after Stabilization begins (agree on a date with the Documentation Project Manager). 
4. Notify the marketing committee once the feature list is mostly (80%) done (you have some input from each SIG, and they indicate that they "most" of their work submitted). They may ask for a summary of the release and key features. It is up to the release manager to provide this guidance to the marketing committee. The release manager may discuss with the Release SIG or any other SIG to figure this out.
5. Once you reach the date to stop accpeting PRs to the Feature list. Notify the Documentation Project Manager to take the feature list and begin the Release Notes. From this point forward, any changes needed to the release documentation should be done by coordinating with the Documentation Project Manager.

### 1.3 More about how Milestones are used
For each release, Github milestones are used to track bugs found in the stabilization branches of each repo involved in the release. For example, for the 22.20.0 release, the [Release/2210 milestone](https://github.com/o3de/o3de/milestone/11) captures all of the bugs found during release stabilization of the O3DE repo.

Milestones are used as follows:
* When bugs are found in the stabilization branch, the reported bug is added to the Milestone by the release manager. (these instructions should be posted/clarified in the Release "Key Information")
    * This means that the release manager will need to watch incoming bugs, and for any bugs reported against the stabilization branch, they should add the bug to the release milestone.
* Each SIG will use the milestone to understand which issues are outstanding (and should be fixed).
* For some Milestone issues, we may choose to not fix them. For example a minor issue found very late in the stabilization process. If an issue will not be fixed for the release then (1) it should be agreed upon by the Release Manager and owning SIG (2) Add a comment to the issue indicating that the issue should get a "release note" and make sure to "@" the Documentation Project Manager (3) upon confirmation from the Documentation Project Manager, remove the milestone from the issue
* The Release Manager will use the milestone to monitor the number of outstanding bugs, to understand how the project is progressing towards being stable.
* All bugs in the Milestone must be closed before the release can go out. 

*Exit Criteria:*
*1. All of the [General Steps](#1.1-General-Steps) are complete.*
*2. Ideally, but not required. All of the planning tasks are complete on the project board. If not all tasks are complete, it is up to the release manager and co-release manager to understand and accept any risk before moving onto Phase 2.*


## Phase (2 of 4): Pre Release (includes Code Stabilization)
*Intent: Accomplish all tasks needed to prepare the codebase for release. Complete all documentation and marketing materials.
Begins: 6-8 weeks prior to release. This Phase may begin before previous phases are completed, at the discretion of the Release Manager.
Entry Criteria: Project board exists and Pre-Release tasks were created during the Release Planning Phase.*

### 2.1 Communication during Stabilization
It is crucial to maintain strong communication with the community and throughout stabilization. This includes but not limited to:
 - **Release Manager** At least 1 week before stabilization, posting a notification to #sig-all and #sig-release Discord channels giving them a heads up.  For example: https://discord.com/channels/805939474655346758/816043864858951710/1011404890364444712
 - **Release Manager** When the stabilization branch is created, post a notification to #sig-all and #sig-release Discord channels. This is listed as a step in the stabilization process, but listing it again here 
 - **Release Manager** Midway through the stabilization, posting a notification informing the community of the remaining time.
 -  **Release Manager** communicate regularly with each SIG in Discord to ensure they are aware of the outstanding bugs in the Stabilization branch (the bugs can be found in the Github milestone). 
 -  **Release Manager** post regularly in #sig-all and #sig-release with statistics about the progress toward stabilizing the release. These communications  should include Total number of bugs found, Bug Fixed so Far, Bug remaining.
 - **Release Manager** communicate with the Documentation Program Manager to ensure that the release notes are kept up to date. This is important because during stabilization there will be bugs that do not get fixed and in some cases these bugs will need to be documented as known issues. 

### 2.2 Steps
 1. **Release Manager** is responsible for ensuring all Github issues in the "Pre Release" phase of the project board are completed. 
	 -  Prioritize the Feature Grid Process and make sure you reach out to SIGs ASAP about updating their feature Grids.
 2.  **Release Manager** is responsible for overall maintenance and accuracy of the project board.
 3. **Release Manager** is responsible for all tasks assigned to them  identified in the [Stabilization Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Stabilization%20Process.md), which includes periodic community duties. For example, communicating to the community via Discord #sig-all, to inform the community that stabilization phase has begun.
 4. On the day we end stabilization (according to plan) it is up to the **Release Manager** to make a determination on whether the stabilization branch is stable enough to be releases.  A release is considered stable when (1) there are no more blocker or critical bugs in the Stabilization branch (2)  and there is agreement from the parties involved in the release.
 5. Per the [Stabilization Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Stabilization%20Process.md), as of Release 22.10.0, stabilization takes approximately 5 weeks from beginning stabilization to declaring the stabilization branch as "stable"

 Then the stabilization branch is merged back to O3DE/main to create the release. After the release is published and all of the code has been merged back to development, the stabilization branch is deleted. During the Stabilization Phase the development branch is used in the same way that it is always used – code submissions to the development branch are not restricted in any way.

### 2.3 Stabilization Process
[Stabilization Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Stabilization%20Process.md)

### 2.4 Feature Grid Process
Currently, updating the Feature Grid is a brute force manual process, by which the Release Manager requests the other SIGs to update the process. See all of the feature grid issues from the 22.10 release here:  https://github.com/o3de/o3de/projects/18?card_filter_query=grid  

During Phase 2, it is up to the Release Manager to work with SIGs to get them to update the Feature Grid. The Documentation Project Manager is responsible for publishing the Feature Grid to the O3DE website. For more information refer to the [Feature Grid](./Docs%20Release%20Process.md#feature-grid) section in the Docs Release Process. 

### 2.5 Documentation Release Process

The Documentation Project Manager is responsible for the following items:
* **O3DE Docs Stabilization**
* **Release Notes**
* **Feature Grid**
* **C++ API Reference Generation**
* **Documentation Versioning**
* **Version Information**
Each of these tasks are further explained in the [Docs Release Process](./Docs%20Release%20Process.md). 

*Exit Criteria: All Pre-Release Steps are complete*

## Phase (3 of 4): Release Day
*Intent: Accomplish all tasks needed to deploy the release so that it is available for download.
Begins: day of release
Entry Criteria: All pre-release steps are complete. Prior to Release Day you will have had 2 opportunities to go through the Release day work (1) In the Planning phase of the release, there will be a task "Prepare for Launch Call" which will be the first time you read through all of the steps in the launch call (2) In the Pre-Release phase there will be a "dry run" of the release day call.*

### 3.1 Steps
1. Hold the release call on Release Day. You should have an issue in your project in the "Release Day' phase, called "Execute Launch for O3DE...", similar to [this task for the 22.10.0 Release](https://github.com/o3de/o3de/issues/11096).
2. After roll call is taken, ask if anyone on the call has a reason to postpone the release. Discuss any concerns. 
3. During the call, walk through the steps in your Release task. Ask each owner to perform their task and ask them to confirm once they are done. The work for LFS Binary Objects is expected to take a while, and will not be complete during the call. This is OK.
4. The final steps involve verification. After verification, the release is done. At this point confirm with everyone that they do not have any remaining work. Confirm the plan for LFS Binary Objects with the owner - basically you need them to confirm with you once that work is complete. Congratulations, the release is now available to the community!
5. In Discord #marketing-committee post a note informing them that the release is available. 

*Exit Criteria: All Release Day Tasks are complete.*

## Phase (4 of 4): Post-Release
*Intent: Perform activities that typically occur after release day.* 
Begins immediately after the release. The work in this phase may be minimal, depending on the release,

### 4.1 Steps
1. Go through the "Post Release" phase of the Github project board and ensure the tasks get completed. Reach out to the owners of each task as needed to make sure they complete their tasks.
2. Make sure all previous tasks are fully completed closed (you may have minor things you wanted to follow up on).
3. Make any updates to this documentation as needed. This documentation should reflect the current release process.
4. Open a discussion to gather feedback on the release, similar to https://github.com/o3de/sig-release/discussions/101  . Post to Discord #sig-all and #sig-release to ask for feedback. 
5. In a future sig-release meeting review the discussion with the Release SIG. In the meeting address comments,  then if needed generate new issues of things that should be changed.


## Appendix A: Opportunities and Potential Improvements
1. **Feature List Process:** The ideal way to generate a feature list would be to run a query against pull requests, since the O3DE codebase itself is the source of truth for what has been added since the last release. Although running a query against Github would be ideal, this is not yet possible for O3DE. To achieve this ideal state, you would need to introduce and some standardization for pull requests so that the feature descriptions and details are always present for significant features. More here on simplifying the process https://github.com/o3de/sig-release/discussions/107
2. **Lack of clear overall metrics on Release Readiness:** Through discussions we realized that release readiness likely requires project-wide input (performance, ux, quality, security). Today we mainly look at bug count. We need to get project-wide input and figure out which metrics we should monitor.
3. **We don't have a link on the downloads page for the stabilization build.** We should work with the Build SIG to make sure they get a link up the day we create the stabilization branch, so the community can more easily get and test the build. It's listed here https://github.com/o3de/o3de/issues/13208 so that it will be done for future releases. We may want to also get it on the downloads page on the website.
4. **Feature Grid Process** Currently, updating the Feature Grid is a brute force manual process, by which the Release Manager requests the other SIGs to update the process. See all of the feature grid issues from the 22.10 release here:  https://github.com/o3de/o3de/projects/18?card_filter_query=grid  . SIG-Release  thinks this can be made easier by potentially making the feature grid updating a requirement of SIGs on a recurring basis. 
Why we are not trying to change this right now? We are asking SIG to work on roadmaps in Jan 2023, we do not want to add additional requests to SIG at this time.  
