# Introduction to Hábrók

Hábrók is the current high-performance computing cluster of the RUG. It is a collection of servers with powerful CPUs and GPUs, so it can be very helpful in cases where you have to run computationally expensive or long-running programs, e.g., when training or evaluating the language models in your final project.

This document aims to give you an overview of the cluster and how to use it in the context of this course. A more comprehensive documentation of the cluster can be found [here](https://wiki.hpc.rug.nl/habrok/start).

## Getting Access

If you are using Hábrók for the first time, you must request an account first. This can be done through [IRIS](https://iris.service.rug.nl/) under *Research and Innovation Support* → *Computing and Research Support Facilities* → *Computing (Hábrók, Merlin)* → *Request Habrok account*.

You can find more information on how to get access and the usage policies of Hábrók [here](https://wiki.hpc.rug.nl/Hábrók/introduction/policies).

## Accessing the System

There are various ways to access the cluster, depending on your [operating system](https://wiki.hpc.rug.nl/Hábrók/connecting_to_the_system/connecting). However, the most basic and reliable way to connect is over the command line through SSH. If you are not familiar with it, you can find a basic tutorial on how to connect [here](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys#basic-connection-instructions) or use the command below. You will be asked to enter your password afterward.

```sh
ssh username@Hábrók.hpc.rug.nl
```

You can use the `exit` command to close your connection to the cluster.

A [Web Portal](https://portal.hpc.rug.nl/public/start.html) is also available, which you can use to carry out some basic tasks like file management.

## System Overview

The Hábrók cluster consists of a collection of powerful servers ([system specifications](https://wiki.hpc.rug.nl/Hábrók/introduction/cluster_description)), which usually can run computationally expensive operations at a much higher speed than your laptop or desktop computer. Each user has access to several different disk [storage areas](https://wiki.hpc.rug.nl/Hábrók/data_management/storage_areas) for their data. In general, the directory for your user can be found in a subfolder named after your username in each of the different areas (e.g., `/home/S123456789`).

### home

This is the main storage area you will be connected to when accessing the system. It is mainly meant to store settings, your actual program files, and smaller data sets. It is limited to 20GB of space per user and will be backed up daily.

### scratch

This system is meant to be used for more temporary data, such as caches of a preprocessed dataset or intermediate results of your scripts. It has a very large limit of 10TB of disk space, but files older than 30 days will get removed from the system.

### local

Each individual node on the cluster also has 1TB of internal disk space available. When you run a job on a node, this space will be available for you to use and can be accessed by using the environment variable `$TMPDIR` in your script. Copying your data to this space can help speed up your script if your job has to read or write data from files frequently. Keep in mind, however, that you can only use this space while your job is running. All data remaining on an individual node will be deleted after your job is finished.

> To keep track of your overall and available space on any of these areas, you can use the `pgquota` command. An example is shown [here](https://wiki.hpc.rug.nl/Hábrók/data_management/quota). Do so frequently and delete any data not needed anymore to avoid running out of space in your home directory. It usually fills up quicker than anticipated.

## Using The System

On Hábrók, you generally cannot just start your program as you would on your machine. Instead, the system works by creating a job script, which defines what scripts and commands to run and in which configuration. Once you submit a job, it is copied over to one of the servers in the cluster, which will run your previously defined script.

However, before you can submit a job, you first need to get your code onto the cluster. The easiest way to do that is to clone your files from a git repository like you would when working locally on your machine. Files that are too big to be uploaded to Git can either be downloaded directly to the system as part of the workflow in your code or, alternatively, be copied over manually beforehand. To do that, a free FTP client like [Filezilla](https://filezilla-project.org/) is a good option. However, multiple other ways are available to copy data to the cluster, which are outlined [here](https://wiki.hpc.rug.nl/Hábrók/data_management/transferring_data). Make sure to copy or download the data to a fitting storage area, as the space in your `/home` directory is relatively limited.

For all subsequent chapters, we assume you are using Python, as this is the language you will most likely use for your final project. Information specific to other languages can be found [here](https://wiki.hpc.rug.nl/Hábrók/examples/start).

### Configuring the Environment

#### Modules

Another important thing to take care of before you start a job on Hábrók is to ensure all necessary requirements, such as libraries your project depends on, are installed and configured. On Hábrók, a lot of software is available in optimized versions through so-called *modules*, which need to be enabled first to access their functionality.

> In general, it is always better to load one of the preconfigured modules for any package you might need, as those have been optimized for use on the cluster and can bring some serious performance improvements over using the same package downloaded from the internet.

To find out if a module for a certain package is available, you can use the `module avail` command. For example, to look for the available modules for PyTorch, you can run:

```sh
module avail pytorch
```

This will give you the following output:

```sh
---------------------------------- /cvmfs/hpc.rug.nl/versions/2023.01/rocky8/x86_64/amd/zen3/modules/ai -----------------------------------
   PyTorch/1.12.0-foss-2022a-CUDA-11.7.0    PyTorch/1.12.1-foss-2022a-CUDA-11.7.0    PyTorch/2.1.2-foss-2022b (D)

  Where:
   D:  Default Module

If the avail list is too long consider trying:

"module --default avail" or "ml -d av" to just list the default modules.
"module overview" or "ml ov" to display the number of modules for each name.

Use "module spider" to find all possible modules and extensions.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".
```

As you can see, there are multiple versions of PyTorch available that have been optimized for use on the cluster. If you want to know in more detail what the naming of the different modules means, you can find additional information [here](https://wiki.hpc.rug.nl/Hábrók/software_environment/toolchains). Generally speaking, though, you should try to use modules with the same suffix (e.g., `fosscuda-2020b` here), as those will usually be compatible with each other.

After having found the modules that you want to use, you can load them with the `module load` command as follows:

```sh
module load PyTorch/2.1.2-foss-2022b
```

Finally, to clear all loaded modules, e.g., when you want to switch to a different project, you can run the `module purge` command. Additional information on how to work with modules can be found [here](https://wiki.hpc.rug.nl/Hábrók/software_environment/module_system).

#### Virtual Environments

Another essential step in configuring your environment is to create a virtual environment, as that will ensure that your dependencies are installed in an isolated place and will be shared across the different nodes and job runs. The best place to install these dependencies is usually on the `/home` directory.

To create a virtual environment, you must first load a module with a version of Python. In this case, we load the latest version of python available on Hábrók:

```sh
module load Python/3.8.6-GCCcore-10.2.0
```

> Since the latest available version of Python is 3.8.6, you need to ensure that you are not using any features that have only been introduced in later versions of Python, as you might run into errors otherwise. Usually, this is not too big of an issue, as the most common functions are all available in Python 3.8, but it can save you the occasional headache when debugging your code.

Now you can create your virtual environment with the following command:

```sh
python3 -m venv /home3/$USER/.envs/my_env
```

This tells Python to create the new environment within the `/home3` space in your user directory (retrieved through the `$USER` variable) in a folder called `/.envs`. You can replace the last part with a more descriptive name for your project. Generally, it is recommended to have a separate virtual environment per project, but you could, in theory, also just create one environment which you will use for all of your projects.

Afterwards, you should activate your new environment by running

```sh
source /home3/$USER/.envs/my_env/bin/activate
```

You can now start installing your dependencies. As a first step, it is usually good to update some of the standard packages used to install other packages by running

```sh
pip install --upgrade pip
pip install --upgrade wheel
```

⚠️ Before you start installing any other dependencies, you should load any available modules you plan to use, as that will prevent python from installing different versions of the packages already provided through the module. A common case for the final project would be to e.g. load the latest version of the PyTorch module by running

```sh
module load PyTorch/2.1.2-foss-2022b
```

After that has been done, install all your other dependencies as usual, either directly (`pip install package_name`) or from a requirements file (`pip install -r requirements.txt`).

More information about installing packages for Python can be found [here](https://wiki.hpc.rug.nl/Hábrók/software_environment/installation_of_extra_applications_or_libraries) and [here](https://wiki.hpc.rug.nl/Hábrók/examples/python).

### Running a Job

After your environment has been set up and you downloaded your code from Git, it is time to configure and run a job. To do that, you need to define a jobscript, which will tell the system what code to run and what hardware you want to run it on. While that might sound complicated, a jobscript is simply a file containing some configuration and the commands to load your environment and start your script. A simple example could look something like this:

```sh
#!/bin/bash
#SBATCH --time=00:01:00
#SBATCH --partition=regular

# ensure that there are now left-over modules loaded from previous jobs
module purge

#load the python module
module load Python/3.8.6-GCCcore-10.2.0

# load your previously created virtual environment
source /home3/$USER/.envs/my_env/bin/activate

# make sure to load all needed modules after activating your virtual environment now
# this ensures that all the dependencies are loaded correctly inside the environment
module load PyTorch/2.1.2-foss-2022b

# start your program
python3 main.py
```

You can start the job with the command `sbatch jobscript.sh` where `jobscript.sh` is the name of your jobscript file. This will then start a job with a time limit of 1 minute on any available node. When starting the job, you will be given a jobID, which you can use to get further information about it later by using the `jobinfo` command followed by the jobID. In most cases, however, your job will not start running immediately. In the case that all nodes are currently in use, Hábrók uses a priority-based scheduling system to determine which jobs to run next. The exact formula can be found [here](https://wiki.hpc.rug.nl/Hábrók/advanced_job_management/job_prioritization), but in general, your job will be given less priority the longer it runs and the more restrictions it has on the hardware it should run on (e.g. a 2-day job requesting 12 CPU cores will have a lower priority than a single-core job that only runs for 30 minutes). It might therefore take a few hours before your job will actually start.

> Usually, the system is a lot less busy during the night. Use this to your advantage by submitting your long-running jobs in the evening so that you will be able to see the results in the next morning and do not waste time with waiting.

When your job has started running, all its outputs will be written to an output file located in the directory where your job has been started from. The name of this file is, by default, `slurm-jobID.out`. You can write all contents of this file to the command line after your job has finished by using the command `cat slurm-jobID.out` or view the real-time output while the job is still running (similar to a command line output on your machine) by using the following command

```sh
tail -n 10 -f slurm-jobID.out
```

### Job Configuration

There are many configuration options available to define exactly how your job should be run on the cluster. All of them need to be defined using the `#SBATCH --command=` syntax shown above. The probably most important one of those options is the `--time` option shown above since it defines the maximum time your job will be allowed to run after it has been started. **Even if your job is not yet finished, it will be canceled when that time runs out.** However, since longer jobs will be given less priority, try to set this to a limit that is only marginally higher than the runtime you expect for your program. A complete overview of the syntax for this command can be found [here](https://wiki.hpc.rug.nl/Hábrók/job_management/scheduling_system#time).

> If you cannot yet estimate how long your script will run, but you expect it to run for a longer time, it is often a good idea to initially set the time parameter to a high value such as a full day (`#SBATCH --time=24:00:00`) and adjust it to a more realistic value after it has run at least once and you can roughly estimate the actual runtime.

Another important command is the `partition` to use for the job, which defines the overall type of resources available to it. Each partition gives you access to different hardware types and has different time limits. An overview can be found [here](https://wiki.hpc.rug.nl/habrok/job_management/partitions).

There are also commands available to specify the number of requested nodes (`--nodes`), tasks (`--ntasks`), if your script should start multiple tasks in parallel, CPU cores (`--cpus-per-task`), and memory (either `--mem` or `--mem-per-cpu`). Remember that increasing those values over their standard definition will lower the priority of your job.

> ⚠️: Only request multiple nodes or CPU cores if you know that your program can utilize them. Otherwise, you will just be wasting resources without any additional performance benefit. When in doubt, always try to increase the number of CPU cores that your script uses first (i.e., multiprocessing/multithreading) since this is usually significantly easier to achieve than increasing the number of physical nodes (i.e., distributed processing)

Lastly, there are several configuration options available that will allow you to get a better overview of your submitted jobs. `--job-name` enables you to specify a custom name for your job, and `--output` allows you to give a custom name to the job output file. `--mail-user` and `--mail-type` enable you to specify an email address and events you want to be notified about, such as when your job has started, ended, or failed.

A more comprehensive overview of available configuration options can be found [here](https://wiki.hpc.rug.nl/Hábrók/job_management/scheduling_system#job_scripts).

Finally, let's insert some of those additional commands into the previously created job script:

```sh
#!/bin/bash
#SBATCH --time=02:00:00
#SBATCH --partition=regular
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=6
#SBATCH --mem=16GB
#SBATCH --job-name=simple_job
#SBATCH --mail-type=ALL
#SBATCH --mail-user=s.tudent@student.rug.nl

# ensure that there are now left-over modules loaded from previous jobs
module purge

#load the python module
module load Python/3.8.6-GCCcore-10.2.0

# load your previously created virtual environment
source /home3/$USER/.envs/my_env/bin/activate

# make sure to load all needed modules after activating your virtual environment now
# this ensures that all the dependencies are loaded correctly inside the environment
module load PyTorch/2.1.2-foss-2022b

# start your program
python3 main.py
```

### Running a Job on a GPU Node

When using Hábrók in the context of this course, you will likely want to use a node with a GPU to take advantage of the faster training and inference times this can give you compared to using your machine. The Hábrók cluster has [two types](https://wiki.hpc.rug.nl/Hábrók/advanced_job_management/running_jobs_on_gpus#different_gpu_nodes) of high-performance GPUs available. To be able to utilize them, you will have to slightly modify your jobscript to run on the GPU partition (`--partition=gpu`) and specify how many GPUs you want to use (`--gres=gpu:1`).

> ⚠️: Note that unless you know how to set up your scripts to utilize more than one GPU located on different devices, you should generally not request more than one GPU at a time.

You can also specify to use only a specific type of GPU, such as the more powerful Nvidia V100, by modifying the option above: `--gres=gpu:v100:1`

Whenever you run a job on a GPU node, you will always block the entire node for yourself. You can, therefore, generally request all the available resources of this one node without any penalty in prioritization (`--cpus-per-task=12`and `--mem=120GB`). An optimized job script for a GPU job would therefore look something like the following:

```sh
#!/bin/bash
#SBATCH --time=12:00:00
#SBATCH --partition=gpu
#SBATCH --gres=gpu:v100:1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=12
#SBATCH --mem=120GB
#SBATCH --job-name=simple_job
#SBATCH --mail-type=ALL
#SBATCH --mail-user=s.tudent@student.rug.nl

# ensure that there are now left-over modules loaded from previous jobs
module purge

#load the python module
module load Python/3.8.6-GCCcore-10.2.0

# load your previously created virtual environment
source /home3/$USER/.envs/my_env/bin/activate

# make sure to load all needed modules after activating your virtual environment now
# this ensures that all the dependencies are loaded correctly inside the environment
module load PyTorch/2.1.2-foss-2022b

# move cached datasets to the /scratch directory
export HF_DATASETS_CACHE="/scratch/$USER/.cache/huggingface/datasets"

# move downloaded models and tokenizers to the /scratch directory
export TRANSFORMERS_CACHE="/scratch/$USER/.cache/huggingface/hub"

# start your program
python3 main.py
```

As you can see, we also specified a few additional commands in the jobscript, which are specific to using the 🤗 [transformers](https://huggingface.co/docs/transformers/index) and [datasets](https://huggingface.co/docs/datasets/index) libraries. Setting those variables before starting your main program will tell the libraries to use the `/scratch` area to save all cached versions of your downloaded and modified datasets, models, and tokenizers, ensuring that those will not take up any of the limited space in your `/home` directory. The 🤗 libraries will use those cached versions whenever possible, speeding up your processing time by not having to re-download and process them every time you run your script.

## Useful CLI Commands

If you do not have much experience working with the command line, it may seem overwhelming initially, but luckily, the basics can be mastered quickly. This is an overview of the most common and useful commands you will need when working on the cluster:

| `ls` | This will show you all files and folders in the current directory|
|------|------------------------------------------------------------------|
| `cd` | Use this command to navigate through the folder hierarchy e.g. by writing `cd ./folder` to navigate into a subfolder. The special command `cd ..` will move up one level in the hierarchy, while the command `cd .` refers to the current directory.
| `mkdir` | This will create a new subfolder in the current directory|
| `rm` | This will remove a file in the current directory. Use `rm -r` to remove a folder and all of its contents|
| `cat`| This will print all lines in a file to the console. Very useful to quickly check the configuration of a job script or view the outputs of a finished job|
| `tail`| This will print the last 5 lines of a file. Use the `-n` parameter to increase the number of lines and the `-f` to get a real-time view of lines as they are printed to the file|

While these commands hopefully give you a good start on how to work on the command line, the Hábrók documentation also has a more comprehensive tutorial about working on the command line ([part1](https://wiki.hpc.rug.nl/Hábrók/command_line/working_on_the_command_line_-_part_1) and [part2](https://wiki.hpc.rug.nl/Hábrók/command_line/working_on_the_command_line_-_part_2)).
