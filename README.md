# example-pending-github-status-check
An example repository where a required status check for merging is pending when the check is pushing on the branch.

## How to reproduce
Open a new pull request and push a change. You can update the `src/input.txt` file for example.
Once you pushed, the [`check` action](https://github.com/loic-h/example-pending-github-status-check/blob/main/.github/workflows/check.yml) will be triggered and commit a change by overwritting the [`log.txt` file](https://github.com/loic-h/example-pending-github-status-check/blob/main/log.txt).
Branch protection rule is setup to have the check action required in order to merge in the main branch.

## Expected result
The push done by the action does not trigger the check, [as per design](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#triggering-new-workflows-using-a-personal-access-token). No check being triggered, it should not be required before merging.

## Actual result
The PR is waiting for a check that is never triggered. The check list shows zero action done; the PR still detected a change in the git history and expect the check to be green before allowing the merge.
