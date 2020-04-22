---
title:  "Computational Biology 101: Selecting and installing a package manager"
header:
  teaser: "images/commandline-example-helloworld.jpg"
permalink: "/2020/InstallingAPackageManager"
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

published: true
comments: true
---

Installing programs on a Unix machine/terminal can be a dark and scary place, particularly when it comes to things like 'dependencies', that's when someone has written a bit of software (let's call it program X), and that software relies on another bit of software (program Y), but when you install X, Y second isn't automatically installed, so you have to work out how to install Y too, then program Z because Y relies on Z!! It's a nightmare.

Package managers are designed to make this process simple, by installing all dependencies that you may need when you want to install software X. Aah, much better.
But there are choices to make when you are picking your package manager! So I'm going to provide some information and brief instructions for two of these choices: Homebrew and Conda.

<!–-break–->

# Installing a package manager
If you're not planning on using your local instance for anything except connecting to the cloud, you can potentially skip installing a package manager as most basic programs can be installed with the command you used to update/upgrade your Unix instance. For example, if you wanted to install the text editor Vim, you could simply write:

```terminal
sudo apt install vim
```


However it is useful to have some of the same tools available on your local machine in case you need to run some quick analysis offline, so I recommend still installing a package manager on your local machine.

## Homebrew/Linuxbrew
My personal preference is Homebrew/Linuxbrew (Mac = Homebrew, Unix = Linuxbrew), but really this is due to old habits, it's the package manager I started with, and therefore I've stuck with it. If you're willing to put in a bit of extra work for greater flexibility than Conda is perhaps the better way to go.

Brew is the simplest level of package manager, you 'brew' your programs, it installs everything to the same folder (/home/linuxbrew/), and will always keep itself up to date. Additionally, you can easily update all your various installed packages to the latest versions. The trick is, you may not always want the latest version! This is because some software may be designed to work with a particular version of a dependency, and brew will automatically update everything rendering this software no longer functional. Similarly you may wish to ensure you use the same version of a tool for the length of a project so that you can be sure there is consistency in your analysis (and so when you're writing your manuscript, it's easier to say which version you used). If you want that functionality then Conda is the option you should go with. If all you're looking for is a simple way to install tools, and keep the up to date, linuxbrew is the best option in my opinion.

The installation instructions below are taken from https://brew.sh/

This first step isn't strictly necessary, but I've often found it saves some issues down the line

```terminal
sudo apt install build-essential curl file git
```

Next, copy the below command to the terminal and hit ENTER

```terminal
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

The installation will ask you to hit ENTER shortly after starting, so don't get up just yet.

Finally, run the final few command *one by one* to add linuxbrew to your `PATH`. The `PATH` is essentially a list of locations for your terminal to find installed programs in. Without this step, you won't easily be able to run your tools, they'll be installed but will only run if you 'point' directly at them.

```terminal
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
```

Now test to see if the installation worked

```terminal
brew install hello
```

Hopefully you'll not encounter any errors; regardless of whether you do it never hurts to run the following to check if linuxbrew identifies any issues with your installation

```terminal
brew doctor
```

This command will output solutions to any errors that may have crept in during the installation process.

Final suggestion; homebrew likes to check every time you try to install anything that you have the latest version of homebrew installed too. This is great, but can be annoying if you're installing several things in the same time period! Run the below command to keep homebrew from checking for updates of itself for a half hour.

```terminal
echo "export HOMEBREW_AUTO_UPDATE_SECS=1800" >> ~/.bashrc`
```

To keep homebrew up to date on your own time, use:

```terminal
brew update
```

To update homebrew and update all the programs you've got installed:

```terminal
brew update
```

To install a tool, it's a simple matter of typing

```terminal
brew install SOMETOOL
```

Obviously replacing `SOMETOOL` with a program of your choice.

The software homebrew can install come from a list of tools it has 'formula' for, stored in 'taps' (get it?). To make sure you have access to a huge suite of bioinformatics tools for linux, make sure to add some extra taps with the following commands

