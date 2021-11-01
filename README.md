# Studying Property Tax Fraud with Unsupervised ML

## Overview & Results
I analyzed 1 million+ records of New York City properties and uncovered possible property tax fraud. Using **unsupervised outlier detection** algorithms, I narrowed down records which appear suspicious and flagged them for e.g., further human review. The benefit lies in **automating** a process that would otherwise require more manual labor.

## Data Description
1,070,994 records, 32 features, year 2010. Please see `Data_Quality_Report.pdf` for details e.g., histograms and aggregate statistics on individual features.

## Algorithmic Methodology
The two algorithms I used are principal components analysis (PCA) and autoencoder; I implemented them in `scikit-learn` and `Tensorflow`, respectively.

PCA works on mean-centered data, and so the origin --- whether before or after a PCA transform --- corresponds to the mean (i.e. arthimetic average) of all data points. I detected outliers by calculating the distance of each data record to the origin; larger distances correpond to likely outliers, in the sense that they are further away from the mean. In principle, I can detect outliers this way without first applying PCA, but PCA is useful for removing possibly spurious patterns in the data while allieviating the curve of dimensionality. In other words, applying PCA first can help make outlier detection more robust.

An autoencoder provide a compressed representation of the data, and we measure the representation's fidelity by how well the autoencoder reconstructs (training) data records --- e.g. as measured by Euclidean distance. For the purpose of outlier detection, the idea is that the autoencoder would make a larger mistake when reconstructing outliers; therefore, we can flag the hard-to-reconstruct records for e.g. further human review.