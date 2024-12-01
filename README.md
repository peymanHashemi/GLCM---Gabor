# Texture-Based-Feature-Extraction-and-Unsupervised-Semantic-Segmentation
This project focuses on understanding and leveraging texture for feature extraction and semantic segmentation, a critical task in computer vision. The project is divided into two parts: GLCM-based feature extraction and Gabor filter feature extraction, followed by unsupervised clustering for semantic segmentation.

# Content
- Table of Contents
  * [Part 1: GLCM-Based Feature Extraction and Semantic Segmentation](#part-1-glcm-based-feature-extraction-and-semantic-segmentation) 
  * [Part 2: Gabor Filter-Based Feature Extraction and Semantic Segmentation](#part-2-gabor-filter-based-feature-extraction-and-semantic-segmentation)  
  * [METHOD Part 1](#Part-1)
  * [METHOD Part 2](#Part-2)
 

# Part 1: GLCM-Based Feature Extraction and Semantic Segmentation
Description
To extract texture features using Gray Level Co-occurrence Matrices (GLCM) and perform unsupervised semantic segmentation by clustering pixel features.

* ### 1. Patch Extraction:

Divide the input image into patches. Each patch represents a window centered around a pixel. The size of the patch determines the granularity of feature extraction.
For each patch, extract the central pixel and treat the patch as a separate image.

* ### 2. GLCM Feature Extraction:

Compute the GLCM for each patch to capture texture information. The matrix encodes how often pairs of pixel intensities occur at a specified distance and orientation.
Derive statistical features like correlation, contrast, and homogeneity from the GLCM.

* ### 3. Dimensionality Reduction:

Since GLCM computation can be resource-intensive, reduce the number of gray levels and image resolution to speed up processing.

* ### 4. Clustering with K-Means:

Use the extracted features to perform clustering with the K-Means algorithm. Each pixel is assigned to a cluster, and the final segmentation map is reconstructed from the cluster assignments.

* ### 5. Analysis:

Evaluate the results for different images and explain the limitations of using GLCM for complex textures like stripes or repetitive patterns.

# Part 2: Gabor Filter-Based Feature Extraction and Semantic Segmentation

Description

To extract features using Gabor filters and compare the results with GLCM-based segmentation.

* ### 1. Gabor Filters:

Apply a bank of Gabor filters to the image. Each filter is tuned to a specific frequency and orientation, making them ideal for capturing texture details.
Unlike GLCM, Gabor filters operate on the entire image and extract features at every pixel location.

* ### 2. Feature Extraction:

Generate a feature map for each pixel based on the Gabor filter responses. These features are then used as inputs for the clustering process.

* ### 3. Clustering with K-Means:

Similar to the GLCM approach, apply the K-Means algorithm to the Gabor-based features and reconstruct the segmentation map.

* ### 4. Comparison and Analysis:

Compare the performance of GLCM and Gabor filters in segmenting different textures. Discuss the strengths and weaknesses of each method and provide insights into their applications.

Here's how you can include the clickable links in your README file:

---

### **References and Resources**

For further guidance, you can use the following resources:  

1. [Patch Extraction from Image](https://scikit-image.org/docs/stable/api/skimage.util.html#skimage.util.view_as_window)  
2. [GLCM Guide](https://scikit-image.org/docs/stable/auto_examples/features_detection/plot_glcm.html)  
3. [Parallel Processing of Patches](https://stackoverflow.com/questions/48373944/how-to-apply-a-function-in-parallel-to-multiple-images-in-a-numpy-array)  

---

# METHOD

## Part 1
* ### 1. Patch Extraction
I began by splitting each input image into small, fixed-size patches. The center pixel of each patch acted as the reference point for extracting local texture features. I used this approach to ensure that features were contextually relevant rather than relying solely on global image statistics. The patch size was a critical parameter, as smaller patches retained local details while larger ones captured broader texture patterns.

* ### 2. GLCM Feature Calculation
For each patch, I computed a Gray Level Co-occurrence Matrix (GLCM). This matrix helped quantify the spatial relationship between pixel intensities. I focused on key statistical features like dissimilarity, contrast, homogeneity, and energy. Depending on the task, I adjusted the distance and angles used for calculating GLCM to capture texture patterns effectively.

* ### 3. Clustering with K-Means
After extracting features for all patches, I passed them to the K-Means clustering algorithm. The idea was to group pixels into clusters based on their texture features. This step effectively segmented the image into regions with similar texture properties.

* ### 4. Challenges and Optimization
One significant challenge was computational complexity. To manage this, I reduced the number of gray levels and employed parallel processing when extracting features from large images. These optimizations drastically reduced runtime without sacrificing accuracy.

## Results Part 1:

<img style="width:700px" src="https://github.com/user-attachments/assets/36fe3f42-6b0b-4e75-8224-75813a073017"> <br>
<img style="width:500px" src="https://github.com/user-attachments/assets/3bf45e55-ecc1-46af-838c-be0c1453946d"> 

### ** For  step by step results check notebook**

* ### Analysis

  ### Strengths:
     The GLCM method performed well in distinguishing regions with distinct texture, such as separating objects from the background. It effectively captured fine details, which were useful        in scenarios with subtle texture differences.
  ### Weaknesses:
     The method struggled with textures that were similar in GLCM metrics but differed visually, like striped patterns. Additionally, the reliance on local patches sometimes led to blocky         segmentation when patches spanned regions with varying textures.

## Part 2

* ### 1. Applying Gabor Filters
In this part, I used a bank of Gabor filters tuned to different orientations and frequencies. These filters are excellent for capturing texture patterns because they mimic the human visual system's response to edges and textures. I applied the filters directly to the entire image, generating feature maps that highlighted specific texture components.

* ### 2. Feature Extraction and Clustering
For each pixel, I extracted the response values from all applied Gabor filters. This created a feature vector for each pixel, which I then fed into the K-Means algorithm. The clustering results were used to segment the image based on texture patterns.

* ### 3. Parameter Tuning
I experimented with different filter sizes, scales, and orientations to find the optimal settings for each image. Larger filters captured broader patterns, while smaller ones focused on finer details. This flexibility allowed for more adaptive feature extraction compared to the patch-based GLCM approach.

## Results Part 1:

<img style="width:800px" src="https://github.com/user-attachments/assets/cbb4a1f4-d1bb-47d1-96ae-e43786f3eeb0"> <br>
<img style="width:900px" src="https://github.com/user-attachments/assets/8693e1d2-0e87-44ce-9960-830b58324f65"> 

* ### Analysis
 
  ### Strengths:
     Gabor filters excelled at capturing edge-based and repetitive textures, making them ideal for images with well-defined patterns. They were also computationally efficient since they           operated on the entire image without the need for patch extraction.
  ### Weaknesses:
     The method was sensitive to variations in texture orientation and scale. In some cases, slight changes in filter parameters led to significant differences in segmentation results,            requiring careful tuning.

* ### Comparison and Conclusion
  
  ### GLCM vs. Gabor:
     While GLCM provided detailed local texture features, it was computationally expensive and less flexible. On the other hand, Gabor filters offered a more holistic approach to texture          analysis, albeit with sensitivity to parameter choices.

  ### Best Use Cases:
     GLCM is ideal for tasks that require fine-grained texture analysis, especially when local context is crucial. Gabor filters are better suited for images with distinct edge-based              textures and repetitive patterns.
