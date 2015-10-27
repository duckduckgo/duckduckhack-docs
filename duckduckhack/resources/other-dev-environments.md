# Other Development Environments

For the vast majority of contributors, the best, simplest, and quickest way to develop on DuckDuckHack is to use the **free, web-based Codio environment**. Instructions on setting up Codio can be found in the section on [setting up your development environment](#). 

However, some developers prefer working on either a local environment or a virtual machine. This guide addresses setting up DuckPAN on environments other than Codio.

## About DuckPAN

DuckPAN is an application built to aid DuckDuckHack developers. It is mainly used to generate the required files for new Instant Answers, where the developer can then focus on implementing functionality. DuckPAN also assists developers in testing the triggering and visual display of Instant Answers.

## Overview of Environments

Aside from the preferred [Codio web-based environment](#), there are three other environments you can set up:

- [**Install DuckPAN locally**](#installing-duckpan-locally). This **requires Linux or Mac OS X**. We suggest you install [Ubuntu](http://www.ubuntu.com/download).
- The [**DuckDuckHack Virtual Machine Image**](#duckduckhack-development-virtual-machine)
- The [**Vagrant virtual environment**](#vagrant-virtual-environment)

_**Note on Windows systems:** Local development is not possible on Windows environments. Windows users can use either Codio or the virtual machine._

Once DuckPAN is up and running, be sure to continue to the [using DuckPAN](#using-duckpan) section below.

## Universal Notes

### Operating Systems

Currently, DuckPAN has been developed on, and works well with **Ubuntu**. More specifically, we regularly build, test and run DuckPAN on **Ubuntu 12.04**. We have also successfully installed and run DuckPAN on older and newer Ubuntu releases, e.g. Ubuntu 10.04, 12.10, and 13.04.

Developers have also been successful running DuckPAN on other Linux distros (e.g. Arch, Debian) and on Mac OS X 10.8 and later, but **we make no promises that it will work outside of Ubuntu**.

As well, **there have been reported issues with installing DuckPAN on Windows**, so we don't recommend you go down that path.

That being said, we are more than willing to help you debug any installation problems, so please come to us with your problems and we'll try to get your issues sorted out. If you'd like some help from our community, feel free to engage with them on the [DuckDuckGo forum](http://duck.co/).

### Perl Versions

We run our DuckPAN tests against Perl 5.16 and 5.18 using Travis (https://travis-ci.org/duckduckgo/p5-app-duckpan). We suggest you install Perl 5.16 via Perlbrew for local development. The Codio boxes come with Perlbrew and Perl 5.18 already installed.

------

## Installing DuckPAN Locally

_**Note**: You don't need to install DuckPAN locally if you're using our DuckDuckHack virtual machine or the Vagrant virtual environment. It's already installed for you!_

To install DuckPAN, open your terminal and run:

```
curl http://duckpan.org/install.pl | perl
```

[This script](https://github.com/duckduckgo/p5-duckpan-installer) will setup [local::lib](https://metacpan.org/module/local::lib), which is a way to install Perl modules without changing your base Perl installation. If you already use `local::lib` or [perlbrew](https://metacpan.org/module/perlbrew), don't worry, this script will intelligently use what you already have.

If you didn't have a `local::lib` before running the install script, you will need to run the script twice. It should tell you when like this:

```
please now re-login to your user account and run it again!
```

If everything works, you should see this at the end:

```
EVERYTHING OK! You can now go hacking! :)
```

Note that with `local::lib` now installed, you can easily install [Perl modules](http://search.cpan.org/) with [cpanm](https://metacpan.org/module/cpanm).

```
cpanm App::DuckPAN
App::DuckPAN is up to date.
```

### Adding Shell Completion

Some of our awesome community members have written shell completion scripts for DuckPAN, which should save you tons of time. Feel free to improve these, or contribute new ones!

#### Bash

- Submitted by: [mattr555](https://github.com/mattr555)
- link: https://github.com/mattr555/dotfiles/blob/master/bin/duckpancomp.sh

#### Z Shell

- Submitted by: [elebow](https://github.com/elebow)
- link: https://github.com/elebow/duckpan-completion

### Dealing With Installation Issues

If during the course of your DuckPAN install you run into errors, don't panic, there are a few things you can try.

First, try running the install command again (`curl http://duckpan.org/install.pl | perl`), this often solves issues related to any dependencies.

If that doesn't work, you should investigate the build.log and see what's wrong. It might be a dependency issue which you can resolve by manually installing whichever dependency is missing via `cpanm`.

If it still won't install with `cpanm` try adding `--notest` to the cpanm command:

```
cpanm Test::More --notest
```

If that still doesn't work, you can also try using `--force`:

```
cpanm Test::More --force
```

If this ***still*** doesn't work, please create a GitHub Issue in the DuckPAN Repo [here](https://github.com/duckduckgo/p5-app-duckpan/issues). Be sure to paste the contents of your `build.log` and also let us know the details of your OS (`$ uname -a` is great). Once you've made the issue, we'll work with you to try and solve any problems you're having.

------

## Vagrant Virtual Environment

The Vagrant-based DuckDuckHack virtual environment provides a similar sandbox to the DuckDuckHack VM, but rather than downloading a prebuilt VM, Vagrant creates an environment for you based on the defined configuration.  Vagrant is an awesome tool for building development environments.  One command - `vagrant up` - gets you a complete working environment in minutes.  Something go wrong with the environment?  No messing around with snapshots.  Tear the VM down and build a fresh environment.  The DuckDuckHack Vagrant environment uses Chef cookbooks and the DuckPAN installer script, so configuration is transparent and easily shared.

Through the Vagrant configuration, you can easily switch back and forth between a headless-mode and the traditional VirtualBox interface.  The configuration defaults to headless.


### Setup Instructions

Refer to [the duckpan-vagrant readme](https://github.com/shedd/duckpan-vagrant#installation) for installation instructions.

Once the environment has been built, **the DuckPAN client is installed and ready to go.** You can now clone the Instant Answer repos and start developing/testing.

If you run into any issues, please file an issue in the [duckpan-vagrant issue page](https://github.com/shedd/duckpan-vagrant/issues).


##### Quick Overview of key Vagrant CLI commands

There are a couple of key Vagrant commands that you'll use to manage your environment.

```
$ vagrant

up       - Build environment from Vagrantfile or resume a previously halted environment.
ssh      - Connect to your running VM via SSH.
suspend  - Pause the VM, storing its current state to disk.
resume   - Bring a suspended VM back to life.
reload   - The equivalent of running a halt followed by an up.  Use this when you make changes to Vagrantfile.
halt     - Shut down the VM. Tries to gracefully shutdown first; if that fails, it will forcefully shut the VM down.
destroy  - Stop the currently running VM and blow everything away.
```

Run these commands from the directory containing your `Vagrantfile`.

For more information, please see the (excellent) [Vagrant docs](http://docs.vagrantup.com/).

------

## DuckDuckHack Development Virtual Machine

The purpose of our DuckDuckHack VM is to provide a sandbox for DuckDuckGo Instant Answer development that is quick to set up and start working with.


#### DDH VM Breakdown

- Ubuntu 12.04 LTS
- Perl 5.16.3 (managed by Perlbrew)
- build-essential (for make, gcc, cc, etc)
- cpanminus (managed by Perlbrew)
- App::DuckPAN
- XFCE Window Manager
- SublimeText, vim, emacs
- Firefox (Configured via fixtracking.com)
- Platform specific virtualization guest tools (optimizes hardware emulation)


#### For VirtualBox hosts

ddh-vbox-2014-12-23.ova:

MD5: 02a0fb03db2b2466504bf9fbc894c7dd

https://ddg-community.s3.amazonaws.com/ddh-vbox-2014-12-23.ova


#### For VMWare hosts

ddh-vmw-2014-12-23.ova:

MD5: 6ecdeb8ead2c2eb7a9aba1db22359c4b

https://ddg-community.s3.amazonaws.com/ddh-vmw-2014-12-23.ova


#### Roadmap

- Docker support
- Public AMI for use on EC2


### Installing the Virtual Machine

To use the Virtual Machine, you will need to download and install **VirtualBox**, **VMWare Workstation** or **VMWare Player**, depending on your current OS.

Then you will need to import the VM.


#### VirtualBox (free)

Website: https://www.virtualbox.org/
Supports: Windows, OS X, Linux


##### Import the VM

1. Download the OVA
2. Open VirtualBox, click "File" and then click "Import Appliance"
3. Click "Open appliance..." and select the DuckDuckHack virtual appliance OVA file -- click "Next"
4. Click "Import"


#### VMWare Player (free)

Website: https://www.vmware.com/products/player/
Supports: Windows, Linux


##### Import the VM

1. Download the OVA
2. Open VMWare Player, and click "Open a Virtual Machine"
3. Choose a storage path for the Virtual Machine -- click "Import"


### Using the Virtual Machine


#### Logging into the VM

Once you have installed the virtual machine you should be able to start up the VM and login with the following credentials:
- **username** : `vagrant`
- **password** : `duckduckhack`


#### Cloning the repository on the VM

**The DuckPAN client has already been installed for you.** To use it, you must 1st clone your Instant Answer git repository.

If you haven't already done so, [Determine your Instant Answer Type](https://duck.co/duckduckhack/determine_your_instant_answer_type) and follow GitHub's instructions to [fork](https://help.github.com/articles/fork-a-repo) the Instant Answer repository.

The Instant Answer repositories are:
+ [zeroclickinfo-goodies](https://github.com/duckduckgo/zeroclickinfo-goodies)
+ [zeroclickinfo-spice](https://github.com/duckduckgo/zeroclickinfo-spice)

Then, run the git clone command to clone the repository. The URL is the **SSH clone URL** listed on the right side of the github webpage for your forked repository. (You can also use the **HTTPS clone URL**.)

```
git clone URL
```

_**If your Github password doesn't work**, you may need to enter a [Personal Access Token](https://github.com/settings/tokens) instead. Simply copy and paste your token from your [Github Settings](https://github.com/settings/tokens). (This happens if you have set up [Github's Two-Factor Authentication](https://github.com/blog/1614-two-factor-authentication) feature.)_

#### Happy Hacking!

See the instructions below on [Using DuckPAN](#using-duckpan).

------

## Using DuckPAN

Running `$ duckpan` with no commands will output some help information. More details on the DuckPAN commands can be found in the [DuckPAN Readme](https://github.com/duckduckgo/p5-app-duckpan#using-duckpan).

The next section on [testing triggers](https://duck.co/duckduckhack/testing_triggers) will show you how to use DuckPAN to interactively test your triggers.
