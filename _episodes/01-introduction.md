---
title: "Introduction"
teaching: 10
exercises: 0
questions:
- "What is the point of these exercises?"
- "How do I find the data I want to work with?"
objectives:
- "To understand why we need special tools to find the data"
- "To understand the basics of how the datasets are divided up"
keypoints:
- "Accessing the data is non-trivial, but there are tools to help with this."
---

In this lesson, we'll walk through the process of finding out what data and 
Monte Carlo is available to you, how to find it, and how to examine what 
data is in the individual data files. 

First of all, let's understand how the data is stored and why we need certain
tools to access it. 

# XRootD

Some of this history can be found [here](https://indico.cern.ch/event/523410/contributions/2355713/attachments/1367327/2071864/XWS-Tokyo-History.pdf).

HEP data presents challenges due to the size of the datasets and the heterogeneity of 
the data itself. The latter comment refers to the fact that for much of the processing
of the data, the size of each event is different from one event to the next. This issue
is solved with the ROOT filesystem, which can efficiently deal with this type of 
"blocky" data. But experiments will often have thousands or even millions of individual 
ROOT files for the raw or processed data and this can be difficult to organize 
and access on a filesystem.

In 1997, the BaBar experiment decided to use a commercial database from Objectivity. 
However after a couple of years of running, the database was not scaling and a new solution
was sought. This led to the development of and first deployment of 
[XRootD](https://xrootd.slac.stanford.edu/) at SLAC for BaBar, but it has gone on to be used
in most HEP experiments.

XRootD can be thought of as a database that keeps track of where files live on disk, but it
can also *serve up* data from those files! Yes, the files exist somewhere on the file system,
but we don't generally access them directly. 
So many of the tools and scripts we use within CMS have XRootD baked into them.

Beyond that, the data you will be accessing, either from a docker image or VM, is
not on your machine and instead lives somewhere on disk at CERN. So just typing

~~~
ls -l
~~~
{: .bash}

for these directories will not work. 

Fortunately, we have provided some simple tools to find out where these datasets and files are. 
Once we find them, we have also provided some simple tools to inspect these files to get a first-order
look at what's inside them. 


{% include links.md %}
