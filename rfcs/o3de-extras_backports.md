# Release Strategy for o3de-extras

# Summary:

A release strategy is essential for maintaining the integrity and usability of software projects. The motivation behind this document is to establish a clear and effective release strategy for the `o3de-extras` repository. In particular, it addresses the need to meet the release cycle of the Open 3D Engine (O3DE) while enabling users to backport certain Gems from the newest release to older versions of O3DE. This strategy aims to ensure that users can benefit from the latest features and improvements without being forced to upgrade their entire O3DE installation.

## Current Release Process:

Currently, the `o3de-extras` repository is released together with the O3DE engine. This means that whenever a new version of O3DE is released, the `o3de-extras` repository is also updated and released. Similarly to the O3DE engine, the `o3de-extras` repository follows a branching strategy that includes a `main` branch for stable releases, a `stabilization` branch for preparing new releases, and a `development` branch for ongoing work.

The release of the `o3de-extras` repository can be summarized as follows:
1. Create a new `stabilization` branch from the `development` branch when a new O3DE release cycle begins.
2. Perform necessary updates and testing on the `stabilization` branch to ensure compatibility with the upcoming O3DE release.
3. Update version numbers in relevant `gem.json` and `template.json` files within the `o3de-extras` repository to differentiate the new release from previous ones.
4. Merge the changes into the `main` branch of the `o3de-extras` repository out of the `stabilization` branch.
5. Tag the `main` branch of the `o3de-extras` repository with the same version number as the O3DE release.
6. Generate the release packages for modified Gems and Templates and upload them to the release folder.
7. Generate the `repo.json` file that contains the metadata for the Gems and Templates included in the release.
8. Upload the `repo.json` file to the `canonical.o3de.org` repository, which is used by the O3DE Project Manager to pull the available Gems and Templates.

## Backporting Strategy:

The mechanisms implemented in the O3DE Project Manager allow users to install Gems and Templates from the `o3de-extras` repository based on the published `repo.json` file. The metadata stored in this file includes the version numbers of each Gem and Template, lists the compatible O3DE engine versions, and provides download URLs for the release packages. This means, that developers can backport Gems and Templates from the latest `o3de-extras` release to older O3DE engine versions, as long as the metadata in the `repo.json` file is correctly set.

The release strategy for backporting Gems and Templates from the `o3de-extras` repository can be summarized as follows:
1. Identify the Gems and Templates that are to be backported to older O3DE engine versions.
2. Create a new branch from the respective commit of the `main` branch of the `o3de-extras` repository, named `backports/<o3de-version>`, where `<o3de-version>` is the target O3DE engine version for the backport. Use the human-readable format for simplicity (e.g. `backports/25051` for version 25.05.1).
3. Backport the changes (use separate *Pull Requests* for each backport), update the version numbers in the relevant `gem.json` and/or `template.json` files to reflect the backported version.
4. Modify the compatibility information in the `gem.json` and/or `template.json` files to include the target O3DE engine version.
5. Test the backported Gems and Templates in the target O3DE engine version to ensure functionality and compatibility.
6. Generate the release packages for the backported Gems and Templates and upload them to the release folder.
7. Generate a new `repo.json` file that includes the backported Gems and Templates, ensuring that the metadata reflects the correct version numbers and compatibility information.
8. Upload the updated `repo.json` file to the `canonical.o3de.org` repository, ensuring that users can access the backported Gems and Templates through the O3DE Project Manager.

The backporting process is manual and requires additional effort to ensure that the backported Gems and Templates are compatible with the target O3DE engine version. It very often requires code changes to ensure compatibility, especially if there are significant differences between the O3DE engine versions. Therefore, it should be used sparingly and only for Gems and Templates that provide significant value to users of older O3DE engine versions. We do not intend to backport all Gems and Templates to all older O3DE engine versions, but rather focus on specific Gems and Templates that are in high demand or provide critical functionality.

## Problems and Considerations:

1. **Documentation**: The repository with the documentation for the O3DE follows the same release cycle as the O3DE engine. This means that there is no space for the documentation of backported Gems and Templates.
2. **Notification**: Users of the O3DE Project Manager are not notified about the availability of backported Gems and Templates.
3. **Versioning**: The versioning scheme for backported Gems and Templates needs to be clearly defined to avoid confusion. This should be a part of the versioning efforts.
