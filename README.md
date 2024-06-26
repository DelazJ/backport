Backport is a [JavaScript GitHub Action](https://help.github.com/en/articles/about-actions#javascript-actions) to backport a pull request by simply adding a label to it.

It can backport [rebased and merged](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-merges#rebase-and-merge-your-pull-request-commits) pull requests with a single commit and [squashed and merged](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-merges#squash-and-merge-your-pull-request-commits) pull requests.
It thus integrates well with [Autosquash](https://github.com/marketplace/actions/autosquash).

This action is a fork of https://github.com/tibdex/backport, it adds support for backporting _rebase merges_ and _merge commits_, _squash_ commits are also supported.

# Usage

1.  :electric_plug: Add this workflow [.github/workflows/backport.yml](.github/workflows/backport.yml) to your repository.
2.  :speech_balloon: Let's say you want to backport a pull request on a branch named `production`.
    Then label it with `backport production`. (See [how to create labels](https://help.github.com/articles/creating-a-label/).)
3.  :sparkles: That's it! When the pull request gets merged, it will be backported to the `production` branch.
    If the pull request cannot be backported, a comment explaining why will automatically be posted and the pull request will be labeled with `failed backport`.

_Note:_ multiple backport labels can be added.
For example, if a pull request has the labels `backport staging` and `backport production` it will be backported to both branches: `staging` and `production`.


## Customizing

### inputs

Following inputs can be used as `step.with` keys

| Name               | Type    | Description                       |
|--------------------|---------|-----------------------------------|
| `add_labels`       | String  | Comma separated list of labels to add to the backport PR. |
| `github_token`     | String  | Token for the GitHub API. Set this to a personal access token (PAT) of a user which is collaborator with write permissions on the repository to make workflows run on backport pull requests. |
| `title_template`   | String  | Template for the title of the opened PR. E.g. `[Backport {{base}}] {{originalTitle}}` |
