## Installation
- ModuleNotFoundError: No module named 'numpy.dtypes'
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip install "numpy>=1.26.4,<2.0" --upgrade
```
- ModuleNotFoundError: No module named 'ruamel'
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip install ruamel.yaml
```
- ImportError: cannot import name 'core' from 'jax.extend' (/home/fanglin/miniforge3/envs/skyrim3/lib/python3.10/site-packages/jax/extend/__init__.py)
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y jax jaxlib  &&
pip install "jax[cuda12]"==0.4.26 -f https://storage.googleapis.com/jax-releases/jax_releases.html
```
- ImportError: libcudnn.so.9: cannot open shared object file: No such file or directory
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip install jaxlib==0.4.26+cuda12.cudnn89 -f https://storage.googleapis.com/jax-releases/jax_releases.html --force-reinstall
Looking in links: https://storage.googleapis.com/jax-releases/jax_releases.html
```
- ERROR: No matching distribution found for jaxlib==0.4.26+cuda12.cudnn89
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y jax jaxlib jax-cuda12-plugin jax-cuda12-pjrt  &&
pip install "jax[cuda12_pip]==0.4.26" -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html --force-reinstall
```
- ImportError: libcudnn.so.9: cannot open shared object file: No such file or director
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y torch torchvision torchaudio jax jaxlib nvidia-* 2>/dev/null || true && pip install torch==2.9.1+cu121 torchvision==0.20.1+cu121 torchaudio==2.9.1+cu121 \
    --extra-index-url https://download.pytorch.org/whl/cu121 && pip install "jax==0.4.26" "jaxlib==0.4.26+cuda12.cudnn89" \
    -f https://storage.googleapis.com/jax-releases/jax_releases.html \
    --no-deps --force-reinstall && pip install "dm-haiku==0.0.12" --force-reinstall
```    
- ERROR: No matching distribution found for torch==2.9.1+cu121
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y torch torchvision torchaudio jax jaxlib nvidia-* dm-haiku earth2mip 2>/dev/null || true
(skyrim3) ⬢  fedora ➜  skyrim2 pip cache purge
(skyrim3) ⬢  fedora ➜  skyrim2 pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
(skyrim3) ⬢  fedora ➜  skyrim2 pip install "jax[cuda12]"==0.4.26 -f https://storage.googleapis.com/jax-releases/jax_releases.html --force-reinstall --no-deps
```
- AttributeError: module 'jax.extend.core' has no attribute 'JaxprEqn'
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip install "dm-haiku==0.0.12" --force-reinstall
```
-AttributeError: module 'jax.interpreters.xla' has no attribute 'xe'
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip install --upgrade "dm-haiku>=0.0.13" --force-reinstall
```
- jaxlib._jax.XlaRuntimeError: INVALID_ARGUMENT: DLPack tensor is on GPU, but no GPU backend was provided.
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y jax jaxlib jax-cuda12-plugin jax-cuda12-pjrt  &&
pip install "jax[cuda12]"==0.4.32 -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html --force-reinstall --no-cache-dir
```
- ERROR: No matching distribution found for jaxlib<=0.4.32,>=0.4.32
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y jax jaxlib jax-cuda12-plugin jax-cuda12-pjrt dm-haiku flax && pip install --upgrade jax jaxlib "jax-cuda12-plugin[with-cuda]" jax-cuda12-pjrt
```
- ModuleNotFoundError: No module named 'haiku'
```bash
(skyrim3) ⬢  fedora ➜  skyrim2 pip install --upgrade dm-haiku flax
```
## Modified files
```bash
cp ./modified/graphcast.py /home/fanglin/miniforge3/envs/skyrim3/lib/python3.10/site-packages/earth2mip/networks/graphcast.py
cp ./modified/casting.py /home/fanglin/miniforge3/envs/skyrim3/lib/python3.10/site-packages/graphcast/casting.py
cp ./modified/common.py ~/miniforge3/envs/skyrim3/lib/python3.10/site-packages/skyrim/common.py
```
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTg4NDQwNjAsMTEwMDI2MDMwNiwtNz
IzNTY0ODA3LC0xNjA0Njc0MjI0XX0=
-->