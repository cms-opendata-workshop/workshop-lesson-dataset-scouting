---
title: "What data and Monte Carlo are available?"
teaching: 5
exercises: 10
questions:
- "What data and run periods are available?"
- "What triggers were used when the data was taken?"
- "What Monte Carlo samples are available?"
objectives:
- "To be able to navigate the directory structure"
- "To be able to find what triggers and Monte Carlo datasets there are by finding the relevant directories"
keypoints:
- "The triggers are all given their own subdirectories"
- "The Monte Carlo samples all have their own subdirectories"
- "Navigating these directories is a good first-order way to find out what is available"
---

## Data and triggers

We make a distinction between *data* which comes from the real-life CMS detector
and *Monte Carlo* data. In general, when we say *data*, we mean the real, CMS-detector-created
data.

The main data available is from what is known as **Run 1** and spans 2010-2012. These run
periods can also be broken into **A**, **B**, **C**, and so-on, sub-periods. 

Let's run our script again, but focusing on the data directories

~~~
python list_contents_of_directories.py
~~~
{: .language-bash}

~~~
...
Run2010A
Run2010B
Run2011A
Run2011B
Run2012B
Run2012C
...
~~~
{. output}

We can take a closer look at this by adding one of these directories to our script
as a command-line argument.

~~~
python list_contents_of_directories.py Run2012B
~~~
{: .language-bash}
~~~
...
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/Run2012B
-------

BJetPlusX
BTag
Commissioning
DoubleElectron
DoubleMuParked
DoublePhoton
DoublePhotonHighPt
ElectronHad
HTMHTParked
HcalNZS
JetHT
JetMon
MET
MinimumBias
MuEG
MuHad
MuOnia
MuOniaParked
NoBPTX
PhotonHad
SingleElectron
SingleMu
SinglePhoton
TauParked
TauPlusX
VBF1Parked
db

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/Run2012B
~~~
{: .output}

These are a listing of the *triggers* which were used when the data was collected. You will have
a dedicated lesson on working with and understanding these triggers but for now, just know that they
select out some subset of the collisions based on certain criteria. 

Some of them are quite difficult to intuit what they mean. Others should be roughly understandable. For example, 

* **SingleMu** required at least one muon above a certain momentum threshol. 
* **DoublePhoton** required at least two photons above a certain energy threshol. 

**MinimumBias** events are taken without any trigger or selection criteria. 

