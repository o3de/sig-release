  
# O3DE Major Release Process
V1.3 Updated May, 2024. 
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
 4.  **Release Manager** creates the Key Information 
		* Create a github Issue similar to https://github.com/o3de/sig-release/issues/64. 
		* Send a communication similar to the following:

Description|Type|Send To|Example Message
--|--|--|--
Initial post about the key information in the upcoming release |Discord| #sig-all, #marketing-committee ,#sig-release |The planned date for our next release is May 3, 2023 Stabilization to begin Mar 15, 2023. The release schedule and information are here [https://github.com/o3de/sig-release/issues/133](https://github.com/o3de/sig-release/issues/133 "https://github.com/o3de/sig-release/issues/133") If you have any concerns with the schedule please comment under the issue. Thanks.

5. **Release Manager** should maintain the Key Information throughout the release. Key Information should be updated as more information about the release is known, or when details change. If Key information changes then
	*	update the "Key Information" github issue.
	*	 Send a communication similar to the following:

Description|Type|Send To|Example Message
--|--|--|--
Update of the key information in an upcoming release|Discord|#sig-all, #marketing-committee ,#sig-release|The key information for our next release has changed. Please see the latest details at [https://github.com/o3de/sig-release/issues/133](https://github.com/o3de/sig-release/issues/133 "https://github.com/o3de/sig-release/issues/133") If you have any concerns with the schedule please comment under the issue. Thanks.

 6. **Release Manager** creates a project board for the release with all tasks in the O3DE Repository. Refer to the project board and tasks from the previous release, then manually create tasks in your new release  1-by-1 based on the previous release's tasks. Previous project boards are located at https://github.com/o3de/o3de/projects?type=classic
 7. **Release Manager** ensures all Planning tasks on the project board are completed, either by completing them or assigning them to others.
 8. **Release Manager**  has a Planning task on the project board to identify all Release Roles. These release roles should be updated in the Key Information once known.

