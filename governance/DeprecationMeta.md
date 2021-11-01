# Deprecation Meta

# Overview

This document contains high-level information about O3DE's approach to deprecation.

It details language and terms used when categorizing types of deprecation.

## Philosophy

When modifying existing code that external customers rely on we should strive wherever possible to not break them when making changes.

If code is to be changed or removed, we should let customers know ahead of time with a reasonable notice period (approximately 2 releases (2-3 months))

## Product Deprecation vs API Deprecation

We define *Product* deprecation as deprecating (and then replacing or removing) a system or feature (usually user facing).

We define *API* deprecation as a change to a public API which would cause customer code to no longer compile or behave unexpectedly. Put another way, *API* deprecation is a change to an API which requires customer action should the deprecated code be removed.

If your deprecation need fits the description of Product - please consult these documents for the process to follow:

[Product Deprecation](ProductDeprecation.md)

If your deprecation aligns more closes with an API deprecation, please consult this document:

[API Deprecation](ApiDeprecation.md)