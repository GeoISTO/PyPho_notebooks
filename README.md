# PyPho_notebooks
Notebooks to illustrate [PyPho](https://github.com/GeoISTO/PyPho) usage and make it easier to use without install.

## Notebooks

### Running the notebooks online

#### Binder

The notebooks can be used directly online without installation thanks to [Binder](https://mybinder.org/).

Notebooks:
1. Minimal Example: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/GeoISTO/PyPho_notebooks/HEAD?urlpath=%2Fdoc%2Ftree%2F01_minimal+example.ipynb)

#### Devnotes:
* trying to make a repo from [cookiecutter](https://github.com/cookiecutter/cookiecutter) and [pyvsita cookie cutter](https://github.com/pyvista/cookiecutter-pyvista-binder?tab=readme-ov-file)
* may have to make a binder folder with proper requirements

1. go to folder ```cd where_to_crete_repo```
1. New env ```conda create -n pypho_binder python=3.12 pipx```
1. activate ```conda activate pypho_binder```
5. add path to git: ```set PATH=%PATH%;Path_to_Git\Git\bin```
5. run the cookiecutter ```pipx run cookiecutter gh:pyvista/cookiecutter-pyvista-binder```
6. Publish the created repo to Github

### Running the notebooks on your computer

The folder [notebooks/](./notebooks/) provides Jupyter notebooks to showcase the available tools in [PyPho](https://github.com/GeoISTO/PyPho).  
To make your own tests while making sure the notebooks work you can duplicate the proposed notebooks in the same folder.  
**Dev Note:** To avoid versionning the test notebooks, please have their name match: ```*-local.ipynb```

For the Notebooks to work, you'll need to install pypho with the *[nb]* option (this principally install jupyter along with the other dependencies).
1. **[optional] Install [Miniforge](https://github.com/conda-forge/miniforge)** This will setup **conda** for managing environments and point only to *conda-forge*
1. **[optional, but recommended] Create and environment**, for example with conda, adapt the python version:
    ```
    conda create -c conda-forge -n pypho_nb python=3.12
    ```
2. **[If working with an environment] Activate the environment**:
    ```
    conda activate pypho_nb
    ```
3. **Install PyPho**:
    ```
    python -m pip install pypho[nb]
    ```

## Development

### Remove local information from the versionning

`.gitattributes` is setting up a `jq` filter `nbstrip` to remove metadata and execution counts from notebooks before commit.

To be effective, you must add the following piece of script in the .git/config:

	[filter "nbstrip"]
	clean = "jq --indent 1 \
			'(.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
			| .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
			| .cells[].metadata = {} \
			'"
