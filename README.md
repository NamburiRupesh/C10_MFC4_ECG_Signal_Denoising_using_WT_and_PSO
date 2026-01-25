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

## **Project Outline**
The objective of this project is to remove noise from ECG signals using a hybrid approach that combines Wavelet Transform for signal decomposition and Particle Swarm Optimisation (PSO) for optimal parameter selection, thereby improving signal quality and diagnostic reliability.

The project workflow consists of the following steps:

1. **ECG Signal Acquisition**  
   - Load ECG signals from a dataset or recorded source.

2. **Preprocessing**
   - Normalize ECG signals and remove baseline wander and artifacts if present.

3. **Wavelet Transform (Completed)**  
   - Apply Discrete Wavelet Transform (DWT) to decompose the ECG signal into multiple frequency sub-bands.
   - Separate noise-dominant components from useful ECG information.
   - Reconstruct the signal using selected wavelet coefficients.

4. **Feature and Parameter Extraction**
   - Extract relevant parameters from wavelet coefficients for optimization.

5. **Particle Swarm Optimisation (PSO) (Planned)**  
   - Optimize wavelet parameters and threshold values using PSO.
   - Improve denoising performance by minimizing noise while preserving ECG morphology.

6. **Denoised Signal Reconstruction**
   - Reconstruct the ECG signal using optimized parameters.

7. **Performance Evaluation**
   - Evaluate denoising effectiveness using metrics such as Signal-to-Noise Ratio (SNR), Mean Square Error (MSE), and visual comparison.

---

## **Updates**


---

## **Challenges / Issues Faced**
- Understanding ECG signal characteristics and different noise sources.
- Selecting suitable wavelet functions and decomposition levels.
- Implementing wavelet-based denoising effectively.
- Integrating PSO with wavelet-based denoising methods.

---

## **Future Plans**
- Complete implementation of **Particle Swarm Optimisation (PSO)**.
- Optimize wavelet thresholds and parameters using PSO.
- Compare results with traditional denoising methods.
- Improve quantitative and visual analysis of denoised ECG signals.
- Document results and findings in detail.

