# c3tools
Scripts to help automate using a device with a big.LITTLE SoC as a compute node for primality testing. It's recommended that these scripts be executed from within a multiplexer such as tmux, and that the device be controlled from a computer via ssh.

## Prerequisites
* mlucas binary at ~/mlucas
* These tools in ~/c3tools, With git installed and an active internet connection you can do this with 'cd ~ && git clone https://github.com/sillygitter/c3tools'
* A working Linux environment with bash, cat, cd, cp, date, echo, exit, ln, mkdir, mv, perl, pkill, rm, sensors, sleep, tar
* Any previous attempt at running a given script purged. The scripts will exit whenever they want to create a directory that already exists to avoid accidentally deleting something

## setup script
This script takes a user-supplied cluster configuration and creates a working environment from it. It:
* Creates a worker directory for each cluster
* Has mlucas generate mlucas.cfg files for each cluster in turn with all the other clusters under load
* Edits the timings in the generated mlucas.cfg files to be contiguous

## bench script
This script benchmarks with simultaneous tests on each cluster at key FFT lengths. The script takes ~20 hours to complete and puts all results in a tarball. The tests include:
* One hour of simultaneous 1024K FFT
* Two hours of simultaneous 2560K FFT
* Three hours of simultaneous 4608K FFT
* Four hours of simultaneous 7680K FFT
* Ten hours of simultaneous 18432K FFT
From these results the combined throughput of the SoC at each FFT length can be calculated.

## plotter script
A simple script that periodically dumps temperature data from the 'sensors' command to file. Used by the bench script, can be used on its own.
