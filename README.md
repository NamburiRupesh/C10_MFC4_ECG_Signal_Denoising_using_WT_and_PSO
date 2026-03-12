# **MFC4 Project – README**

## **Project Topic**
**An Efficient ECG Signal Denoising Technique Based on the Combination of Particle Swarm Optimisation and Wavelet Transform**

---

## **Team Members**
- **Rupesh Namburi** – CB.SC.U4AIE24234  
- **Karlapati Sreeshanth** – CB.SC.U4AIE24225  
- **Gandrothu Karthik** – CB.SC.U4AIE24217  
- **Yaramati Uday Sri** – CB.SC.U4AIE24260  

---

## **Base / Reference Paper(s)**
- **An Efficient ECG Signals Denoising Technique Based on the Combination of Particle Swarm Optimisation and Wavelet Transform**  
  *Heliyon, 2024*  
  Paper Link: https://www.cell.com/heliyon/fulltext/S2405-8440(24)02202-3
---

## Introduction

Electrocardiogram (ECG) signals represent the electrical activity of the human heart and play a crucial role in diagnosing cardiovascular diseases. A typical ECG waveform consists of the **P wave, QRS complex, and T wave**, which correspond to different stages of the cardiac cycle. Accurate analysis of these components helps clinicians detect abnormalities such as arrhythmias, myocardial infarction, and other cardiac disorders.

However, ECG signals recorded in practical environments are often contaminated by various types of noise and artifacts. These disturbances distort important signal characteristics and reduce the reliability of automated diagnostic systems. Therefore, effective ECG signal denoising is a critical preprocessing step in biomedical signal processing.

ECG signals are considered **NON-STATIONARY**, meaning that their statistical properties, such as frequency content and amplitude, vary over time. Because of this time-varying behavior, traditional signal processing techniques based on fixed frequency assumptions are often insufficient for effective noise removal.

To address this problem, time–frequency analysis techniques such as the Discrete Wavelet Transform (DWT) are widely used. DWT analyzes signals at multiple scales, enabling effective separation of noise from useful ECG components. However, the performance of wavelet-based denoising depends on selecting appropriate parameters such as the wavelet basis, decomposition level, and thresholding method.

In this project, we implement an ECG denoising framework that combines Wavelet Transform with Particle Swarm Optimisation (PSO). DWT decomposes the ECG signal into different frequency components, while PSO automatically optimizes the denoising parameters. This hybrid approach improves the signal-to-noise ratio (SNR) while preserving important ECG features.

### Key Concepts

- **ECG Signal Analysis** – Study of electrical activity of the heart through P wave, QRS complex, and T wave.
- **Noise Removal** – Eliminating artifacts such as power line interference and Gaussian noise.
- **Wavelet Transform (DWT)** – Decomposes signals into multiple frequency components for effective noise separation.
- **Particle Swarm Optimisation (PSO)** – Optimizes wavelet parameters to improve denoising performance.
- **Signal Reconstruction** – Rebuilds the ECG signal while preserving important morphological features.

---

## ECG Noise Reduction using Wavelet Transform (WT)

### Overview

Wavelet Transform (WT) is an effective signal processing technique used for analyzing **non-stationary signals** such as ECG signals. Unlike traditional Fourier-based methods, WT provides both **time-domain and frequency-domain analysis**, allowing efficient separation of noise from useful signal components.

Wavelet Transform can be categorized into two main types:

- **Continuous Wavelet Transform (CWT)**
- **Discrete Wavelet Transform (DWT)**

In this project, **Discrete Wavelet Transform (DWT)** is used for ECG signal denoising because of its computational efficiency and ability to perform **multi-resolution analysis**.

---

### Mathematical Representation of DWT

The Discrete Wavelet Transform is defined as:

$$
C(a,b) = \sum_{n \in Z} x(n)\, g_{j,k}(n)
$$

Where:

- $C(a,b)$ = Wavelet coefficient  
- $x(n)$ = Input ECG signal  
- $g_{j,k}(n)$ = Scaled and shifted wavelet function  
- $a = 2^{-j}$ = Scale parameter  
- $b = k2^{-j}$ = Translation parameter  
- $j, k \in Z$

The scaled wavelet function is defined as:

$$
g_{j,k}(n) = 2^{j/2} g(2^j n - k)
$$

This equation represents the **scaled and translated version of the mother wavelet**, which is used to analyze different signal frequencies.

---

### Wavelet-Based ECG Denoising Procedure

The wavelet denoising process consists of three main stages:

1. **Signal Decomposition**
2. **Thresholding**
3. **Signal Reconstruction**

