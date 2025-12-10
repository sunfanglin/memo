## Installation
```bash
ModuleNotFoundError: No module named 'numpy.dtypes'
(skyrim3) ⬢  fedora ➜  skyrim2 pip install "numpy>=1.26.4,<2.0" --upgrade

ModuleNotFoundError: No module named 'ruamel'
(skyrim3) ⬢  fedora ➜  skyrim2 pip install ruamel.yaml

ImportError: cannot import name 'core' from 'jax.extend' (/home/fanglin/miniforge3/envs/skyrim3/lib/python3.10/site-packages/jax/extend/__init__.py)

(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y jax jaxlib  &&
pip install "jax[cuda12]"==0.4.26 -f https://storage.googleapis.com/jax-releases/jax_releases.html

ImportError: libcudnn.so.9: cannot open shared object file: No such file or directory

(skyrim3) ⬢  fedora ➜  skyrim2 pip install jaxlib==0.4.26+cuda12.cudnn89 -f https://storage.googleapis.com/jax-releases/jax_releases.html --force-reinstall
Looking in links: https://storage.googleapis.com/jax-releases/jax_releases.html

ERROR: No matching distribution found for jaxlib==0.4.26+cuda12.cudnn89
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y jax jaxlib jax-cuda12-plugin jax-cuda12-pjrt  &&
pip install "jax[cuda12_pip]==0.4.26" -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html --force-reinstall

ImportError: libcudnn.so.9: cannot open shared object file: No such file or director
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y torch torchvision torchaudio jax jaxlib nvidia-* 2>/dev/null || true && pip install torch==2.9.1+cu121 torchvision==0.20.1+cu121 torchaudio==2.9.1+cu121 \
    --extra-index-url https://download.pytorch.org/whl/cu121 && pip install "jax==0.4.26" "jaxlib==0.4.26+cuda12.cudnn89" \
    -f https://storage.googleapis.com/jax-releases/jax_releases.html \
    --no-deps --force-reinstall && pip install "dm-haiku==0.0.12" --force-reinstall
    
ERROR: No matching distribution found for torch==2.9.1+cu121
(skyrim3) ⬢  fedora ➜  skyrim2 pip uninstall -y torch torchvision torchaudio jax jaxlib nvidia-* dm-haiku earth2mip 2>/dev/null || true
zsh: no matches found: nvidia-*
(skyrim3) ⬢  fedora ➜  skyrim2 pip cache purge
Files removed: 1858 (12281.6 MB)
(skyrim3) ⬢  fedora ➜  skyrim2 pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MTU5MDc4LC0xNjA0Njc0MjI0XX0=
-->