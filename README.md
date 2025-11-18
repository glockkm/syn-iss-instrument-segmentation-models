Syn-ISS Instrument Segmentation (MICCAI 2023)
Baseline models and dataset generation pipeline for the Syn-ISS Challenge: Synthetic Data Surgical Instrument Segmentation.
This work was developed as part of the EndoVis Challenge track at MICCAI 2023 and publicly hosted on Synapse.

Project link: https://www.synapse.org/Synapse:syn50908388/wiki/620516

Overview:
The Syn-ISS Challenge addresses the limitations of real surgical datasets by providing a fully synthetic, simulator-derived dataset for benchmarking instrument segmentation algorithms.
Participants were asked to train models on synthetic data and evaluate performance on held-out synthetic test data. The objective was to validate the use of simulation-based data for developing robust segmentation algorithms transferable to real surgical environments.

Problem Statement:
Surgical data collection and annotation are resource-intensive and limited in scale. Synthetic data offers free ground truth, high variability, and reproducibility.
This challenge provided training and testing datasets derived from a virtual reality surgical simulator video. The models are evaluated on their ability to segment surgical instruments accurately using only synthetic imagery.

Subtasks:
* Binary segmentation

Goal: Identify instrument from background

Input: RGB image 

Output: Binary mask where 1 = instrument, 0 = background

* Multiclass (parts) segmentation

Goal: Identify different parts of instruments

Input: RGB image

Output: Labeled mask where 0 = background, 1 = shaft, 2 = wrist, 3 = jaw

Dataset:
* Images captured from a virtual reality simulator using OBS Studio.

* Automated labeling generated directly from simulation metadata.

* Manual verification on 10% of the dataset for quality control.

* Synthetic dataset includes Bipolar Forceps and Monopolar Scissors.

* Dataset available on Synapse (see project link above).

Important dataset notes:
* White overlay in top-left corner hides non-usable display elements.

* Auto-labeling includes fine detail segmentation and small-pixel artifacts.

* Mask colors and class mapping follow the challenge definitions.

Model Description:
Two baseline models were implemented:

* Binary segmentation model using EfficientNet-based Feature Pyramid Network (FPN) architecture.

* Multiclass segmentation model using the same backbone with modified output channels.

Both models were intentionally kept simple (no custom augmentations or advanced tuning) to serve as a fair and reproducible vanilla baseline for challenge participants.

Files Included:
micc_279_challenge_binary.ipynb – Binary segmentation model notebook that contains training
testing_for_micc_279_binary_model.ipynb – Binary segmentation model notebook that contains testing/inference 
micc_279_challenge_multiclass.ipynb – Multiclass segmentation model notebook that contains both training and testing/inference in the same notebook
NOTE: Full dataset available via Synapse link above

Training Details:
* Framework: PyTorch and segmentation_models_pytorch

* Backbone: EfficientNet encoder

* Loss: Dice + BCE for binary, cross-entropy for multiclass

* Evaluation metrics: IoU, Dice coefficient

* Training/validation split: 80/20 synthetic images

Usage:
Clone the repository:
git clone https://github.com/glockkm/syn-iss-instrument-segmentation-baseline.git

Open the notebooks in Jupyter or Colab.

Adjust dataset paths and train the model using provided cells.

Evaluate predictions and visualize segmentation overlays.

Example Output:
Input image: synthetic surgical scene
Output (binary mask): highlighted instrument pixels
Output (multiclass mask): shaft (yellow), wrist (red), jaw (green)

Follow the steps below to reproduce the experiments and visualize results:
* Environment setup
Install dependencies either via pip or Conda.

pip install -r requirements.txt
or
conda env create -f environment.yml
conda activate syn-iss-seg

* Dataset preparation
The synthetic dataset can be downloaded from the Synapse challenge page:
https://www.synapse.org/Synapse:syn50908388/wiki/620516

Unzip the dataset and set the correct image and mask directory paths inside each notebook before running.

* Binary segmentation baseline
a. Open micc_279_challenge_binary.ipynb

Trains a binary segmentation model using an EfficientNet-based Feature Pyramid Network (FPN).

Produces a model checkpoint after training.

b. Open testing_for_micc_279_binary_model.ipynb

Loads the trained binary model and runs inference on test images.

Visualizes predicted instrument masks and evaluates Dice/IoU scores.

* Multiclass segmentation baseline
a. Open micc_279_challenge_multiclass_cleaned.ipynb

Trains a multiclass segmentation model for instrument part segmentation (shaft, wrist, jaw).

Includes built-in inference and visualization after training.

Evaluates class-wise segmentation performance on synthetic test data.

* Viewing results
The notebooks output visual comparisons showing:

Original simulator image

Ground truth mask

Predicted binary or multiclass segmentation mask
Quantitative metrics such as IoU and Dice coefficients are printed after inference.

Notes:
All notebooks are compatible with Google Colab.

GPU runtime is recommended for training.

Model weights and results can be saved to Drive or local storage as configured in the notebooks.

Organizers:
Anand Malpani
Kimberly Glock

This work was part of the MICCAI 2023 EndoVis Syn-ISS Challenge and supported by Surgical Science.

License:
MIT License — for academic and research demonstration only.
