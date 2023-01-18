# Reliability and validity of brain-gastric phase synchronization

Python implementation of the analysis from Levakov et al. 2023 paper, "Reliability and validity of brain-gastric phase 
synchronization".

## Getting started
First make sure you have the following prerequisites:
- Python 3.7+
- FSL
- Docker
- Python packages: numpy, scipy, nibabel, pandas, matplotlib, scikit-learn, nilearn, fslpy, mne-python, bioread, nipype

Prepare the folder structure specified here under [Expected folder structure](#expected-folder-structure).
Copy the data from [link](data) to the corresponding folders in the project folder.
Copy the code from this repository to corresponding folders in the project folder.
Finally, run the main script `main_voxel_based.py` from the project folder.

## Scripts description:
* `main_voxel_based.py` - screens the subjects and runs list, run all the relevant scripts on all of them, then runs the second level analysis.

* Gastric initial preprocessing:
  * `egg_analysis/preprocess_gastric.py` - Preprocessing the EGG data

* Brain initial preprocessing:
  * `brain_analysis/run_fmriprep.py` - Running fMRIprep using Docker SDK
  * `brain_analysis/fmriprep_cleaning.py` - Confound regression
  * `ppu_analysis/add_cardiac_confound.py` - Adds cardiac confound to fmriprep confounds file based on niphlem RETROICOR method
  * `brain_analysis/brain_preprocessing.py`- additional preprocessing steps - spatial smooting + bandpass filtering 

* Assessing gastric-brain synchrony:
  * `synchrony_analysis/signal_slicing.py` - slicing the EGG signal according to the fMRI
  * `synchrony_analysis/voxel_based_analysis.py` - subject-level analysis of gastric-brain coupling
  * `synchrony_analysis/voxel_based_second_level.py` - second level analysis of gastric-brain coupling

* Additional important scripts:
  * `config.py` - defines global variables that are shared across analysis scripts, mainly preprocessing options.
  * `dataframes/brain_meta_data.csv` - a table listing all runs with relevant meta-data, quality control measures and manual configurations if exist (dominant channel, etc.).
  * `gastric_utils.py` - EGG processing related functions
  * `spect_utils.py` - spectrogram related analysis functions

## Expected folder structure:

Folder structure inside [main_project_path]:

    |-- BIDS_data
    |   |-- soroka
    |   |   |-- sub-LA
    |   |   |-- sub-...
    |-- fmriprep
    |   |-- out
    |   |-- tmp
    |   |-- freesurfer
    |   |-- run_logs
    |-- physio
    |   |-- sub-LA
    |   |-- sub-...
    |-- code
    |   |-- egg_analysis
    |   |-- brain_analysis
    |   |-- ppu_analysis
    |-- plots
    |   |-- brain_gast
    |-- derivatives
    |   |-- brain_gast
* BIDS_data - contains the raw data in BIDS format
* fmriprep - contains the fmriprep outputs and temporary files
* physio - contains the electrogastrogram + oximeter data
* code - contains the analysis scripts
* plots - contains the plots generated by the analysis scripts (mainly for quality control)
* derivatives - contains the analysis outputs and intermediate files

## Citing

If you use this code, please cite:

    Levakov, G., Ganor, S. & Avidan, G. (2023), “Reliability and validity of brain-gastric phase synchronization”, Human brain mapping, (under review).

### Issues
Please [raise an issue](https://github.com/GidLev/cepy/issues) if you have any questions/ comments regarding the code.
