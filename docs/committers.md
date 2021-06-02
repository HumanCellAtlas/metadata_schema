# The Human Cell Atlas: Metadata Update Process for Committers

## Table of Contents
- [Introduction](#introduction)
- [General steps of the update process](#general-steps-of-the-update-process)
- [Specific how-to for making changes](#specific-how-to-for-making-changes)
- [Schema update review process](#schema-update-review-process)
- [Committer guidelines](#committer-guidelines)
- [Adding new committers](#adding-new-committers)
- [Glossary of roles](#glossary-of-roles)

## Introduction

This document serves as an SOP for committers who are ultimately responsible for changes to the metadata standards.

**What is in this document?**
 - Directions for how to incorporate feedback into the metadata standards
 - Expectations for contributions to be accepted or rejected

**Who should be reading this document?**
 - HCA DCP internal developers

**What *isn't* in this document?**
- Description of what defines [major, minor, and patch changes](evolution.md#schema-versioning) to the metadata schema
- Directions for [reporting bugs](contributing.md#reporting-bugs) in the metadata schema

## General steps of the update process

1. **Receive request for update to the metadata standard.** A person (the "Contributor") can suggest changes to the metadata standards via three main routes:
    1. Create a GitHub issue on the metadata-schema repo for either [updates](https://github.com/HumanCellAtlas/metadata-schema/issues/new?template=schema_update.md) or [new schemas](https://github.com/HumanCellAtlas/metadata-schema/issues/new?template=new_schema.md)
    1. Email the HCA DCP helpdesk at [data-help@humancellaltas.org](mailto:data-help@humancellaltas.org)
    1. Make a pull request against the develop branch of the metadata-schema GitHub repo

    There are two main types of suggestions: (1) **updates** to existing schemas and (2) addition of **new** schema(s).

    1. To request an **update** to an existing schema, the following pieces of information are required:

        1. For which schema is a change/update being suggested?
        1. What should the change/update be?
        1. What new field(s) need to be added?
            - Details for requesting **new field(s)** outlined below
        1. Why is the change requested?

    1. To request a **new** schema, the following pieces of information are required:

        1. What is the proposed name of the new schema?
        1. What field(s) should the new schema contain?
            - Details for requesting **new field(s)** outlined below
        1. Why is the new schema needed? Specifically, why does the current metadata standard not meet your need?
    
    For **each new field** requested, the following pieces of information are required:
    
    1. Field name
    1. Field description
    1. Whether the field should be optional or required
    1. An example valid value for this field
    1. If this field needs a controlled vocabulary or ontology. If yes, what those values should be or which ontology should be followed.
    
    If the suggested update comes in the form of a pull request, the above information should be self-evident between the JSON schema itself and the pull request message. If this isn’t clear either from the pull request or the message sent through email or git, then the assigned committer will seek clarification before continuing to step 3.

1. **Assign Committer to review the suggestion.** A person (the "Committer") with commit rights on the metadata-schema repo will be assigned to each suggestion (issue/email/PR). The Committer will be responsible for reviewing the suggestion, noting any consequences of the suggestion, contacting appropriate HCA teams for feedback, and making announcements to ensure the whole community has an opportunity to provide input. 

1. **Make pull request if one does not exist.** If the suggestion came in the form of a GitHub issue or email, then the Committer needs to make the suggested update and a pull request against develop. If the Contributor has a GitHub account, they should be encouraged to make the suggested update and a pull request. When a pull request is made, a test suite of tools will automatically run that validates the updates. 

    **NB** Currently this test suite of tools is not complete, and the tools that do exist must be run manually by the Reviewer.

1. **Annotate the pull request (version, stability) and run unit tests.** The Committer should classify the suggested update by the type of version change (major, minor, patch) and the stability category (high, medium, or low). These classifications can be indicated in the pull request description. Specifically, the version change classification will be indicated in the `update_log.csv` file. The Committer should also ensure the metadata-schema repo unit tests have been run and pass. Example spreadsheets and JSON documents will potentially need to be updated.

1. **Notify community about the update request.** The Committer should announce the suggested update/PR on the #hca-metadata and #dcp Slack channels so everyone can have an opportunity to comment over the time frame specified by the combination of stability level and version change. The Committer should also tag specific developers who could be impacted by the change. 

1. **Start the community review period.** The Committer starts the clock on the review period as indicated by the [update acceptance process](#schema-update-acceptance-process). The Committer and any other assigned internal reviewers ("Reviewers") should actively respond to feedback on the proposed update, making any indicated changes in the pull request.

1. **Pre-release the update.** Once the review period is over, if the update is accepted then the Committer merges the pull request into develop following the [release process](release_process.md). The update is now considered "pre-released".

## Before making changes

1. **Clone** the metadata-schema repository into your local environment (should only need to do this once).

        git clone git@github.com:HumanCellAtlas/metadata-schema

1. **Install** the following requirements:
   1. [Python 3](https://www.python.org/downloads/)
   1. [pre-commit](https://pre-commit.com/#quick-start)

## Specific how-to for making changes

This section outlines steps for Committers to make suggested changes to the metadata schema via pull requests.

1. **Navigate** to the metadata-schema repo.

        cd metadata-schema
    
1. **Switch** to the staging branch. All suggested changes should be based on the current staging branch.

        git checkout staging

1. **Make** and **switch** to a new working branch from develop. Name the branch following the convention: `initials-brief-desc-of-branch-scope`. Optionally, you can tag a GitHub issue (e.g. `Issue222`) or JIRA ticket (e.g. `HCA-123`) in the branch name.

        git checkout -b mf-new-mouse-module-Issue222

1. **Make** changes locally to the new working branch. After making changes, it is important to run the `src/schemas_are_valid_json.py` script locally (which are also run by Travis CI after each push). The script checks whether each .json file in the `json_schema/` folder is valid JSON format. Ensure the script exits with status 0 (you should see `Process finished with exit code 0` printed to the terminal) before committing changes. If the test fails, you will have to debug and fix the errors in the changes you made.

1. **Document** the changes in the `update_log.csv` file. This file is used by the automated release scripts to build the release changelog and increment the version number for the correct metadata schema. Unlike the changelog file, which is a running log of all metadata schema changes, the update_log file should only contain the documented changes for this branch, so the file should be empty apart from the header row when you first check out a new branch. An entry into `update_log.csv` should contain the path to the schema that was changed, the type of change (major, minor, or patch) and the description of the change that should go into the changelog, for example:

    `module/ontology/disease_ontology,patch,Fixed a typo in description of text field in disease_ontology. Fixes #000,,`

    Only list one schema per line and only list schemas that you have actually changed as the release script will automatically identify dependent schemas. If multiple schemas are being updated in a single PR, order the lines in the `update_log.csv` file with patch changes first, then minor, then major. Each line should end in a double comma, signifying the empty columns for version number and release date, which will be filled in by the release script. Not including the commas will cause the release script to fail. If there is a comma in the change message, the message needs to be quoted:

    `type/biomaterial/organoid,patch,"Added user friendly names for fields a, b, c and d",,`

    The change message should start with one of: *Added, Changed, Removed, Fixed, Deprecated, or Security*. These keywords are used in the changelog to classify types of changes.  

    ***New schemas only***

    1. If you added a new schema, **add** the name of the new schema in `json_schema/versions.json` in the correct location and with version number 0.0.0. For example, if you added a new biomaterial module `my_new_module`, your addition to the `versions.json` file would be:

           [...]
            "module": {
            "biomaterial": {
                [...],
                "my_new_module": 0.0.0
            },
            [...]

    1. The corresponding entry in the `update_log.csv` file should be marked a major version update so that the release script sets the version number of the new schema to `1.0.0`.

    ***Breaking changes only***

    1. If you made a breaking (major) change to a property, including adding a new required property, renaming a property, removing a property or moving a property to a different schema, please fill in the `property_migrations.json` file following the correct pattern. Example migrations can be found in `examples/sample_property_migrations.json`.
    
    1. Do **NOT** fill in a value for the `effective_from/_source/_target` property, just insert blank quotes. This will be completed by the release script.

    1. If you are unsure how to fill in the `property_migrations.json` file, contact a wrangler for help.

    ***Note:*** *We currently don't have a process for capturing breaking changes not included in the above categories, such as changing the type of a field from a string to a number or from free text to ontology. Therefore such changes don't need to be captured in `property_migrations.json` for now.*

1. **Stage** and **commit** your changes to the working branch often. We recommend committing after making a few logically grouped changes to help track changes and to increase granularity for rollbacks (if needed). Use helpful/short messages in commit statements. If the commit specifically fixes/addresses a current GitHub issue, add the phrase "Fixes #000" to the commit statement, replacing "000" with the number of the issue. This phrase is handy because when the changes are merged into the master branch, it automatically closes the issue indicated.

        git add <changed files>
        git commit -m "Helpful commit message here. Fixes #000."
    
    Example commit message: "Created new mouse module with mouse-specific fields. Fixes #142."

1. **Push** the committed changes to the working branch.

        git push origin mf-new-mouse-module-Issue222

1. **Continue** to make, stage, and commit changes to the working branch - ensuring that the two Travis CI scripts pass - until you have completed and pushed all the changes within the scope of your new branch. In GitHub, **create** a pull request against the develop branch. In the comment section of the PR, fill out "Release notes" and "Reviews requested" sections as directed by the PR template. 

1. **Request** additional Reviewer(s), if required, in GitHub to signal that a PR needs to be reviewed. If the changes are ultimately approved by all indicated Reviewer(s) and no objections are raised, the last Reviewer should run the pre-release process and merge the PR. **The Committer should not merge their own PR.** The Reviewer who merges the PR should then delete the branch unless otherwise specified by the Committer.

## Schema update review process

All the people needed for review is automatically assigned through pullapprove. The guidelines for wranglers are as follows:

A pull request should be reviewed within a specified **review timeframe**. The review timeframe starts when the Committer who opens the PR tags the appropriate number of Reviewers to review. All changes have a 2 week timeframe. Exceptions can be made if a PR is particularly complex. Weekend days and US/UK holidays do not count towards the review timeframe. 

The **reviewer number** is the number of Wranglers who need to have reviewed the pull request before it is merged. Patch schema updates should be assigned 1 wrangler, while major and minor schema updates should be assigned 2 wranglers. Exceptions can be made if a PR is particularly complex or specific persons are required for a review.

In cases of more than 1 requested wranglers:
- The first reviewer should review the pull request and approve or reject the changes. If changes are approved, the first reviewer should tag the remaining Reviewer in a comment. If changes are rejected, the Reviewer should request further changes and then follow up with a review of the new changes from the Committer.
- The second reviewer should review the pull request and approve or reject the changes. If changes are approved, the second reviewer should merge the pull request. If changes are rejected, the Reviewer should request further changes and then follow up with a review of the new changes from the Committer. If the changes are then approved, the second reviewer should merge the pull request.
- If a Reviewer can not do the review in the assigned timeframe, the Reviewer is responsible for unassigning himself or herself as a Reviewer, assigning a replacement Reviewer, and notifying the new Reviewer in a tagged comment in the pull request.

In cases of 1 requested Reviewer, the Reviewer fulfills the roles of both first and second Reviewer.

| | Major update | Minor update  | Patch update |
|:-|:-|:-|:-|
| Review timeframe | 5 working days | 5 working days | 3 working days |
| Reviewer number | 2 | 2 | 1 |

> Table 1: Review timeframe and reviewer numbers for types of schema updates

## Committer guidelines

1. *Do not merge your own PR.* This ensures that at least one other person has reviewed the suggested changes and has approved them. 
    1. Exception 1: For PRs that affect documentation only, the same person can make/merge the PR if another person with commit privileges specifically approves it using the GitHub approval mechanism.
1. *Be clear and descriptive in PR comments/commits.* 
    1. Refer to GitHub issues that the PR addresses by adding `Fixes #000` to at least 1 commit statement in the PR (where 000 is replaced by the actual GitHub issue number). 
    1. Tag a specific person if the PR addresses their issue or if the change affects their work.
    1. Include reasoning behind changes that could be controversial (e.g. reason why a field name changes, but no reason needed to fix a typo in a field description).
1. *Group commits by functional changes*
    1. In order to have a clear history, group changes in the least amount of commits possible. When needed, use `git rebase` to squash commits.

## Adding new committers

A nominated group of metadata working group members will have commit access to the metadata-schema repo.  Committers are members of the working group who have permission to merge and accept pull requests to the metadata-schema repo.

Committers are not allowed to skip the review process. Any person including the committers who wish to make a change to a metadata schema module this process must be followed.

Anyone can request to join the committer team. When a request is received, the existing committers will discuss the request and vote on the addition of the new member. This process should be rapid and the requestor should hear the outcome within 72 hours.


## Glossary of roles

**Contributor**

- Does not have commit/merge privileges to metadata-schema repo
- Suggests changes to the metadata standard (email/GitHub issue/PR)
- Reviews PRs

**Committer**

- Has commit/merge privileges to the metadata-schema repo
- Turns update requests into GitHub issues
- Is assigned to GitHub issues by himself/herself or another Committer
- Makes changes/PRs
- Announces PRs to community (Slack/mailing list)
- Reviews PRs
- Merges PRs

**Reviewer**

- Is assigned to review PRs by Committer
- Reviews PRs
- If also a Committer:
    - Has commit/merge privileges to the metadata-schema repo
    - Merges PRs
