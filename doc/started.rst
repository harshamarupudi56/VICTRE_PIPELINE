Getting started
===============

Requirements
------------

dependencies:

python=3.7
numpy
scipy
numba
mkl
matplotlib
scikit-image
scikit-learn
spyder
ipython
glob2
pip:
pynrrd # image/data file formats
pydicom
h5py
nibabel
python-csv
temp
sys
os
subprocess


Installation
------------

Before proceeding, make sure you have all the requirements listed above.

Fiji can be installed from the official website. BoneJ must be added as a plugin within the Fiji installation. Instructions can be found from the official website.

Clone the repository

git clone https://github.com/BoneJ_Headless

Execute the installation script:

source install.sh

Install the required python libraries.
Usage
-----

First try BoneJ_Module.py to launch individual metrics on a single image:

BoneJ_Module.py

You might need to use python3 instead of python.

Each example requires an input and output directory to set by the user, along with the voxel size of the image, and the Fiji directory path.

All image segmentation files are acompanied by an .nrrd. The .nrrd file can be opened in software Fiji as well. Sample ROIs are included in Data/Trabecular_Bone_ROIs
