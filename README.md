# Landscape Classification

**University exam project**, developed for the Introduction to Deep Learning exam at the University of Milano-Bicocca. Authors: Mattia Toffolo, Vasile Cerchez, and Francesco Galimberti.

A comparison of convolutional neural networks for classifying natural and urban landscapes, implemented in R with Keras.

## Data and Approach

The [Intel Image Classification dataset](https://www.kaggle.com/datasets/puneet6060/intel-image-classification) contains about 14,000 training images and 3,000 test images across six classes: buildings, forest, glacier, mountain, sea, and street. Images are processed as 150 x 150 RGB tensors with pixel values rescaled to [0, 1]; 25% of the original training set is reserved for validation.

Six configurations were compared: a baseline CNN, a deeper CNN, dropout, data augmentation, dropout combined with augmentation, and an ImageNet-pretrained VGG19 network fine-tuned from `block4_conv1`.

## Original Results

| Model | Reported Test Accuracy |
| --- | --- |
| Baseline CNN | 75.93% |
| Deeper CNN | 81.88% |
| CNN with dropout | 85.50% |
| CNN with data augmentation | 75.60% |
| CNN with dropout and data augmentation | 72.77% |
| Fine-tuned VGG19 | **91.10%** |

These values come from the original report, not newly reproduced benchmarks. Dropout improved the custom CNN, while augmentation reduced the training/validation gap but lowered test accuracy in these experiments. VGG19 achieved the best reported result, at a higher computational cost. Ambiguous images containing multiple landscape types remain a limitation.

## Repository Contents

- [ConvolutionalNeuralNetworks.R](ConvolutionalNeuralNetworks.R): original analysis, reformatted with relative paths and missing class-directory definitions added.
- [Presentazione.pdf](Presentazione.pdf): original presentation in Italian.
- [relazione_IDL_landscape_classification.pdf](relazione_IDL_landscape_classification.pdf): original written report in Italian.
- [rmakdown_IDL_landscape_classification.pdf](rmakdown_IDL_landscape_classification.pdf): original rendered analysis.
- [install_dependencies.R](install_dependencies.R): installs the R package used by the script.

## Running the Analysis

The dataset and trained models are not included. Download the images from Kaggle and arrange them as follows, preserving all six class subfolders in each split:

```text
intel_immagini/
  train/
    buildings/  forest/  glacier/  mountain/  sea/  street/
  test/
    buildings/  forest/  glacier/  mountain/  sea/  street/
```

With this repository as the R working directory:

```r
source("install_dependencies.R")
# Configure a compatible legacy Keras 2 / TensorFlow backend before training.
source("ConvolutionalNeuralNetworks.R")
```

The helper installs the R package only, not its Python backend. Historical package versions were not recorded; the original generator-based Keras API may need a compatible older environment. Training all six networks is computationally expensive, and VGG19 weights require an initial download. The visualization examples also expect `train/buildings/392.jpg` and at least seven building images.

Model architectures, hyperparameters, and evaluation steps are preserved. Evaluation uses fixed numbers of batches rather than consistently covering the full test set, so reported scores should not be treated as newly verified full-test benchmarks. This repository archives the exam work rather than modernizing its training pipeline. The dataset remains subject to its original terms.
