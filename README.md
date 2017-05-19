# Applying Jet Calibrations and Systematics
## Using xAODAnaHelpers

### package to check out

xAODAnaHelpers

```bash
git clone https://github.com/UCATLAS/xAODAnaHelpers.git
```

Get the recommended tags of the following packages from SVN:
```
JetCalibTools
xAODBTaggingEfficiency
JetUncertainties
JetResolution
JetSelectorTools
JetJvtEfficiency
```

Set up RootCore
```bash
rcSetup Base,2.4.27
```

make a directory for configuration files and copy over the config files you want to use
also copy over any GRL files you need
```bash
mkdir xAODAnaHelpers/data/config
cp config/<config_file> xAODAnaHelpers/data/config
mv <GRL_file.xml> xAODAnaHelpers/data
```

compile RootCore and run setup scripts to prepare for running on the grid
```bash
rc find_packages
rc compile
lsetup rucio
lsetup panda
voms-proxy-init -voms atlas
```

To run jobs on the grid:

```bash
xAH_run.py --files <list_of_ds_names.txt> --config $ROOTCOREBIN/data/xAODAnaHelpers/config/<config_file> --inputList --inputRucio --submitDir <submit_dir> prun --optGridMergeOutput 1.0 --optGridNFilesPerJob 1.0 --optGridOutputSampleName="user.<user_name>.%in:name[1]%.<other_taggs_you_want>"
```

For MC jobs, also include the --isMC option before the prun argument. For AFII MC, include both --isMC and --isAFII