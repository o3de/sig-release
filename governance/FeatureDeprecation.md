# Feature Deprecation

# Overview

This document aims to describe how to handle system/feature level deprecations that will impact customers.

## Steps

When looking to deprecate a feature from O3DE, please follow the run book below:

1. Start the sig notification process ideally three releases prior to final deprecation:
    1. Contact sig-documentation to ensure they are able to make any required changes.
    1. Contact sig-release to let them know of the planned deprecation.
        1. GitHub issue should cover:
            - What is being deprecated
            - Why it's being deprecated. 
            - Target deprecation date.
            - How does this impact customers? 
            - Detail what tech will be replacing the feature and whether the new tech will have feature parity. 
            - Who can I contact if I have questions, concerns or general feedback.
    1. If there are no concerns from sig-release and the relevant sig the feature applies to:
        - Communicate to the sig that the feature is on the path to deprecation (Impactful Change notification on Discord).
        - Update the status of the deprecation plan in the relevant sig meetings.
    1. Make the replacement available (that is feature competitive with the original feature).
        - See how many customers plan to stay with the old version.
        - Deprecate (remove) the older feature, usually within 90 days.
