![](https://github.com/DIDSR/VICTRE_PIPELINE/actions/workflows/test.yml/badge.svg) ![](https://img.shields.io/github/license/DIDSR/VICTRE_PIPELINE)

VICTRE AUTOMATIC PIPELINE
===========
![](https://user-images.githubusercontent.com/5750606/41682198-0b250648-74a5-11e8-9578-f93602efa5ab.png)\
***Virtual Imaging Clinical Trial for Regulatory Evaluation***

Clinical trials are expensive and delay the regulatory evaluation and early patient access to novel devices. In order to demonstrate an alternative approach, a recent effort at the Division of Imaging, Diagnostics, and Software Reliability at the U.S. Food and Drug Administration (known as the VICTRE project) demonstrated the replication of one such clinical trial using completely in-silico tools and compared results in terms of imaging modality performance between the human trial and the computational trial. The VICTRE trial involved imaging approximately 3000 digital breast models in digital mammography and digital breast tomosynthesis system models. On this page we are making all the in silico components of VICTRE freely available to the community.

* **Citation:** "Evaluation of Digital Breast Tomosynthesis as Replacement of Full-Field Digital Mammography Using an In Silico Imaging Trial." Aldo Badano, Ph. D., Christian G. Graff, Ph. D., Andreu Badal, Ph. D., Diksha Sharma, M. Sc., Rongping Zeng, Ph. D., Frank W. Samuelson, Ph. D., Stephen Glick, Ph. D., and Kyle J. Myers, Ph. D.  *JAMA Network Open. 2018;1(7):e185474; [doi:10.1001/jamanetworkopen.2018.5474](https://doi.org/10.1001/jamanetworkopen.2018.5474)*.

* **Documentation**: Full documentation can be found here: https://didsr.github.io/VICTRE_PIPELINE/

* **Test the VICTRE Pipeline on precisionFDA**: We created a sample VICTRE full pipeline app on precision FDA that [you can access here](https://precision.fda.gov/home/apps/app-GFVKP880Gqb7fqkf8VvfXFkV-1)  (needs registration).

* **Overview of the VICTRE project** A 1-hour summary presentation of the project and findings was given at the FDA Grand Rounds on 3/14/2019 and [can be found here](https://collaboration.fda.gov/p5wx8epckk7p/).

**Note**: All code is under CC0 (Creative Commons 1.0 Universal License) except for the FBP code that is a derivation of a GPL3 code and remains as GPL3.

*VICTRE team: Aldo Badano, Ph. D., Christian G. Graff, Ph. D., Andreu Badal, Ph. D., Diksha Sharma, M. Sc., Rongping Zeng, Ph. D., Aunnasha Sengupta, Miguel A. Lago, Ph. D., Frank W. Samuelson, Ph. D., Stephen Glick, Ph. D., and Kyle J. Myers, Ph. D.*

Disclaimer
----------

This software and documentation (the "Software") were developed at the Food and Drug Administration (FDA) by employees of the Federal Government in the course of their official duties. Pursuant to Title 17, Section 105 of the United States Code, this work is not subject to copyright protection and is in the public domain. Permission is hereby granted, free of charge, to any person obtaining a copy of the Software, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, or sell copies of the Software or derivatives, and to permit persons to whom the Software is furnished to do so. FDA assumes no responsibility whatsoever for use by other parties of the Software, its source code, documentation or compiled executables, and makes no guarantees, expressed or implied, about its quality, reliability, or any other characteristic. Further, use of this code in no way implies endorsement by the FDA or confers any advantage in regulatory decisions. Although this software can be redistributed and/or modified freely, we ask that any derivative works bear some notice that they are derived from it, and any modified versions bear some notice that they have been modified. 

The VICTRE pipeline
-------------------
The code included in this repository will allow you to compile and execute the full VICTRE pipeline including:

1. Breast phantom generation ([source](https://github.com/DIDSR/breastPhantom), [documentation](https://breastphantom.readthedocs.io/en/latest/))
2. Breast phantom compression ([source](https://github.com/DIDSR/breastCompress), [documentation](https://breastcompress.readthedocs.io/en/latest/))
3. Breast phantom cropping
4. Mass generation ([source](https://github.com/DIDSR/breastMass), [documentation](https://breastmass.readthedocs.io/en/latest/))
5. Lesion insertion
6. MCGPU projection ([source and documentation](https://github.com/DIDSR/VICTRE_MCGPU))
7. DBT reconstruction ([source](https://github.com/DIDSR/VICTRE/tree/master/FBP%20DBT%20reconstruction%20in%20C), [documentation](https://github.com/DIDSR/VICTRE/blob/master/FBP%20DBT%20reconstruction%20in%20C/README_recon.md))
8. Lesion-absent and lesion-present ROI extraction

Requirements
------------
* For phantom generation
  * cmake 3+
  * gcc/g++
  * VTK library
  * Lapack library
  * boost library
* For phantom compression
  * FEBio
  * gcc/g++
  * cmake 3+
  * VTK library
  * Lapack library
  * boost library
* For mass generation
  * gcc/g++
  * cmake 3+
  * VTK library
  * Lapack library
  * boost library
* For MCGPU projection
  * CUDA 10.4+
  * NVIDIA GPU (8GB+ recommended)
  * gzip
  * (Optional) openMPI 
* For reconstruction
  * gcc/g++
* For the unified pipeline script
  * Python 3.6+
  
Installation
------------

Before proceeding, make sure you have all the requirements listed above. You can also install the required libraries using this:

` sudo apt-get install cmake vtk7 libvtk7-dev 
      libblas-dev liblapack-dev libopenmpi-dev
      libboost-dev libboost-program-options-dev 
      libproj-dev zlib1g-dev gzip
`

Clone the repository 

`git clone https://github.com/DIDSR/VICTRE_PIPELINE`

Execute the installation script:

`source install.sh`

Follow the instructions and compile the 5 parts. You might need to edit the `install.sh` file to change the route of some libraries at the beginning.

Install the required python libraries:

`pip install numpy scipy termcolor progressbar2 h5py pydicom`

> You might need to use `pip3` instead of `pip`.

Download `FEBio 2.x` from the [official website](https://febio.org/febio/febio-downloads/) as a standalone executable and add it to the path (replace `{{{routetofebio}}}` with the path to your FEBio installation on this line):

`export PATH="$PATH:{{{routetofebio}}}/FEBio-2.9.1/bin"`

> You can also add that line to your `.bashrc` file to make it permanent. Note the version number for FEBio on the path, it might be different.

Usage
-----

Copy the examples files to the parent folder and run them in a GPU-enabled machine with CUDA:

`python example1.py`

> You might need to use `python3` instead of `python`.

Each example file starts the pipeline from a different step, use `example1.py` to start from the phantom generation (it will need hours to complete), use `example5.py` to start from the projection step (it will finish in about ~10 minutes depending on your computer). When finished, you will find the results in the `results` folder under the `1` subfolder.

* `p_1.raw.gz`: original phantom
* `pc_1.raw.gz`: compressed phantom
* `pc_1_crop.raw.gz`: cropped compressed phantom
* `pcl_1.raw.gz`: compressed original phantom with the inserted lesions
* `pcl_1.loc`: file containing the coordinates of the inserted lesions in the phantom
  * Last number is the lesion type: `1` for calcification clusters, `2` for masses
* `projection_DM1.raw`: contains the DM projection  in raw format
* `reconstruction1.raw`: contains the DBT reconstruction in raw format
* `ROIs.h5`: contains the lesion-present and lesion-absent regions of interest.
* `ROIs`: subfolder will also contain the ROIs in raw format (size is specified in the code, `109 x 109 x 9` in the examples)
  * `ROI_DM_XX_typeT`: DM cropped image for lesion number `XX` of lesion type `T` (absent regions will have `T < 0`)
  * `ROI_DBT_XX_typeT`: DBT cropped volume for lesion number `XX` of lesion type `T` (absent regions will have `T < 0`)
  * `T = 1` for calcification clusters, `T = 2` for masses

> All ``raw`` files are acompanied by an ``.mhd`` file that contains the size information. The ``.mhd`` file can be opened in software like [ImageJ](https://imagej.nih.gov/ij/)

Documentation
-------------

Full documentation can be found here: https://didsr.github.io/VICTRE_PIPELINE/

*This code is currently in development, use with caution.*