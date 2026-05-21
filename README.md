# Monet Style Transfer using CycleGAN

This project is based on the Kaggle competition **GANs – Getting Started (Monet Painting Dataset)**. The goal is to build a generative model that can transform real landscape photographs into Monet-style paintings using deep learning.

This is a classic **image-to-image translation** problem where the model learns to map one visual domain (photos) to another (paintings) without paired examples.

---

## Problem Statement

The objective is to generate realistic Monet-style images from regular landscape photographs.

Since there is no one-to-one mapping between photos and paintings, this is treated as an **unpaired image translation problem**, solved using a CycleGAN model.

The final output is evaluated based on how visually similar the generated images are to real Monet paintings (Kaggle uses MiFID score for evaluation).

---

## Dataset

The dataset is provided by Kaggle and includes:

- `monet_jpg/` – 300 Monet-style paintings  
- `photo_jpg/` – 7038 landscape photographs  

### Key Details:
- Image size: 256 × 256 pixels  
- Format: RGB images  
- No pairing between images in the two domains  

This makes the problem suitable for CycleGAN, which does not require paired training data.

---

## Exploratory Data Analysis (EDA)

During EDA, the dataset was inspected to understand structure and quality.

### Observations:
- Monet dataset is small (300 images) compared to photos (7038 images)
- All images are consistent in size (256 × 256)
- No missing or corrupted images were found
- The two domains have very clear visual differences in style and texture

### Key Insight:
Monet paintings have softer textures and artistic brush strokes, while photos are more detailed and realistic. This difference makes style transfer a suitable use case for GANs.

---

## Data Preprocessing

The following preprocessing steps were applied:

- Resizing all images to 256 × 256 (if needed)
- Normalizing pixel values to [-1, 1]
- Shuffling and batching using `tf.data`
- Applying random transformations (augmentation during training)

---

## Model Architecture

The project uses a **CycleGAN architecture**, which consists of:

### Generator (ResNet-based)
- Convolutional downsampling layers
- Residual blocks (to preserve structure)
- Transposed convolutions for upsampling
- Tanh activation at output

The generator learns to translate images between photo and Monet domains.

### Discriminator (PatchGAN)
- Convolutional network that classifies image patches
- Focuses on local texture and style consistency
- Helps improve fine-grained realism

---

## Loss Functions

The model is trained using multiple loss components:

- **Adversarial Loss** – encourages realistic image generation  
- **Cycle Consistency Loss** – ensures input structure is preserved  
- **Identity Loss** – helps maintain color consistency  

These losses help stabilize training and ensure meaningful translation between domains.

---

## Training Details

- Epochs: 10  
- Batch size: 1  
- Optimizer: Adam (learning rate = 2e-4, β1 = 0.5)  
- Image size: 256 × 256  
- Framework: TensorFlow / Keras  

---

## Model Training

The model was trained using two generators and two discriminators in a cyclic training loop:

- Photo → Monet → Photo  
- Monet → Photo → Monet  

This cycle helps enforce consistency between domains and improves output quality.

---

## Results

After training, the model was able to generate Monet-style images from real landscape photos.

### Observations:
- Early epochs produced blurry or gray outputs
- After continued training, style transfer improved significantly
- Final outputs captured Monet-like colors, brush strokes, and textures
- Semantic structure of input images was preserved

---

## Summary of Setup

| Component | Details |
|----------|--------|
| Model | CycleGAN |
| Generator | ResNet-based (6 residual blocks) |
| Discriminator | PatchGAN |
| Dataset | 7038 photos, 300 Monet paintings |
| Image Size | 256 × 256 |
| Epochs | 10 |
| Evaluation | Visual inspection (MiFID used by Kaggle) |

---

## Key Learnings

- CycleGAN works well for unpaired image-to-image translation
- Residual blocks help preserve structure during style transfer
- PatchGAN is effective for learning texture-level realism
- GAN training is unstable and requires careful tuning
- Small datasets (like Monet paintings) can still produce good results with the right architecture

---

## Challenges

- Training instability in early epochs
- Initial outputs were low quality and gray
- Required careful tuning of learning rate and batch size
- Computational cost was high compared to standard CNN models

---

## Future Improvements

- Train for more epochs to improve image quality
- Experiment with different generator architectures
- Use advanced GAN variants for stability improvements
- Add better evaluation metrics beyond visual inspection
- Try higher-resolution training for sharper outputs

---

## Conclusion

This project demonstrates how CycleGAN can be used for unpaired image-to-image translation. Despite limited Monet training data, the model was able to learn stylistic transformations and generate visually convincing outputs.

It provided hands-on experience with generative models, adversarial training, and deep learning for computer vision tasks.

---

## Author

Nushin Anwar  
Master’s Student – Machine Learning / AI
