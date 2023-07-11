# Environment, Package and Project Manager
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

## 4 ways to create a virtual environment
- [Native | Puenv | Conda | Poetry](https://github.com/kyaiooiayk/Environment-Package-and-Project-Manager/edit/dev/virtual_environment.md)
***
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

## `Poetry` is better than `pip` at managing conflicts
- If `pip` complains that a library to be installed has a conflict with the dependency requirements specified in another library, it still goes ahead. This could cause bugs to occur during runtime, which is definitely not what we want.
- Before installing or updating any libraries, Poetry will check the dependency requirements of all the existing libraries that are installed, and any dependency conflict that is discovered would cause the installation process to be stopped. Although this could mean a bit more initial effort to resolve conflicting versions of libraries, this also ensures that there are no dependency conflicts within the project that could lead to bugs later on.
***

## Installing `poetry`
- Although you can run: `pip install poetry` and then verify install with: `which poetry`, this will install poetry in a specific Python installation. This isn’t recommended as this might conflict with other system files, and it makes using Poetry consistently with different versions of Python and different virtual environments difficult.
- If you are on mac install `pipx` with: `brew install pipx`, and the `pipx ensurepath`
- Install it with: `pipx install poetry`. 
- For Mac users, create (if it does not exist) a .zshrc file in your home folder with the following: `export PATH="$HOME/.local/bin:$PATH"`
***

## How to create a `xx.toml` and `xx.lock` files
- Navigate to your project folder and create a new Poetry-managed with: `poetry new <project_name>`. This command creates a subdirectory named <project_name> and populates it with a project scaffold.
```
project_name
├── pyproject.toml
├── README.md
├── package_name
│   └── __init__.py
└── tests
    └── __init__.py
```
- This includes:
  - `pyproject.toml` which is  managed for you, but you can still edit it.
  - `README.md`: An empty README for Python documentation. 
  - A subdirectory with the project name that contains the code for your project.
- Navigate into you new `project_name` folder and create a `lock` file with: `poetry lock` if it is not there.
- Check all is ok with: `poetry show` 
***

## Installing a python environment within Poetry
- Keep in mind that poetry is python-project manager, so next step is to decide which python environment to use.
- Poetry saves all the env here: `~/Library/Caches/pypoetry/virtualenvs/` if you are in a Mac.
- Let us assume you have a ready virtual environment you'd like to use. Say this is a conda env located at: `/opt/anaconda3/bin/python`
- You can use it with: `poetry env use /opt/anaconda3/bin/python`. This will create a virtualenv located here: `<your project name>-VtigPj2m-py3.9 in /Users/gm_main/Library/Caches/pypoetry/virtualenvs`
- Alternatively, when you created a proejct poetry creates one for you. In thiat case all you have to do is: `poetry env use ~/Library/Caches/pypoetry/virtualenvs/aa-VtigPj2m-py3.11`
- If you want to get basic information about the currently activated virtual environment, use: `poetry env info`
- Poetry-managed virtual environment lives in a central directory on the system, away from any projects associated with it. As a result, deleting a project directory does not also delete the corresponding virtual environment. Go to the root directory of the Poetry project and run: `poetry env remove python`.
***

## Why `xx.toml` and `xx.lock` files are bette than `requirements.txt`
- If some packages are not required in production then we would need two files and the do:
  - Install only development dependencies: `pip install -r requirements-dev.txt`
  - Installing only production dependencies `pip install -r requirements.txt`
- Poetry, however, makes it much easier to organize dependencies for development and production. The example below shows how easy it is to do this in the `pyproject.toml` file:
```shell
[tool.poetry.dependencies]
numpy = "^1.22.3"
pandas = "^1.4.2"

[tool.poetry.dev-dependencies]
black = "^21.7b0"
isort = "^5.9.3"
pytest = "^6.0"
```
- Installing is done as follows:
  - Installing only production dependencies: `poetry install --no-dev`
  - Installing both development and production dependencies: `poetry install`
  - Installing production dependency: `poetry add numpy`
  - Installalling development dependency: `poetry add pytest --dev`
- To persist the metedata ((i.e. package names and version numbers)), we generally use the command `pip freeze > requirements.txt`. With Poetry, we have the poetry.lock file, which basically stores only the metadata of dependencies that do not have conflicts with one another. The `poetry.lock` file is created automatically when we run `poetry install` for the first time. This file is also updated automatically whenever we run poetry add to install new dependencies, poetry update to update dependency versions, or `poetry lock` to check for conflicts in the dependencies listed in `pyproject.toml`. 
***

## Library from private repositories
- This is something that Poetry can do but Pip cannot. In Poetry, we could specify the following configuration in the pyproject.toml file to tell Poetry to search within both PyPI and the private repository.
```
[[tool.poetry.source]]
name = "name-of-private-repo"
url = "url-of-private-repo"
secondary = true
```
- The secondary parameter basically tells Poetry to search for and install libraries from PyPI first, and only go to the private repository if some of the libraries cannot be found in PyPI. 
***

## How to create a `requirements.txt` file (the old way)
- See this [link](https://github.com/kyaiooiayk/Awesome-Python-Programming-Notes/blob/main/tutorials/requirements.md)
***

## Initialising a pre-existing project
- Instead of creating a new project, Poetry can be used to ‘initialise’ a pre-populated directory. To interactively create a pyproject.toml file in directory pre-existing-project: `poetry init`
***

## References
- [Basic usage](https://python-poetry.org/docs/basic-usage/)
- [Does it make sense to use Conda + Poetry?](https://stackoverflow.com/questions/70851048/does-it-make-sense-to-use-conda-poetry)
- [Why you should use Poetry instead of Pip or Conda for Python Projects](https://blogs.sap.com/2022/05/08/why-you-should-use-poetry-instead-of-pip-or-conda-for-python-projects/)
- [Poetry installed but `poetry: command not found`](https://stackoverflow.com/questions/70003829/poetry-installed-but-poetry-command-not-found)
- [How to manage Python projects with Poetry](https://www.infoworld.com/article/3527850/how-to-manage-python-projects-with-poetry.html)
***
