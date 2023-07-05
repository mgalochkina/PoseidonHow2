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
