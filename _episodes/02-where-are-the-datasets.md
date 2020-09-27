---
title: "Where are the datasets?"
teaching: 5
exercises: 5
questions:
- "Where do I find datasets for data and Monte Carlo?"
objectives:
- "Be able to find the data and Monte Carlo datasets"
keypoints:
- "The data and Monte Carlo are stored in directories with names that give you some insight as to what they contain"
---

## Install a helper script

As we said in the previous section, accessing these files can be tricky. So we've written a very simple
ROOT script in python that will help you list the contents of these directories. We've unimaginitively named it
`list_contents_of_directories.py`. Let's install it first. 

From within your `src` directory, you will pull down this command with `wget`. 

~~~
cd ~/CMSSW_5_3_32/src
cmsenv
wget https://raw.githubusercontent.com/cms-opendata-workshop/workshop-lesson-dataset-scouting/master/scripts/list_contents_of_directories.py
~~~
{: .language-bash}

~~~
Resolving raw.githubusercontent.com... 199.232.36.133
Connecting to raw.githubusercontent.com|199.232.36.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1033 (1.0K) [text/plain]
Saving to: `list_contents_of_directories.py'

100%[====================================================================================================================================================================================================>] 1,033       --.-K/s   in 0s

2020-09-27 07:04:57 (24.1 MB/s) - `list_contents_of_directories.py' saved [1033/1033]
~~~
{: .output}

## Using the script

We can get the usage just by running it without any command-line options.

~~~
python list_contents_of_directories.py
~~~
{: .language-bash}
~~~
To list the contents of any subdirectories of

root://eospublic.cern.ch//eos/opendata/cms/

just add them to the commandline options.

Example:
python list_contents_of_directories.py
python list_contents_of_directories.py Run2011A
python list_contents_of_directories.py Run2011A/SingleMu


200927 07:08:43 091 secgsi_InitProxy: cannot access private key file: /home/cmsusr/.globus/userkey.pem
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/
-------

Commissioning10
MonteCarlo2010
MonteCarlo2011
MonteCarlo2012
MonteCarlo2016
MonteCarlo2018
MonteCarloCASTOR
MonteCarloUpgrade
Run2010A
Run2010B
Run2011A
Run2011B
Run2012B
Run2012C
configuration-files
datascience
derived-data
documentation
environment
hep-tutorial-2012
hidata
luminosity
masterclass-2014
software
trigger-information
upload
validated-runs

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/
~~~
{: .output}

Let's examine what this is telling us.

### Top storage location

By default, the script lists the contents of 

~~~
root://eospublic.cern.ch//eos/opendata/cms/
~~~
{: .code}

This is where the CMS open data is stored. Note that the `root:` that prepends the directory/location tells our script to 
go out to find these ROOT files at `eospublic.cern.ch`. However, you won't be able to just direct your web browser to this location. 

### Listings

The next thing that is printed out is a list of directories. Some of them (e.g. `luminosity`) won't directly contain
datasets of interest, but you should see directories like

~~~
...
MonteCarlo2010
MonteCarlo2011
MonteCarlo2012
...
Run2010A
Run2010B
Run2011A
Run2011B
Run2012B
Run2012C
...
~~~
{: .code}

And these will be the directories where we will start to look for our data.







{% include links.md %}

