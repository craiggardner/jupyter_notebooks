# jupyter notebooks for HPC MPI
I've needed a crash course in JupyterHub and Notebooks as I've tried to use them in an HPC environment.  I know
quite a bit about HPC, but I'm not a data scientist.  A colleague introduced my Jupyter, and I've enjoyed learning
to use it.

I stumbled upon Daan Van Hauwermeiren's ipyparallel tutorial located at 
https://github.com/DaanVanHauwermeiren/ipyparallel-tutorial/blob/master/02-ipyparallel-tutorial-direct-interface.ipynb 
And that has been extraordinarly helpful.  His tutorial really put me over the edge from NOT understanding
to actually understanding how iPython and ipyparallel can acutally work with an HPC engine.  Many thanks to him.

Here is a rough draft of what I do to setup the HPC side of things, followed by the setup of the ipyparallel
profile and running the engines, so that my notebook can use the MPI engines.

This demo and environment uses MPI.  Note that I've also tried to establish a similar environment for use with SLURM, but I haven't been successful yet.  Let me be clear: SLURM works great, but I've been unsuccesful integrating ipyparallel with SLURM, despite going through a dozen different examples that can be found by googling.

## Setup HPC
I won't go into detail here.  Just a general overview.
  * Install base HPC cluster, with a head node and N compute nodes
  * Ensure that hostnames resolve (DNS), and that time synchornization is acceptable (chrony, ntpd)
  * Install the MPI engine of your choice.  I used MPICH simply because of familiarity. Run mpi-selector to select your MPI engine.
  * Setup NFS/NIS for standard users in the cluster.
  * Create a user.  I used the username scientist for my demo.  Ensure the user can access the compute nodes and has write access to her NFS home directory.  This is really imporant because JupyterHub will install user-hosted ipyparallel software in the user's home dir (under ~/.local/) that needs to be consistent across all of the compute nodes.
  * I shared password-less ssh auth keys for the scientist user to make it easier for her to connect to the various compute nodes.
  
## Test MPICH
  * Login to the head node as scientist user
  * Download sources that have example code that useful for testing.  I like the CPI command.
    * I downloaded http://www.mpich.org/static/downloads/3.2.1/mpich-3.2.1.tar.gz
  * Extract sources  e.g.: tar xzf mpich-3.2.1.tar.gz
  * Change to examples/ directory
  * Compile the cpi example code   e.g.: mpicc cpi.c -o cpi
  * Run a test that uses the cpi command that passes the computation workload to the HPC compute nodes:
    * e.g.: mpiexec -n 4 -host host1,host2,host3,host4 cpi
  
## (pending) Install, Setup, and Run JupyterHub and iPython's ipyparallel

## (pending) Configure ipyparallel profile for MPI

## (pending) Startup the ipyparallel ipengine on each of the HPC compute nodes

## (pending) Connect to Jupyter web client for scientist user

## (pending) Load the notebook file

## (pending) Start the JupyterHub-side cluster engine

## (pending) Run the notebook
