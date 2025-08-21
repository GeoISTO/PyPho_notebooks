# PyPho_notebooks
Notebooks to illustrate [PyPho](https://github.com/GeoISTO/PyPho) usage and make it easier to use without install.

## Notebooks

### Running the notebooks online

The notebooks can be used directly online without installation.\
This is achieved through nbviewer.

Notebooks:

### Running the notebooks on your computer

The folder [notebooks/](./notebooks/) provides Jupyter notebooks to showcase the available tools in [PyPho](https://github.com/GeoISTO/PyPho).  
To make your own tests while making sure the notebooks work you can duplicate the proposed notebooks in the same folder.  
**Dev Note:** To avoid versionning the test notebooks, please have their name match: ```*-local.ipynb```

For the Notebooks to work, you'll need to install pypho with the *[nb]* option (this principally install jupyter along with the other dependencies).
1. **[optional, but recommended] Create and environment**, for example with conda, adapt the python version:
    ```
    conda create -c conda-forge -n pypho_nb python=3.11
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
