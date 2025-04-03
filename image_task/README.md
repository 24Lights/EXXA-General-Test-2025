
First , I built a **simple autoencoder** and checked if it can reconstruct the given image. Idea is, if it can reconstruct, then the latent dimension , which is far more lighter than the actual image can be used for clustering.

But the result : 
![image](https://github.com/user-attachments/assets/7a9c19b4-81c0-4cd5-b957-d24fae9b7ae4)


We can observe that the reconstructed image is blurry, has lots of noise , completely avoided the exoplanet presence and ring structure and elevated the pixel intensity


Then i moved on with **variational autoencoders** and it can ( add a point on how vae is better than simple autoencoder for this task) . Slightly better result than before.

![image](https://github.com/user-attachments/assets/a6b697ca-89bc-40f6-b342-572709233b34)

It somewhat preserved the structure but intensified the pixels as before and isse with grains.

Then i experimented with **Alexnet** in the encoder layer and had cnn layers in decoder

![image](https://github.com/user-attachments/assets/6cd90a6c-8a26-400a-966f-da5d0877c05d)

as we can see, it had a bad performance

Then i studied these models, it was evident that model is forgetting the local structures ..........

Then i tried with UNET architecture with skip connections

![image](https://github.com/user-attachments/assets/4ede5f4d-3185-42ff-ab26-7307b026e648)

![image](https://github.com/user-attachments/assets/5fbce993-bc94-4de2-bb43-c5801d7a54fe)

As we can see, the structure is preserved, exoplanets are reconstructed properly .

This is not a perfect reconstruction as w ecan see there is a slight noise and pixels are intensified but its btter than the preious 3 models
