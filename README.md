# Intro to python for data analysis

Welcome to this intro workshop. Please read the following instructions carefully - ask a demonstrator if something is not working for you.

## Intro slides

https://docs.google.com/presentation/d/1sI9aAuMo_I0bShzbD1BG-Ia-Qk7dK841DU5MuXNdxVM/edit?usp=sharing

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
# load the completed cells from a previous workshop
git checkout rm-2019-11-session1
```

### Installing dependencies

You have two options here - `miniconda` or `virtualenv`. Choose your favourite.

#### (with miniconda)

2a) we will now setup a python environment on the server. There are lots of ways to do this - one is to use `miniconda`. Run the following commands:

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

#### (with virtualenv)

2b) Instructions for using `virtualenv` are as follows:

```
# from inside the python-workshop folder
module load python/3.8.<TAB> # hit tab here to autocomplete to the latest available 3.8 version, then press enter. 3.8.2 at the time of writing
# the last argument here is a name for the folder which will hold all the virtualenv files
# it can be anything e.g. `mycoolvenvname`, but we'll use `venv`
python3 -m venv venv
# the next line is important - it sets up all the paths
# You will need to rerun this each time you log in to the server
# Notice that venv/bin/activate is a bash script, in the local folder
source venv/bin/activate
```

3) we are now ready to install the python dependencies for this project

```
pip install -r requirements.txt
```

### Viewing Notebooks - Option 1 - Running the notebooks via a terminal

4a) We also need to install the following package as well

```
pip install euporie
```

This lets us view/run the notebooks without needing to setup [SSH tunneling](https://github.com/aim-qmul/python-workshop/blob/master/SSH-for-AIM.md). Type `euporie 02<TAB>` to autocomplete the notebook name, then hit enter. The instructions for using euporie can be found at https://github.com/joouha/euporie#key-bindings

### Viewing Notebooks - Option 2 - Running the notebooks in a browser

4b) From inside the `python-workshop` folder, run:

```
jupyter notebook
```

It should print out some messages with a section that says:

```
Or copy and paste one of these URLs:
        http://localhost:8888/?token=ed355834fbd<rest of a token here>
     or http://127.0.0.1:8888/?token=ed355834fbd<rest of a token here>
```

Do as it says and copy one of those into your web browser. It won't work until we complete the next step.

- Open a new terminal window and run the following command to setup an [SSH tunnel](https://github.com/aim-qmul/python-workshop/blob/master/SSH-for-AIM.md) (assuming you are on a Mac or Linux) - *NB Remember to replace jxr01 with your username*:

```
ssh -J jxr01@frank.eecs.qmul.ac.uk jxr01@bibury.eecs.qmul.ac.uk -NL 8888:localhost:8888
```

This won't produce any output and will appear to hang. Don't worry. If you see an error, make sure nothing else is running locally on port 8888. Also make sure you have your ssh keys set up[^1].

- Go back to the browser window from the previous step and refresh the page

[^1]: `ssh-add -L` will show what is currently in your ssh keychain. If it is empty, you probably need to run `ssh-add -K ~/.ssh/id_rsa`

## (Optional) Running locally

- Download the files for this workshop by clicking on the green "clone or download" button, then "Download ZIP", and unzip. Alternatively, clone the repo.
- Start by following the first few notebooks online (here on GitHub), until you'll have your python environment ready.
- After that, from the command line, activate your virtual environment, run `jupyter notebook` and follow along.

## Books and resources

### If Python is your first programming language

* The Quick Python Book 

Aimed at programmers who are new to python

### If you already know another programming language well

* Python for Data Analysis - Wes Mckinney

Beginner-intermediate level book for manipulating and analysing data with Pandas

* Thinking in Python - Bruce Eckel

More advanced python programming and design paradigms. A software engineering perspective. Very useful for writing good, clean python code and maintaining larger software projects.

* [Understanding all of Python, through its builtins](https://sadh.life/post/builtins)

The whole language, explained, in a single page. Whats not to like?

### Other useful links

* [The Zen of Python](https://www.python.org/dev/peps/pep-0020/)
* [Matplot lib for papers](https://github.com/jbmouret/matplotlib_for_papers)
* [Numpy tutorial](https://cs231n.github.io/python-numpy-tutorial/)
* [Intro to types with Python](https://auth0.com/blog/typing-in-python/)
* [Pandas tutorials](https://pandas.pydata.org/pandas-docs/dev/getting_started/tutorials.html)
