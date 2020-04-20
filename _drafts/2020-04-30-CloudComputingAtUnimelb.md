---
title:  "Computational Biology 101: Connecting to the Cloud @ UniMelb"
header:
  teaser: "images/commandline-example-helloworld.jpg"
permalink: "/2020/CloudComputingAtUnimelb"
published: true
comments: true
tags:
  - bash
  - "University of Melbourne"
  - "High performance computing"
  - "Computational Biology 101"
  - Unix
  - education
  - coding
  - MediaFlux
---

The University of Melbourne offers staff and students a valuable array of cloud computing options. These include:
1. Melbourne Research Cloud (MRC): Individual instances (virtual computers) on which you can run everything from a Linux computer, an R server, or a virtual GUI (graphical user interface) operating system. If you set up a Linux instance, it's akin to running one on your local computer, just with the potential for more power.
- Pros:
  + Just like running a local Linux installation, if you can run the terminal, you can run the MRC.
  + Your own personal instance, no waiting in a queue
  + You can save and share your image/installation between 'instances'
- Cons:
  + Not as much power as a High Performance Cluster
  + Typical flavour (instance set up options) has a very small primary hard drive capacity (30 GB), so you have to make sure to run your programs, store your data, and set temporary directories in your attached Volume (the data drive you'll set up)

2. Spartan High Performance Computer: This is the University's super computer, that can run jobs (programs/pipelines) that need up to 1.5 TB of RAM (yes, that's a lot of RAM!), multiple cores for massive parallel processing, or GPU based jobs that can accelerate your research.
- Pros:
  + Unlimited cosmic power (well, kind of)!
  + You can have a 'project' for your research group, so multiple team members can access the same project folder/data (if you set permissions correctly).
  + Wonderful and responsive IT support
- Cons
  + Slightly steeper learning curve, as rather than running programs, you submit your 'jobs' to a 'queue', and they run when the resources are available. 


- key settings
chmod u=rw,go-rwx ~/mykey.pem

- remove old temp files
sudo find /tmp -type f -atime +10 -delete
