# Task description :
The aim is to discover intrinsic groupings based on learned features without using any explicit labels.

## Initial ideas and data format :

The data given was in .fits, it had a structure below 

![image](https://github.com/user-attachments/assets/9b293a10-6b90-4102-a2f7-91b7fa1591d1)

The relevant data is stored in the Primary segment, with each image having a shape of (600, 600, 4)—i.e., 600×600 pixels across 4 channels. A total of 150 such samples were provided.

My idea was to train an autoencoder model, capture the image features and then use these features to do the clustering.

Several techniques can be used for clustering. I experimented with  K-means, Gaussian mixture models (GMMS), and Hierarchical density-based spatial clustering with noise ( HDBSCAN) 

K - means Simple and efficient for spherical clusters but sensitive to outliers.

Gaussian mixture models: Assumes Gaussian distribution

Hdbscan : Handles noise and discovers clusters of varying densities, but we need to tune the parameters.

## Data preprocessing :

To ensure robustness, two different normalization strategies were applied:

**Global Normalization:** Scaling across all 4 channels simultaneously.

**Per-Channel Normalization:** Each channel was normalized independently to its own min-max range.

## Visualisation of samples :

A sample would look like this 
![image](https://github.com/user-attachments/assets/cab459b7-d97b-4ca8-8f35-dc972b81212e)

 Observations: a.Channel 3 contains minimal information—often appearing as a uniform color or containing redundant contours.
 b. Channels 1 & 2 show strong visual similarity, indicating potential redundancy.

To be sure, a correlation operation is done.

## Channel usefulness :

![image](https://github.com/user-attachments/assets/6c0d1b8e-becd-453b-a222-bf6f9ff7cfac)

![image](https://github.com/user-attachments/assets/7937da38-e997-4b3f-9fe8-65dc3c4cefdd)

We can now safely omit channel 3 and take channel 0, as it explains most of the variance.

## Model building and selection :

NOTE: Although this is a clustering task, reconstruction was performed first to validate the expressiveness of latent embeddings.
Multiple deep architectures from the image reconstruction task were experimented with. The best results for clustering were achieved using a 2D convolutional autoencoder (convauto).

After this step, the latents are extracted for all the image samples. I used PCA and TSNE visualizations, reduced this latent space into 2 components, and then visualized them.


![image](https://github.com/user-attachments/assets/47f12e6d-74d4-46cd-8377-88a0220b4381)
![image](https://github.com/user-attachments/assets/1bf16b88-02e8-45e2-92b6-b7d2ebc77d8d)


To determine the optimal number of clusters, clustering was performed for k = 2 to k = 6 using K-Means, and the Silhouette Score was computed:

![image](https://github.com/user-attachments/assets/66580ec1-656c-4b31-8999-4c6eda721416)

Primarily, I clustered with K-Means but also experimented with Gmms and hdbscan 

Below are the best-scored ones 

![image](https://github.com/user-attachments/assets/6bcbf124-4c0f-4471-9056-47f754998224)

![image](https://github.com/user-attachments/assets/080bbec6-177a-4977-85e3-c11e09edb759)

![image](https://github.com/user-attachments/assets/0cac185f-9179-4517-ae38-34f40fc5b036)

##  Visualising the actual data and observations

I plotted these samples against their ID numbers (list indices) 

![image](https://github.com/user-attachments/assets/a21fc3a1-44c7-4b21-80a9-f4ea355c9cee)

**Observations:**

### Cluster 1
1. Contains samples with consistent global brightness and distinct contour patterns.
2. Multiple well-defined rings and dark gaps.
3. Spiral arms and asymmetries are visible in some disks.
4. The ring structures are often off-center or elliptical, suggesting disk inclination or non-axisymmetry.
5. Disk structures suggest gravitational interactions, indicative of planet-disk coupling.

### Cluster 2
1. Contains more uniformly distributed brightness patterns, possibly representing noise-dominated or feature-absent images.
2. Bright, highly symmetric ring-like structures.
3. Overall smooth brightness gradient, often circular in geometry.
4. These could be debris disks or evolved protoplanetary disks with less massive material.
5. The presence of a central cavity but without internal substructures may suggest that planet formation is advanced or complete.
6. No visible asymmetries, spirals, or warps.





 




