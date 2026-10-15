# workshop-reproducible-research-binder_example
A repository showing how to use Binder with Jupyter notebooks

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/NBISweden/workshop-reproducible-research-binder_example/HEAD?labpath=supplementary_material.ipynb)

Click the badge to open `supplementary_material.ipynb` in JupyterLab on
[mybinder.org](https://mybinder.org).

## Repository layout

| Path | Content |
| --- | --- |
| `binder/environment.yml` | Conda environment used by Binder to build the image |
| `supplementary_material.ipynb` | The notebook |
| `results/` | Input data used by the notebook |
| `references.bib` | References cited in the notebook |

Binder (via [repo2docker](https://repo2docker.readthedocs.io)) looks for
configuration files in the `binder/` folder first. Keeping them there separates
the build setup from the content.

## Tips for fast and reproducible builds

- **Pin versions** in `binder/environment.yml`. This makes the build
  reproducible and makes the conda solve faster. Pin `python` to a minor
  version only (e.g. `3.14`) so that repo2docker can use its pre-built base
  environment.
- **Do not list `jupyterlab` or `notebook`**. repo2docker already installs them.
- **Use the default kernel** (`python3`) in the notebook metadata. Binder does
  not have kernels named after your local environments.
- **Link to a tag, not `HEAD`, during a course.** Every new commit gives a new
  image that must be built before the first user can start. Create a tag
  (e.g. `git tag course-2026 && git push --tags`), replace `HEAD` with the tag
  name in the link, and open the link once yourself before the course so the
  image is built and cached.
- **Keep content and environment apart** if the content changes often. Put the
  environment in one repository and pull the notebooks in with
  [nbgitpuller](https://nbgitpuller.readthedocs.io). Content changes then never
  trigger a new build.
