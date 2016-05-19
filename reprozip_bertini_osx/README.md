# ReproZip Example Playable on Mac OS X#

This example includes a ReproZip Package created on a Mac OS X machine using a Linux Virtual Machine running under
[Virtual Box](https://www.virtualbox.org/wiki/VirtualBox). It assumes you are comfortable using the command line,
[git](https://git-scm.com/), and installing packages using [homebrew](http://brew.sh/).

The software used in the example is the Bertini package http://bertini.nd.edu/

To start with, download this repo:

```
git clone https://github.com/daspos/Docker-Workshop-Use-Case-2
```

## Virtual Box and Docker Setup

1. Install the VirtualBox VM Manager, using this package:

 http://download.virtualbox.org/virtualbox/5.0.20/VirtualBox-5.0.20-106931-OSX.dmg

2. Install Docker and boot2docker via brew:

 ```
 brew install docker
 brew install boot2docker
 ```

## Running ReproUnzip

Reprounzip is available for Mac OS as a python package. Python should already be installed- you can
check the version by typing *python --version*

1. Install reprounzip and reprounzip-docker

 ```
 sudo pip install reprounzip
 sudo pip install reprounzip-docker
 ```

2. Get Docker Running

 ```
 boot2docker init  # This will download a boot2docker image ISO- could take a minute or two)
 boot2docker up  # ( The initial iamge startup could take several minutes)
 eval "$(boot2docker shellinit)"*  # (gets docker talking to vitrualbox via boot2docker)
 ```

3. Running ReproUnzip (and Bertini)

 We are ready to try and reproduce the Bertini run we captured.

 1. First, find the packed ReproZip file `bertini_example1.rpz` in the directory `Docker-Workshop-Use-Case-2/reprozip_bertini_osx`
 2. Setup reprounzip for a run with the command `reprounzip docker setup bertini_example1.rpz example1_homedir` - this will create the directory `example1_homedir`, and will likely take a few minutes.
 3. Now, run the unpacked example: `reprounzip docker run example_homedir`   The full output is availble in the `example1.out` file
 4. The command `reprounzip docker download example1_homedir` will show all of the Bertini Result files which are available for download
```
Output files:
  - nonsingular_solutions
  - raw_data
  - midpath_data
  - main_data
  - real_finite_solutions
  - start
  - finite_solutions
  - output
  - raw_solutions
  - singular_solutions
  - failed_paths
```

# Using ReproZip within a VM

 If you made it this far, and would like to try your hand at creating a ReproZip rpz, follow the instructions below.

##Building a Linux VM Using Vagrant##
 You'll need a Linux VM where you can install your software and reprozip, then build the rpz. You should already have VirtualBox installed on your Mac for running such a VM . There is a tool, Vagrant, which helps with  building and installing VMs. Install the Mac
version from here: 

 https://releases.hashicorp.com/vagrant/1.8.1/vagrant_1.8.1.dmg

 There is a file in the `reprozip_bertini_example` directory named *Vagrantfile*. Copy this file to the directory on your Mac from which you'll be working, then *cd* to that directory, and run the command

```
vagrant up
```
 Vagrant will attempt to use this file to build and provision a centos7 linux VM, and install the Bertini Software, using VirtualBox as the VM Host. If you've never run an Centos7 image on your Mac before, Vagrant will need to download the image, whivh could take 10+ minutes over a wireless connection. Vagrant will generate a large amount of output as it progresses through this process. The output capture from our testing run in included in the `vagrantup.out` file

 When the ``vagrant up`` command finishes, there should be a VM running, with the Bertini software installed, that you can use
to create an rpz. Verify this with the command

```
$ vagrant status
Current machine states:

default                   running (virtualbox)
```

##Using Reprozip within the VM##

 Vagrant has a Secure Shell option to allow you to connect to your new VM- run the command ``vagrant ssh``. You will be connected as the *vagrant* user. Run the command ``ls``:

```
vagrant@bertinivm ~]$ ls
BertiniLinux64_v1.5  BertiniLinux64_v1.5.tar.gz  sync
[vagrant@bertinivm ~]$
```

 You can see a directory 'BertiniLinux64_v1.5' where Bertini was installed.

 Let's run one of Bertini's canned examples and use ``reprozip trace`` to capture that execution session:

```
vagrant@bertinivm ~]$ reprozip trace BertiniLinux64_v1.5/bin/bertini BertiniLinux64_v1.5/examples/zero_dim/basic_example/input
```

This will produce output very similiar to the Bertini Reprounzip run we did earlier, and will produce the configuration we need to pack it:

```
vagrant@bertinivm ~]$ reprozip pack bertini_example1.rpz
```

You should now (at long last) have a ``bertini_example1.rpz`` suitable for unzipping.
