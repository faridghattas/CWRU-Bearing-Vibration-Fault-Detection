# CWRU Bearing Vibration Fault Detection: Digital Signal Processing & Rule-Based AI

## 📌 Project Overview
This project delivers an industrial-grade **Vibration Analysis and Fault Detection Pipeline** utilizing the world-standard **Case Western Reserve University (CWRU) Bearing Dataset**. 

Rather than relying purely on data-driven black-box machine learning, this framework implements core **Digital Signal Processing (DSP)** methodologies—specifically **Fast Fourier Transform (FFT)** and **Envelope Analysis (Hilbert Transform Demodulation)**—coupled with a physical rule-based classifier. The system isolates and diagnoses structural mechanical failures (Inner Race, Outer Race, and Ball Faults) at varying severity levels ($0.007"$, $0.014"$, and $0.021"$).

---

## 📊 Methodology & DSP Pipeline

### 1. Time-Domain Exploration
Raw acceleration signals sampled at **12 kHz** were extracted from `.mat` files. In the time domain, faulty bearings display distinct periodic impulses (shocks) caused by rolling elements striking localized defects, contrasted against the stationary, low-amplitude profile of a healthy engine.

### 2. Fast Fourier Transform (FFT)
The signal was mapped from the Time Domain to the Frequency Domain using FFT. The operating frequency ($1\times \text{RPM}$) and its higher harmonics ($2\times, 3\times \text{RPM}$) were calculated to screen for synchronous macro-faults like unbalance or misalignment.

### 3. Envelope Analysis (High-Frequency Demodulation)
Early-stage bearing defects generate low-energy micro-impacts that are easily masked by high-frequency structural noise in a standard FFT. To extract these latent structural signatures:
* The raw signal was bandpass-filtered around the structural resonance zone.
* An **Envelope Amplitude Demodulation** was executed via the **Hilbert Transform**.
* This isolates the impact repetition frequencies, matching them explicitly to theoretical bearing defect frequencies (**BPFI, BPFO, BSF**).

---

## 📈 Engineering Evolution & Results

Below is the comparative statistical breakdown of the detection matrix across the dataset spectrum:

| Dataset File | Defect Type | Defect Severity | FFT Baseline Peak | Envelope Demod. Peak | Diagnostic Output | Status |
| :--- | :--- | :---: | :---: | :---: | :--- | :---: |
| `Time_Normal_1_098` | Healthy Baseline | `0.000"` | 29.5 Hz ($1\times\text{RPM}$) | None | **Normal Operation** | ✅ Pass |
| `IR007_1_110` | Inner Race | `0.007"` | Masked / Noise | 162.2 Hz ($\approx\text{BPFI}$) | **Inner Race Fault** | ✅ Detected |
| `OR021_6_1_239` | Outer Race | `0.021"` | 105.8 Hz ($\approx\text{BPFO}$) | 105.8 Hz ($\approx\text{BPFO}$) | **Critical Outer Race Fault**| ✅ Critical |

---

---

## 🔬 Visualizations & Diagnostic Reports

### 🔹 1. Time-Domain Signal Characterization
We plot the first 2,000 continuous data points to contrast stable baseline behavior against localized impact mechanics.
![Time Domain Signals](assets/normal_and_inner_signal.png)
*Figure 1: High-energy periodic impact spikes in the 0.007" Inner Race fault signal compared to the low-amplitude stationary noise of the healthy baseline.*

### 🔹 2. Frequency-Domain Transformation (Standard FFT)
Transforming the signals via Fast Fourier Transform reveals the raw macro-spectral energy distribution up to 3,000 Hz.
![Standard FFT Spectrum](assets/Vibration_Spectrum_\(FFT\)_Normal_Inner_Freq.png)
*Figure 2: Frequency spectra showcasing how early-stage bearing micro-faults are easily masked by high-frequency background structural resonances in a baseline FFT.*

### 🔹 3. Advanced Amplitude Demodulation (Envelope Spectrum)
Applying the Hilbert Transform unmasks the hidden physical repetition rates by extracting the pure defect modulation envelope.
![Envelope Spectrum Analysis](assets/Envelope_Spectrum_-_Inner_Race_Fault.png)
*Figure 3: Demodulated envelope spectrum isolating clear, sharp peaks matching the theoretical kinematic Inner Race Defect Frequency (BPFI) at 162.2 Hz and its 2nd Harmonic.*

### 🔹 4. Final System Classifier Performance
The architectural scaling from a 2,048 window to an 8,192 ultra-high resolution window eliminated spectral leakage, yielding pristine class separation.
![Final Confusion Matrix](assets/Confusion_Matrix_-_Intelligent_Fault_Detection_System.png)
*Figure 4: Professional multi-class Confusion Matrix demonstrating the high-fidelity deterministic classification achieved by embedding exact physics-informed spectral features.*

---

---

## 🧠 Core Engineering Competencies Demonstrated
1. **Advanced DSP Architectures:** Proficient with `scipy.signal` structures, Nyquist frequency boundaries, windowing, and analytical signal generation via Hilbert transforms.
2. **Deterministic Modeling:** Built an automated rule-based diagnostic matrix that maps empirical frequency spectra directly onto physical kinematic defect equations ($1\times\text{RPM}$, $\text{BPFO}$, $\text{BPFI}$).
3. **Domain Expertise (Mechanical Fault Diagnosis):** Demonstrates deep understanding of mechanical vibration physics, eliminating the need for vast training data by exploiting exact physical constraints.

---

## 🚀 Quick Start & Installation

```bash
# Clone the repository
git clone [https://github.com/faridghattas/CWRU-Bearing-Vibration-Fault-Detection.git](https://github.com/faridghattas/CWRU-Bearing-Vibration-Fault-Detection.git)

# Install dependencies
pip install -r requirements.txt
