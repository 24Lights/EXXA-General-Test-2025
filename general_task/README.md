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



## 



 