```terminal
brew tap brewsci/bio
```

```terminal
brew tap brewsci/science
```

That's it, you've got your package manager set up and you're ready to install all the tools!

## Conda/Miniconda
Conda, or more correctly Miniconda, is a package manager with an immense amount of flexibility if used correctly. Miniconda acts in a similar way to homebrew in that it will install all necessary dependencies for your software of choice, the difference being it will also check the version number of the required dependency and ensure correct, older versions are not overwritten. This could create problems if you're running multiple projects from the same terminal *BUT* Conda runs from within 'environments', so you can have an environment for project A and project B, and the programs won't interfer with each other. You just have to get used to loading up the 'environment' when you start your work.

**Note:** If you're planning on working with microbiome analysis package QIIME2 then you'll need to work with Miniconda to install it.

### Download Conda

You can download Miniconda by [clicking here](https://docs.conda.io/en/latest/miniconda.html)
There are several choices available, 32 or 64 bit, and Python 2.7 and 3.x (depending on the current version of Python 3). If you're unsure what one to pick then the likely answer is the latter of both (64/3.x), as the other options are 'legacy'.

Copy the link location for this version and type the following commands

```terminal
wget LINK
```

or presuming the current version available is for Python 3.7 (as it was at time of writing), you can just use the command below for MacOS

```terminal
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
```

or the below command for Linux (Ubuntu)

```terminal
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

You're downloading both the package manager and Python 3.x, so that's one less program to install.
Now to install Conda; I'll stick with the Linux process, but the below instructions come from the official page and you can find the [MacOS install process there too](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)

Simply run the following command

```terminal
bash Miniconda3-latest-Linux-x86_64.sh
```

Follow the prompts (just keep the defaults/answer 'yes' unless you're keen to change things) and after it has completed set up close and re-open your terminal.

The first thing you might notice is that your prompt has changed a little. Instead of being

```terminal
USERNAME@COMPUTER:~$
```

It will say:

```terminal
(base)USERNAME@COMPUTER:~$
```

This is telling you that you're in your 'base' environment of Miniconda. Anything you need to use all the time, and where versions don't matter so much, you can install at your 'base' level. To update conda at any time, just use the below command

```terminal
conda update conda
```

Now to access all the fun bioinformatics programs, you'll need to point Conda in the right direction. Start by adding the Bioconda repository to your Conda installation. Run these *one by one* and *in order*.

```terminal
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

Now you can install tools by simply typing the below and entering 'y' when prompted

```terminal
conda install SOMETOOL
```

Conda will assess the dependencies required and install the tools. But the best use of Conda is creating your environments. Lets say you're running a project that needs to trim some fastq reads, de novo assemble a genome, and then annotate it.

```terminal
conda create -n denovo fastp megahit prokka
```

The above command will create a conda environment called "denovo", and install fastp, megahit, and prokka.
Then you just have to activate the environment by running

```terminal
conda activate denovo
```

You'll notice your (base) next to your prompt now says (denovo) and you'll have access to the installed tools. All your folders are still in the same place, just where the command line is looking for programs has changed.
You can still install programs as you need them, just do so from within your activated environment.

If you want to return to your base environment, just run

```terminal
conda deactivate
```

If you ever forget what environments you've created, they're stored in `~/miniconda3/envs/` or you can use the command `conda envs`

Once you've finished your analysis and are writing your manuscript, you can export your environment for others to use by simply running either

```terminal
conda create --clone ENVNAME --name NEWENV
```

 to clone the whole environment, or simply create a 'YAML' text file, which tells conda what to install, by running the following (replacying envname with whatever you'd like to call your environment)

 ```terminal
conda env export --name ENVNAME > envname.yml
```

## Finished!
You're all set to install packages, and/or run environments, and do some science! Now perhaps it's time to connect yourself to the Melbourne Research Cloud, or the Spartan High Performance Computing Network?
