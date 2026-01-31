# Project title
The Sparse and Low Rank Interpretation of SVD based Denoising for Vibration Signals

----
# Team Members

CB.SC.U4AIE24207 - Arepalle Charan Kumar Reddy (cb.sc.u4aie24207@cb.students.amrita.edu)

CB.SC.U4AIE24231 - Manda Rohit vardhan (cb.sc.u4aie24231@cb.students.amrita.edu)

CB.SC.U4AIE24239 - Pagala Sai Vandith Reddy (cb.sc.u4aie24239@cb.students.amrita.edu)

CB.SC.U4AIE24265 - Sirigiri Saradhi (cb.sc.u4aie24265@cb.students.amrita.edu)

---
#  Project Outline

## 1. Project Overview

This project implements and analyzes SVD-based denoising techniques for vibration signals acquired from rotating machinery bearings

The work focuses on transforming raw vibration signals into structured matrix representations and applying optimization-driven singular value manipulation to enhance fault-related components while suppressing noise.

The implementation is carried out entirely in MATLAB.

## 2. Problem Context

Raw vibration signals collected from industrial rotating machinery are:

- highly noisy,
- non-stationary,
- and often mask weak fault-related impulses.

Traditional time-domain and frequency-domain analysis techniques fail to reliably reveal fault signatures under these conditions.
SVD-based denoising provides a promising framework, but existing approaches often suffer from:

- amplitude distortion,
- heuristic parameter selection,
- and inconsistent denoising performance.

This project addresses these limitations through structured low-rank modeling and sparsity-aware optimization.

## 3. Motivation

Vibration signals from rotating machinery bearings are highly noisy and non-stationary, especially during early fault stages, making fault-related features difficult to detect using conventional time- or frequency-domain analysis. Singular Value Decomposition (SVD) is widely used for vibration signal denoising, yet most existing approaches rely on heuristic singular value manipulation without clear theoretical justification. As a result, traditional SVD methods often suffer from amplitude distortion, information loss, and inconsistent denoising performance.

This project is motivated by the need to understand why SVD-based denoising works and how it can be made more reliable and physically meaningful. By interpreting SVD denoising within a sparse and low-rank optimization framework, the project reveals the mathematical foundations of commonly used methods such as TSVD and RSVD and demonstrates how weighted ℓ₁-norm regularization leads to adaptive and stable denoising. Applying this theory to real bearing vibration data shows that fault-related impulsive features and characteristic frequencies can be enhanced more clearly while preserving signal amplitude, making the approach both theoretically insightful and practically valuable for machinery condition monitoring.

## 4. Objectives

- To model vibration signal denoising as a sparse and low-rank optimization problem using a matrix representation of time-series data.
- To analyze and compare classical TSVD, heuristic reweighted SVD (RSVD), and weighted soft-threshold SVD (WSSVD)
- To implement fault classification using machine learning models trained on features extracted from WSSVD-denoised signals.
- To denoise acoustic signals (.wav/mp3), validating its robustness beyond vibration-only data.

## 5. Methodology

### Data Acquisition

IMS bearing vibration dataset (raw acceleration signals sampled at 20 kHz).

### Signal Preprocessing

- Mean removal
- Amplitude normalization
- Fixed-length segment selection (1 second).

### Matrix Construction

Conversion of the 1D vibration signal into a Hankel-like structured matrix using maximum overlap.

This step enables low-rank modeling of periodic fault impulses.

### Singular Value Decomposition

SVD is performed on the Hankel matrix

  𝑌 = 𝑈𝛴𝑉'

Singular value energy distribution is analyzed.

### Denoising Methods Implemented

- TSVD (Truncated SVD) - Hard thresholding derived from ℓ₀-norm regularization.

- RSVD (Reweighted SVD) - Singular values reweighted using Periodic Modulation Intensity (PMI) computed from singular vectors.

- WSSVD (Weighted Soft SVD) (Proposed method) - Weighted ℓ₁-norm optimization leading to adaptive soft-thresholding.

Signal Reconstruction

- Overlap-add reconstruction from denoised matrices back to the time domain.

### Fault Feature Enhancement

- Envelope analysis
- Square envelope spectrum
- Fault frequency identification (BPFO, BPFI) using bearing geometry.

---

# Results and Discussion
The proposed SVD-based denoising framework was evaluated using raw vibration signals from the IMS bearing dataset. A one-second vibration segment sampled at 20 kHz was used to construct a Hankel-structured matrix with maximum overlap, resulting in a matrix of size 40×19961. Visualization of the constructed matrix confirmed the expected Hankel structure, validating correct signal-to-matrix transformation. Singular Value Decomposition revealed a rapidly decaying singular value distribution, with the first ten singular values capturing approximately 67% of the total energy, indicating a strong low-rank characteristic of the vibration signal.

Three denoising methods—TSVD, RSVD, and WSSVD—were implemented and compared. TSVD retained only the first ten singular values through hard truncation, which reduced noise but introduced significant information loss. RSVD applied heuristic reweighting based on Periodic Modulation Intensity (PMI), selectively emphasizing components with strong periodic content. However, this approach altered singular value magnitudes directly, leading to amplitude distortion. In contrast, WSSVD applied weighted soft-thresholding derived from weighted ℓ₁-norm minimization, adaptively shrinking singular values while preserving their relative amplitude structure.

