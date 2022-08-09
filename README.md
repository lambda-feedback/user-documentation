# Documentation
Documentation build using mkdocs

## Setup
To serve locally, download the requirements (mainly [mkdocs](https://www.mkdocs.org/getting-started/), [mkdocs-material](https://squidfunk.github.io/mkdocs-material/getting-started/) and [evaldocsloader](https://github.com/lambda-feedback/EvalDocsLoader))

```bash
pip install -r requirements.txt
```

Navigate to where you have cloned this repository and run

``` 
mkdocs serve 
```

Notes: 
- There is no need to build this documentation as a github action was setup to automatically build and deploy it to gh-pages after every commit
- You can ignore errors related to the evaldocsloader plugin, you most likely won't need its external documentation page loading features when developing locally

## Documentation Development
Some links you might find useful when authoring documentation content: 
- [MkDocs Documentation](https://www.mkdocs.org/user-guide/writing-your-docs/#writing-your-docs)
- [MkDocs-Material Documentation](https://squidfunk.github.io/mkdocs-material/reference/)
- [MkDocs Macros Plugin](https://mkdocs-macros-plugin.readthedocs.io/en/latest/)