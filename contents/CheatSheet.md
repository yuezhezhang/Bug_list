## Resources
* [Conda cheat sheet](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)
* [Pip cheat sheet](https://opensource.com/sites/default/files/gated-content/cheat_sheet_pip.pdf)

## Conda Common Commands

| Meaning | Command |
| :--     | :--     |
| Disable default activate | `conda config --set auto_activate_base false`|
| Create env named robot | `conda create --name robot` or `-n`|
| Activate the env | `conda activate robot` |
| Deactivate the current env | `conda deactivate`         |
| Verify conda installed  | `conda info` |
| Update conda to the current version | `conda update conda` |
| Search for a package | `conda search PACKAGENAME` |
| Install a package | `conda install pip` |
| Install a package from a specific channel | `conda install --channel conda-forge boltons` |
| Update a package | `conda update PACKAGENAME`        |
| Check which python  | `which python`    |
| Show python version | `python --version` |
| Check which pip | `which pip` |
| List installed packages in current env  | `conda list` |
| Save env to a text file|  `conda list --explicit > robot.txt` or `conda env export > environment.yml` |
| List all the envs   | `conda env list`   |
| Create env from a text file | `conda env create --file robot.txt` or `-f`|
| Delete an env and everything | `conda env remove --name robot`        |
| Remove one or more packages from a env| `conda remove --name robot toolz boltons` |

## Pip Common Commands
| Meaning | Command |
| :--     | :--     |
| Install package from PyPI | `pip install PACKAGENAME`|
| Install package in China | `pip install PACKAGENAME -i https://pypi.tuna.tsinghua.edu.cn/simple` |
| Install package with specific version| `pip install PACKAGENAME==2.22.0` |
| Install package within range| `pip install PACKAGENAME>=2.22.0, <3` |
| Show details of installed package| `pip show PACKAGENAME` |
| List installed packages | `pip list` or `pip freeze`|
| Sava packages in a text file| `pip freeze > requirements.txt`|
| Install packages from a text file| `pip install -r requirements.txt` |

## Apt install
* `apt-get install` for system-wide package install
* `conda install` for current env install
* Not everything available in `apt-get install` is available in `conda install`
* `apt list --installed` lists all the packages installed using apt
* `dpkg -L package_name` checks the path for the installed package
* `dpkg -l package_name` checks the version for the installed package

## Q&A
### 1. [Using pip to install packages to conda environment](https://stackoverflow.com/questions/41060382/using-pip-to-install-packages-to-anaconda-environment)
* `conda create --name env_name`
  * Double check the dependency of python when creating the env from `environment.yml`, pip may inherit packages from other env
* `conda activate env_name`
* `conda install pip`
* `which -a pip`
* `pip install package_name` or `/anaconda/envs/venv_name/bin/pip install package_name`

### 2. [Build the package](https://packaging.python.org/en/latest/tutorials/packaging-projects/)
* [short tutorial](https://medium.com/@codebyteexplorer/build-your-first-python-package-with-pyproject-toml-19e2119edbca)
* Create `pyproject.toml`
* Put `__init__.py` to mark the directory as a package
* `python install -e.`
