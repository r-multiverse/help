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

After the one-time registration process described below, each package in `r-releases` continuously deploys to `r-universe`. Every new [tag and release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) in your package's GitHub/GitLab repository automatically publishes at <https://r-releases.r-universe.dev> and becomes available to install from there. No matter how many releases you create in your own personal GitHub account, you do not need to interact with `r-releases` again unless you wish to change the link or remove the package from <https://r-releases.r-universe.dev>. In other words, you as the maintainer are in complete control. This painless maintainer-driven experience was made possible by the incredible infrastructure of [rOpenSci's R-universe system](https://ropensci.org/r-universe/) and clever breakthrough insights by [Jeroen Ooms](https://github.com/jeroen/) and [Charlie Gao](https://github.com/shikokuchuo/).

# Before you contribute

The [code of conduct](https://github.com/r-releases/help/blob/main/CODE_OF_CONDUCT.md) governs all forms of participation in the `r-releases` project, including package contributions, issues, discussions, and the development of infrastructure. Both administrators and contributors are subject to its terms.

# How to register your package with `r-releases`

The one-time registration process proceeds as follows.

1. Put the source code of your R package in a public [GitHub](https://github.com) (or [GitLab](https://gitlab.com)) repository with the `DESCRIPTION` file at the root of the project. Example: <https://github.com/r-lib/gh>.
2. Create a [tag and release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) for the latest production version of your package. Example: <https://github.com/r-lib/gh/releases/tag/v1.4.0>.
3. Open a [GitHub pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) to <https://github.com/r-releases/r-releases> to contribute a text file to the [`packages` folder](https://github.com/r-releases/r-releases/tree/main/packages). The name of the text file must be the name of your package, and the URL must include the correct owner and the correct repository.

In the overwhelming majority of cases, the text file for (3) is in URL format: it contains a single line with the package URL and a [the standard terminating newline character](https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline) (which the GitHub web interface includes automatically if editing there). In rare exceptions, the package is in a subdirectory of the GitHub repository. If that is the case, then the text file should be a JSON list with fields `package`, `url`, `subdir`, and `branch`, where `branch` must be `"*release"`. Example:

```
{
  "package": "paws.analytics",
  "url": "https://github.com/paws-r/paws",
  "subdir": "cran/paws.analytics",
  "branch": "*release"
}
```

# How to edit or remove packages

To edit or remove one or more packages, submit a pull request to edit the files in the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder. To protect the package ecosystem, these kinds of pull requests are always flagged for manual review and never automatically merged.

# Reviewing package contributions and edits

In the vast majority of cases, a periodic GitHub Actions workflow will automatically merge your pull request to incorporate your changes into <https://github.com/r-releases/r-releases>. However, your pull request will be flagged for manual review if:

1. Your pull request changes or removes an existing package entry.
2. There is something non-standard about a contributed package URL.
3. The package entry is in JSON format.
4. There was an error in processing your package contribution.

If you can change your contribution to avoid manual review, please close your pull request and submit a different one. Otherwise, an `r-releases` administrator will manually review your contribution.

# How the R universe is built

Periodically, a GitHub Actions workflow collects all the packages and URLs from the [`packages`](https://github.com/r-releases/r-releases/tree/main/packages) folder and builds the `packages.json` file for the R universe at <https://github.com/r-releases/r-releases.r-universe.dev>. <https://r-releases.r-universe.dev> periodically refreshes to include the latest release of each package in `packages.json`.

# Ownership and attribution

Each submitted package URL must be authentic and genuine. The URL must be the true location of the package according to its true owners. If a URL in https://github.com/r-releases/r-releases/tree/main/packages points to the wrong place, please submit a pull request to <https://github.com/r-releases/r-releases> to fix the URL. If you do not know the correct URL or do not want to submit a pull request, please open an issue at <https://github.com/r-releases/help/issues>.

# Getting help

Please report bugs to <https://github.com/r-releases/help/issues> and send other feedback and questions to <https://github.com/r-releases/help/discussions>. Please note that <https://github.com/r-releases/r-releases> can only accept pull requests to add or modify package entries.
