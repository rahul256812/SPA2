# 21CSE453T Speech Recognition — FT-3 Activity (Unit 3)
## From Voice to Text and Back: Complete Understanding of ASR and TTS

**Course:** 21CSE453T Speech Recognition  
**Faculty:** Dr. Akella S Narasimha Raju (103585)  
**Academic Year:** AY 2026-27 ODD  

---

### Pipeline Architecture
$$\text{Speech} \xrightarrow{\text{Framing / STFT}} \text{Log-Mel Spectrogram} \xrightarrow{\text{Acoustic Modeling}} \text{ASR} \xrightarrow{\text{CTC / Autoregressive Decoding}} \text{Text} \xrightarrow{\text{TTS Engine}} \text{Speech}$$

---

### Project Repository Contents

- **`RegNo_Name_FT3.ipynb`**: Complete end-to-end executable Colab notebook implementing all 15 activity steps.
- **`RegNo_Name_FT3_Report.pdf`**: Formatted 2-page mini-report covering objectives, acoustic analysis, CTC mechanics, WER tables, and TTS round-trip.
- **`disfluent_speech.wav`**: 16 kHz Mono WAV audio file (15.52 s) containing 5 clinical stutter disruptions (word repetitions, syllable repetitions, sound prolongations, and silent blocks).
- **`TTS_output.wav`**: 16 kHz Mono WAV audio file (6.53 s) synthesized from the cleaned ASR output.
- **`asr_architecture_diagram.png`**: High-resolution architecture comparison diagram (CTC vs. Whisper Encoder-Decoder).
- **`waveform_with_disruptions.png`**: Time-domain speech waveform with shaded disruption regions.
- **`log_mel_spectrogram_annotated.png`**: 80-band log-Mel spectrogram with acoustic annotations.
- **`original_vs_tts_comparison.png`**: Side-by-side waveform and spectrogram comparison of disfluent speech vs. TTS speech.
- **`DEMONSTRATION_SCRIPT_TEMPLATE.md`**: Timed 3-minute oral presentation guide for demonstrations and viva.

---

### Key Experimental Findings

1. **Acoustic Disruption Signatures:**
   - **Repetitions ("I-I-I", "m-m-market"):** Clustered, repeating vertical harmonic stacks separated by glottal pauses.
   - **Prolongations ("sssssunny", "ssssome"):** Stationary, flat high-frequency friction noise (>4 kHz) without vocal fold periodicity.
   - **Silent Blocks:** Complete 1.8-second acoustic void ($-\infty$ dB) across all 80 Mel frequency bands.

2. **CTC Behavior vs. Autoregressive Encoder-Decoder:**
   - **CTC (`facebook/wav2vec2-base-960h`):** Fricative prolongations merge into a single character via CTC Rule 1 (merging consecutive identical tokens). Repetitions survive because glottal pauses emit the CTC blank token `_`. Result: **0.00% WER against verbatim reference**, ideal for clinical speech therapy diagnostics.
   - **Whisper (`openai/whisper-small`):** Autoregressive Transformer decoder leverages an internal linguistic language model prior to suppress stutter repetitions and blocks, outputting fluent grammatical text. Result: **0.00% WER against clean reference**, ideal for consumer voice assistants.

3. **TTS Resynthesis & Round-Trip:**
   - Duration decreased from **15.52 s to 6.53 s** (57.9% reduction in temporal overhead).
   - Running ASR on the TTS output achieved **0.00% WER**, verifying complete lossless recovery of the intended semantic message.
