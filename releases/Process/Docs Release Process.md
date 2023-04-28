# O3DE Docs Release Process

The **Open 3D Engine (O3DE) Documentation** is released in conjunction with the O3DE codebase, so that each release has a complementary set of documentation accurate to the functionality present in the release. This guide contains all of the information needed to update the O3DE Documentation for an upcoming release. It's a sub-process of the overarching [Major Release Process](./Major%20Release%20Process.md). The O3DE Documentation is maintained in the [`o3de.org`](https://github.com/o3de/o3de.org) repo, and most updates will result in pull requests (PRs).

*This document is owned by the Docs and Community SIG and maintained in sig-release repository. To make updates to this document, please reach out to the #sig-docs-community channel in the O3DE Discord and create a pull request.*

## Docs Release Process Runbook

The Docs Release Process Runbook outlines the steps that the Docs Project Manager must take for the upcoming O3DE release. It supplements the overarching [Major Release Process Runbook](./Major%20Release%20Process.md#major-release-process-runbook), which details the process across all roles of the release process. 

The schedule for the time-sensitive release process is as follows:

**Phase (1 of 4): Planning**

* **Create Stabilization Branch:** The `stabilization` branch is where documentation stabilizes for the upcoming release. It's created from `development` and merged to `main` on release day. 
* **Draft Release Notes:** After the Release Manager creates the initial feature list, the Docs Project Manager is responsible for authoring the release notes in Markdown. 

**Phase (2 of 4): Pre-Release**

* **O3DE Docs Stabilization**: The docs stabilization process involves maintenance of the the `stabilization` branch up until release day.
* **Finalize Release Notes**: The release notes must be in a PR to `stabilization`, reviewed by the Release Manager and other SIGs, and ready to merge. 
* **Feature Grid**: After all SIGs update their feature grid, finalize the feature grid in Markdown and create a PR to `stabilization`. 
* **C++ API Reference Generation**: Generate the API reference for the source code. This includes the frameworks and Gems in the `o3de` repo, as well as canonical Gems in other repos, as determined by Release SIG. 
    <!-- Follow the instructions in [C++ API Reference Generation](). -->
* **Documentation Versioning**: For documentation versioning, which refers to the management of multiple docs versions, the current (soon-to-be prior) version of the docs must be branched off of `main` and captured in its own branch. Additionally, the docs version selector in the website must be updated accordingly.
* **Version Information:** Update the website to display the correct version number for the upcoming release, and ensure that the versions for system requirements are also up-to-date. 

**Phase (3 of 4): Release Day**

Follow [Release Day](./Major%20Release%20Process.md#phase-3-of-4-release-day) instructions in the O3DE Major Release Process document.

**Phase (4 of 4): Post-Release**

Follow [Post-Release](./Major%20Release%20Process.md#phase-4-of-4-post-release) instructions in the O3DE Major Release Process document.


Additional details for these steps are described in the remainder of this document.

## O3DE Docs Stabilization 

The docs stabilization process involves preparing the `o3de.org` repository for release. During this time, we branch off of the `development` branch to create the `stabilization` branch.

The scheduling and communication of the docs stabilization process should be the same as the code stabilization process. Work with the Release Manager to coordinate this. 

✅ **Completion requirement**: (End of pre-release) The stabilization branch contains all of the changes for the upcoming release, including the release notes and feature grid. Any website bugs or broken links must be resolved.


### Git workflow

During the stabilization period, all new PRs must continue to be made to the `development` branch. The Docs Project Manager will regularly cherry-pick commits that are intended for the release from `development` to `stabilization`.

### Create a stabilization branch

**Note**: The following instructions demonstrate one way to create a branch. Additional methods are listed in [Creating a branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository#creating-a-branch) in the GitHub Docs. Whichever way you choose, make sure that you create the branch from `development`. 

To create a stabilization branch:

1. In the [branches overview](https://github.com/o3de/o3de.org/branches) section in the [`o3de.org`](https://github.com/o3de/o3de.org/) repository, click **New branch** to open the **Create a branch** dialog.

1. For **Branch name**, name the branch `stabilization/<version>`, where `<version>` is the version number of the upcoming release. That means if the upcoming release is 2305, then this branch must be named `stabilization/2305`. 

1. For **Branch source**, select `development`. 

1. Click **Create branch**. 

![Image: Create a stabilization branch](/files/releases/Process/create-stabilization.png)

### Merging the stabilization branch

At least a week before release day, create a PR from `stabilization` to `main`. Allow enough time before release day to resolve any merge conflicts or other issues. 

On release day, work with the Release Manager to release the documentation on schedule. You must merge the stabilization branch to `main` by using a merge commit - **avoid squashing or rebasing**. 


## Release Notes

✅ **Completion requirement**: (Pre-release phase) For completion, a PR must be merged into `development` and cherry-picked to `stabilization` that adds the release notes for the upcoming O3DE version. As an example, refer to this [PR](https://github.com/o3de/o3de.org/pull/2021/files) and the resulting published [release notes](https://www.o3de.org/docs/release-notes/22-10-0/).

### Draft Release Notes

During the planning phase, the Release Manager coordinates with each SIG to draft the feature list, which consists of key highlights and a more comprehensive list of changes for the upcoming release. Afterwards, the Docs Project Manager is responsible for using the feature list to prepare the release notes, which is what's published to the website. As an example, the [22.10.0 Feature List](https://github.com/o3de/sig-release/blob/b8d0e38b681a3133f3b111f839ec01d91953ded2/releases/22.10.0/22100%20feature%20list.md) eventually resulted in the [22.10.0 Release Notes](https://github.com/o3de/o3de.org/blob/b9d92bff7a56dd5fd7f5d732ee55a8935b1ca5aa/content/docs/release-notes/22-10-0/_index.md). 


1. Create a release notes Markdown file that's based on the feature list that the Release Manager provides. 

1. Create a branch from `stabilization` to add the release notes in. 

1. Add the release notes to the folder `/content/docs/release-notes/<version>`. It's also good practice to follow the same naming convention as [past release notes versions](https://github.com/o3de/o3de.org/tree/main/content/docs/release-notes).

1. Create a PR to `stabilization`. This involves manually cleaning up the release notes Markdown file, such as resolving broken links and fixing its style and formatting. As an example, refer to the published release notes of past versions, such as [22.10.0](https://www.o3de.org/docs/release-notes/22-10-0/).


**Note**: Between the planning and pre-release phases, the release notes will likely fluctuate. This is due to the code stabilization process, where bugs are addressed, features are stabilized, and known issues are found. It's critical for the Release Manager and Docs Project Manager to communicate and check in with other SIGs regularly. 


### Finalize Release Notes

The release notes must be in a PR to `development` and cherry-picked to `stabilization`. The PR requires a review and approval from the Release Manager. It's also good practice to add a docs reviewer (@sig-docs-community-reviewers) to review the release notes for grammar and style. Optionally, you can request a reviewer from each SIG for their awareness and in case any changes need to be made. This is optional as long as there are other methods for SIGs to communicate possible changes regarding release notes.  


## Feature Grid

The feature grid records the state of each feature system within O3DE for the upcoming version. The feature grid is typically published alongside the release notes. Each SIG is responsible for updating their feature grid during the pre-release phase. Then, the Docs Project Manager is responsible for finalizing the feature grid.

**Tip**: **** For a punctual and smooth release process, SIGs should update their feature grids early, leaving at least a week for the Docs Project Manager to finalize the feature grid. This also allows time for any last minute changes to the feature grid.

✅ **Completion requirement**: (Pre-release phase) For completion, a PR must be merged into `development` and cherry-picked to `stabilization` that adds all feature grids that have been updated for the upcoming O3DE version. As an example, refer to this [PR](https://github.com/o3de/o3de.org/pull/2021/files) and the resulting [published feature grid](https://www.o3de.org/docs/release-notes/archive/22-05-0/feature-state/).


### SIG Feature Grids

**Instructions for SIGs**:

1. Each SIG must use the [Feature State Form](https://o3de.github.io/community/features/form.html) to generate a JSON file that contains their updated feature grid. For more instruction, refer to [O3DE SIG Features Editing tool](https://github.com/o3de/community/tree/main/features).

    **Note**: It's not possible to save updates through the Feature State Form. Instead, a JSON file must be generated and uploaded, as explained in the next step.

1. Then, each SIG must create a PR submitting their JSON file to the `[/features/sigjson](https://github.com/o3de/community/tree/main/features/sigjson)` folder of the `o3de/community` repo. 

After the PR is merged, the updated feature grid will appear in the Feature State Form.


### Finalize Feature Grid

After SIGs have updated their feature grids, the Docs Project Manager can finalize all features grids in a Markdown file. Cleaning up the feature grid is a manual process that can require a lot of effort - ensure you have at least a week to clean and finalize. 

1. Go to the [Feature State Form](https://o3de.github.io/community/features/form.html). 

1. Click **Create Release Markdown**.

    ![Image: Generate a Markdown of the Feature Grid (1/2)](/files/releases/Process/finalize-feature-grid.png)

1. Enter the version number of the upcoming release. Click **OK**. 

    ![Image: Generate a Markdown of the Feature Grid (2/2)](/files/releases/Process/finalize-feature-grid-2.png)

1. Create a branch from `stabilization` to add the feature grid in. 

1. Add the feature grid to the folder `/content/docs/release-notes/<version>`. It's also good practice to rename the file to match [past feature grid versions](https://github.com/o3de/o3de.org/tree/main/content/docs/release-notes). 

1. Clean up the feature grid Markdown file, such as resolving broken links and fixing its style and formatting. For formatting, refer to the published feature grids of past versions, such as [22.10.0](https://github.com/o3de/o3de.org/blob/379ef5d04e418d80d96aa39ccac5bdf7bb4c3117/content/docs/release-notes/22-10-0/feature-state.md). 

1. Create a PR to `development`. The PR requires a review and approval from the Release Manager. It's also good practice to add a reviewer from each SIG for their awareness and in case any changes need to be made.


## Documentation Versioning

Documentation versioning refers to the management of multiple versions of documentation. Approaching the next O3DE release, the latest (soon-to-be prior) version of the documentation must be branched off of `main` and captured in its own branch, named after the latest O3DE version number. For example, the [O3DE 2205](https://github.com/o3de/o3de/releases/tag/2205.0) release coincides with the docs version branch [`version/2205`](https://github.com/o3de/o3de.org/tree/version/2205), which deploys to `https://version-2205--o3deorg.netlify.app/` . On release day, the documentation version for the new release will then be considered the "latest" version.

✅ **Completion requirement**: (End of pre-release phase) For completion,  a PR must be merged into `development` and cherry-picked to `stabilization` that updates the Docs Version Selector such that the upcoming version points to `o3de.org` and the prior versions point to their corresponding branch deploys.

![Image: Docs Version Selector in O3DE Docs](/files/releases/Process/docs-versioning-sample.png)


### Create a branch for the current docs version

**Note**: The following instructions demonstrate one way to create a branch. Additional methods are listed in [Creating a branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository#creating-a-branch) in the GitHub Docs. Whichever way you choose, make sure that you create the branch from `main`. 

1. In the [`o3de.org`](https://github.com/o3de/o3de.org/) repository, open the branch selector dropdown menu to create a new branch from `main`. 

1. Name the new branch `version/<version-number>`, where `version-number` is the latest O3DE version, prior to the upcoming release. That means if the upcoming release is 23.05 and the latest release is 22.10, then this branch must be named `version/2210`. 

1. Create the branch from `main`.

![Image: Create docs version branch](/files/releases/Process/create-docs-version-branch.png)


### Create a branch deploy for the current docs version

This step must be completed by someone with access to the [`o3de.org` site](https://app.netlify.com/sites/o3deorg/) in Netlify.

As defined in [Branches and deploys](https://docs.netlify.com/site-deploys/overview/#branches-and-deploys) in the Netlify Docs, a *branch deploy* is a version of the website based on a specified branch. You must create a branch deploy for the new docs version branch that you created in the previous step.

1. After logging into Netlify, go to **[Branches and deploy contexts](https://app.netlify.com/sites/o3deorg/settings/deploys#branches-and-deploy-contexts).**

    You can also navigate there from the [`o3de.org` site](https://app.netlify.com/sites/o3deorg/) in Netlify by going to **Site settings** > **Build & Deploy** > **Continuous deployment** > **Branches and deploy contexts**.

1. Click **Edit settings**.

1. Next to **Branch deploys**, under the **Let me add individual branches** option, in **Additional branches**, add the name of the new branch. Ensure that the name you enter exactly matches the actual branch name in GitHub.

    ![Image: Create a branch deploy in Netlify](/files/releases/Process/netlify-deploy-branches.png)

1. Click **Save**.

The URL of the new branch deploy will be at `<branch-name>--o3deorg.netlify.app/`. Note that a "/" in the branch name will be replaced by a "-". For example, [version-2205--o3deorg.netlify.app/](http://version-2205--o3deorg.netlify.app/). 


### Update the Docs Version Selector

1. Create a branch from `development` for creating the PR to update the Docs Version Selector. 

1. Open the `config.toml` file in the `o3de.org` repository.

1. Navigate to `[params.docs]`. Here, you will update the parameters for `versions`. 

1. In the list of `versions`, update the link for the latest version to point to the URL of the new branch deploy. For example, for `22.10` branch, the URL must be updated to `version-2210--o3deorg.netlify.app/`.
    
    Order matters, since it determines the order of the options available in the version selector dropdown. Use the following convention: [current release], [development], [previous releases in descending chronological order].

1. Create a new entry in the list for the upcoming release version that links to `https://www.o3de.org`.

1. Create a PR against `development`. 

1. After the PR is merged, cherry-pick the commit from `development` to `stabilization`, following the Git workflow.

1. On launch day, or soon after, cherry-pick the commit to all earlier branches (for example `version/2205`, `version/2210`).

**Example** - Updating the Docs Version Selector in `config.toml`

Before:

```yaml
[params.docs]
# Docs version data format: ["display name", "baseURL"]
# Note: A version that has "www.o3de.org" in its baseURL will get " (latest)" appended to its display name in the version selector.
versions = [
  ["22.10", "https://www.o3de.org"],
  ["development", "https://development--o3deorg.netlify.app"],
  ["22.05", "https://version-2205--o3deorg.netlify.app"]
]
```

After:

```yaml
[params.docs]
# Docs version data format: ["display name", "baseURL"]
# Note: A version that has "www.o3de.org" in its baseURL will get " (latest)" appended to its display name in the version selector.
versions = [
   ["23.05", "https://www.o3de.org"],
  ["development", "https://development--o3deorg.netlify.app"],
  ["22.10", "https://version-2210--o3deorg.netlify.app"],
  ["22.05", "https://version-2205--o3deorg.netlify.app"]
]
```



## Version Information

Update the website to display the correct version number for the upcoming release, and ensure that the versions for system requirements are also up-to-date. As an example, this [PR](https://github.com/o3de/o3de.org/pull/2007/files) updates version information for a past O3DE release. For all updates, create a PR to the `development` branch. 

✅ **Completion requirement**: (End of pre-release phase) For completion, a PR must be merged into `development` and cherry-picked to `stabilization` that updates all necessary version information.


### Update O3DE's Version Number

Make sure to update the O3DE version numbers in the following locations:

* For the [O3DE Download](https://www.o3de.org/download/) page:

    1. Open the following files in the `o3de.org` repo.

        * `layouts/partials/download/content-windows.html`
        * `layouts/partials/download/content-linux.html`

    1. In the `download_release` div class, replace the previous O3DE version with the new version number. 
        For example:

        ```html
        <div class="download_release">O3DE 22.10.0 Release</div>
        <p class="download_notes">Read the <a href="https://o3de.org/docs/release-notes/">Release Notes</a> to learn more about O3DE 22.10.0 Release.</p>
        ```

* For the [Installing O3DE for Linux](https://www.o3de.org/docs/welcome-guide/setup/installing-linux/) page, in the file `content/docs/welcome-guide/setup/installing-linux.md`. 


### Update System Requirement Versions

Make sure that version numbers are up-to-date in the following locations:

* For version-specific shortcodes, in the [`layouts/shortcodes/versions`](https://github.com/o3de/o3de.org/tree/main/layouts/shortcodes/versions) directory. 

    These shortcodes allow us to define version numbers in one file and reuse the shortcode throughout the documentation. Learn more about [how Hugo shortcodes are used in O3DE Documentation](https://www.o3de.org/docs/contributing/to-docs/style-guide/shortcodes/). 

* For the [System Requirements](https://www.o3de.org/docs/welcome-guide/requirements/) page, in the file `content/docs/welcome-guide/requirements.md`.

* For everything else, use a tool to search for version numbers throughout the `o3de.org` repo. You can also reach out to the #sig-platforms channel in the O3DE Discord to help identify what needs to be updated.


*As new documentation is written, there may be new file locations to update. Please update this document as needed.*
