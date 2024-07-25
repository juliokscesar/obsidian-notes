# Python Virtual Environments
Python venvs (virtual environments) makes it easy to manage separate package installations for different projects. It creates a "virtual" isolated Python installation. Every package in the virtual environment can be installed only there and not interfere with the "base" environment (the global system environment).

It is not supposed to be portable since we just carry all the packages used in a `requirements.txt` file and then just recreate it when using the project in another system.

Python venv can be created with a simple command:
```shell
python3 -m venv .venv
```
this creates a ".venv" folder inside the project's folder. This folder should be excluded from any repositories (such as using a .gitignore). Then we activate it to make sure that the virtual-environment specific python binaries (such as `python` interpreter and `pip` executable will be put there and then be used:
```shell
source .venv/bin/activate
# and confirm with:
which python
```
While venv is activated, pip will install packages into that specific environment.
To deactivate the venv, just call
```shell
deactivate
```

Everything can be found [here](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments)

## Conda
[Getting Started](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)
Conda is a command line tool for package and environment management that has big advantages over only using python's pip:
Conda can deal with requirement packages *outside* of python packages, while pip only deals with python-specific packages (that includes a "setup.py"). Including packages that includes softwares written in any other language not necessarily Python.
### Anaconda and Miniconda
Anaconda is a GUI tool that already includes a bunch more packages (including conda, numpy, scipy, ipython notebook, etc) and allowsto use conda without having to run commands on the command line.

Conda itself is not a binary command, it is a Python package. To make conda work, it is needed to create a Python environment and install package `conda` into it.

Miniconda is a package that only install conda and its dependencies. Arch [Conda Wiki Page](https://wiki.archlinux.org/title/Conda) explains everything.
In my endeavourOS system, I'm installing [miniconda3](https://aur.archlinux.org/packages/miniconda3) aur package.

# YOLOv5
"You-Only-Look-Once"
A object detection algorithm. It comes with pre trained models and can be fine-tuned with custom datasets.
It is a python open-source package and can be found [here](https://github.com/ultralytics/yolov5).

From the [documentation](https://docs.ultralytics.com/yolov5/), YOLOv5 is an object detection model designed to deliver high-speed, high-accuracy results in real-time.

It is built on PyTorch (a machine learning library based on the Torch library for C++).

