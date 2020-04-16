---
title:  "Computational Biology 101: Selecting and installing a package manager"
header:
  teaser: "images/commandline-example-helloworld.jpg"
permalink: "/2020/04/15/InstallingAPackageManager"
tags:
  - bash
  - conda
  - Homebrew
  - "University of Melbourne"
  - "High performance computing"
  - "Computational Biology 101"
  - Unix
  - education
  - coding
---

Installing programs on a Unix machine/terminal can be a dark and scary place, particularly when it comes to things like 'dependencies', that's when someone has written a bit of software (let's call it program X), and that software relies on another bit of software (program Y), but when you install X, Y second isn't automatically installed, so you have to work out how to install Y too, then program Z because Y relies on Z!! It's a nightmare.

Package managers are designed to make this process simple, by installing all dependencies that you may need when you want to install software X. Aah, much better.
But there are choices to make when you are picking your package manager! So I'm going to provide some information and brief instructions for two of these choices: Homebrew and Conda.

# Installing a package manager
If you're not planning on using your local instance for anything except connecting to the cloud, you can potentially skip installing a package manager as most basic programs can be installed with the command you used to update/upgrade your Unix instance. For example, if you wanted to install the text editor Vim, you could simply write:

`sudo apt install vim`

However it is useful to have some of the same tools available on your local machine in case you need to run some quick analysis offline, so I recommend still installing a package manager on your local machine.

## Homebrew/Linuxbrew
My personal preference is Homebrew/Linuxbrew (Mac = Homebrew, Unix = Linuxbrew), but really this is due to old habits, it's the package manager I started with, and therefore I've stuck with it. If you're willing to put in a bit of extra work for greater flexibility than Conda is perhaps the better way to go.

Brew is the simplest level of package manager, you 'brew' your programs, it installs everything to the same folder (/home/.linuxbrew/), and will always keep itself up to date. Additionally, you can easily update all your various installed packages to the latest versions. The trick is, you may not always want the latest version! This is because some software may be designed to work with a particular version of a dependency, and brew will automatically update everything rendering this software no longer functional. 

sudo apt-get install build-essential curl file git

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile


echo "export HOMEBREW_AUTO_UPDATE_SECS=1440" >> ~/.bashrc

brew install hello

brew install python



- key settings
chmod u=rw,go-rwx ~/mykey.pem

- remove old temp files
sudo find /tmp -type f -atime +10 -delete
