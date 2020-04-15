---
layout: single
title:  "Computational Biology 101: Getting a Unix command line on Windows 10"
header:
  teaser: "images/commandline-example-helloworld.jpg"
categories:
  - "Computational Biology 101"
  - Unix
  - education
  - coding
tags:
  - bash
  - conda
  - Homebrew
  - "University of Melbourne"
  - "High performance computing"
---

# Install a package manager
If you're not planning on using your local instance for anything but connecting to the cloud, you can skip this step. However it is useful to having

## Homebrew/Linuxbrew

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
