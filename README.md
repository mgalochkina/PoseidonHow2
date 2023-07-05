# PoseidonHow2
a guide for using WHOI's HPC cluster (Poseidon) on Windows for dummies (me) 

# Getting onto Poseidon (Windows)
### Option 1: Command Line
Open Command Line
```
cmd
```
Log onto Poseidon
```
ssh username@poseidon.whoi.edu
```
_Note: this will require you to type in your password (same as email password) every time_

Check working directory
```
pwd
```
This should output:
```
/vortexfs1/home/username
```
### Option 2: download MobaXTerm
1. Download [MobaXTerm](https://mobaxterm.mobatek.net/).
2. Set up SSH keys (should just work on it's own)
```
ssh username@poseidon.whoi.edu
```
Log in using your WHOI username and password. This will require you to set up a one-time MobaXTerm password. Set that up and save it somewhere.

### Getting onto MATLAB
Check which MATLAB modules are available on Poseidon
```
module avail matlab
```
The options should be:
* matlab/r2018b
* matlab/r2019b
* matlab/r2020a (default)
* matlab/r2020b
* matlab/r2022a

Load the appropriate module file
```
module load MATLAB/2020a
```

Add your MATLAB script (scriptname.m) to your Poseidon directory

Run MATLAB (this is based on the YCRC code -- might be slightly different for Poseidon?)
```
#!/bin/bash
#SBATCH --job-name myjob
#SBATCH --cpus-per-task 4
#SBATCH --mem 18G
#SBATCH -t 8:00:00

module load MATLAB/2021a
# assuming you have your_script.m in the current directory
matlab -batch "your_script"
```
### Possibly useful links
[UTS HPC Documentation](https://hpc.research.uts.edu.au/getting_started/running/)

