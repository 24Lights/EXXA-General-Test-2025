# Task description :
To perform clustering of given data based on some features which are not explicitly available. This is purely an unsupervised learning task

## Initial ideas and data format :

The data given was in .fits , it had a structure as below 

![image](https://github.com/user-attachments/assets/9b293a10-6b90-4102-a2f7-91b7fa1591d1)

Here, the first one,i.e the primary is the relevant one . This has the shape (600,600,4). There are total 150 such samples.

My idea was to train an autoencoder model , capture the image features and then use these features to do the clustering.

For clustering , there are several techniques which can be used . I experimented with  K-means , Gaussian mixture models (GMMS) and Heirarcial density based spacial clustering with noise ( HDBSCAN) 

K - means : (give a pro and a con)

Gaussian mixture models :(give a pro and a con)

Hdbscan :(give a pro and a con)

## Data preprocessing :

I normalised the data in 2 different ways , a. normalise throughout the image ( across all 4 channels) b. normalised every channel separately to experiment with the robustness of each technique

## Visualisation of samples :

A sample would look like this 
![image](https://github.com/user-attachments/assets/cab459b7-d97b-4ca8-8f35-dc972b81212e)

 Observations: a. we can clearly see that the channel 3 has not much information with it . Either entirely a color fill or very slight curves which are already covered in other channels
 b. we can also see that channel 1,2 is almost similar to each other

To be sure , a corelation operation is done.

## Channel usefulness :

![image](https://github.com/user-attachments/assets/6c0d1b8e-becd-453b-a222-bf6f9ff7cfac)

![image](https://github.com/user-attachments/assets/7937da38-e997-4b3f-9fe8-65dc3c4cefdd)

We can now safely omit channel 3 and take channel 0 only as it explains most of the variance

## Model building and selection :

NOTE : In the notebook run there will be reconstructions as well for this task as i done that first and then used the latents to perform clustering . I experimented all the models from Image task to see which model's latents are better for clustering. Finally i used AutoEncoders with 2d convolutional layers ( named as 'convauto')

After this step , the latents are extracted for all the image samples . I used PCA and TSNE visualisations , reduced this latent space into 2 components and then visualised them .


![image](https://github.com/user-attachments/assets/47f12e6d-74d4-46cd-8377-88a0220b4381)
![image](https://github.com/user-attachments/assets/1bf16b88-02e8-45e2-92b6-b7d2ebc77d8d)


Then the clustering was done. I had to choose the n_clusters. So i experimented with a range of clusters from 2 to 6 and checked the silhoutte scores. It was found that n_clusters = 2 has the best silhoutte score overall 

![image](https://github.com/user-attachments/assets/66580ec1-656c-4b31-8999-4c6eda721416)

Primarily i clustered with K-Means but also experimented Gmms and hdbscan 

The below are the best scored ones 

![image](https://github.com/user-attachments/assets/6bcbf124-4c0f-4471-9056-47f754998224)

![image](https://github.com/user-attachments/assets/080bbec6-177a-4977-85e3-c11e09edb759)

![image](https://github.com/user-attachments/assets/0cac185f-9179-4517-ae38-34f40fc5b036)

##  Visualising the actual data and observations

I plotted these samples against their ID numbers (list indices) 

![image](https://github.com/user-attachments/assets/a21fc3a1-44c7-4b21-80a9-f4ea355c9cee)

Observations :

Cluster 1 : <placeholder>

Cluster 2 : <placeholder>




 




