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

- Additional references include standard literature on Discrete Wavelet Transform (DWT) and Particle Swarm Optimisation (PSO) for signal denoising and feature optimisation.

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
