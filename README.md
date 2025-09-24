# PyPho_notebooks
Notebooks to illustrate [PyPho](https://github.com/GeoISTO/PyPho) usage and make it easier to use without install.

## Notebooks

### Running the notebooks online

The notebooks can be used directly online without installation thanks to [Binder](https://mybinder.org/). 
See instructions in the dedicated repository: [PyPho on Binder](https://github.com/GeoISTO/PyPho_binder?tab=readme-ov-file#notebooks-on-binder)


### Running the notebooks on your computer

The folder [notebooks/](./notebooks/) contains Jupyter notebooks to showcase the available tools in [PyPho](https://github.com/GeoISTO/PyPho).  
You can either download the notebooks you want or completely clone the repository. 
To make your own tests while making sure the notebooks work you can duplicate the proposed notebooks in the same folder.  
**Dev Note:** To avoid versionning the test notebooks, please have their name match: ```*-local.ipynb```

### Installation
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

## Licences

The notebooks are under the [CeCILL-B licence](./Licence_CeCILL-B_V1-en.txt)

The datasets are under CC-BY 4.0 licence (see [datasets/dataset_licence.txt](datasets/dataset_licence.txt)) with attribution to Gautier LAURENT (2025)
ISTO, UMR 7327, Univ Orléans, CNRS, BRGM, OSUC, F-45071 Orléans, France

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
