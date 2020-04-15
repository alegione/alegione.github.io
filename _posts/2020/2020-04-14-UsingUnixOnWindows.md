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

So you want to use the command line to do some computational biology? Or perhaps some *\*gulp*\* bioinfomatics? Well lets get you started in as simple a way as possible. This guide is intended primarily for University of Melbourne staff and students with access to the Melbourne Research Cloud, Spartan High Performance Computer, and MediaFlux data server, but up until the latter stages it should be suitable for most command line starters

This guide will *NOT* take you through the basics of Unix commands themselves unless it's absolutely required, I strongly encourage utilising some the wonderful online resources available for this purpose.

If you have an Apple computer, you already have a terminal interface to use, so that's about the one benefit of Apples sorted. IF you're on a Windows device, hopefully you're using Windows 10, with which we are able to install the Windows Subsystem for Linux **(WSL)** to run a Unix terminal. An important distinction to make, the Windows cmd.exe is *not* the same as Unix command line, and the commands used a vastly different.

# Before you started
Some things you'll need to be ready to do:
  + Have your work saved, you'll probably have to restart your machine at least Concierge
  + Be connected to the internet! We'll be downloading lots of things from here

# Installing Ubuntu on a Windows 10 device
## Enabling WSL on your device/computer
Adding Ubuntu capabilities to your Windows 10 computer is a relatively painless process (note Windows S, on some modern Windows tablets, will not work).
1. Open the Start menu and search 'Windows Features', select the option displayed below
![Image of Windows Features Search Result]({{site.baseurl}}/images/WindowsFeaturesSearch.jpg)

2. From the long list of available features, select 'Windows Subsystem for Linux' right near the bottom
![Image of WSL check]({{site.baseurl}}/images/WSLcheck.jpg)

3. Restart your computer when requested.

Now to install Ubuntu!
- Open up the 'Windows Store' app from your start menu
- Search Ubuntu - there will be several versions, stick with the 'unnumbered' version, this will be the latest 'stable' release. Ubuntu 14 and 16 are older versions that some systems still require, but we can ignore that for now.
- Install the Ubuntu software and once it's installed the software

**Note:** If you have a computer running something older than Windows 10, then you'll need to use [PuTTY](https://www.putty.org/) as your terminal, this will connect directly to the Melbourne Research Cloud (MRC), MediaFlux, or Spartan, rather than having your own local version of Ubuntu


# Initial terminal set up
+ The terminal will ask you to create an 'account', this can be something as simple as your first name, or something similar to your university username, it's up to you!
+ You'll need to create a password, make this something easy for you to remember and difficult for anyone else to guess, we'll use the password whenever administrative privileges are needed (e.g. installing programs or modifying permissions)
     + Important note! Passwords do not appear when you type them in like in a Windows environment (e.g. Password123 won't appear as ***********), it will remain blank, if you make a mistake just hit the backspace more times than you've typed letters and you'll be fine!
+ Get ready to make yourself a cup of tea, because the next step will take a while
+ Run the following commands (you'll be asked for your newly created password, and part way through the screen might change and a yes/no option will pop up, select 'yes')
`sudo apt update && sudo apt full-upgrade -y && sudo apt autoremove && sudo apt clean`

To briefly explain the command, `sudo` elevates privileges so that we can install things, `apt` is the Ubuntu 'store' much like Google play or the Apple store, the `update` command updates the list of all the current software available and where to download it, and the `full-upgrade` command will take any software you've presently got installed and bump it up to the latest version. The addition of the `-y` is what we call an 'option', in this case it's telling the installer to automatically agree (that is, say yes) to upgrading any software found to be out of date. Finally the `autoremove` and `clean` commands will remove any unnecessary programs or downloaded installers from your system afterwards.

**Note:** Each of the commands separated by `&&` can be run separately (one command/line at a time), but stringing them together with the `&&` means that each command will run if the preceding command completes successfully and you don't have to keep checking to see if the previous command has finished.

# Setting up links to frequently used folders
If you're used to using Windows Operating Systems, the literal black box of the command line can be quite daunting. But think of your initial starting point on the command line as being inside your 'User' directory in Windows (called a 'Home' directory in Ubuntu). The folders 'above' are equivalent to the C drive, with the various system folders you won't need to worry too much about. In the initial terminal, the Home folder is shortened to ~ for simplicity, but the actual path is `/home/YOURNAME/`. You could make new folders and generate files in this home directory, but the easiest thing to do is to create shortcuts to the Windows directories you're already using. Technically the Linux file system is possible to find from inside the Windows Explorer graphical interface, but it's recommended not to play around with it lest you break your installation. The shortcut command for Unix is `ln`
If you want to create a shortcut to your Documents folder in Windows, you'd run something similar to the following (dependant on where your Documents folder is)
`ln -s /mnt/c/Users/YOURNAME/Documents documents`

`/mnt/` is the directory for your Windows drives, your WSL Ubuntu will be able to recognise most drives, but it unfortunately falls short with some extension MicroSD situations on tablets.
`-s` is the option to create a symbolic link, which is akin to a 'shortcut' in Windows

The link we've created is in your home directory, and therefore the path ~/documents will take you to your Windows Documents folder.

A trickier example is the University of Melbourne's OneDrive folders, which are called 'OneDrive - The University of Melbourne' by default. Unix considers spaces as separators between commands, so OneDrive - The University of Melbourne, is six separate inputs to the command line: "OneDrive", "-", "The", "University", "of", "Melbourne". To get around this issues, quotation marks are your friend. Text inside quotation marks is read as a single long string, so our command would be: `ln -s "/mnt/c/Users/YOURNAME/OneDrive - The University of Melbourne" onedrive`

**Note:** You may notice that for both commands, the shortcuts were both lowercase, this is just a time saver. Unix commands are case sensitive, and you could have 3 folders called "Alistair", "alistair", and "ALISTAIR". Sticking to a consistent theme for your folders and files will help you navigate your Unix environment.

# What now?
Now you're ready to use your Unix terminal! If you're now planning on connecting to one of the various cloud systems you can jump right ahead to that
Or, if you want to install a package manager locally (this helps you to install any of the bioinformatics tools you may want to use on your own computer, not in the cloud), then you can do that too.

Guides for each of these steps will hopefully appear soon
