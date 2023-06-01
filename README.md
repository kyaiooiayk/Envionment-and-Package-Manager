# Envionment-and-Package-Manager
Envionment &amp; Package Manager | Conda vs. Poetry
***

## Conda vs. poetry
- Conda and Poetry have different purposes, but are largely redundant:
  - `Conda` is primarily a environment manager (in fact not necessarily Python), but it can also manage packages and dependencies.
  - `Poetry` is primarily a Python package manager (say, an upgrade of pip), but it can also create and manage Python environments (say, an upgrade of Pyenv).
***

## From experience
- Conda seems to be best as a environment manager and can be used for compiling and installing non-python packages, especially CUDA drivers.
-  Poetry is more powerful than Conda as a Python package manager (dependencies).

## References
- [Does it make sense to use Conda + Poetry?](https://stackoverflow.com/questions/70851048/does-it-make-sense-to-use-conda-poetry)
- [Why you should use Poetry instead of Pip or Conda for Python Projects](https://blogs.sap.com/2022/05/08/why-you-should-use-poetry-instead-of-pip-or-conda-for-python-projects/)
***
