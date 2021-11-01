# API Deprecation

> Unsure about what type of deprecation you're facing? Please see this page for more information - [Deprecation Meta](DeprecationMeta.md)

> Wondering if this applies to you? This process only applies to public APIs - if you're sure consumers of your API will not be impacted, making an immediate change is okay.

## Overview

Examples of a API deprecation:

- Renaming a function
- Renaming a class/EBus
- Changing a function signature
- Removing a function
- Removing a class/EBus
- Changing the address type of an EBus
- Changing the preconditions of a function
- e.g. Function no longer handles nullptrs or parameter values must now fall within a specified range (e.g. between `0.0` and `1.0`).

## Process

### Golden Rule

> Do not make any breaking changes to an API when first deprecating it (this includes adding the `AZ_DEPRECATED` macro). The code must work exactly as before.

### Steps (Guide)

1. Identify the code to be deprecated (something resembling one of the API deprecation examples outlined in the Overview).
1. Create a new GitHub issue with the name "Deprecate <Function/Type Name>"
    1. Add the Deprecation label.
    1. In the Description, add a preliminary Release Note (what do you want to say to the customer about this change).
    1. Fill in the Release Note Required field to identify which release this deprecation will be going out in.
1. Add a `O3DE_DEPRECATION_NOTICE(<GHI Number>)` comment right above the API call.
    1. e.g.
```c++
    // O3DE_DEPRECATION_NOTICE(GHI-1234)
    AZ::Entity* CreateEditorEntity(const char* name) = 0;
```
> Aside: To make searching easier, only add API comments to the function/type declarations, not definitions.
1. Create second GHI to add `AZ_DEPRECATED` to the API.
    1. Add the Deprecation label.
    1. Link the issues together.
    1. _Note: If it isn't possible to use the `AZ_DEPRECATED` macro, create a ticket and make a note it will apply in Release + 2 (so a maximum of only two GHIs need be created in this case)_
1. _LATER_ (after the first issue is Closed, i.e. a Release has actually happened) create another GitHub issue to remove the code entirely (please see Tracking Information below for details about this).
    1. Add the Deprecation label.
    1. Link this issue to the second issue.
    1. Add the `AZ_DEPRECATED` macro to the code (leaving the `O3DE_DEPRECATION_NOTICE` comment in place to help with searching) and submit (referencing both Git Hub numbers in the CL description).
1. _MUCH LATER_ (after the second issue is Closed, i.e. the second Release has actually happened)
    1. Remove the code and create a PR
    1. Set final issue to be Closed (will be closed by release team)
    1. You're done!

### Tracking (Informational)

1. When a Release is imminent, sig-documentaion will (rip)grep the repo for all occurrences of `O3DE_DEPRECATION_NOTICE`
1. They will confirm what stage the issue is in (following the issue chain) and add the info in the Description to the Release Notes.
1. sig-documentation will then update the issue to Closed
    1. When this happens, the engineer who began the deprecation will get a notification from GitHub of the change, and at this time they know it is okay to move to the next stage (add `AZ_DEPRECATED` (part 2), delete code (part 3)).

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

It is now required to first use the comment identifier `O3DE_DEPRECATION_NOTICE`, and a second pass (corresponding to the second Git Hub issue), to add `AZ_DEPRECATED`.

`AZ_DEPRECATED` cannot be used effectively as a first step in deprecation because the warning generated will cause a compiler error for many customers building with warnings as errors.

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