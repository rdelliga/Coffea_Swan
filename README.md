# Coffea_Swan
A repository for storing my analysis in coffea with the Swan Notebook (virtual environment used: CentOS 7 gcc11), for Coffea documentation see

https://coffeateam.github.io/coffea/index.html

The branch master contains the codes, when you change one of them and you want to save these local changes to your remote github repository do

git status
git add fileX 
git commit -m “whatever message explaining changes”
git push origin master

the password required to push a change is a token. My accounts's default identity are rdelliga@cern.ch and rdelliga.

The file  WV_VBS_cutscheck.ipynb contains the implementation of cuts without opening multiple files and without using parallelization, which instead are implemented in  WV_VBS_mainAnalysis.ipynb.
The last one read a fileset.json file produced by using the scrit make_fileset_json.ipynb, which read the txt files for the bck events (W+jets) in the folder bkg_files_txt that are produced via shell by the command

voms-proxy-init -voms cms -valid 192:00
dasgoclient -query="file dataset=/WJetsToLNu_HT-100To200_TuneCP5_13TeV-madgraphMLM-pythia8/RunIISummer20UL18NanoAODv9-106X_upgrade2018_realistic_v16_L1v1-v1/NANOAODSIM" > WJetsToLNu_HT-100To200.txt 

where the first line is to obtain valid proxy, while in the second line the command > WJetsToLNu_HT-100To200.txt allows to put the output of the command dasgoclient (see https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookLocatingDataSamples#CliDas) in a txt file.
To search the dataset for the analysis, you can use the data aggregation system (DAS) at the link https://cmsweb.cern.ch/das/ by searching

dataset=/WJetsToLNu_HT*_TuneCP5*/RunIISummer20UL18NanoAODv9-106X_upgrade2018_realistic*/NANOAODSIM

observe that the string is composed of three parts: process/campaign/format. 
Instead the files for the signal are copied locally inside the Coffea/signal_files folder and are obtained by the merging of the files located here:

/eos/cms/store/group/phys_higgs/cmshmm/amarini/

by using the command hadd.
The file output.pkl contains the output of WV_VBS_mainAnalysis.ipynb, which is analyzed in the notebook WV_VBS_mainPlots.ipynb to produce plots, so one doesn't need to run the processor from the start when opening a notebook, but only needs to read the file.
The files Events.C and Events.h are automatically generated and shows the name of all the variables of the Events (Ttree) inside the root file.
To generate those file, you must open a .root file with root and do
Events->MakeClass()




