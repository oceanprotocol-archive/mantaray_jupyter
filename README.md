# mantaray_jupyter
The target for the [Mantaray IPython scripts](https://github.com/oceanprotocol/mantaray/tree/develop/ipython_scripts), converted to Jupyter Notebook format. 

This repo is git-cloned into a running jupyter hub notebook instance. 

Jupyter notebooks are automatically created by a Travis deployment triggered from [mantaray](https://github.com/oceanprotocol/mantaray). 

The repo relies on a utilities library which is cloned and pip-installed into the virtual environment. This allows devevelopment in the source repo (mantaray) and testing in the deployed notebooks (which have a different path and environment). This sub-package is found in the `utilities_subpackage` folder, and is called `mantaray_utilities`.
