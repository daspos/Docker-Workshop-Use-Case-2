
#ReproZip Example Playable on Mac OS X#

This example includes a ReproZip Package created on a Mac OS X machine using a Linux Virtual Machine running under 
[Virtual Box](https://www.virtualbox.org/wiki/VirtualBox). It assumes you are comfortable using the command line,
[git](https://git-scm.com/), and installing packages using [homebrew](http://brew.sh/)


To start with, download this repo

*git clone https://github.com/daspos/Docker-Workshop-Use-Case-2*

##Virtual Box and Docker Setup##

1. Install the VirtualBox VM Manager, using this package:


...http://download.virtualbox.org/virtualbox/5.0.20/VirtualBox-5.0.20-106931-OSX.dmg

2. Install Docker and boot2docker via brew

... *brew install docker*
... *brew install boot2docker*


##Running ReproUnzip##

Reprounzip is available for Mac OS as a python package. Python should already be installed- you can
check the version by typing *python --version*

1. Install reprounzip and reprounzip-docker

... *sudo pip install reprounzip* 
... sudo pip install reprounzip-docker

2. Get Docker Running

..._boot2docker init_   ( This will download a boot2docker image ISO- could take a minute or two)
...*boot2docker up*     ( The initial iamge startup could take several minutes)
...*eval "$(boot2docker shellinit)"*  (gets docker talking to vitrualbox via boot2docker)

3. Running ReproUnzip (and Bertini)

...We are ready tp try and reproduce the Bertini run we captured 
..1. first, find the packed ReproZip file bertini\_example1.rpz in the directory Docker-Workshop-Use-Case-2/reprozip\_bertini\_osx
..2. setup reprounzip for a run with the command *reprounzip docker setup bertini\_example1.rpz example1\_homedir* - this will create the directory example1\_homedir, and will likely take a few minutes.
..3. Now, run the unpacked example: *reprounzip docker run example\_homedir*   The full output is availble in the example1.out file 
..4. The command *reprounzip docker download example1\_homedir * will show all of the Bertini Result files which are available for download
Output files:
    nonsingular_solutions
    raw_data
    midpath_data
    main_data
    real_finite_solutions
    start
    finite_solutions
    output
    raw_solutions
    singular_solutions
    failed_paths

#.#Using ReproZip within a VM#
 
