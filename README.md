# Rapids Single Cell Comparison 

## Description
Comparison of `singlecell-rapids` and `scanpy` for single-cell RNA-seq data analysis


## Container information
| | |
| :--------------: | :------------- |
| **URL/repo** | https://github.com/scverse/rapids_singlecell |
| **URL/docerfile** | https://github.com/cellgeni/dockage/blob/master/rapids-singlecell/Dockerfile_0.14.1 |
| **URL/container** | https://quay.io/repository/cellgeni/rapids-singlecell |
| **Version** | `0.14.1` |

## Running on FARM

Create an interactive job with GPU access
```bash
bsub -Is \
    -G cellgeni \
    -q gpu-interactive \
    -n 8 -M "16GB" \
    -R "select[mem>16GB] rusage[mem=16GB]" \
    -gpu "mode=shared:j_exclusive=no:gmem=16000:num=1" \
    /bin/bash
```

Run jupyter
```bash
singularity exec \
  --bind /lustre,/nfs \
  --nv \
   /nfs/cellgeni/singularity/images/rapids-singlecell-0.14.1.sif \
  jupyter server \
	  --no-browser \
	  --ServerApp.ip=0.0.0.0 \
	  --ServerApp.port=7878 \
	  --ServerApp.allow_remote_access=True \
	  --ServerApp.allow_origin='*' \
	  --IdentityProvider.token='password'
```

Open ssh connection in separate terminal
```bash
ssh -L 7878:localhost:7878 farm22-gpu0204
```