# Intro to python for data analysis

Welcome to this intro workshop. Please read the following instructions carefully - ask a demonstrator if something is not working for you.

## (Recommended) Running on the AIM servers

1) Run the following commands, one line at a time. Lines beginning with `#` are comments to explain what is going on.

```
# Assuming you have ssh aliases setup already
ssh bibury
# navigate to your home directory
cd ~
# clone this repo
git clone https://github.com/aim-qmul/python-workshop.git
# cd into the new folder
cd python-workshop
```

2) we will now setup a python environment on the server. There are lots of ways to do this but the easiest is to use `miniconda`. Run the following commands:

```
# load the miniconda module
# you might need to run `module unload python/3.x.x` first
module load miniconda
# create a new conda environment
conda create --name python-workshop python=3.8
# this line is needed to get things working on the AIM servers
source /import/linux/miniconda/3/4.7.12/etc/profile.d/conda.sh
# finally, activate the conda environment
conda activate python-workshop
```

You should see the bash prompt has changed to

```
(python-workshop) -bash-4.2$
```

3) we are now ready to install the python dependencies for this project

```
pip install -r requirements.txt
```

- We also need to install the following package as well

```
pip install euporie
```

This lets us view/run the notebooks without needing to setup SSH tunneling. Type `euporie 02<TAB>` to autocomplete the notebook name, then hit enter. The instructions for using euporie can be found at https://github.com/joouha/euporie#key-bindings


## (Optional) Running locally

- Download the files for this workshop by clicking on the green "clone or download" button, then "Download ZIP", and unzip. Alternatively, clone the repo.
- Start by following the first few notebooks online (here on GitHub), until you'll have your python environment ready.
- After that, from the command line, activate your virtual environment, run `jupyter notebook` and follow along.
