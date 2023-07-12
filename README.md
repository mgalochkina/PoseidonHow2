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

### Getting onto MATLAB (interactively)
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

Load the appropriate module file (the bottom code will give you the default MATLAB r2020a
```
module load matlab
```
Add your MATLAB script (scriptname.m) to your Poseidon directory
Then enter
```
matlab /vortexfs1/scratch/mgalochkina/SLURM/scriptName.m
```
This will open Poseidon's MATLAB GUI, where you can run things just as you would on your PC. Not sure if this is any faster?

### Getting onto MATLAB (non-interactively)
#### AKA your command line becomes MATLAB's command window
```
module load matlab
matlab -nodisplay /vortexfs1/scratch/mgalochkina/SLURM/scriptName.m
```

### Submitting a MATLAB script to Poseidon
Below is an example script. I entered the script into Notepad++ and saved as a .sh file named ERA5_get.sh

```
#!/bin/bash
#SBATCH --partition=compute         # Queue selection
#SBATCH --job-name=serial_job       # Job name
#SBATCH --mail-type=END             # Mail events (BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=email@whoi.edu  # Where to send mail
#SBATCH --ntasks=1                  # Run on a single CPU
#SBATCH --mem=1gb                   # Job memory request
#SBATCH --time=00:15:00             # Time limit hrs:min:sec
#SBATCH --output=serial_job_%j.err  # Standard error
#SBATCH --output=serial_job_%j.out  # Standard output
##SBATCH --nodelist=pn[041-048,086] # Nodes to include
##SBATCH --exclude=pn[007-020].     # Nodes to exclude

echo "Running on node(s): $SLURM_NODELIST starting in: `pwd`"
date

module load matlab                  # Load the matlab module
 
# echo "Running graph script on a single CPU core"
 
matlab -nodisplay -nosplash -nodesktop /vortexfs1/scratch/mgalochkina/SLURM/ERA5_get.m
 
date
```

When I ran this, I encountered the following error (below). I was able to fix this using the [following link](https://wikis.ovgu.de/hpc/doku.php?id=guide:dos_unix_linebreaks).

```
sbatch: error: Batch script contains DOS line breaks (\r\n)
sbatch: error: instead of expected UNIX line breaks (\n).
```

### Possibly useful links
[UTS HPC Documentation](https://hpc.research.uts.edu.au/getting_started/running/)

### Stuff from Shawn
```
module load anaconda
module list
cat ERA5_get.m % shows you contents of file
```
### Random Bits and Bobs
hash with space = comments
hash with NO space = an actual line of code in bash

Unix has *vi* editor that helps edit code in the command line

### Submitting queues
See who is running what
```
squeue -h
```

Types of nodes:
-compute (the most common one)
-scavenger (only uses the nodes when nobody else is using it)
-bigmem

See what you're running
```
squeue -u mgalochkina
```

```
sbatch run-jupyterlab.sh
```
