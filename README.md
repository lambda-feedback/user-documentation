# Lambda Feedback User Documentation

This repository contains the user documentation for the Lambda Feedback platform. The documentation is built using [MkDocs](https://www.mkdocs.org/) and the [Material theme](https://squidfunk.github.io/mkdocs-material/) and is hosted on [GitHub Pages](https://lambda-feedback.github.io/user-documentation/).

## Usage

This section guides you through the installation of the necessary dependencies and how to serve and build the documentation locally.

### Pre-requisites

- [Python 3.11](https://www.python.org/downloads/) or higher
- [Poetry](https://python-poetry.org/docs/#installation)

### Installation

To serve or build the documentation locally, you have to install its dependencies. The documentation mainly builds on the following libraries:

- [MkDocs](https://www.mkdocs.org/getting-started/)
- [MkDocs-Material](https://squidfunk.github.io/mkdocs-material/getting-started/)
- [EvalDocsLoader](https://github.com/lambda-feedback/EvalDocsLoader)

To install the dependencies using Poetry, run the following command:

```bash
poetry install
```

### Serving the Documentation

To serve the documentation locally, run the following command:

```bash
poetry run mkdocs serve
```

This will start a local server at `http://127.0.0.1:8000/user-documentation/` where you can view the documentation.

> [!NOTE]
> You can ignore warnings or errors related to the EvalDocsLoader plugin, as long as you do not want to load external documentation pages for evaluation functions.

### Building the Documentation

To build the documentation, run the following command:

```bash
poetry run mkdocs build
```

This will build the documentation in the `site` directory.

### Fetching Evaluation Function Documentation

To fetch the documentation for evaluation functions, the `EvalDocsLoader` plugin is used. The plugin is already installed as a dependency in the `pyproject.toml` file.

When the necessary environment variables are set, the plugin will fetch the documentation for available evaluation functions automatically, and add them to the documentation.

The following environment variables are required:

- `API_KEY`: The API key for the lambda feedback API.
- `GITHUB_TOKEN`: A [GitHub Private Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) with the `repo` scope to fetch the documentation from evaluation function repositories.

To set the environment variables, you can use the `export` command in your terminal:

```bash
export API_KEY="<your-api-key>"
export GITHUB_TOKEN="<your-github-access-token>"
```

After setting the environment variables, you can serve or build the documentation as described above.

## Deployment

The documentation is deployed to [GitHub Pages](https://pages.github.com/) using a GitHub Actions workflow. Deployment is done automatically after every commit to the `main` branch, as well as at midnight every day, UTC.

## Documentation Development

Some links you might find useful when authoring documentation content:

- [MkDocs Documentation](https://www.mkdocs.org/user-guide/writing-your-docs/#writing-your-docs)
- [MkDocs-Material Documentation](https://squidfunk.github.io/mkdocs-material/reference/)
- [MkDocs Macros Plugin](https://mkdocs-macros-plugin.readthedocs.io/en/latest/)
