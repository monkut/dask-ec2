# dec2

Easily launch a cluster on Amazon EC2 configured with `dask.distributed`,
Jupyter Notebooks, and Anaconda.

## Installation

You can install `dec2` and its dependencies from the
[conda-forge](https://conda-forge.github.io/>) repository using
[conda](https://www.continuum.io/downloads):

```bash
$ conda install dec2 -c conda-forge
```

You can also install `dec2` using pip:

```bash
$ pip install dec2
```

## Usage

**Note:** `dec2` uses
[`boto3`](http://boto3.readthedocs.io/en/latest/index.html) to interact with
Amazon EC2. You can configure your AWS credentials using
[Environment Variables](http://boto3.readthedocs.io/en/latest/guide/configuration.html#environment-variables)
or [Configuration Files](http://boto3.readthedocs.io/en/latest/guide/configuration.html#configuration-files).

The `dec2 up` command can be used to create and provision a cluster on Amazon EC2:

```bash
$ dec2 up --help
Usage: dec2 up [OPTIONS]

Options:
  --keyname TEXT                Keyname on EC2 console  [required]
  --keypair PATH                Path to the keypair that matches the keyname
                                [required]
  --name TEXT                   Tag name on EC2
  --region-name TEXT            AWS region  [default: us-east-1]
  --ami TEXT                    EC2 AMI  [default: ami-d05e75b8]
  --username TEXT               User to SSH to the AMI  [default: ubuntu]
  --type TEXT                   EC2 Instance Type  [default: m3.2xlarge]
  --count INTEGER               Number of nodes  [default: 4]
  --security-group TEXT         Security Group Name  [default: dec2-default]
  --volume-type TEXT            Root volume type  [default: gp2]
  --volume-size INTEGER         Root volume size (GB)  [default: 500]
  --file PATH                   File to save the metadata  [default:
                                cluster.yaml]
  --provision / --no-provision  Provision salt on the nodes  [default: True]
  --anaconda / --no-anaconda    Bootstrap anaconda  [default: True]
  --dask / --no-dask            Install Dask.Distributed in the cluster
                                [default: True]
  --notebook / --no-notebook    Start a Jupyter Notebook in the head node
                                [default: True]
  --nprocs INTEGER              Number of processes per worker  [default: 1]
  -h, --help                    Show this message and exit.
```

The minimal required arguments for the `dec2 up` command are:

```
$ dec2 up --keyname my_aws_key --keypair ~/.ssh/my_aws_key.pem
```

This will create a `cluster.yaml` in the directory that it was executed, and
this file is required to use the other commands in the CLI.

Once a cluster is running, the `dec2` command can be used to create or destroy
a cluster, ssh into nodes, or other functions:

```bash
$ dec2
Usage: dec2 [OPTIONS] COMMAND [ARGS]...

Options:
  --version   Show the version and exit.
  -h, --help  Show this message and exit.

Commands:
  anaconda          Provision anaconda
  dask-distributed  dask.distributed option
  destroy           Destroy cluster
  notebook          Provision the Jupyter notebook
  provision         Provision salt instances
  ssh               SSH to one of the node. 0-index
  up                Launch instances
```
