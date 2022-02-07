# PytorchLightning Tutorials

[![Build Status](https://dev.azure.com/PytorchLightning/Tutorials/_apis/build/status/PyTorchLightning.Tutorials-publishing?branchName=main)](https://dev.azure.com/PytorchLightning/Tutorials/_build/latest?definitionId=11&branchName=main)
[![Code formatting](https://github.com/PyTorchLightning/lightning-tutorials/actions/workflows/ci_code-format.yml/badge.svg?event=push)](https://github.com/PyTorchLightning/lightning-tutorials/actions/workflows/ci_code-format.yml)
[![Deploy Docs](https://github.com/PyTorchLightning/lightning-tutorials/actions/workflows/docs-deploy.yml/badge.svg)](https://github.com/PyTorchLightning/lightning-tutorials/actions/workflows/docs-deploy.yml)
[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/PyTorchLightning/lightning-tutorials/main.svg)](https://results.pre-commit.ci/latest/github/PyTorchLightning/lightning-tutorials/main)

This is the Lightning Library - collection of Lightning related notebooks which are pulled back to the main repo as submodule and rendered inside the main documentations.
The key features/highlights:

- we keep the repo **light-weighted** - notebooks are stored in rich script format
- all scripts/notebooks are tested to be **fully executable**
- fully **reproducible** by saving runtime env. details

For more details read our blogpost - [Best Practices for Publishing PyTorch Lightning Tutorial Notebooks](https://devblog.pytorchlightning.ai/publishing-lightning-tutorials-cbea3eaa4b2c)

## Adding/Editing notebooks

This repo in main branch contain only python scripts with markdown extensions, and notebooks are generated in special publication branch, so no raw notebooks are accepted as PR.
On the other hand we highly recommend creating a notebooks and convert it script with [jupytext](https://jupytext.readthedocs.io/en/latest/) as

```bash
jupytext --set-formats ipynb,py:percent my-notebook.ipynb
```

### Contribution structure

The addition has to formed as new folder

- the folder name is used for the future notebooks
- single python scripts with converted notebooks (name does not matter)
- metadata named `.meta.yaml` including following info:
  ```yaml
  title: Sample notebooks
  author: [User](contact)
  created: YYYY-MM-DD
  updated: YYYY-MM-DD
  license: CC BY-SA
  # multi-line
  description: |
    This notebook will walk you through ...
  requirements:
    - package  # with version if needed
  # define supported - CPU|GPU|TPU
  accelerator:
    - CPU
  ```

### Suggestions

- For inserting images into text cells use MarkDown formatting, so we can insert inline images to the notebooks directly and drop eventual dependency on internet connection -> generated notebooks could be better shared offline
- If your images need special sizes, use `![Cation](my-image.png){height="60px" width="240px"}`
- If your notebook is computational or any other resource (CPU/RAM) demanding use only GPU accelerator option in meta config

### Known limitations

- Nothing major at this moment

## Meantime notes

On the back side of publishing workflow you can find in principle these three steps

```bash
# 1) convert script to notebooks
jupytext --set-formats ipynb,py:percent notebook.py

# 2) testing the created notebook
pytest -v notebook.ipynb  --nbval

# 3) generating notebooks outputs
papermill in-notebook.ipynb out-notebook.ipynb
```
