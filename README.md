# R-releases

R-releases is a community-curated [R-universe](https://r-releases.r-universe.dev) of R packages releases. The GitHub repository at <https://github.com/r-releases/r-releases> allows anyone to register packages. After a package is registered once, [R-universe](https://r-universe.dev) automatically builds and checks every new release and makes it available to install from https://r-releases.r-universe.dev. In other words, the R-releases package repository is decentralized, and package maintainers have complete control over deployment.

# The QA for R

A traditional software version cycle begins with the development phase, where myriad bugs are expected, and ends with the production phase, which promises a safe user experience. R-releases is a middle ground in the sense that:

1. Each package release has the full endorsement of its own maintainer. R-releases always gives you a version that its developer chose to distribute for general use.
2. The user is still responsible for judging whether a package is safe to use. This judgement may require more than a novice understanding of [testing](https://r-pkgs.org/testing-basics.html), [versions](https://r-pkgs.org/lifecycle.html#sec-lifecycle-version-number), and non-default installation tools.

# But better than QA

R-releases aims to facilitate production as well. In addition to its encapsulated centralized repository of releases, R-releases will provide modular functions to monitor the health of packages and maintain a healthy local package library. Visit https://github.com/r-releases/help/issues for updates on the development of these features.

# How to install a package from R-releases

To install a package from R-releases (for example, `jsonlite`), open R and run:

```r
install.packages("jsonlite", repos = "https://r-releases.r-universe.dev")
```

If the package has dependencies in CRAN but not R-releases, please contribute them to R-releases as described below. As a temporary workaround for installation, you can include CRAN as a backup:

```r
install.packages(
  "jsonlite",
  repos = c("https://r-releases.r-universe.dev", "https://cloud.r-project.org")
)
```

# Continuous maintainer-driven deployment

Each package only needs to register once. After registration, every new [release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) automatically deploys to <https://r-releases.r-universe.dev> without needing to go through R-releases again. In other words, the package maintainer is in complete control. This painless maintainer-driven experience was made possible by the incredible infrastructure of [rOpenSci's R-universe system](https://ropensci.org/r-universe/) and insights from [Jeroen Ooms](https://github.com/jeroen/) and [Charlie Gao](https://github.com/shikokuchuo/).

# Before you contribute

The [code of conduct](https://github.com/r-releases/help/blob/main/CODE_OF_CONDUCT.md) governs all forms of participation in the R-releases project, including package contributions, issues, discussions, and the development of infrastructure. Administrators, moderators, and contributors are all subject to its terms.

# How to register your package with R-releases

The one-time registration process proceeds as follows.

1. Ensure that the package source code exists in a public [GitHub](https://github.com) (or [GitLab](https://gitlab.com)) repository with the `DESCRIPTION` file at the root of the project. Example: <https://github.com/r-lib/gh>.
2. Ensure that the package has a [release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) for the latest production version of your package. Example: <https://github.com/r-lib/gh/releases/tag/v1.4.0>.
3. Open a [GitHub pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) to <https://github.com/r-releases/r-releases> to contribute one or more text files to the [`packages` folder](https://github.com/r-releases/r-releases/tree/main/packages) with R package listings.

The overwhelming majority of text files in (3) will be in simple URL format, which has has 3 requirements:

1. The name of the file is the package name.
2. The file contains a single line with the package URL. The URL must be authentic and genuine. It must be the true GitHub/GitLab location of the package according to its owners, or an active mirror of the true location.
3. The file ends with a [newline character](https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline). (A terminating newline is included automatically if you create the file using the GitHub web interface.)

In rare cases, the package may be in a subdirectory of a GitHub repo, in which case the contents of your text file may be a JSON list with fields `package`, `url`, `subdir`, and `branch`, and the `branch` field must be `"*release"`. [Example](https://github.com/r-releases/r-releases/blob/main/packages/paws.analytics):

```json
{
  "package": "paws.analytics",
  "url": "https://github.com/paws-r/paws",
  "subdir": "cran/paws.analytics",
  "branch": "*release"
}
```
<br/>

[![R-releases status](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fr-releases.r-universe.dev%2Fapi%2Fpackages%2Fmirai&query=%24.Version&label=R-releases)](https://r-releases.r-universe.dev/mirai)

To add a dynamic 'R-releases' badge for package readme files, like the one above, copy the following markdown snippet, replacing 'pkgNAME' with the actual package name in both places it appears:

```md
[![R-releases status](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fr-releases.r-universe.dev%2Fapi%2Fpackages%2FpkgNAMEquery=%24.Version&label=R-releases)](https://r-releases.r-universe.dev/pkgNAME)
```

# How to edit or remove packages

To edit or remove one or more packages, submit a pull request to edit the files in the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder. To protect the package ecosystem, these kinds of pull requests are always flagged for manual review and never automatically merged.

# How pull requests are reviewed

An automated process periodically scans each new pull request to https://github.com/r-releases/r-releases. Depending on the results of the automated checks, the bot automatically merges the pull request, closes it, or flags it for manual review. In the latter case, an R-releases moderator will manually review your pull request and contact you if there are questions. For more information on the manual review process and when it gets triggered, please visit <https://github.com/r-releases/help/blob/main/review.md>

# How the R-releases universe is built

Periodically, a GitHub Actions workflow collects all the packages and URLs from the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder and builds the `packages.json` file for the universe at <https://github.com/r-releases/r-releases.r-universe.dev>. <https://r-releases.r-universe.dev> periodically refreshes to include the latest release of each package in `packages.json`.

# Ownership and attribution

Each submitted package URL must be authentic and genuine. The URL must be the true location of the package according to its true owners. If a URL in https://github.com/r-releases/r-releases/tree/main/packages points to the wrong place, please submit a pull request to <https://github.com/r-releases/r-releases> to fix the URL. If you do not know the correct URL or do not want to submit a pull request, please open an issue at <https://github.com/r-releases/help/issues>.

# Getting help

Please report bugs to <https://github.com/r-releases/help/issues> and send other feedback and questions to <https://github.com/r-releases/help/discussions>. Please note that <https://github.com/r-releases/r-releases> can only accept pull requests to add or modify package entries.
