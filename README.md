# MediScanAI

MediScanAI is an AI-powered healthcare assistant that helps users analyze symptoms and validate medicines from pill/package images.  
It combines symptom-based disease retrieval, OCR-based medicine name extraction, medicine-use matching, voice input support, and LLM-generated explanations in one modular pipeline. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

---

## Features

- Predicts probable diseases or conditions from user-entered symptoms
- Accepts pill or medicine package images and extracts medicine text using OCR
- Matches detected medicine against likely conditions or symptoms
- Suggests whether the medicine appears suitable or not
- Supports spoken symptom input through Whisper-based transcription
- Uses an Ollama-powered LLM to generate readable medical guidance
- Modular backend design for OCR, retrieval, embeddings, prompting, formatting, and speech input
- Streamlit-based frontend for simple interaction and testing :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

---

## Project Idea

The main goal of MediScanAI is to assist users in two ways:

1. **Symptom-based analysis**  
   The user enters symptoms, and the system retrieves the most probable disease or condition from a medical dataset.

2. **Medicine validation from image input**  
   The user uploads a pill/package image, and the system extracts the medicine or active ingredient name using OCR.  
   - If symptoms were already provided, the system checks whether the detected medicine is appropriate for the likely condition.
   - If symptoms are not provided, the system returns the likely diseases/conditions that the detected medicine can be used for.

The final response is generated in a more user-friendly way using a local LLM through Ollama. :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5}

---

## How It Works

The pipeline follows these steps:

1. **User input**
   - Text symptoms are entered manually
   - Optionally, the user can upload a medicine/pill image
   - Spoken symptom input can also be transcribed using Whisper

2. **Text preprocessing**
   - User symptom text is normalized
   - OCR text is cleaned and joined for downstream retrieval

3. **Retrieval**
   - The system retrieves relevant disease data from the symptom query
   - It retrieves medicine and drug-dictionary matches from OCR text and combined query text
   - Sentence-transformer embeddings and FAISS-style retrieval are used for semantic matching

4. **Analysis**
   - The system compares likely diseases/symptoms with the detected drug indications
   - It checks whether the medicine appears relevant to the condition

5. **Response generation**
   - Retrieved context is passed to an Ollama-based LLM
   - The LLM generates the final explanation, alternatives, and warnings

6. **Frontend display**
   - Results are shown through a Streamlit interface in a structured form :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

---

## Tech Stack

### Languages and Frameworks
- Python
- Streamlit

### AI / ML / NLP
- Sentence Transformers
- FAISS
- PaddleOCR / PaddleX
- Faster-Whisper / Whisper
- Ollama

### Other Libraries
- OpenCV
- Pillow
- RapidFuzz
- NumPy
- Matplotlib
- python-dotenv :contentReference[oaicite:8]{index=8}

---

## Project Structure

```text
MediscanAI/
│
├── backend/
│   ├── core.py
│   ├── core_new.py
│   ├── embeddings.py
│   ├── formatter.py
│   ├── formatter_new.py
│   ├── llm.py
│   ├── ocr.py
│   ├── prompt.py
│   ├── retriever.py
│   ├── utils.py
│   └── whisper.py
│
├── frontend/
│   ├── app.py
│   └── app_new.py
│
├── tests/
│   ├── test_embeddings.py
│   ├── test_llm.py
│   ├── test_ocr.py
│   ├── test_pipeline.py
│   ├── test_pipeline_new.py
│   ├── test_retriever.py
│   ├── test_utils.py
│   └── test_whisper.py
│
├── requirements.txt
└── README.md