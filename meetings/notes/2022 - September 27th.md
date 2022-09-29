## Meeting Details

- **Date/Time:** September 27th, 2022 @ 5:00pm UTC / 10:00am PDT
- **Location:** [Discord SIG-Release Voice Room](https://discord.gg/Z2bzwCRJEz)
- **Moderator**: @tonybalandiuk
- **Note Taker**: @vincentvincent
- **Agenda**: https://github.com/o3de/sig-release/issues/96

## SIG Updates
**What happened since the last meeting?**

### 22.10.0 Release
* On 9/23 SIG-Release decided to update the release schedule to push code freeze from 9/27 to 9/30. This allows contributes to submit bug fixes through 9/30 without having to use the exception process.

## Meeting Notes
1. Release Update details O3DE Release 22.10.0 Key Information
    1. Royal is concerns about the release stabilization due to O3DE Con on October 17th. Proposing to release the installer with known issues and then use point updates strategy.
2. Feature Grid Update
    1. 1 completed, and 7 are in progress. You can see the status in [this](https://github.com/o3de/o3de/projects/18) board.
3. Update on Release Process Documentation.
    
    No updates.
3. Update on Roadmap Proposed RFC Suggestion =Keeping O3DE Roadmap Up-to-Date Process= #79
    1. Not yet updated. Will update the RFC with Release manager use case and SIG UI/UX roadmap as a reference.

4. from @stramer- I noticed that you don't have a nomination for reviewer/maintainer template in issues reviewer/maintainer template
    1. The maintainer doesn't know which members to ask for a review in the exception process.
    2. Create the discussion about who has permission and review.
    3. Owner: Danilo.

5. Vincent - propose for "fast track" exceptions. A fast track is a for an exception request with 0 code change e.g an image swap
    1. Depends on the image and whether it will affect the codebase.
    2. Tony proposes the guideline instead of someone reviewing every exception. We want to streamline the process.
        1. Add the blast radius of the change.
        2. Reviewer and maintainer will review the
        3. Here is what you need to do to create an exception request guideline. Owner: Tony.
    3. Danilo proposes to review the blast radius to decide whether we need an exception or not.
        1. Danilo brings up a point that people need to be clear about the maintainer role. Owner: Danilo.
6. @Ulrick28 asked whether we should change this meeting to 30 mins
    1. We will do the parking lot technique, where we will focus on the agenda for the 30 minutes and then follow up meeting on the next 30 minutes.

## Action Items
1. @vincentvincent to update the Roadmap RFC by next week.
2. @tonybalandiuk to create a guideline instead of someone reviewing every exception.
3. @danilo to create the discussion about who has permission and review.
4. @danilo to post maintainer role responsibilities.
