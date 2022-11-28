## Meeting Details

- **Date/Time:** November 22nd, 2022 @ 5:00pm UTC / 10:00am PDT
- **Location:** [Discord SIG-Release Voice Room](https://discord.gg/Z2bzwCRJEz)
- **Moderator**: @tonybalandiuk
- **Note Taker**: @vincentvincent
- **Agenda**: https://github.com/o3de/sig-release/issues/96

## SIG Updates
**What happened since the last meeting?**
1. Met on 11/15 to review the Release 22.10.0 feedback and determine next steps Feedback on the O3DE Release 22.10.0 (Feedback due by 10/31) #101
2. There's an issue about codeowners maintenance for merging docs during docs stabilization Set up process for maintenance of o3de.org CODEOWNERS during stabilization/release #108 - looks like release manager(s) will be given permission to merge docs during the next release. Overall, we should probably work more closely with sig-docs-community since we share the same release process and have dependencies during release.

## Meeting Notes
1. Discuss next release date ~ Mid-April?
    1. We need to have a discussion with marketing and discuss with other SIGs before making any decision dates. It will before the GDC 2023 (February 2023) or after GDC 2023 (around May 2023).
    2. Tony to reach out to marketing team to understand their thoughts on the next release date in relation with GDC 2023.
2. @tonybalandiuk Update on Release Process Documentation.
    1. Tony to publish the draft into GitHub so others can review it this week or next week.
3. @vincent6767 - Roadmap Maintenance Roadmap Process Quick Updates.
    1. No updates. Would like to focus on the release feedback before driving this to completion.
4. Any objection to posting a "Feature list" for next release so people have a place to leave notes on features they are delivering to dev?
    For any features that SIG team contributed to dev where the SIG wants to indicate that the PR/issue warrants a release note, please add the "release-note" label. Then add a comment to the issue with the release note, like "Release Note: this is our release note for this feature. It's a super awesome feature that does this and that"
5. Simplify the release notes tracking process
    1. There is a discussion about whether RFC is mandatory whenever we submit PR. There are three work buckets in terms of this
        1. Major features - require RFC. 
        2. Minor features
        3. Bugs fixing.
    2. Danilo to post a comment about the buckets in the discussion: https://github.com/o3de/sig-release/discussions/107

## Action Items
1. Tony to reach out to marketing team to understand their thoughts on the next release date in relation with GDC 2023.
2. Tony to publish the draft into GitHub so others can review it this week or next week.
3. Danilo to post a comment about the buckets in the discussion: https://github.com/o3de/sig-release/discussions/107
