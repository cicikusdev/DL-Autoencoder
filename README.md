# Deep Learning-Based Intrusion Detection System (CNN vs. AE-CNN)

## Overview
This repository contains the implementation of a Deep Learning-based Intrusion Detection System (IDS). The project explores and compares two different neural network architectures to classify network traffic as either "Normal" or "Attack" using the benchmark **NSL-KDD dataset**.

## Architectures Investigated
1. **CNN-Based Classifier:** A standard Convolutional Neural Network adapted for 1D structured/tabular network data.
2. **Autoencoder-CNN (AE-CNN) Hybrid Model:** A joint architecture where the *Encoder* part of an Autoencoder is utilized as a feature extractor prior to the CNN classifier. This approach aims to reduce dimensionality and extract robust, non-linear representations of the network traffic before classification.

## Dataset
* **NSL-KDD:** A widely used dataset for evaluating intrusion detection systems. The categorical features were one-hot encoded, and numerical features were scaled appropriately before feeding them into the models.

## Evaluation Metrics & Visualizations
The models are evaluated and compared based on their classification performance on the test set. The following metrics are reported:
* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix

**Visual Analysis Included:**
* Training vs. Validation Loss
* Training vs. Validation Accuracy

## Results
--Standart CNN--
* Accuracy: 0.7524
* Precision: 0.9199
* Recall: 0.6189
* F1-score: 0.7399

--AE-CNN--
* Accuracy: 0.7988
* Precision: 0.9257
* Recall: 0.7030
* F1-score: 0.7991

# Unsupervised Anomaly Detection in Network Traffic using Variational Autoencoders (VAE)

## Overview
This project implements an anomaly-based Intrusion Detection System (IDS) using a **Variational Autoencoder (VAE)**. Unlike traditional signature-based systems or supervised classifiers, this model relies entirely on **unsupervised learning**. The network is trained exclusively on "Normal" network traffic, allowing it to learn the underlying statistical distribution of benign behavior. Any traffic deviating from this learned distribution is flagged as an anomaly (potential attack).

## Architecture Details
The VAE architecture consists of:
* **Encoder:** Compresses the 122-dimensional (post-processing) NSL-KDD input features into a compact 4-dimensional latent space.
* **Reparameterization Trick:** Models the latent space as a continuous statistical distribution (mean and log variance) rather than fixed points, preventing overfitting and enabling robust anomaly detection.
* **Decoder:** Reconstructs the original network traffic features from the sampled latent vector.
* **Custom Loss Function:** A combination of Mean Squared Error (Reconstruction Loss) and KL Divergence.

## Anomaly Detection Strategy
During the testing phase, both normal and malicious packets are fed into the model. The model successfully reconstructs normal traffic (yielding a low Mean Squared Error) but struggles significantly with unseen attack data, resulting in a **high Reconstruction Error**.

An **Anomaly Threshold** was dynamically determined using the 95th percentile of the reconstruction errors from the normal training data. Packets exceeding this threshold are classified as attacks.

## Performance & Results
The model achieved highly reliable metrics, specifically minimizing "alert fatigue" by keeping the false positive rate extremely low.

* **ROC-AUC Score:** 89.49%
* **Precision:** 93.11%
* **Recall:** 78.46%
* **F1-Score:** 85.16%
* **False Positive Rate (FPR):** 7.67%

### Visualizations
The repository includes the following visual analysis:
1. **Reconstruction Error Distribution:** Demonstrating the clear separation between normal traffic and anomalies along with the defined threshold.
2. **ROC Curve:** Visualizing the trade-off between the true positive rate and false positive rate.

## Author
* **Umay Ece & Emirhan Kesim** 
