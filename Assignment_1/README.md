# **Title: Learn Probability Density Functions using Roll-Number-Parameterized Non-Linear Model**
## **1. Methodology**
### **Step 1: Feature Transformation**
Title: Learn Probability Density Functions using Roll-Number-Parameterized Non-Linear Model
Dataset: Consider NO2 as feature (x).
Link: https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data
Tasks to be performed
➔ Step-1: Transform each value of x into z using the transformation function given below.
z = Tr(x) = x + arsin(brx) (1)

where ar = 0.05 ∗ (r mod 7), br = 0.3 ∗ (r mod 5 + 1)
where, mod returns remainder and r is your UNIVERSITY ROLL NUMBER.
➔ Step-2: Learn parameters of the following probability density function using any
estimation technique or by using any machine learning technique.

p̂(z) = c ∗ e
−λ(z−μ)
2
(2)
Where, p̂(z) is the predicted probability of the transformed variable z. In this step, you
have to learn parameters λ, μ and c in Eq.(2).
➔ Step-3: Submit the values of the parameters (λ, μ and c) through the following link.
Submission Link: https://forms.gle/jYF3MDKozRnSCHvR8
