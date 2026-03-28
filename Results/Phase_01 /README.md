# 📊 Phase 01 — Audio Signal Processing Visualizations

All visualizations below are generated from the Hindi Female TTS corpus.  
Sample audio used: `train_hindifem_00035.wav`  
*(sentence: "कार्य के समय हमारी भुजाएं कमजोर नहीं होतीं")*

---

## 1️⃣ Raw Audio Waveform (Sample Index)

<img width="1012" height="624" alt="Raw Audio Waveform" src="https://github.com/user-attachments/assets/1d7ca24b-dde8-4e22-97ec-e2760a40fbc9" />


### What This Shows
The time-domain representation of the raw audio signal plotted 
against **sample index** (number of audio samples).

### Key Observations
- **X-axis:** Sample Index (0 to ~85,000 samples)
- **Y-axis:** Amplitude (ranges from -0.8 to +0.8)
- **Total samples:** ~88,000 at 48kHz sampling rate
- The signal starts and ends with **silence** (flat line near 0)
- Multiple **speech bursts** visible — correspond to individual words
- Peak amplitude reaches **±0.8** indicating good recording quality
- **Symmetric waveform** confirms clean studio recording

### Why It Matters
This is the raw digital representation of the speaker's voice.  
Each spike corresponds to a spoken syllable or word in the Hindi sentence.

---

## 2️⃣ Raw Audio Waveform (Time Domain)

<img width="1012" height="624" alt="Raw Audio Waveform (2)" src="https://github.com/user-attachments/assets/996b56ee-5b02-4040-903a-8d9d42ff4c31" />


### What This Shows
Same audio signal but now plotted against **actual time in seconds** — 
more meaningful for speech analysis.

### Key Observations
- **X-axis:** Time (0 to 4 seconds)
- **Y-axis:** Amplitude (-0.8 to +0.8)
- **Total duration:** ~4 seconds for this utterance
- Clear **inter-word pauses** visible as gaps between bursts
- Speech energy is **concentrated between 0.4s and 3.7s**
- The **leading and trailing silence** (0–0.4s, 3.7–4s) is standard 
  studio padding

### Difference From Plot 1
Plot 1 uses raw sample numbers. This plot uses real time (seconds),  
making it easier to understand speech timing and rhythm.

---

## 3️⃣ Spectrogram (Hz)

<img width="822" height="393" alt="Spectrogram(Hz)" src="https://github.com/user-attachments/assets/d3b67f56-6c7b-4af4-b8de-7013d9fcf299" />


### What This Shows
A **Short-Time Fourier Transform (STFT)** based spectrogram showing 
how frequency content changes over time.

### Key Observations
- **X-axis:** Time (0 to 4 seconds)
- **Y-axis:** Frequency (0 to ~11,000 Hz)
- **Color:** Brightness = energy intensity (yellow = high, black = low)
- Most speech energy is **concentrated below 4000 Hz**
- **Vertical striping pattern** = individual phonemes being spoken
- Clear **harmonic structure** visible as horizontal bands (especially 
  below 2000 Hz) — characteristic of voiced Hindi speech
- **Silence regions** appear as completely dark vertical bands

### Why It Matters
Shows which frequencies are active at each moment in time.  
This is the foundation for all further acoustic analysis.

---

## 4️⃣ Mel Spectrogram

<img width="1817" height="833" alt="Mel Spectrogram" src="https://github.com/user-attachments/assets/20180609-465f-4daf-a1bc-fc60e3f5a576" />


### What This Shows
Spectrogram converted to the **Mel scale** — a perceptual frequency 
scale that mimics how the human ear perceives sound.

### Key Observations
- **X-axis:** Time (0 to 4 seconds)
- **Y-axis:** Frequency in Mel scale (0 to ~8192 Hz shown, 
  but compressed at higher frequencies)
- **Color scale:** 0 to +160 (yellow = high energy, black = silence)
- Energy is **heavily concentrated in low-to-mid frequencies** 
  (0–1500 Hz range) — shown by bright yellow/orange at bottom
- **Higher frequencies (above 2048 Hz)** appear dark = low energy
- The Mel scale compresses high frequencies and expands low 
  frequencies — matching human hearing perception

### Why It Matters for TTS
TTS systems use Mel spectrograms as their **target output**.  
Neural TTS models (Tacotron2, FastSpeech) learn to generate 
Mel spectrograms which are then converted to audio.

---

## 5️⃣ Log Mel Spectrogram

<img width="1831" height="833" alt="Log Mel Spectrogram" src="https://github.com/user-attachments/assets/529c304f-b12c-45b8-9cfa-78e658eacc66" />


### What This Shows
The Mel Spectrogram converted to **logarithmic (dB) scale** — 
this better represents how humans perceive loudness differences.

