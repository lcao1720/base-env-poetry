## Demo of using poetry (1.8.3)

### prerequisite
```
pip install poetry
```

### 1. How to create a new project
`poetry-demo` is used as the project name here in this setup
```
poetry new poetry-demo
```
- A new folder will be created after running the first command
- Inside the folder
    - a folder with simlilar name as the project name, replacing _dash_ with _underscore_ (`poetry_demo`), and __init__.py in it
    - a `tests` folder, along with __init__.py
    - **pyporject.toml**
    - README.md
- remember to cd to the folder with `pyporject.toml` file
Note that you can also create a pyproject.toml with 
```
poetry init
```


### 2. How to specify the python version
change the python version in [pyproject.toml](pyproject.toml)
 ```
[tool.poetry.dependencies]
python = "^3.11"
```

### 3. How to install the specified python version
```
poetry install
```
You will be able to see the installed python version, virtualenv path, and [poetry.lock](poetry.lock) file, which will store all dependencies and related links from now on.

### 4. Activate/Deactivate the env
```
poetry shell
```
The current env name comes with the python version, e.g, `poetry-demo-py3.11`
In order to deactivate the env, simply use
```
exit
```
for shortcut, `ctrl+D` on Windows and `control+D` on Macbook.


### 5. Basic lookup
```
# view all envs
poetry env list

# remove existing env
poetry env remove <env_to_be_removed>
# to remove the current env without listing the env path
poetry env remove $(poetry env info --path)
```
chances are, you will see an error 


### 6. update Poetry version
```
poetry self update
```
the change will also be loaded to `.lock` file.


### 7. What if poetry uses conda env
```
poetry env info --path
```
This returns the current poetry env path. If you find poetry is not actually using proper env, or even python version (take 3.11.9 as example)
- for Macbook, install `Homebrew` first.
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- then add the following line to your shell's rc file
```
export PATH="/opt/homebrew/bin:$PATH"
```
- next, install python for the system, no need to specify patch version in the command, brew will automatically install the latest version. Similarly, if you don't specify minor version with `@3.x`, the latest (version 3.12) will be installed.
``` 
brew install python@3.11
```
- go back to [step4](#4-activatedeactivate-the-env) to complete the rest


### 8. Add packages
- Add finite packages
```
poetry add <package1> <package2>
```
- if you already have dependency list, you may also add `requirements.txt` file in the current project folder and paste the dependencies in. Then use
```
poetry self add poetry-plugin-import
poetry import
```
to import dependencies to `[tool.poetry.dependencies]` section in .toml file.

- for dev environment, add new group with poetry
```
poetry add --group dev ipdb black pre_commit setuptools
```
the list will be added to `[tool.poetry.group.dev.dependencies]`

### 9. install dependencies
```
poetry install --with dev
```
`--with` notation allows poetry to install different groups of dependencies.




