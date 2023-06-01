# Envionment-and-Package-Manager
Envionment &amp; Package Manager | Conda vs. Poetry
***

## Dependencies
- They are functionalities in external libraries and packages (libraries and packages that do not come with our programming environment by default.
***

## Intro on  `Conda`, `pip` and `Poetry`
  - Conda is a dependency management tool that comes with Anaconda. Anaconda is typically used by beginners in data science who are starting out in Python programming, and do not want to worry too much about about installing the common dependencies needed for data science work, such as numpy, pandas, jupyter and scikit-learn.
  - Pip: Pip is a dependency management tool that comes together with the standard Python installation for Windows, and can be installed via Homebrew for MacOS and the distribution app manager for Linux systems (e.g. apt for Debian and Ubuntu).
  - Poetry is a newer dependency management tool that is gaining visibility and popularity for Python users. The use of `pyproject.toml` and `poetry.lock` files make it similar to the way the Node Package Manager (npm) for Node.js works. More information about Poetry can be found in its documentation.
***

## Conda vs. poetry
- Conda and Poetry have different purposes, but are largely redundant:
  - `Conda` is primarily a environment manager (in fact not necessarily Python), but it can also manage packages and dependencies.
  - `Poetry` is primarily a Python package manager (say, an upgrade of pip), but it can also create and manage Python environments (say, an upgrade of Pyenv). It seems to be best choice for production-grade code.
***

## From experience
- Conda seems to be best as a environment manager and can be used for compiling and installing non-python packages, especially CUDA drivers.
-  Poetry is more powerful than Conda as a Python package manager (dependencies).
***

## Why Poetry is better for production code
- By typing `conda list` you realise how many packages (mostly unecessay) are actually installed. This is useful for get you off the ground quicklyand if you do not want to spend too much time trying to figure out how to get the dependencies they need. However, when it comes to an actual project in production,  this is impotant. Of course, there is also Miniconda, which uses Conda underneath too without all these additional packages, but…
- Run the following test and see how many packages ar actually installed:
  - Installation of `numpy` via conda:  `conda install -c conda-forge numpy==1.22.3` and check it via `conda list` (it would not show unless another packahge like `pandas` which uses `numpy` is installed!)
  - Installation of `numpy` via pip: `pip install numpy==1.22.3` and check it via `pip list`
***

## `Poetry` is better than `pip` at managing conflict
- If `pip` complains that a library to be installed has a conflict with the dependency requirements specified in another library, it still goes ahead.This could cause bugs to occur during runtime, which is definitely not what we want.
- Before installing or updating any libraries, Poetry will check the dependency requirements of all the existing libraries that are installed, and any dependency conflict that is discovered would cause the installation process to be stopped. Although this could mean a bit more initial effort to resolve conflicting versions of libraries, this also ensures that there are no dependency conflicts within the project that could lead to bugs later on.
***

## How to create a `requirements.txt` file
- See this [link](https://github.com/kyaiooiayk/Awesome-Python-Programming-Notes/blob/main/tutorials/requirements.md)
***

## References
- [Does it make sense to use Conda + Poetry?](https://stackoverflow.com/questions/70851048/does-it-make-sense-to-use-conda-poetry)
- [Why you should use Poetry instead of Pip or Conda for Python Projects](https://blogs.sap.com/2022/05/08/why-you-should-use-poetry-instead-of-pip-or-conda-for-python-projects/)
***