### Key Observations
- **X-axis:** Time (0 to 4 seconds)
- **Y-axis:** Frequency (Hz, Mel-scaled)
- **Color scale:** -50 dB (blue) to +20 dB (red)
- **Red regions** = high energy speech sounds (vowels, voiced consonants)
- **Blue regions** = silence or very low energy (pauses between words)
- Low frequencies (0–512 Hz) are **consistently red** = strong 
  fundamental frequency of the female voice
- Mid frequencies (512–4096 Hz) show **alternating red/blue** = 
  formant structure of individual phonemes
- High frequencies (above 4096 Hz) are **mostly blue** = 
  little energy in this female voice

### Comparison With Plot 4
Plot 4 (linear Mel) exaggerates strong signals.  
Plot 5 (log Mel) gives a more balanced, perceptually accurate view —  
which is why **log Mel is used in all modern TTS/ASR systems**.

---

## 6️⃣ MFCC Heatmap (13 Coefficients)

<img width="744" height="393" alt="Mfcc Extract 13 Coefficients Extracted" src="https://github.com/user-attachments/assets/f9de5244-a0f4-4ef4-99ec-e6844565e451" />


### What This Shows
**Mel-Frequency Cepstral Coefficients (MFCCs)** — the most widely 
used features in speech processing, shown as a heatmap over time.

### Key Observations
- **X-axis:** Time (0 to 4 seconds)
- **Y-axis:** 13 MFCC coefficients (MFCC_1 at bottom to MFCC_13 at top)
- **Color:** Red = high positive value, Blue = high negative value
- **MFCC_1 (bottom row)** appears **bright blue** = very large 
  negative values (~-500) representing overall signal energy
- **MFCC_2 to MFCC_13** appear **mostly reddish** = moderate 
  positive values (0 to +100) representing spectral shape
- The **varying pattern across time** captures changing phoneme 
  characteristics as each word is spoken
- **Vertical bands of blue** in MFCC_1 correspond to silence 
  between words

### What Each Coefficient Captures
| Coefficient | What It Represents |
|-------------|-------------------|
| MFCC_1 | Overall energy / loudness |
| MFCC_2–4 | Broad spectral shape (vowel identity) |
| MFCC_5–8 | Mid-level spectral detail |
| MFCC_9–13 | Fine spectral texture |

### Why It Matters
MFCCs are the **standard input features** for traditional ML-based 
speech recognition and duration prediction models.

---

## 7️⃣ Average Acoustic Profile (Spectral Envelope)

<img width="866" height="475" alt="Average Acoustic Profile (Spectral Envelope)" src="https://github.com/user-attachments/assets/dbc7a8b0-d116-4947-a816-d0f2c95e777e" />


### What This Shows
The **mean value of each MFCC coefficient** averaged across the 
entire audio file — giving a single acoustic "fingerprint" 
of the speaker's voice.

### Key Observations
- **X-axis:** MFCC Coefficient Index (MFCC_1 to MFCC_13)
- **Y-axis:** Mean Magnitude (averaged over all time frames)
- **MFCC_1 mean = -310** (large negative) = reflects the 
  log energy offset in cepstral analysis — completely normal
- **MFCC_2 mean = +110** (largest positive) = dominant 
  spectral tilt of female voice
- **MFCC_3 onwards** → values hover near zero with small 
  fluctuations → fine spectral details average out over time
- The **sharp drop from MFCC_2 to MFCC_3** is characteristic 
  of clean, studio-quality speech

### Why It Matters
This profile is unique to this speaker and recording style.  
It serves as a **baseline acoustic fingerprint** for the  
Hindi female voice corpus used throughout this project.

---

## 📋 Summary Table

| # | Visualization | Domain | Tool Used | Key Insight |
|---|--------------|--------|-----------|-------------|
| 1 | Raw Waveform (Samples) | Time | librosa | ~88K samples per utterance |
| 2 | Raw Waveform (Time) | Time | librosa | ~4 sec average duration |
| 3 | Spectrogram (Hz) | Time-Frequency | STFT | Energy below 4000 Hz |
| 4 | Mel Spectrogram | Perceptual | librosa | Low-freq dominance |
| 5 | Log Mel Spectrogram | Perceptual (dB) | librosa | Used in modern TTS |
| 6 | MFCC Heatmap | Cepstral | librosa | 13 coefficients extracted |
| 7 | Avg Acoustic Profile | Statistical | numpy | Speaker fingerprint |

---

## 🔧 How These Were Generated

All plots generated using Python with the following libraries:
- `librosa` — audio loading and feature extraction
- `matplotlib` — visualization
- `numpy` — numerical operations

See full code in:  
📓 [`notebooks/phase_01_eda_signal_processing/audio_signal_processing.ipynb`](../../../notebooks/phase_01_eda_signal_processing/)
```
