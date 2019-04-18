fmriqa
======

qa scripts for fMRI data

- creates a summary report of quality for an fMRI dataset
- estimates FD/DVARS (Power et al., 2012)
- performs Greve et al./fBIRN spike detection

Dependencies:
- statsmodels
- numpy
- nibabel
- matplotlib
- scikit-learn
- reportlab

USAGE: fmriqa.py bold_mcf.nii.gz (or any suitably named file)

- this main program takes in a motion-corrected image and performs QA
-- report is saved to a subdirectory called QA
- it assumes that the following also exist in the same directory (if infile is called bold_mcf.nii.gz):
-- bold_mcf_brain_mask.nii.gz: BET mask
-- bold_mcf.par: motion parameters generated by mcflirt

Useful output files for accounting for motion in first level feat models (found in QA dir):
- confound12.txt
  - columns 1-6:   motion parameters from mcflirt (translation and rotation in x, y, and z directions)
  - columns 7-12:  derivatives of motion parameters

- confound24.txt
  - first 12 columns are from confound12.txt
  - second 12 columns are first 12 squared
 
- fd.txt
  - framewise displacement (1=volume above threshold, 0=volume below threshold)

- dvars.txt
  - DVARS: square root of the variance in intensity between consecutive volumes

- scrubdes.txt
  - tr x nuisance regressor(s) dummy coded for volumes above FD threshold
  
- scrubvol.txt
  - volumes above threshold
  
- confound.txt
  - confound12.txt
  - fd.txt
  - dvars.txt
  - scrubdes.txt
