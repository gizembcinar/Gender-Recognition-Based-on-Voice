
# Gender Recognition Based on Voice
Voice based gender recognition using:
  - **The Free ST American English Corpus dataset**
  - **Mel-frequency cepstrum coefficients (MFCC)**
  - **Gaussian mixture models (GMM)**
  - **K-Means models (GMM)**
  
## Dataset
The  **The Free ST American English Corpus dataset (SLR45)**  can be found on [SLR45](http://www.openslr.org/45/). It is a free American English corpus by [Surfingtech](www.surfing.ai), containing utterances from 10 speakers (5 females and 5 males). Each speaker has about 350 utterances.

## Theory

#### Voice features extraction
Implementation steps of MFCC are given below

1) Frame the signal into short frames.
2) For each frame calculate the periodogram estimate of the power spectrum.
3) Apply the mel filterbank to the power spectra, sum the energy in each filter.
4) Take the logarithm of all filterbank energies.
5) Take the DCT of the log filterbank energies.
6) Keep DCT coefficients 2-13, discard the rest.
7) There are a few more things commonly done, sometimes the frame energy is appended to each feature vector. Delta and Delta-Delta features are usually also appended.


#### Gaussian Mixture Model
According to D. Reynolds in [Gaussian_Mixture_Models](https://pdfs.semanticscholar.org/734b/07b53c23f74a3b004d7fe341ae4fce462fc6.pdf):
A Gaussian Mixture Model (GMM) is a parametric probability density function represented as a weighted sum of Gaussian component densities. GMMs are commonly used as a parametric model of the probability distribution of continuous measurements or features in a biometric system, such as vocal-tract related spectral features in a speaker recognition system. GMM parameters are estimated from training data using the iterative Expectation-Maximization (EM) algorithm or Maximum A Posteriori(MAP) estimation from a well-trained prior model.

#### Algorithm
The steps below are followed in order to develope a robust voice recognition model. Also sklearn, scipy, IPython, python_speech_features libraries are used.

####Training Part :

**1)** Extract All Voice Sample
**2)** Seperate them based on gender with shuffling
**3)** Train Female file (2/3 of dataset)
        •	Feature Extraction: Extract Mel Frequency Cepstral Coefficient
        •	Create a Model: Train GMM models basen on MFCC
        •	Create a Model: Train Kmeans models basen on MFCC
**4)** Save models for two genders as Females and Males

####Testing Part:
**1)** Feature Extraction: Extract Mel Frequency Cepstral Coefficient for testing sample
**2)** Compute likelihoods score by using Males GMM model
**3)** Compute likelihoods score by using Females GMM model
**4)** Compare scores
**5)** Decission male or female according to comparing scores. Biggest one is winner
**6)** Repeate all steps for Kmeans models

## Dependencies
This script require the follwing modules/libraries: sklearn, scipy, IPython, python_speech_features


## Results and disscussion
-  Accuracy of gender detection is **99%** with  MFCC = 12, #Mixture components=16, 	# Kmeans components=16
-  GMM modeling is found to be more suitable than K-means modeling for gender recognition
-  Detailed report can be found **report.pdf** file



