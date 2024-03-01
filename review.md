# Manual review

As the [README](https://github.com/r-releases/help/blob/main/README.md) explains, updates to the `r-releases` package listings come from pull requests to https://github.com/r-releases/r-releases from members of the R community. In the vast majority of package contribution requests, a GitHub app automatically merges pull request. However, some pull requests need to be manually reviewed by an `r-releases` moderator. This document describes this manual review process. The goals are to:

1. Ensure that all pull requests are reviewed using a consistent set of standards and principles that do not vary from moderator to moderator.
2. Ensure these standards and principles are clear and transparent for the R community.

## The automated review process

The [`review_pull_requests.yaml`](https://github.com/r-releases/r-releases.r-universe.dev/blob/main/.github/workflows/review_pull_requests.yaml) [GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions) workflow runs periodically and reviews each new open pull request using [`r.releases.utils::review_pull_request()`](https://github.com/r-releases/r.releases.utils/blob/main/R/review_pull_request.R). Depending on the results of the automated checks, the bot will automatically merge the pull request, close it, or flag it for manual review. The bot will post an informative comment explaining the decision, and it may add a GitHub label to the pull request for triage purposes.

The pull request is automatically closed if:

1. It attempts to add/modify/delete a file outside the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder.
1. It attempts to add/modify/delete a file in a subdirectory of the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder.

The pull request is automatically flagged for manual review if:

1. It attempts to modify or delete any existing file in [`packages`](https://github.com/r-releases/r-releases/tree/main/packages).
1. A contributed text file is not a single-line file.
1. The single line in the text file is does not have a [standard newline character](https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline).
1. The text file looks like a custom JSON entry (for packages in a subdirectory of a GitHub repository).
1. The name of the name of the text file is not a valid R package name.
1. The URL in the text file cannot be parsed.
1. The URL scheme is anything other than https.
1. The domain of the URL is anything other than github.com or gitlab.com.
1. The URL points to an organization or user such as https://github.com/r-lib instead of a repository such as https://github.com/r-lib/gh.
1. The version-controlled repository name in the URL is different from the name of the file. (For example, if the file is named `gh` package, then the URL https://github.com/r-lib/gh-package would be flagged for manual review, but https://github.com/r-lib/gh would not.)
1. If the repository is part of the CRAN mirror at https://github.com/cran. (A fundamental goal of `r-releases` is to exist as independently from CRAN as possible.) 

## The manual review process

