# Voice Cloning TTS Model Comparison – `your_tts` vs `vits`

## Overview
This project evaluates and compares **two Text-to-Speech (TTS) models** from [Coqui TTS](https://github.com/coqui-ai/TTS):

- **`your_tts`** – Multilingual, zero-shot **voice cloning** model.  
- **`tts_models/en/ljspeech/vits`** – VITS model trained on **LJ Speech**, optimized for natural English speech, but **not designed for voice cloning**.  

The objective was to analyze **voice similarity (cloning quality)** and **performance (time taken)** between the two models.

---

## Vision
My long-term vision is to **generate audiobooks in the author's own cloned voice – multilingual**.  

- It should take only a **few hours** to generate a full audiobook in **any given language**.  
- I am experimenting with different models to evaluate **which best fits this goal**.  

---

## Methodology

1. **Reference Voices**  
   - Several `.wav` reference recordings were used for cloning.  

2. **Text Samples**  
   - Multiple text passages/pages were synthesized for each voice.  

3. **Evaluation Metrics**  
   - **Cosine Similarity**: Speaker embedding similarity between original and cloned audio (higher = closer to target voice).  
   - **Performance (Time Taken)**: Average time per sample across models.  

4. **Visualization**  
   - Bar charts comparing similarity per model & voice.  
   - Performance plots comparing average synthesis times.  

---

## 📂 Data File Structure
data/
├── Sample_Voice1/
│   ├── voicefile_001.wav
│   ├── voicefile_002.wav
│   ├── voicefile_003.wav
│
├── Sample_Voice2/
│   ├── voicefile_001.wav
│   ├── voicefile_002.wav
│   ├── voicefile_003.wav
│
├── Sample_Voice3/
│   ├── voicefile_001.wav
│   ├── voicefile_002.wav
│   ├── voicefile_003.wav


Generated voice cloned files stored with Naming convention


<file_name>_<model_name>_<page_name>.wav 

data/
├── Sample_Voice1/
│   ├── results/
│   │   ├── voicefile_001_xtts_v2_Page1.wav
│   │   ├── voicefile_001_your_tts_Page2.wav
│   │   ├── voicefile_002_vits_Page3.wav
│
├── Sample_Voice2/
│   ├── results/
│   │   ├── voicefile_001_xtts_v2_Page1.wav
│   │   ├── voicefile_002_your_tts_Page2.wav
│   │   ├── voicefile_003_vits_Page3.wav

---

##  Results & Analysis

###  Voice Similarity
- **`your_tts`**:  
  - Achieved **high similarity scores**, demonstrating effective zero-shot voice cloning.  
  - Adapted well across multiple reference speakers.  

- **`vits (ljspeech)`**:  
  - Produced **natural-sounding speech**, but similarity scores were **low** since it is **not a cloning model**.  
  - Output voice sounded closer to its **pretrained speaker (LJ Speech)** rather than the reference voice.  

 **Conclusion**: `your_tts` is clearly superior for cloning tasks, while `vits` is better suited for general English TTS when cloning is not required.

---

### Performance (Time Taken)
- **`vits`**:  
  - **Faster inference speed** due to single-speaker optimization.  
- **`your_tts`**:  
  - Slightly slower, as it processes **reference embeddings** for cloning.  

 **Conclusion**:  
If **speed and natural English speech** are the goal → `vits` wins.  
If **voice cloning accuracy** is required → `your_tts` is the better choice.  

---

## Key Takeaways
- **For cloning:** Use `your_tts`.  
- **For fast & natural English TTS:** Use `vits`.  
- Future work can include testing **`xtts_v2`** for even more natural multilingual cloning.  

---

## Output Structure

1. **Audio Files** – Stored under `data/sample_voice<number>/results/<file_name>_<model_name>_<page_name>.wav 
2. **Similarity Scores** – CSV file: `multi_model_voice_similarity.csv`  
3. **Performance Metrics** – CSV file: `performance_metrics.csv`  
4. **Charts** – PNG charts comparing models  

---

##  How to Run

1. Clone the repo & install dependencies:
   ```bash
   git clone <repo-url>
   cd project_root
   pip install -r requirements.txt
   ```

2. Run the notebook or Python script to generate audio & evaluate:
   ```bash
   jupyter notebook notebooks/VoiceCloning_Comparison.ipynb
   ```

3. Results will be saved inside `/outputs/`.

---

##  Future Work
- Add **XTTS-v2** and **Eleven-labs** to evaluation.  
- Explore **scaling to full audiobook generation** in multiple languages.  
- Investigate **GPU optimization** for faster inference.  