![Wavelet ECG Denoising Process](images/wavelet_denoising.png)

**Figure 1:** Wavelet-based ECG denoising process showing the decomposition, thresholding, and reconstruction stages.

As shown in **Figure 1**, the ECG signal is first decomposed into multiple levels using the Discrete Wavelet Transform (DWT). Each decomposition level separates the signal into approximation coefficients (cA) and detail coefficients (cD). The detail coefficients primarily contain high-frequency components where noise is dominant.

In the **thresholding phase**, threshold values are applied to the wavelet coefficients to suppress noise while preserving important signal characteristics.

Finally, in the **reconstruction phase**, the denoised signal is reconstructed using the inverse Discrete Wavelet Transform (iDWT) by combining the processed approximation and detail coefficients.

---
### 1. ECG Signal Decomposition

In the first stage of the wavelet denoising process, the ECG signal is decomposed into multiple levels using the **Discrete Wavelet Transform (DWT)**. At each decomposition level, the signal is separated into two components:

- **Approximation coefficients (cA)** – representing the low-frequency components of the ECG signal.
- **Detail coefficients (cD)** – representing the high-frequency components where most of the noise is present.

The decomposition process is performed using **low-pass and high-pass filters** followed by **downsampling**, producing a multi-resolution representation of the signal.

The approximation and detail coefficients at level *i* are defined as:

$$
cA_i(t) = \sum_{k=-\infty}^{\infty} cA_{i-1}(k)\,\phi_i(t-k)
$$

$$
cD_i(t) = \sum_{k=-\infty}^{\infty} cD_{i-1}(k)\,\psi_i(t-k)
$$

Where:

- $cA_i(t)$ represents the **approximation coefficients** at level $i$
- $cD_i(t)$ represents the **detail coefficients** at level $i$
- $\phi$ represents the **scaling function**
- $\psi$ represents the **wavelet function**

During decomposition, **only the approximation coefficients (cA)** are further decomposed into the next level, while the **detail coefficients (cD)** are directly forwarded to the **thresholding stage** for noise suppression.

This hierarchical decomposition enables efficient separation of high-frequency noise from the useful ECG signal.


---

### 2. Thresholding

Thresholding is the second stage of the wavelet denoising process. After the ECG signal is decomposed using the Discrete Wavelet Transform (DWT), thresholding is applied to the **detail coefficients**, where noise components are dominant. The goal of thresholding is to suppress noise while preserving the important features of the ECG signal.

The threshold value is estimated based on the noise level of the wavelet coefficients. In this work, the **Minimax thresholding technique** is used to determine the optimal threshold value that minimizes the maximum mean square error (MSE) between the original and denoised signals.

The threshold value $\delta$ is calculated as:

$$
\delta =
\begin{cases}
\sigma (0.3936 + 0.1829 \log_2(N)), & N > 32 \\
0, & N \le 32
\end{cases}
$$

Where:

- $\delta$ = Threshold value  
- $\sigma$ = Estimated noise standard deviation  
- $N$ = Length of the signal  

The noise standard deviation is estimated using the **Median Absolute Deviation (MAD)** method:

$$
\sigma = \frac{\text{median}(|D_{ij}|)}{0.6745}
$$

Where:

- $D_{ij}$ represents the **detail coefficients at unit scale**



The general thresholding operation applied to the noisy wavelet coefficients is expressed as:

$$
Z = THR(\hat{X}, \delta)
$$

Where:

- $THR$ represents the **thresholding function**
- $\hat{X}$ represents the **wavelet coefficient**
- $\delta$ represents the **threshold value**

---

### Hard Thresholding

Hard thresholding removes coefficients whose absolute value is smaller than the threshold.

$$
\hat{x}_{di}(l) =
\begin{cases}
\hat{x}_{di}(l), & |\hat{x}_{di}(l)| \ge \delta_l \\
0, & |\hat{x}_{di}(l)| < \delta_l
\end{cases}
$$

![Hard Thresholding](images/hard_threshold.png)

**Figure 2:** Hard thresholding function.

---

### Soft Thresholding

Soft thresholding shrinks the coefficients toward zero after thresholding, producing smoother results.

$$
\hat{x}_{di}(l) =
\begin{cases}
\hat{x}_{di}(l) - |\delta_l|, & |\hat{x}_{di}(l)| \ge \delta_l \\
0, & |\hat{x}_{di}(l)| < \delta_l
\end{cases}
$$

![Soft Thresholding](images/soft_threshold.png)

**Figure 3:** Soft thresholding function.

---

Soft thresholding generally provides smoother signal reconstruction compared to hard thresholding, making it more suitable for ECG signal denoising.
