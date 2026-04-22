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

* **Resync development and main branches**: After a release, the development branch should be in sync with main again, in addition to in-development changes that were not yet released. 
* Follow [Post-Release](./Major%20Release%20Process.md#phase-4-of-4-post-release) instructions in the O3DE Major Release Process document.


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

**Tip**: For a punctual and smooth release process, SIGs should update their feature grids early, leaving at least a week for the Docs Project Manager to finalize the feature grid. This also allows time for any last minute changes to the feature grid.

✅ **Completion requirement**: (Pre-release phase) For completion, a PR must be merged into `development` and cherry-picked to `stabilization` that adds all feature grids, regardless of whether it's been updated or not. As an example, refer to this [PR](https://github.com/o3de/o3de.org/pull/2021/files) and the resulting [published feature grid](https://www.o3de.org/docs/release-notes/archive/22-05-0/feature-state/).


### SIG Feature Grids

For accurate reporting of O3DE features, we highly suggest that all SIGs update their feature grids.

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


## Resync development and main branches 

After a release, the development branch should be in sync with main again, in addition to in-development changes that were not yet released.

### Example: O3DE 23.05 Post-Release

The remainder of this section uses O3DE 23.05 as an example. See PR: https://github.com/o3de/o3de.org/pull/2411

### Plan

* Merge development into main. Main branch should have all the same changes as development (and additional changes that were only pushed to main recently). 
* Reset development branch to main, so development will be at the same point as main again. 
* There’s multiple Git merge strategies, namely *fast-forward* and *three-way* (see [Stack](https://stackoverflow.com/questions/28407020/keep-commits-history-after-a-git-merge))
    * A fast-forward merge is ideal because it keeps the history linear (e.g. if merging dev to main, the individual commits in dev are copy individually to main.) This is not possible most of the time because commits go into main and dev simultaneously, so three-way merge occurs instead. 
    * A three-way merge combines all of the commits into one “merge commit”. (e.g. individual commits in dev are combined into one commit that applies to main).
    * For O3DE Docs, I want to take the individual commits from development that main will accept. It’s not possible to merge fast-forward only. So, I can cherry-pick some commits, which `git log main..development` identifies.  All other changes whose commits cannot be identified (potentially lost), we can identify using `git diff main..development`, and do a merge commit (three-way merge). 

### Remediation steps

Create a new branch from main, called `dev-to-main`. This branch is compliant with the latest in `main`, and will soon contain changes that bring the latest from `development`. 

```
$ git switch -c dev-to-main upstream/main
Switched to a new branch 'dev-to-main'
Branch 'dev-to-main' set up to track remote branch 'main' from 'upstream'.
```

#### Step 1: Create a patch that brings changes from development to main

The reason we apply a patch is because these changes cannot be brought from development to main via a `git pull`. (When we run `git pull`, no commits to pull are identified. [Example](https://stackoverflow.com/questions/16490547/what-is-the-right-way-to-merge-branches-when-git-diff-shows-changes-but-git-m).)

1. Get list of changes that are in development, but not in main. See output: [diff-dev-to-main.txt](https://quip-amazon.com/-/blob/HaY9AAfa8HL/r9p-aiaeFsnMO71JEYxzvA?name=diff-dev-to-main.txt) 

```
$ git diff upstream/main..upstream/development > diff-dev-to-main.txt
```

1. (Optional) View the git diff in a GUI to see the changes more easily. For example, upload the diff output to diffy.com.
    How to understand the list of differences. Lines marked with **`-`** indicate lines that exist in main, but not in development. Lines marked with **+** indicate lines that exist in development, but not in main. 

[Image: image.png]

1. Manually verify that all of these changes in development, are changes we want to bring into main. 
2. Create a patch.

```
$ git diff dev-to-main..upstream/development --binary > diff-2305-post-release.patch

```


You can ensure the patch contains what you expect and does not contain errors using the following commands

* Check if the diff can be applied to this branch. If successful, there is no output.

```

git apply --check diff-2305-post-release.patch
```

* Check the contents of the patch by running `git apply --stat diff-2305-post-release.patch`.  You can [compare the number of files changed](https://stackoverflow.com/a/6584048/19604334) from the `git diff` to the patch by using `wc -l`. (The second one has 170 lines instead of 169 because 1 line is used to summarize the difference. The rest of the lines show the name of the file.)

```
$ git diff dev-to-main..upstream/development --name-only | wc -l
169

$ git apply --stat diff-2305-post-release.patch | wc -l
170
```



#### Step 2: Selectively apply parts of the patch

The patch we created is meant to be applied to main. It contains a complete diff of main and development. Because main has some relevant changes that development doesn’t have, we don’t want to simply apply the entire patch because that would cause undo changes that we want to keep in main.  For each file in the diff, we *likely* want to keep the version that has the more recent changes. 

**Diff spreadsheet**:  [O3DE 23.05 Post-release Diff (dev-to-main)](https://quip-amazon.com/GUASAEa2OKlV)
This diff spreadsheet helps you determine and track which file changes to keep in the patch.
[Image: image.png]Contents of diff spreadsheet:

* Each row corresponds to a file with that’s different between main and development.
* **Filename**: Relative path of file
* **Branch with latest commit**: Specifies the branch that contains the most recent update for this file.
* **Latest commit in dev branch**: Specifies this file’s latest commit in the development branch. If **Branch with latest commit** is “development”, then this file likely contains the changes we want to apply to main, so we should add it from the patch.
* **Latest commit in main branch**: Specifies this file’s latest commit in the main branch. If **Branch with latest commit** is “main”, then this file likely contains the changes we don’t want to apply to main, so we should exclude it from the patch.


Source: [(Stack) Find out which branch has the most recent version of a certain file](https://stackoverflow.com/questions/51795893/find-out-which-branch-has-the-most-recent-version-of-a-certain-file)

```
git branch --all --contains "$(git log --branches 'development' 'main' --format=format:%H -n 1 -- path/to/file)"
```


**To selectively apply parts of the patch**: 

1. Apply the patch. This makes the changes to your local branch. It does not add and commit automatically - you must do this manually and selectively choose which changes to add. 

```
$ git apply diff-2305-post-release.patch
```

    1. You may get warning that says “warning: squelched 46 whitespace errors” and “warning: 51 lines add whitespace errors.” No action is needed.
1. Use the diff spreadsheet and [github.com/o3de/o3de.org](http://github.com/o3de/o3de.org) to manually verify and add the file changes to the patch.
    1. [Image: image.png]
    2. See **[Resolving files that did not output a “branch with latest commit”](https://quip-amazon.com/ZcJyAbfhMb93/O3DE-2305-Post-Release#temp:C:HaY450bc19c99ce456b8a1f1a9be)**
2. Verify the patch was applied

```
$ git apply diff-2305-post-release.patch -R --check && echo already applied
```



#### **Resolving files that did not output a “branch with latest commit”**


In this example, it’s unclear whether `distributable-engine.md` should come from main or development because **Branch with latest commit** field is empty. So, we look at the file’s latest commit in both the development and main branches. This additional context helps us determine which changes to keep. 
[Image: image.png][Image: image.png]
#### **How the diff spreadsheet was created**

[O3DE 23.05 Post-release Diff (dev-to-main)](https://quip-amazon.com/GUASAEa2OKlV),  the “diff spreadsheet”, was created from the list of differences between `main` and `development`. We used it in step 2 as an organization tool to determine which changes in the patch to apply. 

We ran the following commands to get information for the diff spreadsheet. 


* **Get filenames from diff main and development.**

```
git diff upstream/main..upstream/development --name-only
```

* **Get the branch that contains the latest commit for each filename.**

```
git branch -r --contains "$(git log --branches -r --format=format:%H -n 1 -- $in)"
```

* **Combine filename and latest branch for each file:** Outputs filename, branch(es). I post-processed this data so it’s strictly "filename, branch" — filename and branch are in the same line, comma-separated, and only one branch name listed. 

```
git diff upstream/main..upstream/development --name-only |  
while read in; do
    echo "$in, "
    git branch -r --contains "$(git log --branches -r --format=format:%H -n 1 -- $in)"
done
```

* **Get latest commit in both `development` and `main` branch for each file.** While all files’ latest commit are either in `development` or `main` branch, we want to manually compare their latest commit in both development and main branches. This is to verify that we choose the *correct* latest changes.
    * **Latest commit in `development`**

```
git diff upstream/main..upstream/development --name-only |  
while read in; do
    commit=$(git log upstream/development --format=format:%H -n 1 -- $in)  
    echo $commit 
done

```

    * **Latest commit in `main`**

```
git diff upstream/main..upstream/development --name-only |  
while read in; do
    commit=$(git log upstream/main --format=format:%H -n 1 -- $in)  
    echo $commit 
done
```



* **(Optional) Get unique commits and their date.** This is extra information if you want to do a deeper dive into the actual commit of the files and see the timeline these commits were introduced. 

```
git diff upstream/main..upstream/development --name-only |
    while read in; do
        commit=$(git log upstream/development --format=format:'%H (%ad)' -n 1 -- $in);
        echo $commit;
    done
```

    * `--format=format: '%H' (%ad)’`:  Formats the commit as `<commit> (<date>)`. For example, `fed58d3523e9b7f1a984786a8e5b25d67fa65b6e (Mon May 8 15:09:36 2023 -0700)`.



**Excluded from patch**

This PR aims to completely sync `main` and `development`, such that `main` has all current changes. 
The following files from the patch were excluded. These files contain current changes in main, and are not in development. Because the patch introduces changes from development, it would have tried to remove or undo these changes, which we don’t want.

```
$ git diff dev-to-main..upstream/development --name-only |
> while read in; do
>     commit="$(git log --branches -r --format=format:%H -n 1 -- $in)"
>     echo "$in ($commit)"
> done

content/blog/posts/23-05-release.md (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
content/blog/posts/mps-blog.md (9244d7b0462a89ccde647efa9a641c4bfdf2d19f)
content/docs/engine-dev/architecture/bootstrap/_index.md (ade027bae685b21f3b71cdbe8b009dcdcd7aa4ef)
content/docs/engine-dev/frameworks/azcore/_index.md (ade027bae685b21f3b71cdbe8b009dcdcd7aa4ef)
content/docs/user-guide/assets/asset-processor/skip-startup-scan.md (d390819e6ad1d088bf9fd0e3cb7a215ea63eb51f)
content/docs/user-guide/editor/_index.md (68818a800972ab3a372b4f9aca1a03b1dc72786a)
content/docs/user-guide/editor/asset-browser.md (68818a800972ab3a372b4f9aca1a03b1dc72786a)
content/docs/user-guide/gems/reference/debug/imgui.md (ade027bae685b21f3b71cdbe8b009dcdcd7aa4ef)
static/images/blog/23-05-release/image01.jpg (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image01.png (80ee62d1a938464ac4ea7512ace12a2d9dc4a595)
static/images/blog/23-05-release/image02.jpg (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image02.png (80ee62d1a938464ac4ea7512ace12a2d9dc4a595)
static/images/blog/23-05-release/image03.jpg (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image03.png (80ee62d1a938464ac4ea7512ace12a2d9dc4a595)
static/images/blog/23-05-release/image04.png (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image05.png (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image06.png (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image07.jpg (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/blog/23-05-release/image07.png (80ee62d1a938464ac4ea7512ace12a2d9dc4a595)
static/images/blog/23-05-release/image08.jpg (a61897fab4d7fc324f9ebc57eb6cf0f17c02fa79)
static/images/user-guide/assetbrowser/advanced-filter-options.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/asset-browser-welcome.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/asset-management.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/asset-type-filter.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/breadcrumbs-click-navigate.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/breadcrumbs-edit.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/folder-context-menu.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/list-view-button.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/list-view.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/table-view-button.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/table-view.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/thumbnail-view-button.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
static/images/user-guide/assetbrowser/thumbnail-view.png (68818a800972ab3a372b4f9aca1a03b1dc72786a)
```
