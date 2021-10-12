# Documentation
Documentation build using mkdocs

## Setup
To serve locally, download [mkdocs](https://www.mkdocs.org/getting-started/), and [mkdocs-material](https://squidfunk.github.io/mkdocs-material/getting-started/):

```bash
pip install mkdocs
pip install mkdocs-material
```

Navigate to where you have cloned this repository and run

``` 
mkdocs serve 
```

Note: There is no need to build this documentation as a github action was setup to automatically build and deploy it to gh-pages after every commit