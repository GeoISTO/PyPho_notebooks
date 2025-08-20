# PyPho_notebooks
Notebooks to illustrate [PyPho](https://github.com/GeoISTO/PyPho) usage and make it easier to use without install.

## Notebooks

### Online use

The notebooks can be used directly online without installation.\
This is achieved through nbviewer.

Notebooks:


### Local Notebooks
The folder `notebooks/` provides Jupyter notebooks to showcase the available tools in [PyPho](https://github.com/GeoISTO/PyPho).

To make your own tests while making sure the notebooks work you can duplicate the proposed notebooks in the same folder.

To avoid versionning the test notebooks, please have their name match: *-local.ipynb

### Remove local information from the versionning

`.gitattributes` is setting up a `jq` filter `nbstrip` to remove metadata and execution counts from notebooks before commit.

To be effective, you must add the following piece of script in the .git/config:

	[filter "nbstrip"]
	clean = "jq --indent 1 \
			'(.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
			| .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
			| .cells[].metadata = {} \
			'"
