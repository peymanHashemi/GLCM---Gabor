# Texture-Based-Feature-Extraction-and-Unsupervised-Semantic-Segmentation
This project focuses on understanding and leveraging texture for feature extraction and semantic segmentation, a critical task in computer vision. The project is divided into two parts: GLCM-based feature extraction and Gabor filter feature extraction, followed by unsupervised clustering for semantic segmentation.

# Part 1: GLCM-Based Feature Extraction and Semantic Segmentation
Description
To extract texture features using Gray Level Co-occurrence Matrices (GLCM) and perform unsupervised semantic segmentation by clustering pixel features.

### * 1. Patch Extraction:

Divide the input image into patches. Each patch represents a window centered around a pixel. The size of the patch determines the granularity of feature extraction.
For each patch, extract the central pixel and treat the patch as a separate image.

### * 2. GLCM Feature Extraction:

Compute the GLCM for each patch to capture texture information. The matrix encodes how often pairs of pixel intensities occur at a specified distance and orientation.
Derive statistical features like correlation, contrast, and homogeneity from the GLCM.

### * 3. Dimensionality Reduction:

Since GLCM computation can be resource-intensive, reduce the number of gray levels and image resolution to speed up processing.

### * 4. Clustering with K-Means:

Use the extracted features to perform clustering with the K-Means algorithm. Each pixel is assigned to a cluster, and the final segmentation map is reconstructed from the cluster assignments.

### * 5. Analysis:

Evaluate the results for different images and explain the limitations of using GLCM for complex textures like stripes or repetitive patterns.

# Part 2: Gabor Filter-Based Feature Extraction and Semantic Segmentation

Description

To extract features using Gabor filters and compare the results with GLCM-based segmentation.

### * 1. Gabor Filters:

Apply a bank of Gabor filters to the image. Each filter is tuned to a specific frequency and orientation, making them ideal for capturing texture details.
Unlike GLCM, Gabor filters operate on the entire image and extract features at every pixel location.

### * 2. Feature Extraction:

Generate a feature map for each pixel based on the Gabor filter responses. These features are then used as inputs for the clustering process.

### * 3. Clustering with K-Means:

Similar to the GLCM approach, apply the K-Means algorithm to the Gabor-based features and reconstruct the segmentation map.

### * 4. Comparison and Analysis:

Compare the performance of GLCM and Gabor filters in segmenting different textures. Discuss the strengths and weaknesses of each method and provide insights into their applications.
