# EXOnanoAOD
Development of custom cms EXO PAG nanoAOD format


## Setup in CMSSW
```
cmsrel CMSSW_15_0_0_pre3
cd CMSSW_15_0_0_pre3/src
cmsenv
git cms-init
mkdir PhysicsTools
cd PhysicsTools
git clone git@github.com:kerstinlovisa/EXOnanoAOD.git
scram b -j
```
## Enable MDSnano tables
Before EXOnanoAOD is integrated into cmssw, we need the following commit to include the simple table to produce new data-type
```
git remote add kakwok git@github.com:kakwok/cmssw.git 
git cms-addpkg PhysicsTools/NanoAOD
git cherry-pick fb5f0b9 
```
Then un-comment the line in `custom_exo_cff.py`

# Setup
Please include your customizations as python scripts under `python`, and if you need a custom producer add it under `plugins`.

We advice to use the templates in the branch `EXOnanoAOD_template` as base and create a new branch from there. 
```
git checkout EXOnanoAOD_template
git checkout -b your_branch_name
```
Rename the plugin in `plugins/EXOnanoAODProducerTemplate.cc` and python script in `python/custom_exonanoaod_template_cff.py`, and fill them in for your customizations. Edit the test script in `test/Run3_2023_PAT_EXONANO_template.py` to include your customizations under `# EXOnanoAOD customisation`. 

# Test run AOD -> EXOnanoAOD for Run 3
In `test` there is a test config file for Run 3 2023 which runs over one MC file (from TTto2L2Nu dataset). It will run AOD to NanoAOD format directly. 

After adding your customization functions at the end of the script under `# EXOnanoAOD customisation` you should be able to run your customizations with:
```
cmsRun Run3_2023_PAT_EXONANO_template.py
```

# Event size of customized NanoAOD
Check the event size of your custom EXOnanoAOD implementations in your nanoAOD root file (replace `nanoAOD.root`) by running:
```
git cms-add
$CMSSW_BASE/src/PhysicsTools/NanoAOD/test/inspectNanoFile.py nanoAOD.root --size size.html
```
