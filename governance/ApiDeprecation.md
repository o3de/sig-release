# API Deprecation

## Notice

> Wondering if this applies to you? This process only applies to __public__ APIs. If you're sure consumers of your API will not be impacted, making an immediate change is okay.

## Info

> Unsure about what type of deprecation you're facing? Please see this page for more information - [Deprecation Meta](DeprecationMeta.md)

## Overview

Examples of a API deprecation:

- Renaming a function
- Renaming a class/EBus
- Changing a function signature
- Removing a function
- Removing a class/EBus
- Changing the address type of an EBus
- Changing the preconditions of a function
  - e.g. Function no longer handles `nullptr`s or parameter values must now fall within a specified range (e.g. between `0.0` and `1.0`).

## Process

### Golden Rule

> Do not make any breaking changes to an API when first deprecating it (this includes adding the `AZ_DEPRECATED` macro). The code must work exactly as before.

### Steps (Guide)

1. Identify the code to be deprecated (something resembling one of the API deprecation examples outlined in the Overview).
    1. _Note: It's fine to group several related changes into a single deprecation_.
1. Create a new GitHub issue using the Deprecation issue template (this will come with all the required labels/milestones).
    1. In the description, add a preliminary Release Note (what do you want to say to the customer about this change).
1. Add an `O3DE_DEPRECATION_NOTICE(<GHI Number>)` comment right above the API call(s). For example:

    ```c++
        // O3DE_DEPRECATION_NOTICE(GHI-1234)
        AZ::Entity  CreateEditorEntity(const char* name) = 0;
    ```

    > Aside: To make searching easier, only add API comments to the function/type declarations, not definitions.
1. The Deprecation template comes with with three tasks:
    1. Add deprecation notice
    1. Add deprecation warning
        1. _Note: This will vary depending on the language. C++ uses the `AZ_DEPRECATED` macro, Python can use [DeprecationWarning](https://docs.python.org/3/library/exceptions.html#DeprecationWarning). Please ask in the relevant sigs for more detail if required._
    1. Remove deprecated code
        1. _Note: If it isn't possible to perform task 2 (e.g. the language/environment does not support a deprecation warning), indicate it is blocked until another release has occurred._
1. Create a PR with the deprecation notice outlined in __step 3__ (task 1) and add a reference to it on the deprecation GitHub issue.
1. _LATER_ (after the release has actually happened). Create another PR to add the deprecation warning (reference this in the description next to task 2).
    1. E.g. If using C++, add the `AZ_DEPRECATED` macro to the code (leaving the `O3DE_DEPRECATION_NOTICE` comment in place to help with searching) and merge.
1. _MUCH LATER_ (after the next release has happened)
    1. Remove the code and create a PR. Reference this in the description next to task 3.
    1. Close the issue.
    1. You're done!

### Tracking (Informational)

1. When a Release is imminent, sig-documentaion will (rip)grep the repo for all occurrences of `O3DE_DEPRECATION_NOTICE`.
    1. They may also use GitHub directly to search for all issues with the `kind/deprecation` label.
1. They will confirm what stage the issue is in (by reviewing the task list) and add the information in the description to the Release Notes.
1. At this stage, the engineer who began the deprecation will be notified, and at this time they know it is okay to move to the next stage (add `AZ_DEPRECATED` (task 2), delete code (task 3)).

### Find all O3DE_DEPRECATION_NOTICE tags

```bash
# prerequisites
# ripgrep - https://github.com/BurntSushi/ripgrep/releases
# cmder - https://cmder.net/

rg O3DE_DEPRECATION_NOTICE\(GHI\-([0-9]+)\) --replace https://github.com/o3de/o3de/issues/$1 --iglob *.{h,hpp,c,cpp,inl,hxx} -o -I | sort | uniq > deprecations.txt

# this will generate a list of Git Hub issue numbers to be updated when a Release is imminent.
```

### Advice

Use of the `AZ_DEPRECATED` macro is now not allowed when first deprecating an API.

It is now required to first use the comment identifier `O3DE_DEPRECATION_NOTICE`, and a second pass (corresponding to the second task on the GitHub issue), to add `AZ_DEPRECATED`.

`AZ_DEPRECATED` cannot be used effectively as a first step in deprecation because the warning generated will cause a compile error for many customers building with warnings as errors.

The macro is useful for providing more information about how to update a particular call if it is being replaced.

### FAQ

#### Introducing alternative calls

When first deprecating a function, it is advisable to not fix all call sites using the old version of the API. It may be wise to keep both variations active during the first stage of deprecation to ensure both calls do what you expect (e.g. Have the old call delegate to the new API and keep using that version for the first release, before the `AZ_DEPRECATED` macro is added). Depending on the situation it may be advisable to add a unit test to verify the behaviour of both calls. This helps avoid accidental, silent failures earlier.

#### Deprecating EBus Functions

When marking an EBus interface function `AZ_DEPRECATED`, any class that derives from that interface will generate `C4996 deprecation warnings`. This is caused by the `EBus::Handler` (the type that is actually inherited from) calling those functions internally in the EBus template code.

To work around this, you need to wrap any class implementing that interface in

```c++
AZ_PUSH_DISABLE_WARNING(4996, "-Wdeprecated-declarations")
AZ_POP_DISABLE_WARNING
```

```c++
class YourRequests
{
    // ...
    AZ_DEPRECATED(virtual void OldFunction() = 0, "OldFunction is being replaced by NewFunction.");
};

using YourRequestBus = AZ::EBus<YourRequests>;

AZ_PUSH_DISABLE_WARNING(4996, "-Wdeprecated-declarations")
class YourClass
    : public YourRequestBus::Handler
{
    // ...
    void OldFunction() override;
};
AZ_POP_DISABLE_WARNING
```