### 1.2 Create the Feature List 
The Feature List usually begins 6-8 weeks prior to release and ends 1-2 weeks after stabilization begins.  See [Terminology](#terminology) for description of the Feature List.
Entry Criteria: A Pre Release task exists to generate the Feature List, similar to https://github.com/o3de/o3de/issues/11100

Note: This is a highly manual process. There is an opportunity to improve. See Appendix A.

1. Follow the steps outlined for the pre-release task. In the pre-release task step (1) Create a feature list file at [https://github.com/o3de/sig-release/tree/main/releases](https://github.com/o3de/sig-release/tree/main/releases)  under the appropriate release, for example  [22100 feature list.md](https://github.com/o3de/sig-release/blob/main/releases/22.10.0/22100%20feature%20list.md "22100 feature list.md") . The initial feature list file that you create should have a heading for each SIG.  
For pre-release step (4) "Review closed issues to see if anything else should be added."  
	* You will need to Refer to all O3DE Roadmaps to understand which features have been delivered to the codebase.
	  * SIG Roadmaps, for example [the O3DE UI/UX Roadmap.](https://github.com/orgs/o3de/projects/9)
	  * Other roadmaps,  including those published by foundation members. For example [the Roadmap of AWS Contributions to O3DE.](https://github.com/orgs/o3de/projects/11)
	* For each roadmap item delivered to the o3de codebase since the last release, enter a summary into the feature list.
	* If you need assistance, comment under the GHI or reach out to the SIG owning that area of the engine
	* (Optional) Review the submitted pull requests or closed Github Issues. The reason to do this would be to discover any features that were not on the Roadmap, potentially features that were accidentally missed. 
2. Once you have created the feature list, send a communication similar to the following:

Description|Type|Send To|Example Message
--|--|--|--
Notify the O3DE community that the feature list is posted. Request community to update. |Discord|#sig-all, #sig-release|Attention SIGs - the 23.05.0 Feature list is posted at https://github.com/o3de/sig-release/blob/main/releases/23.05.0/23050%20feature%20list.md If you have any features for the upcoming release that are not reflected here, or you want to make some other change, please author a pull request (PR) against this file. Thanks! Tips for your PRs: 1) Add a description of the feature that was delivered. 2) Add links to the PR. 3) Add any additional notes, details, links to videos, etc. that may that will help the community understand the feature.


3. Allow Pull Requests to the Feature List until 1-2 weeks after Stabilization begins (agree on a date with the Documentation Project Manager). 
4. Send a communication similar to the following. Notify the marketing committee once the feature list is mostly (80%) done (you have some input from each SIG, and they indicate that they "most" of their work submitted).  They may ask for a summary of the release and key features. It is up to the release manager to provide this guidance to the marketing committee. The release manager may discuss with the Release SIG or any other SIG to figure this out.

Description|Type|Send To|Example Message
--|--|--|--
Notify the marketing committee that the feature list is posted.|Discord|#marketing-committee|Hi. The 23.05.0 Feature list is posted at https://github.com/o3de/sig-release/blob/main/releases/23.05.0/23050%20feature%20list.md Please review the feature list to get a sense of what's in the release and follow along as this file is updated. This list will eventually become the release notes. 

5. Once you reach the date to stop accepting PRs to the Feature list. 
    * From this point forward, any changes needed to the release documentation should be done by coordinating with the Documentation Project Manager.
    * Send a communication the Documentation Project Manager to take the feature list and begin the Release Notes similar to the following:

Description|Type|Send To|Example Message
--|--|--|--
Notify the documentation PM that you are handing off the feature list to them.|Discord|#sig-docs-community|Hi sig-docs-community! The 23.05.0 Feature list is done https://github.com/o3de/sig-release/blob/main/releases/23.05.0/23050%20feature%20list.md. Please use this feature list to begin work on the release notes. Let me know if you need anything else. Thanks!


### 1.3 More about how Milestones are used
For each release, Github milestones are used to track bugs found in the stabilization branches of each repo involved in the release. For example, for the 22.10.0 release, the [Release/2210 milestone](https://github.com/o3de/o3de/milestone/11) captures all of the bugs found during release stabilization of the O3DE repo.

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
 - **Release Manager** At least 1 week before stabilization, send a communication similar to the following. (Example: https://discord.com/channels/805939474655346758/816043864858951710/1011404890364444712 )

Description|Type|Send To|Example Message
--|--|--|--
Notify the documentation PM that you are handing off the feature list to them.|Discord|#sig-all , #sig-release |Hi sig-docs-community! Just a friendly reminder from that in preparation for the O3DE 22.10.0 Release, the O3DE Stabilization branch will be created next Monday, 8/29, at approximately 10am pacific. Beginning 8/29, bugs may be fixed in the stabilization branch without any exception. New features that you wish to submit into stabilization will require an exception. The exception process can be found at https://github.com/o3de/o3de/projects?type=classic,  in the description for project "stabilization/2210 - Exception Requests". More information about the upcoming release can be found at https://github.com/o3de/sig-release/issues/64 .

 - **Release Manager** When the stabilization branch is created, send a communication similar to the following. Note that this is listed as a step outlined in the stabilization process, but listing it again here (Example: https://discord.com/channels/805939474655346758/805939474655346761/1087495324228124762)

Description|Type|Send To|Example Message
--|--|--|--
Notify the O3DE community of Stabilization start|Discord|#sig-all , #sig-release|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update 5/03. As part of preparing for the upcoming O3DE 23.05.0 Release, on Wednesday 5/03 the branch stabilization/2305 was created in each of the following repositories. We are now in the "release stabilization" phase. Repositories affected: - o3de, - o3de-extras, - o3de-netsoaktest, - o3de-extras, - o3de.org.  Please test the code in these stabilization branches. Test the engine and test any features you added to help improve the quality of the release. When reporting a bugs you find make sure to mention that the bug is present in the stabilization branch.  * Attention SIGs - for anyone triaging GitHub issues  - (1) Please pay close attention to your triage issue queues. You may need to increase your triage frequency while we stabilize the release. (2) If you determine that an issue should be fixed in Stabilization for the 23.05.0 release , please add the issue to the "Release/2305 Stabilization" milestone https://github.com/o3de/o3de/milestone/13. This helps us keep track of all of the work coming into the stabilization branch. If you see a PR come through that is not tied to an issue, please add the PR to the milestone. * As with previous releases, we will use an Exception Project board for code coming into the stabilization branch that requires additional review.  The project here https://github.com/orgs/o3de/projects/49/ . Instructions for using the board can be found by clicking that link, then viewing the readme. Here are the basic guidelines for when to use this Exception Project Board For Bugs: This exception process is only needed for bugs fixed in stabilization per the following schedule: 3/15 through 4/11: Bugs do not require exception. 4/12 through 4/18: Major bugs or below require an exception. Blockers and Criticals can be submitted to stabilization without exception 4/19 through 4/26 : All bug fixes require an exception. For Features: Exception are required for any NEW FEATURES that anyone wants to submit to the stabilization/2305 branch. * If you submit any code to the stabilization branch you DO NOT need to also submit it to the development branch. We have volunteers who will bring these bug fixes to the development branch on a regular basis.* More information about the timeline of upcoming release can be found at https://github.com/o3de/sig-release/issues/133


 - **Release Manager** As you move through stabilization, communicate with the community, informing them of each code freeze per the dates noted in the Key Information.

Description|Type|Send To|Example Message
--|--|--|--
Notify the O3DE community of Code freeze on Major bugs|Discord|#sig-all , #sig-release|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. Beginning Wednesday April 12 at 5pm Pacific time, there is a code freeze on Major bugs and below in the Stabilization branches. Beginning this date, only Blocker and Critical bugs are allowed without the exception process. Major bugs or below requires an exception. If you have an exception in-progress, please continue to get approvals and try to get it merged ASAP. If you have a special circumstance that requires additional time, please communicate with the appropriate SIG and SIG-Release.
Notify the O3DE community of Code freeze on Critical bugs|Discord|#sig-all , #sig-release|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. Beginning Friday April 21 at 5pm Pacific time, only Blocker bugs are allowed via the exception process. No other bug fixes allowed. If you have an exception in-progress, please continue to get approvals and try to get it merged ASAP. If you have a special circumstance that requires additional time, please communicate with the appropriate SIG and SIG-Release.


 -  **Release Manager** communicate regularly with each SIG in Discord to ensure they are aware of the outstanding bugs in the Stabilization branch (the bugs can be found in the Github milestone). 

Description|Type|Send To|Example Message
--|--|--|--
Notify the O3DE SIG of outstanding bugs|Discord|#sig-all and/or specific SIG|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. As we progress through release stabilization, please continue to triage and fix any bugs that are being reported. Current bugs are being reported here (link to release milestone)

 - **Release Manager  - What to do when there are date changes.** As you move through stabilization, if there are any date changes, discuss them with key stakeholders as needed. If you update a date, make sure you update the Key Information and communicate with the community. Here are some example messages for notifying the community.

If this date changes|Notification Type|Send To notify|Example Message
--|--|--|--
Initial stabilization period (also impacts Code Freeze on Major bugs and below)|Discord|#sig-all , #sig-release, @Documentation Project Manager|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. (provide some reason). The Stabilization period will now end on mm/dd. Beginning mm/dd+1 we will begin our code freeze on major bugs and below and only Blocker and Critical bugs are permitted to be fixed in the Stabilization branch without the exception process. Major bugs or below require an exception. If you have a special circumstance that requires additional time, please communicate with the appropriate SIG and SIG-Release.
Code Freeze on Critical Bugs and below|Discord|#sig-all , #sig-release, @Documentation Project Manager |O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. (provide some reason) The code freeze on critical bugs will now begin Friday April 21 at 5pm Pacific time. After that time, only Blocker bugs are permitted to be fixed in the Stabilization branch without the exception process. No other bug fixes allowed. If you have a special circumstance that requires additional time, please communicate with the appropriate SIG and SIG-Release.
QA Final Pass Date|Discord|#sig-all , #sig-release, @Documentation Project Manager|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. (provide some reason) Beginning Friday April 21 at 5pm Pacific time, the O3DE stabilization code will be considered completely frozen. We are now focusing on our final QA pass. Blocker bugs are still permitted to be fixed via the exception process, with risk of delaying the release. If you have a special circumstance that requires additional time, please communicate with the appropriate SIG and SIG-Release.
Release Date|Discord|#sig-all , #sig-release, #marketing-committee, @Documentation Project Manager,@everyone involved in the release call|O3DE 2305 Release Messaging O3DE 23.05.0 Release Update mm/dd. After discussing with (mention who you discussed with) , we have decided to move the release date because (enter you reason here). The new release date is mm/dd. 

 -  **Release Manager** (Optional) post regularly in #sig-all and #sig-release with statistics about the progress toward stabilizing the release. These communications  should include Total number of bugs found, Bug Fixed so Far, Bug remaining.
 - **Release Manager** communicate regularly via Discord and Github with the Documentation Program Manager to ensure that the release notes are kept up to date. This is important because during stabilization there will be bugs that do not get fixed and in some cases these bugs will need to be documented as known issues. 


### 2.2 Steps
 1. **Release Manager** is responsible for ensuring all Github issues in the "Pre Release" phase of the release project board are completed. 
	 -  Prioritize the [Feature Grid Process](#feature-grid-process)  and make sure you reach out to SIGs ASAP about updating their feature Grids.
 2.  **Release Manager** is responsible for overall maintenance and accuracy of the project board.
 3. **Release Manager** is responsible for all tasks assigned to them  identified in the [Stabilization Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Stabilization%20Process.md), which includes periodic community duties. For example, communicating to the community via Discord #sig-all, to inform the community that stabilization phase has begun.
 4. On the day we end stabilization (according to planned date in the Key Information) it is up to the **Release Manager** to make a determination on whether the stabilization branch is stable enough to be releases.  A release is considered stable when (1) there are no more blocker or critical bugs in the Stabilization branch (2)  and there is agreement from the parties involved in the release.
 5. Per the [Stabilization Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Stabilization%20Process.md), as of Release 22.10.0, stabilization takes approximately 5 weeks from beginning stabilization to declaring the stabilization branch as "stable". Then the stabilization branch is merged back to O3DE/main to create the release. After the release is published and all of the code has been merged back to development, the stabilization branch is deleted. During the Stabilization Phase the development branch is used in the same way that it is always used – code submissions to the development branch are not restricted in any way.

### 2.3 Stabilization Process
[Stabilization Process](https://github.com/o3de/sig-release/blob/main/releases/Process/Stabilization%20Process.md)

### 2.4 Feature Grid Process
During this phase of release, it is up to the Release Manager to work with SIGs to get them to update the Feature Grid. The Documentation Project Manager is responsible for publishing the Feature Grid to the O3DE website. For more information refer to the [Feature Grid](./Docs%20Release%20Process.md#feature-grid) section in the Docs Release Process. 

Currently, updating the Feature Grid is a brute force manual process, by which the Release Manager requests the other SIGs to update the process. See all of the feature grid issues from the 22.10 release here:  https://github.com/o3de/o3de/projects/18?card_filter_query=grid  

### 2.5 Documentation Release Process
The Documentation Project Manager is responsible for the following items:
* **O3DE Docs Stabilization**
* **Release Notes**
* **Feature Grid**
* **C++ API Reference Generation**
* **Documentation Versioning**
* **Version Information**
Each of these tasks are further explained in the [Docs Release Process](./Docs%20Release%20Process.md).

The **Release Manager** is responsible for reviewing the release notes once available. This review should happen prior to release. This corresponds to a task in the release project board.  

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

Description|Type|Send To|Example Message
--|--|--|--
Notify the O3DE Marketing that release is available|Discord|#marketing-committee|O3DE 2305 Release Messaging O3DE 23.05.0 The release is now available to download and it is ok to proceed with any marketing activities.

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
