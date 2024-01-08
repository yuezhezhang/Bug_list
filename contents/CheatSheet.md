## Resources
* [Conda cheat sheet](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)
* [Pip cheat sheet](https://opensource.com/sites/default/files/gated-content/cheat_sheet_pip.pdf)

## Conda Common Commands

| Meaning | Command |
| :--     | :--     |
| Create env named robot | `conda create --name robot`|
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
| Save env to a text file|  `conda list --explicit > robot.txt`  |
| List all the envs   | `conda env list`   |
| Create env from a text file | `conda env create --file robot.txt` |
| Delete an env and everything | `conda env remove --name robot`        |
| Remove one or more packages from a env| `conda remove --name robot toolz boltons` |
