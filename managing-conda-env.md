## How to Manage `conda` environments

Open the `miniconda` or `Anaconda` shell prompt. The first step is to configure `conda-forge` as the default package channel by the following commands in the shell.


```
(base) $ conda config --add channels conda-forge
(base) $ conda config --set channel_priority strict
```

Then create a new conda environment,

```
(base) $ conda create -y -n env-name python=3.10
```

where `env-name` is an arbitrary environment name.

After the installation completes, activate the environment with `conda activate`:

```
(base) $ conda activate env-name
(env-name) $
```

To install the necessary packages into this environment,

```
(env-name) $ conda install -y pandas jupyter matplotlib
```

To update a package

```
(env-name) $ conda update pkg-name
```

Again to deactivate this environment,

```
(base) $ conda deactivate env-name
```


To check the info about `conda`

```
(base) $ conda info
```


To list all the conda environments

```
(base) $ conda info --envs
```

To check the installed pacakges in a conda environment,

```
(base) $ conda list -n env-name
```

### Will the `prefix` field cause any problem when environment is created from the yaml file in a different platform?

Ans: Short answer is **No**. For details see [here](https://stackoverflow.com/questions/41274007/anaconda-export-environment-file)

To create a new environment in a subdirectory of the current working directory called `envs`.

```
conda create --prefix ./envs jupyterlab=3.2 matplotlib=3.5 numpy=1.21
```

for details [see here](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#specifying-a-location-for-an-environment).
