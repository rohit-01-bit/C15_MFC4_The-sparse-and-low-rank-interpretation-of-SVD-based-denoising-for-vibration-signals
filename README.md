#**Team Members**

1.Arepalle Charan Kumar Reddy

2Manda Rohit vardhan 

3.Pagala Sai Vandith Reddy 

4.Sirigiri Saradhi 



#**Project Outline** 

This project focuses on the implementation and analysis of SVD-based denoising techniques for
bearing vibration signals. Raw vibration signals acquired from rotating machinery bearings are
inherently noisy and non-stationary, which makes direct fault feature extraction unreliable. To
address this, the project reformulates the denoising task within a structured low-rank and sparse
optimization framework by transforming one-dimensional vibration signals into Hankel-structured
matrices that explicitly capture the periodic characteristics of fault-related impulses.
Singular Value Decomposition is employed to decompose the structured matrices into rank-one
components, enabling controlled manipulation of singular values for noise suppression and fault
enhancement. Three SVD-based denoising methods are implemented and analysed: Truncated
Singular Value Decomposition (TSVD), derived from ℓ₀-norm regularization and hard thresholding;
Reweighted Singular Value Decomposition (RSVD), which incorporates fault-related prior information
through periodic modulation intensity; and Weighted Soft Singular Value Decomposition (WSSVD),
which formulates denoising as a weighted ℓ₁-regularized optimization problem leading to adaptive
soft-thresholding of singular values.
Following singular value modification, the denoised matrices are reconstructed back into timedomain signals using overlap-add averaging. The effectiveness of the denoising process is evaluated
through time-domain analysis, envelope analysis, and square envelope spectrum analysis, enabling
the identification and enhancement of bearing fault characteristic frequencies such as BPFO and its
harmonics.

#updates

1.Acquired IMS Dataset that consists of high-frequency vibration signals measured from
rolling element bearings operating under constant rotational speed and load.

2.Implemented Hankel-type matrix construction from one-dimensional vibration signals using
maximum overlap.

3.Performed Singular Value Decomposition (SVD) on the constructed matrix and verified
singular value distribution, energy concentration, and orthogonality properties numerically.

4.Implemented and validated three denoising methods:

o  TSVD (Truncated SVD) using hard thresholding of singular values.

o  RSVD (Reweighted SVD) using Periodic Modulation Intensity (PMI) to reweight
singular values.

o WSSVD (Weighted Soft SVD) using weighted soft-thresholding derived from
weighted ℓ₁-norm minimization.

5.Verified theoretical consistency by explicitly showing that:

o TSVD corresponds to ℓ₀-norm sparse approximation,

o RSVD corresponds to heuristic reweighting without amplitude fidelity,

o WSSVD follows weighted ℓ₁-norm optimization and preserves amplitude information.

6.Implemented overlap-add reconstruction to convert denoised matrices back into timedomain signals.

7.Conducted quantitative evaluation using relative reconstruction error, demonstrating that
WSSVD achieves significantly lower reconstruction error compared to TSVD and RSVD.

8.Performed envelope analysis and square envelope spectrum analysis on original and
denoised signals, clearly showing enhanced fault characteristic frequencies (BPFO and
harmonics) after WSSVD.

9.Added matrix-level evaluation, comparing Frobenius norms before and after denoising to
quantitatively demonstrate noise suppression while preserving structural information.


#Challenges

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


#Future Work
1. Extension to Real-World Audio-Format Vibration Signals
Extend the current framework to process vibration signals stored in real-world formats such
as .wav or .mp3, enabling perceptual inspection alongside mathematical analysis and
improving practical demonstrability of denoising effectiveness.
2. Integration with Fault Diagnosis Pipeline
Utilize the denoised signals obtained through WSSVD as input to a fault diagnosis stage
involving feature extraction (time-domain, frequency-domain, and envelope-based features)
and supervised classification for automated bearing fault identification.


