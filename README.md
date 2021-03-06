# 2010-mu-mumonitor-dimuon
Validation code for 2010 Mu and MuMonitor datasets, based on dimuon mass spectrum.

You need to work in a Virtual Machine properly contextualized for CMS.
Everything is available on the CERN Open Data Portal http://opendata.cern.ch/VM/CMS/2010.

In order to run the demoanalyzer_cfg.py to create the Commissioning ROOT files, 
you need to create a working area and set up a proper CMS environment.

## Creating the Working Area

This step is only needed the first time.
```
cmsrel CMSSW_4_2_8
```
## Cloning the 2010-commissioning-dimuon repository from Github
Type this command to change directory:
```
cd CMSSW_4_2_8/src
```
For cloning type:
```
git clone https://github.com/cms-opendata-validation/2010-mu-mumonitor-dimuon  Validation/Mu_Mumonitor_dimuon_2010
```

## Setting up the CMS environment
```
cd Validation/Mu_Mumonitor_dimuon_2010
cmsenv
```

## Compiling and Running
```
scram b
cmsRun demoanalyzer_cfg.py
```

After analysis, Mu00.root file should be created. 
Then, is necessary to change input and also output files in demoanalyzer_cfg.py, to save these changes and to rerun program. 
In the datesets directory in the repository from github are index files with names:

```
 CMS_Run2010B_Mu_AOD_Apr21ReReco-v1_0000_file_index.txt
 CMS_Run2010B_Mu_AOD_Apr21ReReco-v1_0001_file_index.txt
 CMS_Run2010B_Mu_AOD_Apr21ReReco-v1_0002_file_index.txt
 CMS_Run2010B_Mu_AOD_Apr21ReReco-v1_0003_file_index.txt
 CMS_Run2010B_Mu_AOD_Apr21ReReco-v1_0004_file_index.txt
 CMS_Run2010B_Mu_AOD_Apr21ReReco-v1_0005_file_index.txt
```
 
These index files are the same as you can find in the open data portal record http://opendata.cern.ch/record/14 , they are copied here for convenience and also for details of the 
analysis you can read comments in the analysis code Mu_MumonitorAnalyzer.cc .        
It necessary to note that whole analysis can take around 21 hours! 
 
When you rerun all six index files you should have six root files with names:
```
 Mu00val.root
 Mu01val.root
 Mu02val.root
 Mu03val.root
 Mu04val.root
 Mu05val.root
```
 
The last thing what you should do is to merge these six root files into one root file.
You do this as follow. In the downloaded repository is also file with name mergeMu.C .
Press command for opening ROOT program: 
```
root
```
In this programe just type command:
```
.x mergeMu.C .
```
This merging creates a root file called MuAllval.root .
To look at this output, write down command in ROOT program: 
```
new TBrowser
```
and navigate to relevant file. The most interesting histogram is GM_mass_log. This is the validation histogram.
