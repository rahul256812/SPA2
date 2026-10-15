# 3-Minute Demonstration Script: From Voice to Text and Back
**Activity:** End-to-End ASR & TTS Pipeline Analysis  
**Student:** Student Name (RegNo)  

---

## Demonstration Timeline & Step-by-Step Spoken Script

### **[0:00 – 0:30] Introduction & Disfluent Audio Demonstration**
- **Action:** Open Colab / screen share. Play `disfluent_speech.wav`.
- **Spoken Script:**
  > *"Good morning. In this activity, I investigate how severe speech disruptions—specifically vocal blocks, repetitions, and sound prolongations—propagate through an end-to-end ASR and TTS pipeline.*  
  > *First, let us listen to the original 29.20-second disfluent recording.*  
  > *[Play audio clip]*  
  > *This recording contains six distinct disruption events: an initial articulatory block prior to speech onset, a pronoun false start repetition at 'I... I am', mid-phrase silent blocks, an alveolar fricative prolongation on 'ssssskills', and a post-lexical hesitation.*  
  > *We established two ground truths: a verbatim transcript containing all acoustic repetitions and prolongations, and a clean transcript reflecting the speaker's intended semantic message."*

---

### **[0:30 – 1:15] Time-Domain Waveform & 80-Mel Spectrogram Analysis**
- **Action:** Scroll to Step 4 and Step 6 plots (`waveform_with_disruptions.png` and `log_mel_spectrogram_annotated.png`).
- **Spoken Script:**
  > *"Moving to Part B: Signal and Features. We sampled at 16 kHz and applied framing with a 25 ms Hann window (400 samples) and a 10 ms hop size (160 samples), computing an 80-band log-Mel spectrogram.*  
  > *Here in the waveform plot, the shaded colored regions pinpoint the disruptions. In the log-Mel spectrogram, we observe three very distinct acoustic signatures:*  
  > *1. Repetitions appear as clustered, repeating vertical harmonic stacks separated by glottal pauses.*  
  > *2. Prolongations on the sibilant 's' show up as flat, stationary horizontal energy bands in high frequencies above 4 kHz without periodic pitch striations.*  
  > *3. The silent blocks are visible as complete acoustic voids across all 80 frequency bands, reflecting complete vocal tract closure."*

---

### **[1:15 – 2:15] ASR Model Comparison, CTC Collapse & WER Breakdown**
- **Action:** Show the ASR Architecture diagram and the Comparison / Alignment Table.
- **Spoken Script:**
  > *"In Part C, we evaluated two contrasting ASR architectures: facebook's wav2vec2-base-960h, which uses Connectionist Temporal Classification (CTC), and openai's whisper-small, which uses an autoregressive encoder-decoder.*  
  > *Wav2Vec2 produced 0.00% WER against the verbatim reference. Looking at the frame tokens, CTC operates under two rules: merging consecutive identical tokens and removing blanks. During the prolongation 'ssssskills', consecutive 'S' tokens merge into a single character, successfully collapsing the stretch. However, during repetitions ('I... I am'), the glottal pauses emit blank tokens '_', which prevents them from merging. Thus, repetitions survive in CTC!*  
  > *Whisper, on the other hand, achieved 0.00% WER against the clean reference. Because its decoder is an autoregressive language model, its internal linguistic prior actively recognizes the repetitions and silent blocks as speech disfluencies and filters them out automatically, outputting pure fluent text!"*

---

### **[2:15 – 3:00] TTS Resynthesis, Side-by-Side Comparison & Key Takeaways**
- **Action:** Play `TTS_output.wav` and show the side-by-side comparison plot.
- **Spoken Script:**
  > *"Finally, in Part D, we passed the clean text into our TTS engine to synthesize speech.*  
  > *[Play TTS audio clip]*  
  > *Comparing the original and synthesized speech, the duration plummeted from 29.20 seconds down to 19.28 seconds—a 34.0% reduction in temporal overhead. The side-by-side spectrograms confirm that all silent voids and choppy energy bursts are replaced with smooth, continuous formant contours.*  
  > *We also conducted a round-trip test by running ASR on the TTS audio, which yielded an exact 0.00% WER.*  
  > *In conclusion: CTC architectures are acoustic-faithful and ideal for clinical diagnostics and speech pathology, while encoder-decoder models act as natural speech cleaners for voice assistants. Thank you!"*

