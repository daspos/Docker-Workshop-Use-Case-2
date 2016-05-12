#Readme for ReproZip: DASPOS Workshop#

This is a repo for Breakout 2 ReproZip a session held at the DASPOS Workshop on Container Strategies for Data & Software Preservation.  More information about the workshop is available at: https://daspos.crc.nd.edu/index.php/workshops/container-strategies-for-data-software-preservation-that-promote-open-science


More information about ReproZip is available on [the project's website](https://vida-nyu.github.io/reprozip/).

This github repository contains info, links, files for participating in the ReproZip Breakout sessions at the DASPOS Workshop Container Strategies for Data & Software Preservation that Promote Open Science held at Notre Dame University 5/19-20/2016 .

The breakout sessions are related to the 5/19/2016  [ReproZip Workshop Talk](https://daspos.crc.nd.edu/index.php/14-daspos/workshops/55-workshop-7speak#vste)  presented by [Vicky Steeves and Rémi Rampin](https://daspos.crc.nd.edu/index.php/14-daspos/workshops/55-workshop-7speak#vste).

## Technology Preview:ReproZip

ReproZip allows you to pack your experiment along with all necessary data files, libraries, environment variables and options.

Anybody can then reproduce the experiment on a different machine, without tracking down and installing the dependencies, or even having to run the same operating system!

ReproZip is a tool aimed at simplifying the process of creating reproducible experiments from command-line executions. It tracks operating system calls and creates a package that contains all the binaries, files, and dependencies required to run a given command on the author’s computational environment. A reviewer can then extract the experiment in his own environment to reproduce the results, even if the environment has a different operating system from the original one.

Currently, ReproZip can only pack experiments that originally run on Linux.

ReproZip works by tracing the systems calls used by the experiment to automatically identify which files should be included. You can review and edit this list and the metadata before creating the final package file.

Packages can be reproduced in different ways, including chroot environments, Vagrant-built virtual machines, and Docker containers; more can be added through plugins.

For more information, check out the [Full Documentation](https://reprozip.readthedocs.io/).
