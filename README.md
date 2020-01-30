# mantaray_jupyter

The target for the [Mantaray IPython scripts](https://github.com/oceanprotocol/mantaray/tree/develop/ipython_scripts), converted to Jupyter Notebook format. 

This repo is git-cloned into a running jupyter hub notebook instance. 

Jupyter notebooks are automatically created by a Travis deployment triggered from [mantaray](https://github.com/oceanprotocol/mantaray). 

The repo relies on a utilities library which is cloned and pip-installed into the virtual environment. This allows devevelopment in the source repo (mantaray) and testing in the deployed notebooks (which have a different path and environment). This sub-package is found in the `utilities_subpackage` folder, and is called `mantaray_utilities`.


# Managing jubyter hub cluster from the command line
*All commands below alias `kubectl` to `kk`.*
*Ensure your credentials are set*
## Pods
List the pods
```
kk get pods --namespace jhub2 | awk '{print $0}' | grep jupyter
```
## PVCs
Delete Persistent Volume Claims
```
# ECHO TEST
for claim in $(kubectl --namespace=jhub2 get persistentvolumeclaims | awk 'BEGIN{} {NR>1} {print $1}' | grep -E "claim-.+"); do echo kubectl --namespace=jhub2 delete persistentvolumeclaims $claim; done

# REAL DEAL
for claim in $(kubectl --namespace=jhub2 get persistentvolumeclaims | awk 'BEGIN{} {NR>1} {print $1}' | grep -E "claim-.+"); do kubectl --namespace=jhub2 delete persistentvolumeclaims $claim; done

# REAL DEAL WITH TIMEOUT
for claim in $(kubectl --namespace=jhub2 get persistentvolumeclaims | awk 'BEGIN{} {NR>1} {print $1}' | grep -E "claim-.+"); do timeout 5 kubectl --namespace=jhub2 delete persistentvolumeclaims $claim; done
```
## Pods
Delete pods
```
# ECHO TEST
for vol in $(kubectl --namespace=jhub2 get persistentvolumes | awk '$6~the_regex {print $1}' the_regex="jhub2/claim"); do echo kubectl --namespace=jhub2 delete persistentvolumes $vol; done

# REAL DEAL
for vol in $(kubectl --namespace=jhub2 get persistentvolumes | awk '$6~the_regex {print $1}' the_regex="jhub2/claim"); do kubectl --namespace=jhub2 delete persistentvolumes $vol; done

# REAL DEAL WITH TIMEOUT
for vol in $(kubectl --namespace=jhub2 get persistentvolumes | awk '$6~the_regex {print $1}' the_regex="jhub2/claim"); do timeout 5 kubectl --namespace=jhub2 delete persistentvolumes $vol; done
```


