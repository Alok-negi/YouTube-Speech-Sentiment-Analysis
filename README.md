# 🎯 YouTube-Speech-Sentiment-Analysis

This project performs **speech-to-text transcription** and **sentiment analysis** on YouTube videos.
It extracts the **audio**, sends it to **AssemblyAI** for transcription + sentiment analysis, and saves the results in text and JSON files.

---

## 📂 Project Files

### 1. `main.py`

* The **entry point** of the project.
* Downloads YouTube video info & audio.
* Calls the transcript and sentiment analysis functions.
* Processes the generated JSON file to count **positive, negative, and neutral** sentences.

---

### 2. `yt_extractor.py`

* Uses **yt\_dlp** to fetch video details.
* Functions:

  * `get_video_info(url)` → Gets metadata (title, formats, etc.).
  * `get_audio_url(video)` → Finds the best `.m4a` audio link.

---

### 3. `api_03.py`

* Handles all communication with **AssemblyAI API**.
* Functions:

  * `upload(filename)` → Uploads audio file to AssemblyAI.
  * `transcribe(audio_url, sentiment_analysis)` → Requests transcription.
  * `poll(transcript_id)` → Checks if transcription is done.
  * `save_transcript(url, title, sentiment_analysis)` → Saves transcript to `.txt` and results (with sentiment) to `.json`.

---

### 4. `api_secrets.py`

* Stores your **AssemblyAI API key** safely.

---

## 📊 Output

1. **Transcript File (`.txt`)** → Full text of the video.
2. **Sentiment JSON File (`_sentiments.json`)** → Each sentence has:

   * `"sentiment"` → `POSITIVE`, `NEGATIVE`, or `NEUTRAL`.
   * `"text"` → The actual spoken sentence.
   * `"start"` / `"end"` → Time range (in milliseconds) of when the sentence was spoken.
   * `"confidence"` → AI’s confidence score.

Example JSON snippet:

```json
{
  "sentiment": "POSITIVE",
  "text": "The new iPhone's display is brighter than before.",
  "start": 9120,
  "end": 21280,
  "confidence": 0.98,
  "speaker": null
}
```

---

## 🔄 Workflow

1. Extract YouTube video info → `yt_extractor.py`
2. Get audio URL → `yt_extractor.py`
3. Upload audio & request transcription → `api_03.py`
4. AssemblyAI transcribes + analyzes sentiment
5. Save results → `.txt` + `.json`
6. `main.py` analyzes sentiment counts & ratios

---
