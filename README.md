# r-releases

`r-releases` is a community-curated [R universe](https://r-releases.r-universe.dev) of R packages deployed as tags/releases on GitHub. The GitHub repository at <https://github.com/r-releases/r-releases> allows anyone to register packages with the [universe](https://r-releases.r-universe.dev). The project is still in its prototype phase, but the goal is to build a production-ready community-wide CRAN-like repository that incentivizes thorough testing and puts control in the hands of the package maintainers.

# Disclaimer

The `r-releases` project is brand new and in its prototype phase. It is not ready for widespread production usage, and policies are subject to change.

# How to install a package from `r-releases`

To install a package from `r-releases` (for example, `jsonlite`), open R and run:

```r
install.packages("jsonlite", repos = "https://r-releases.r-universe.dev")
```

If the package has dependencies in CRAN but not `r-releases`, please contribute them to `r-releases` as described below. As a temporary workaround for installation, you can include CRAN as a backup:

```r
install.packages(
  "jsonlite",
  repos = c("https://r-releases.r-universe.dev", "https://cloud.r-project.org")
)
```

# Continuous maintainer-driven deployment

After the one-time registration process described below, each package in `r-releases` continuously deploys to `r-universe`. Every new [tag and release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) in your package's GitHub/GitLab repository automatically publishes at <https://r-releases.r-universe.dev> and becomes available to install from there. No matter how many releases you create in your own personal GitHub account, you do not need to interact with `r-releases` again unless you wish to change the link or remove the package from <https://r-releases.r-universe.dev>. In other words, you as the maintainer are in complete control. This painless maintainer-driven experience was made possible by the incredible infrastructure of [rOpenSci's R-universe system](https://ropensci.org/r-universe/) and insights from [Jeroen Ooms](https://github.com/jeroen/).

# Before you contribute

The [code of conduct](https://github.com/r-releases/help/blob/main/CODE_OF_CONDUCT.md) governs all forms of participation in the `r-releases` project, including package contributions, issues, discussions, and the development of infrastructure. Administrators, moderators, and contributors are all subject to its terms.

# How to register your package with `r-releases`

The one-time registration process proceeds as follows.

1. Put the source code of your R package in a public [GitHub](https://github.com) (or [GitLab](https://gitlab.com)) repository with the `DESCRIPTION` file at the root of the project. Example: <https://github.com/r-lib/gh>.
2. Create a [tag and release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) for the latest production version of your package. Example: <https://github.com/r-lib/gh/releases/tag/v1.4.0>.
3. Open a [GitHub pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) to <https://github.com/r-releases/r-releases> to contribute one or more text files to the [`packages` folder](https://github.com/r-releases/r-releases/tree/main/packages) with R package listings.

The overwhelming majority of text files in (3) will be in simple URL format, which has has 3 requirements:

1. The name of the file is the package name.
2. The file contains a single line with the package URL. The URL must be authentic and genuine. It must be the true location of the package according to its owners. For `r-releases`, this is always the URL of a repository from GitHub or GitLab, such as https://github.com/r-lib/gh.
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

[![r-releases status](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fr-releases.r-universe.dev%2Fapi%2Fpackages%2Fmirai&query=%24.Version&label=r-releases)](https://r-releases.r-universe.dev/mirai)
To add a dynamic 'r-releases' badge for package readme files, like the one to the left, copy the following markdown construction, replacing 'pkgNAME' with the actual package name in both the places it appears:

```md
[![r-releases status](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fr-releases.r-universe.dev%2Fapi%2Fpackages%2FpkgNAMEquery=%24.Version&label=r-releases)](https://r-releases.r-universe.dev/pkgNAME)
```

# How to edit or remove packages

To edit or remove one or more packages, submit a pull request to edit the files in the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder. To protect the package ecosystem, these kinds of pull requests are always flagged for manual review and never automatically merged.

# How pull requests are reviewed

An automated process periodically scans each new pull request to https://github.com/r-releases/r-releases. Depending on the results of the automated checks, the bot automatically merges the pull request, closes it, or flags it for manual review. In the latter case, an `r-releases` moderator will manually review your pull request and contact you if there are questions. For more information on the manual review process and when it gets triggered, please visit <https://github.com/r-releases/help/blob/main/review.md>

# How the R universe is built

Periodically, a GitHub Actions workflow collects all the packages and URLs from the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder and builds the `packages.json` file for the R universe at <https://github.com/r-releases/r-releases.r-universe.dev>. <https://r-releases.r-universe.dev> periodically refreshes to include the latest release of each package in `packages.json`.

# Ownership and attribution

Each submitted package URL must be authentic and genuine. The URL must be the true location of the package according to its true owners. If a URL in https://github.com/r-releases/r-releases/tree/main/packages points to the wrong place, please submit a pull request to <https://github.com/r-releases/r-releases> to fix the URL. If you do not know the correct URL or do not want to submit a pull request, please open an issue at <https://github.com/r-releases/help/issues>.

# Getting help

Please report bugs to <https://github.com/r-releases/help/issues> and send other feedback and questions to <https://github.com/r-releases/help/discussions>. Please note that <https://github.com/r-releases/r-releases> can only accept pull requests to add or modify package entries.