For more information on these triggers, you can either reach out to the 
organizers through [Mattermost](https://mattermost.web.cern.ch/cmsopeyyndatatheo/channels/town-square)
or wait until the dedicated trigger lesson. 

### Data formats

Let's look a little futher down the directory tree and see what's in `Run2012B/SingleMu`.

~~~
python list_contents_of_directories.py Run2012B/SingleMu
~~~
{: .language-bash}
~~~
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu
-------

AOD
IG
RAW

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu
~~~
{: .output}

These directory names refer to specific file formats. 

* **AOD** stands for *Analysis Object Data*. This is the first stage of data where analysts can really start
physics analysis. Often, the experiment will slim this down and drop some subsets of the data stream into 
*MiniAOD* or the newer *NanoAOD*, but the Run 1 open data is only available for analysis in AOD format.
* **IG** contains files in the `.ig` format which is used in the [ispy](https://ispy.web.cern.ch/1.5.0/)
event-visualization outreach tool. These are not a focus of this workshop. 
* **RAW** files contain information directly from the detector in the form of hits from the TDCs/ADCs. 
These files are not a focus of this workshop. 

### Global tags

If we go even further into the directory, we find
~~~
python list_contents_of_directories.py Run2012B/SingleMu/AOD
~~~
{: .language-bash}
~~~
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu/AOD
-------

22Jan2013-v1

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu/AOD
~~~
{: .output}

This **22Jan2013-v1** is referred to as a *global tag*. It tells the user information about when the 
data was processed and under what conditions it was processed. For example, data is sometimes reprocessed
if studies show that certain calibrations should be updated. We keep track of these calibrations
and reprocessing by assigning that data a *global tag*. 

Given the option and in the absence of other information, you will want to use the latest global tag. 

### ROOT files

Going futher, you will see a listing of numbers, which are just there
based on how the dataset is broken up into smaller chunks and subdirectories
during processing. And then further down from there, are the actual ROOT files!

~~~
python list_contents_of_directories.py Run2012B/SingleMu/AOD/22Jan2013-v1
~~~
{: .language-bash}
~~~
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu/AOD/22Jan2013-v1
-------

110000
20000
20001
20002
20003
20008
20009
20011
20012
20014
20016
20020
20023
20025
20033
20036
20040
30000
30001
30003
30004
file-indexes

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu/AOD/22Jan2013-v1
~~~
{: .output}

~~~
python list_contents_of_directories.py Run2012B/SingleMu/AOD/22Jan2013-v1/20000
~~~
{: .language-bash}
~~~
.
.
.
FC58E224-9471-E211-9572-00259073E374.root
FC623E1C-8C71-E211-AC88-90E6BA0D09B8.root
FC6E5D56-DB71-E211-BABA-E0CB4E29C4F9.root
FC7CDD10-CF71-E211-B9D7-BCAEC53F6D3A.root
FC9044D4-6D71-E211-8531-00259074AE28.root
FCB77912-B571-E211-A66E-00259073E37C.root
FCC962A5-F471-E211-9A79-00261834B516.root
FE033819-CF71-E211-AC74-001E4F3F28C0.root
FE089BBA-6171-E211-9544-00259073E488.root
FE3E5F01-6271-E211-B9EA-00261834B5C1.root
FE3FA220-A471-E211-9E4D-E0CB4E1A1185.root
FE698811-CB71-E211-84E8-E0CB4E29C4D0.root
FE699E57-6571-E211-82D9-20CF305616CC.root
FEA5DE2A-CF71-E211-8166-20CF3027A635.root
FEE493EA-CA71-E211-BD26-001EC9D825CD.root
FEECE39E-8271-E211-8925-20CF305B055B.root
FEFAC0F5-9071-E211-9389-E0CB4E1A11A2.root
FEFB25CE-6171-E211-BDDB-001EC9D27648.root

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/Run2012B/SingleMu/AOD/22Jan2013-v1/20000
~~~
{: .output}


## Monte Carlo

We can go through a similar exercise with the Monte Carlo data. One major difference is that
the Monte Carlo is not broken up by trigger. Instead, when you analyze the Monte Carlo, you will
apply the trigger to the data to simulate what happens in the real data. You will learn
more about this in the trigger exercise. 

Let's look at some of the datasets. 

### Monte Carlo samples

Let's start by looking at what Monte Carlo datasets we have. 

~~~
python list_contents_of_directories.py
~~~
{: .language-bash}

~~~
...
MonteCarlo2010
MonteCarlo2011
MonteCarlo2012
...
~~~
{. output}

~~~
python list_contents_of_directories.py MonteCarlo2012
~~~
{: .language-bash}
~~~
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/MonteCarlo2012
-------

Summer12
Summer12_DR53X

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/MonteCarlo2012
~~~
{: .output}

We see that there are two directories corresponding to when the data was processed. 
Let's look at the second of these. Get ready! There's a lot of output!

~~~
python list_contents_of_directories.py MonteCarlo2012/Summer12_DR53X
~~~
{: .language-bash}
~~~
ADDdiLepton_LambdaT-1600_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-2000_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-2400_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-2800_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-3200_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-3600_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-4000_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-4400_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-4800_Tune4C_8TeV-pythia8
ADDdiLepton_LambdaT-5200_Tune4C_8TeV-pythia8
B0ToJpsiKs_BFilter_TuneZ2star_8TeV-pythia6-evtgen
BBH_HToTauTau_M_125_TuneZ2star_8TeV_pythia6_tauola
.
.
.
tGamma_FCNC_tGc_scaleup_8TeV_protos
tGamma_FCNC_tGu_8TeV_protos
tGamma_FCNC_tGu_mass170_5_8TeV_protos
tGamma_FCNC_tGu_mass174_5_8TeV_protos
tGamma_FCNC_tGu_scaledown_8TeV_protos
tGamma_FCNC_tGu_scaleup_8TeV_protos
ttGG_8TeV-whizard-pythia6
ttbarZ_8TeV-Madspin_aMCatNLO-herwig

The above are the contents of the following directory: 

root://eospublic.cern.ch//eos/opendata/cms/MonteCarlo2012/Summer12_DR53X
~~~
{: .output}

That's a lot of Monte Carlo samples! It's up to you to determine which ones 
might contribute to your background. The names try to give you some sense of
the primary process, subsequent decays, the beam energy 
and specific simulation software (e.g. Pythia), but if you have questions, 
reach out to the organizers through [Mattermost](https://mattermost.web.cern.ch/cmsopeyyndatatheo/channels/town-square).

## Data format

Going a bit deeper, we find another difference between the Monte Carlo and data. 

~~~
python list_contents_of_directories.py MonteCarlo2012/Summer12_DR53X/TTJets_SemiLeptMGDecays_8TeV-madgraph
~~~
{: .language-bash}
~~~
--------------------------------
Listing the contents of

root://eospublic.cern.ch//eos/opendata/cms/MonteCarlo2012/Summer12_DR53X/TTJets_SemiLeptMGDecays_8TeV-madgraph
-------

AODSIM

The above are the contents of the following directory:

root://eospublic.cern.ch//eos/opendata/cms/MonteCarlo2012/Summer12_DR53X/TTJets_SemiLeptMGDecays_8TeV-madgraph
~~~
{: .output}

**AODSIM** is just like the **AOD** format in the data, except that it from the *simulated* Monte Carlo
data. Otherwise, you can process it just like the regular data. One difference is that you will
want to select the Monte Carlo events that pass certain triggers at the time of your analysis, while
that selection was already done in the data by the detector hardware/software itself. 

And going further down, you can find Monte Carlo-specific global tags and then the usual substructre
of directories before coming to the ROOT files. 

> ## Challenge!
> Think about an analysis that you might want to perform. Use the above approach to identify
> * What trigger would be appropriate to search for this signal
> * What Monte Carlo samples might help simulate the background, given the trigger you have chosen
{: .challenge}


{% include links.md %}

