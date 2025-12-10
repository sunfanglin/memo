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

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzkxNzQwNzc4LC0xNjA0Njc0MjI0XX0=
-->