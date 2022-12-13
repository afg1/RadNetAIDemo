# RadNet AI for Optimising Radiotherapy Outcomes Workshop - Coding demonstration



[![DOI](https://zenodo.org/badge/337491840.svg)](https://zenodo.org/badge/latestdoi/337491840)
<a target="_blank" href="https://colab.research.google.com/github/afg1/RadNetAIDemo/blob/master/AIDemonstrationPractical.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>


This notebook will show, briefly, how to build an autosegmentation model for thoracic OARs using pytorch and pytorch-lightning. We will be using some open data from [The Cancer Imaging Archive (TCIA)](https://www.cancerimagingarchive.net/), originally used for a [AAPM challenge](http://www.autocontouringchallenge.org/). This dataset contains 60 patients, each of which has five OARs segmented.

To handle the data, we will use [pydicom](https://github.com/pydicom/pydicom) to load slices and ideas from [dicom-contour](https://github.com/KeremTurgutlu/dicom-contour) to convert RTSTRUCT objects into masks.

We will be using a suite of pre-built pytorch segmentation models in the excellent [segmentation-models](https://github.com/qubvel/segmentation_models.pytorch) package. This package simplifies the building of a pretrained segmentation network in 2D. We will use a 2D approach, looping over slices in the data to segment 3D organs.

Pytorch can be quite intimidating, but is very powerful when you get to grips with it. In the interests of simplicity, we will use a wrapper around pytorch called [pytorch-lightning](https://pytorch-lightning.readthedocs.io/en/latest/). Lightning separates out the different bits of ML, allowing you to write a bit less boilerplate code, and letting us very quickly and easily use best-practise methods to train our models.


# Overview
The steps in this notebook make the following steps:

0. Install prerequisites and set up
1. Load DICOM data containing CT and segmentation and convert to numpy arrays
2. Define some preprocessing and apply it to the CT slices
3. Create a segmentation model, using a library to make a pre-trained model for our segmentation task
4. Train a the model to reproduce the training examples
5. Test the model against the testing data and produce the AAPM competition ranking score

# Running the notebook
This notebook should run anywhere with python and jupyter installed. It will also run on google colab, if you have access to that.

To get started, you only need python + jupyter, all other dependencies will be installed inside the notebook. If you don't want this to mess with your global python environment, I would reccomend using a virtual environment

To open this notebook in colab, click this link: [colab](https://colab.research.google.com/github/afg1/RadNetAIDemo/blob/master/AIDemonstrationPractical.ipynb)
