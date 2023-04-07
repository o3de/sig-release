## Meeting Details

- **Date/Time:** March 28th, 2023 @ 5:00pm UTC / 10:00am PDT
- **Location:** [Discord SIG-Release Voice Room](https://discord.gg/Z2bzwCRJEz)
- **Moderator**: @tonybalandiuk
- **Note Taker**: @vincentvincent
- **Agenda**: https://github.com/o3de/sig-release/issues/151

## SIG Updates
**What happened since the last meeting?**
Roadmap Progress Updates: https://github.com/o3de/sig-release/issues/79
- https://github.com/o3de/sig-release/issues/137
  - SIG Docs community creates PR to mention roadmap in the main websites and the docs website: https://discord.com/channels/805939474655346758/816043864858951710/1087848543483605042
- https://github.com/o3de/sig-release/issues/146
   - Proposed to TSC. Waiting for their response.

Release updates: https://github.com/o3de/sig-release/issues/133
- A stabilization branch was created: https://github.com/o3de/o3de/tree/stabilization/2305
- The first exception was approved: https://github.com/o3de/o3de/pull/15189#issuecomment-1479893413

## Meeting Notes
1. @tonybalandiuk 23.05 RM and release updates (including the feature list): https://github.com/o3de/sig-release/issues/133
* Tony will post the feature list soon so everyone can contribute to it.
   
2. @vincent6767 Roadmap Progress Updates: https://github.com/o3de/sig-release/issues/79
* Updates posted above in the section SIG Updates.
   
3. @chanmosq  https://github.com/o3de/sig-release/issues/109 updates.
* No further action item required. Issue will be closed.
   
4. @AMZN-daimini https://github.com/o3de/sig-release/issues/135 updates. 
* No updates.
   
5. Do we proceed releasing O3DE extras as part of the 23.05 release?
* SIG Release Concerns
  * o3de-extras contains gems from external 3rd parties and we cannot guarantee that any of these will be compatible with the release. 
  * we have no guarantee that the repository is being tested/exercised during release stabilization so we may not discover bugs that may exist in the repo - this introduces risk into the release, affect the trust, user experience and overhead communication in the release notes.
* Brian Colin and geds-dm suggest to we still release the O3DE-extras as part of the next release with an exception. We will only to release the gems that are ready. We can achieve that by removing gems we haven't verified working from stabilization branch X days before the release.
* JT suggests having a task force to identify which gems in the o3de-extras part of the release and make sure those are ready for release.
* No decision is made during this call. @tony and @vincent will continue the discussion in the #sig-release channel.

## Action Items
1. @tony to post the feature list soon so everyone can contribute to it.
2. @tony and @vincent to continue the o3de-extras discussion in the #sig-release channel and tagging relevant stakeholder.
