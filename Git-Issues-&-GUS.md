# Git Issues & GUS

We have two different issue-tracking systems: Git and GUS. This is not ideal because it prevents us from holistically looking at our backlog and getting metrics for all of our work in one place. While Git issues has better integration of linking to off-core code / PRs / other issues, we all know that GUS is the standard at the company.

The motivation of this Git issue triaging process is to account for all work on GUS. This has the benefit of:

- Be able to track all work in one place
- Not treating off-core Git issues as secondary work
- Divide less of our time between the two systems

## Triaging Git Issues

A Git issue is considered triaged once it has the appropriate `Gus:XXX` git label(s) and has the associated work item number in the title. If the number is missing, that implies a work item has yet to be created for it.

### 1. Labels
Depending on if the issue will result in a user story or bug, add the `GUS:story` or `GUS:bug` [label](https://git.soma.salesforce.com/communities/webruntime/labels), respectively. If it is unclear what the work is, add the `investigate` label.

If known, add the label for the release number of the expected Scheduled Build (e.g. `226`). Otherwise, the Scheduled Build will be considered "Backlog".

### 2. Work Item
Create a new GUS work item for the bug or story, if one does not exist.

Add the work item number to the end of the title of the git issue in format: `(@W-######)`.
The description of the GUS work item itself can simply be a link to the git issue. However, if it is a User Story please add the "_As a \_\_\_, I want \_\_\__" persona statement, acceptance criteria, and any other appropriate DoR requirements that are not already included in the git issue description.