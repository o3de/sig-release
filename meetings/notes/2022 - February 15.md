## Meeting Details

- **Date/Time:** February 15, 2022 @06:00pm UTC / 10:00am PT
- **Location:** [Discord SIG-Release Voice Room](https://discord.gg/Z2bzwCRJEz)
- **Moderator:** Joe B
- **Note Taker** Halle F

The [SIG-Release Meetings](https://github.com/o3de/sig-release/tree/main/meetings) repo contains the history past calls, including a link to the agenda, recording, notes, and resources.

## SIG Updates

**What happened since the last meeting?**
- All future releases will use the yy.mm.version format
- Friendly naming convention has been de-prioritized by the marketing committee


## Meeting Agenda

**Discuss agenda and notes**

- Release Cadence still up for discussion
@Ulrick28 (Joe Bryant) to post data (QA, Docs, Website, Legal, Marketing lead times) for the next TSC meeting
Notes:
We decided with the TSC on a 6 month release cadence for now, since an every few months cadence is not possible at this time. Next major release will be late April / early May. We will re-evaluate cadence for the following release.

- @Ulrick28 restarting discussions around Long Term Support timeline
Need to know if LTS is off the table for 2022
How do we support early adopter partners and customers without an LTS? Will need an alternate plan if no LTS.
Notes:
Sig Docs Community is currently in discussion regarding how to version the docs site (for example, hosting  inflight development documentation separate from previous release documentation), and will consider LTS in their planning.
We need better version handling if we want to get to LTS. Currently, gems can't target a version of the engine.
(captured as action below) AMZN Joe B to discuss verify with TSC the assumption that gems need to be able to target a specific version of the engine.
LTS may add effort to release coordination (for example, we may need additional effort in updating the installers, etc.)

- How do we handle downloading older releases of the engine?
Still no plan at the moment
Notes:
This will require web development and infrastructure work. Documentation impacts should also be considered for major releases.
(captured as action below) AMZN Joe B to discuss infrastructure work (e.g. determining a location for storing older O3DE versions), and potential automation, with Sig Build
LF is hiring web developers

- Right now Amazon handles all of the QA resourcing. Future releases will need assistance from outside of Amazon, particularly as O3DE grows. How will we handle QA for future releases?
Notes: 
Joe talked to Sig Build, and they agreed something needs to be done.
We need to solve this, at least partially, for our next release. Currently, testing is performed by Amazon only.
Joe is requesting LF contract QA to assist, as it seems to be common in OS for the org to partner in QA support.

- We currently do not have any available Web Developers to update the website (o3de.org and o3debinaries.org), who is responsible for staffing Web Developers? What is the plan?
Need verification that the Linux Foundation is indeed hiring Web Developers.
Notes:
LF is hiring developers. Per Royal at the last TSC, the goal is to hire them within the month.

- RTE Point Release Retrospective (RTE Point Release Retrospective)
Notes:
Q1: Were the mechanisms and tools we implemented to track the release (for example, the Point Release Project Board, and the Exception Request Project Board) sufficient in keeping everyone informed?
A1: Both tools were useful for tracking and keeping everyone informed. We should evangelize the Exception Request Project Board more. 
(captured as action below) AMZN Halle F will create a GHI issue to finalize and evangelize the Exception Request process and project board.
Q2: Were we transparent enough in terms of the work required and the status of execution?
A2: We may want to make it more obvious what documentation changes are included in a release. This is also a way to recognize the doc work.
(captured as action below) AMZN Stephen T to get feedback from SIG Docs Community regarding if we should make documentation changes more apparent in release notes.
Q3: Do we feel the point release process is clear enough to support non-Amazon contributors in running this process? If not, by what means do we need to bolster the process?
A3: Although we have a good start based on the current mechanisms and tools, the most difficult part will be for for Amazonians to break their reliance on internal processes and tools. This is surmountable, and we can use Finchy to drive perspective (since she has recently joined Amazon and carries with her the contributor perspective)
(captured as action below) AMZN Halle F will send JT the project runbook





## Outcomes from Discussion topics

**Discuss outcomes from agenda**

## Action Items

AMZN Joe B to discuss verify with TSC the assumption that gems need to be able to target a specific version of the engine.
AMZN Joe B to discuss infrastructure work (e.g. determining a location for storing older O3DE versions) with Sig Build
AMZN Halle F will create a GHI issue to finalize and evangelize the Exception Request process and project board.
AMZN Stephen T to get feedback from SIG Docs Community regarding if we should make documentation changes more apparent in release notes.
AMZN Halle F will send JT the project runbook

## Open Discussion Items
