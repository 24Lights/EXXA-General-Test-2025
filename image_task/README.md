## Model Experimentation for Latent Representation Learning

### 1. Initial: Simple Autoencoder

To begin, a **basic autoencoder** was implemented to test whether the model could effectively reconstruct the given disk images. The core hypothesis was that if reconstruction is successful, the compressed latent representation (which is significantly smaller than the original image) could be used for downstream unsupervised clustering.

**Result:**
![image](https://github.com/user-attachments/assets/7a9c19b4-81c0-4cd5-b957-d24fae9b7ae4)

**Observations:**
- The reconstructed images appeared blurry and noisy.
- The exoplanet signatures and ring structures were largely lost.
- There was a notable elevation in pixel intensity, which distorted contrast.
- Overall, the model failed to capture fine-grained spatial patterns.

---

### 2. Improvement: Variational Autoencoder (VAE)

To improve upon the limitations of the simple autoencoder, a variational autoencoder (VAE) was implemented. 

Why VAE?
- Unlike a traditional autoencoder, a VAE imposes a probabilistic distribution (typically Gaussian) on the latent space, leading to more meaningful and continuous latent representations.
- It also enables better generalization and smoother interpolation in latent space.

**Result:**
![image](https://github.com/user-attachments/assets/a6b697ca-89bc-40f6-b342-572709233b34)

**Observations:**
- The reconstruction quality slightly improved over the simple autoencoder.
- The overall disk structure was preserved.
- However, pixel intensity remained exaggerated, noise/grain artifacts persisted.

---

### 3. Experiment: AlexNet-based Encoder

Next, **AlexNet** was integrated as the encoder backbone with a convolutional decoder.

**Why AlexNet?**
- AlexNet is a deep CNN pre-trained on ImageNet, capable of extracting high-level hierarchical features.
- The hope was that it could capture more global contextual patterns than shallow encoders.

**Result:**
![image](https://github.com/user-attachments/assets/6cd90a6c-8a26-400a-966f-da5d0877c05d)

**Observations:**
- Despite the architectural depth, the model performed poorly.
- Reconstructed outputs were inaccurate.


---

### 4. Final Architecture: U-Net with Skip Connections

To address the loss of local structures,  **U-Net-based VAE** was used with skip connections between the encoder and decoder layers.

**Why U-Net with Skip Connections?**
- U-Net is specifically designed to preserve spatial resolution, ideal for segmentation and reconstruction tasks.
- Skip connections help the decoder retain low-level edge and boundary information, reducing blurriness and improving ring clarity.

**Result:**
![image](https://github.com/user-attachments/assets/4ede5f4d-3185-42ff-ab26-7307b026e648)
![image](https://github.com/user-attachments/assets/5fbce993-bc94-4de2-bb43-c5801d7a54fe)

---

## Observations & Future Scope

**Key Observations from Best Model (U-Net VAE):**
- Rings are well-preserved, with improved edge smoothness and structure clarity.
- Exoplanet blobs are retained, though slightly enlarged and diffused.
- Background brightness has increased slightly.
- Spiral arms appear smoother but occasionally broader than the original.
- Faint ring structures are highlighted more clearly than in the input image.

**Future work:**
1. To explore attention-based architectures  to capture both global context and fine structures better.
2. Enhance denoising performance by redefining the loss functions, experimenting with alternative formulations and finding a more strategic approach to combine these losses.
3. Combine VAE and GAN to enhance the  reconstructions.

