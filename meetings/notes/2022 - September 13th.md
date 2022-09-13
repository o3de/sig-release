## Meeting Details

- **Date/Time:** September 13th, 2022 @ 5:00pm UTC / 10:00am PDT
- **Location:** [Discord SIG-Release Voice Room](https://discord.gg/Z2bzwCRJEz)
- **Moderator**: @tonybalandiuk
- **Note Taker**: @vincentvincent
- **Agenda**: https://github.com/o3de/sig-release/issues/93

## SIG Updates
**What happened since the last meeting?**

### 22.10.0 Release
* Features list are being updated https://github.com/o3de/sig-release/blob/main/releases/22.10.0/22100%20feature%20list.md

* Few exception requests got approved.
    * https://github.com/o3de/o3de/pull/11750
    * https://github.com/o3de/o3de/pull/11764

* Worked on documenting the release and stabilization process.

### Process to maintain roadmap
* There are feedback around the [RFC](https://github.com/o3de/sig-release/issues/79). Updated with the RFC and open discussion on how to figure out motivation for the maintainers to keep the roadmap updated.

## Meeting Notes
1. Release Update details O3DE Release 22.10.0 Key Information #64
    * We have low visibility around resolved bugs before and during the stablization branch. This makes it hard to see how many bugs have been resolved and for the release notes
    * Features grid should also updated. Vincent will take on that one.

2. Update on Release Process Documentation.
    * It's being workend on. Tony will complete this after the release 22.10.0. 

3. Update on Proposed RFC Suggestion =Keeping O3DE Roadmap Up-to-Date Process= #79
    * Yuyi and Tony agree to start with each roadmap will have their own roadmap to maintain instaed of single roadmap.
    * Yuyi agrees to the roadmap updates sharing as part of the TSC meeting. She just needs SIG release to her what she and her team needs to do and what information does SIG release needs.

4. We need to identify the overall themes and top 3-4 noteworthy features/capabilities within this next release feature list at https://github.com/o3de/sig-release/blob/main/releases/22.10.0/22100%20feature%20list.md
    * Few themes suggested by the group
        * Easier to onboard others and collaboration
            * Introduce the remote templates and projects.
        * Multiplayer is easier to setup
        * Character development
            * O3DE Motion Matching Gem is ready for experimental use.
        * Artist workflow
            * Asset Processor now supports sharing pre-processed assets via network shared drives
        * Usability improvements

5. How to streamline the release process on the website. Note that the community outreach sig is planning a website redesign but it's not aligned with the Oct release.
    * The marketing team doesn't aware of the release in October 13th, 2022
    * The group agrees this is concerning issue and SIG release will take a look at this procees and see what can be improved.

## Action Items
* @tonybalandiuk to identify bugs created since August 29th
* @tonybalandiuk to create a bug report template during the stablization process.
* @vincentvincent to drive people to updates the features grid and write down the process as part of the release documenation.
* @tonybalandiuk to complete the release process documentation after the 22.10.0 release.
* @vincentvincent to update the [RFC](https://github.com/o3de/sig-release/issues/79) based on the feedback. 
* @tonybalandiuk to let everyone knows how to contribute the theme around the 22.10.0 release.
* @tonybalandiuk to follow up with the marketing team about the marketing needs for 22.10.0 release and have a discussion on how to improve the current process.
