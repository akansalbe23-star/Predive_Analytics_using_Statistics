# Learning Probability Density Function using GAN

## Overview
This project focuses on learning an unknown probability density function (PDF) using data only.
A Generative Adversarial Network (GAN) is used to implicitly model the distribution of a nonlinear
transformation of NO₂ concentration values without assuming any parametric form.

## Dataset
- Name: India Air Quality Data
- Source: Kaggle
- Feature Used: NO₂ concentration (NO2)
- Missing values are removed during preprocessing

## Transformation
The original variable x (NO₂ concentration) is transformed as:
z = x + a_r * sin(b_r * x)

where:
- a_r = 0.5 * (r mod 7)
- b_r = 0.3 * ((r mod 5) + 1)
- r is the university roll number

This nonlinear transformation makes the probability distribution of z analytically unknown.

## GAN Architecture
A one-dimensional GAN is used to learn the distribution of z.

### Generator
- Input: Gaussian noise sampled from N(0,1)
- Layers:
  - Linear (1 → 32) + ReLU
  - Linear (32 → 32) + ReLU
  - Linear (32 → 1)
- Output: Generated sample z_f

### Discriminator
- Input: Real z or generated z_f
- Layers:
  - Linear (1 → 32) + LeakyReLU
  - Linear (32 → 32) + LeakyReLU
  - Linear (32 → 1) + Sigmoid
- Output: Probability of the sample being real

## Training Details
- Loss Function: Binary Cross-Entropy
- Optimizer: Adam
- Training Method: Adversarial training between Generator and Discriminator
- Learning is performed using samples only, without any parametric PDF assumption

## PDF Estimation
- After training, a large number of samples are generated using the Generator
- Generated samples are de-normalized to the original scale
- Kernel Density Estimation (KDE) is applied to estimate the PDF
- The resulting KDE plot represents the learned probability density function

## Observations
- Mode Coverage: Major modes introduced by the nonlinear transformation are captured
- Training Stability: Training stabilizes after initial epochs without divergence
- Quality of Generated Distribution: Generated samples closely match the real transformed data,
  with minor smoothing in the tail regions

## How to Run
1. Download the dataset from Kaggle
2. Place the CSV file in the project directory
3. Set the roll number r in the code
4. Run the script:
   python gan_pdf_learning.py

## Requirements
- Python 3.8+
- PyTorch
- NumPy
- Pandas
- Matplotlib
- SciPy
- scikit-learn

## Notes
- Data normalization is essential for stable GAN training
- Results may vary due to random initialization
- Increasing training epochs improves distribution quality

## Conclusion
This project demonstrates that GANs can effectively learn an implicit probability density function
of a nonlinear transformed variable using data samples only, without any parametric assumptions.

