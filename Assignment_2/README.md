# Learning Probability Density Function using GAN

## Overview
This project learns an unknown probability density function (PDF) using data only.
A Generative Adversarial Network (GAN) is trained on a nonlinear transformation of NO₂
concentration values without assuming any parametric form of the distribution.

---

## Dataset
- Name: India Air Quality Data
- Source: Kaggle
- Feature Used: NO₂ concentration (NO2)
- Missing values are removed before processing

---

## Transformation Parameters (a_r, b_r)
The NO₂ concentration values x are transformed using:
z = x + a_r * sin(b_r * x)

where:
- a_r = 0.5 * (r mod 7)
- b_r = 0.3 * ((r mod 5) + 1)
- r is the university roll number

This nonlinear transformation introduces oscillations and makes the probability
distribution of z analytically unknown.

---

## GAN Architecture Description
A one-dimensional Generative Adversarial Network (GAN) is used to learn the
distribution of the transformed variable z.

### Generator
- Input: Gaussian noise sampled from N(0,1)
- Architecture:
  - Linear (1 → 32) + ReLU
  - Linear (32 → 32) + ReLU
  - Linear (32 → 1)
- Output: Generated sample z_f

### Discriminator
- Input: Real sample z or generated sample z_f
- Architecture:
  - Linear (1 → 32) + LeakyReLU
  - Linear (32 → 32) + LeakyReLU
  - Linear (32 → 1) + Sigmoid
- Output: Probability that the sample is real

---

## PDF Plot Obtained from GAN Samples
- After training, a large number of samples are generated using the Generator
- Generated samples are de-normalized to the original scale
- Kernel Density Estimation (KDE) is applied to the generated samples
- The KDE curve represents the estimated probability density function learned by the GAN
- This plot is compared with the histogram of real transformed samples

---

## Observations

### Mode Coverage
- The GAN captures the major modes introduced by the nonlinear transformation
- No significant mode collapse is observed
- Minor smoothing of sharp peaks is present

### Training Stability
- Initial training shows imbalance between Generator and Discriminator
- Training stabilizes after sufficient epochs
- No divergence or unstable oscillatory behavior is observed

### Quality of Generated Distribution
- Generated samples closely resemble real transformed data
- Overall shape and central regions of the distribution are well preserved
- Slight underestimation in tail regions is observed

---

## Requirements
- Python 3.8+
- PyTorch
- NumPy
- Pandas
- Matplotlib
- SciPy
- scikit-learn

---

## Conclusion
The GAN successfully learns an implicit probability density function of a nonlinear
transformed variable using data samples only, without any parametric assumptions.