Quantitative evaluation using relative reconstruction error clearly demonstrates the superiority of WSSVD. TSVD resulted in a high reconstruction error of 0.5220, indicating excessive loss of signal content. RSVD improved reconstruction accuracy with an error of 0.4654, but still suffered from amplitude degradation. WSSVD achieved a substantially lower reconstruction error of 0.0094, confirming its ability to suppress noise while maintaining signal fidelity. Matrix-level analysis further supports this observation: the Frobenius norm of the denoised matrix decreased by only 0.52%, indicating effective noise reduction without structural distortion.

Time-domain comparisons show that TSVD and RSVD fail to clearly isolate fault-related impulsive components, whereas WSSVD produces a cleaner impulsive waveform consistent with bearing fault characteristics. Envelope spectrum analysis reveals that fault characteristic frequencies such as BPFO (~102.77 Hz) and BPFI (~163.90 Hz) are weak or partially submerged in the original and TSVD-processed signals. RSVD enhances these components but with significantly reduced amplitude. In contrast, WSSVD distinctly enhances BPFO and its harmonics with stable and physically meaningful amplitudes, closely matching the behavior reported in the base paper.

Further processing using resonance band extraction (500–5000 Hz) followed by square envelope spectrum analysis confirms that WSSVD effectively suppresses random impulse interference while enhancing periodic fault features. The square envelope spectrum of the WSSVD-processed signal shows clear peaks at BPFO, 2×BPFO, and 3×BPFO, consistent with early-stage bearing fault behavior described in the experimental study of the base paper.

Overall, the results validate the sparse and low-rank interpretation of SVD-based denoising. TSVD is confirmed as equivalent to ℓ₀-norm minimization with hard thresholding, RSVD as a heuristic weighted approach lacking amplitude fidelity, and WSSVD as a theoretically grounded weighted ℓ₁-norm solution that achieves superior denoising performance with amplitude preservation.

---

# updates

1.Acquired IMS Dataset that consists of high-frequency vibration signals measured from
rolling element bearings operating under constant rotational speed and load.

2.Implemented Hankel-type matrix construction from one-dimensional vibration signals using
maximum overlap.

3.Performed Singular Value Decomposition (SVD) on the constructed matrix and verified
singular value distribution, energy concentration, and orthogonality properties numerically.

4.Implemented and validated three denoising methods:
- TSVD (Truncated SVD) using hard thresholding of singular values.
- RSVD (Reweighted SVD) using Periodic Modulation Intensity (PMI) to reweight singular values.
- WSSVD (Weighted Soft SVD) using weighted soft-thresholding derived from weighted ℓ₁-norm minimization.

5.Verified theoretical consistency by explicitly showing that:

- TSVD corresponds to ℓ₀-norm sparse approximation,
- RSVD corresponds to heuristic reweighting without amplitude fidelity,
- WSSVD follows weighted ℓ₁-norm optimization and preserves amplitude information.

6.Implemented overlap-add reconstruction to convert denoised matrices back into timedomain signals.

7.Conducted quantitative evaluation using relative reconstruction error, demonstrating that
WSSVD achieves significantly lower reconstruction error compared to TSVD and RSVD.

8.Performed envelope analysis and square envelope spectrum analysis on original and
denoised signals, clearly showing enhanced fault characteristic frequencies (BPFO and
harmonics) after WSSVD.

9.Added matrix-level evaluation, comparing Frobenius norms before and after denoising to
quantitatively demonstrate noise suppression while preserving structural information.

---

# Challenges

1. Singular Value Interpretation
Differentiating between noise-dominant and fault-dominant singular components was non-trivial, as
high singular values do not always correspond to fault-related information in non-stationary vibration
signals.
2. Implementation of Optimization-Based Thresholding
Translating theoretical ℓ₀ and weighted ℓ₁ regularization formulations into stable MATLAB
implementations required precise handling of hard and soft thresholding conditions to avoid
numerical inconsistencies.
3. PMI Computation and Stability
Accurate computation of Periodic Modulation Intensity (PMI) from reconstructed singular
components was sensitive to envelope spectrum resolution and frequency bin alignment with fault
characteristic frequencies.
4. Amplitude Preservation vs Noise Suppression Trade-off
Ensuring effective noise suppression without distorting the physical amplitude structure of the
vibration signal required careful validation across TSVD, RSVD, and WSSVD outputs.
5. Signal Reconstruction Accuracy
Overlap-add reconstruction from denoised Hankel matrices had to be carefully implemented to
prevent boundary artifacts and ensure faithful time-domain signal recovery.


# Future Work

1. Extension to Real-World Audio-Format Vibration Signals
Extend the current framework to process vibration signals stored in real-world formats such
as .wav or .mp3, enabling perceptual inspection alongside mathematical analysis and
improving practical demonstrability of denoising effectiveness.
2. Integration with Fault Diagnosis Pipeline
Utilize the denoised signals obtained through WSSVD as input to a fault diagnosis stage
involving feature extraction (time-domain, frequency-domain, and envelope-based features)
and supervised classification for automated bearing fault identification.

# References

1. The sparse and low-rank interpretation of SVD-based denoising for vibration signals
  https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9129272


