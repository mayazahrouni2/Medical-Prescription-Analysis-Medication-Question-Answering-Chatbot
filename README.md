# Medical Prescription Analysis & Medication Question-Answering Chatbot

## Overview
This project implements an end-to-end intelligent system for analyzing medical prescriptions provided as text or images and enabling safe, explainable, and patient-oriented question-answering about prescribed medications.

The system is designed to handle noisy OCR outputs, handwritten prescriptions, and ambiguous medical notation by combining OCR, Large Language Models (LLMs), semantic similarity search, Retrieval-Augmented Generation (RAG), and Explainable AI (XAI) techniques.

The primary objective is to extract structured medication information and provide reliable medical explanations grounded in verified drug databases.

---

## Key Features
- Medical prescription analysis from **images or text**
- Robust handling of **handwritten and noisy prescriptions**
- Structured extraction of:
  - Drug name
  - Dosage
  - Frequency
  - Treatment duration
- Context-aware correction of OCR and extraction errors
- Secure medication matching using verified drug databases
- Safe, patient-oriented medical chatbot
- Explainable AI integration for transparency and trust
- LLM-as-a-Judge evaluation for answer validation

---

## Input & Output Specification

### Inputs
- Medical prescription image (photo or scan) or raw text
- Optional natural-language question from the user

### Outputs
- Structured prescription data:
  - Drug name
  - Dosage
  - Frequency
  - Duration
- Reliable, medically grounded answers about:
  - Usage
  - Precautions
  - Side effects
  - Contraindications

---

## System Architecture & Pipeline

The system follows a multi-stage pipeline designed for robustness, safety, and explainability:

### Step 1 – OCR Text Extraction
- OCR engines evaluated: **Tesseract, EasyOCR, TrOCR, PaddleOCR**
- **PaddleOCR** selected for best performance on noisy and mixed-content prescriptions
- OCR output is treated as **noisy and uncertain**

### Step 2 – Drug Extraction using Large Language Models
- OCR text processed using an LLM accessed via **Esprit TokenFactory API**
- Model used: **LLaMA-3.1-70B-Instruct**
- Extracted entities:
  - Drug names
  - Dosage
  - Posology
  - Duration
- LLM-based approach chosen over classical NER due to:
  - Handwritten text
  - Multilingual prescriptions
  - Limited open-source medical NER models

### Step 3 – Context-Aware Drug Name Correction
- Secondary LLM module corrects drug names using:
  - Dosage patterns
  - Pharmaceutical syntax
  - Treatment duration consistency

### Step 4 – Drug Matching using FAISS Embeddings
- Drug names embedded using **SentenceTransformer**
- Semantic matching performed with **FAISS**
- Reference database: **CIS_bdpm dataset**
  - Maintained by ANSM, HAS, and UNCAM
- Dataset cleaned and normalized for robust matching

### Step 5 – Final Drug List Construction
- Validated medications consolidated into a structured, trusted drug list

### Step 6 – Retrieval-Augmented Generation (RAG)
- Medical answers generated exclusively from validated drug records
- Reduces hallucinations and improves medical safety

### Step 7 – Medical Chat and Patient Guidance
- Patient-oriented explanations:
  - Medication usage
  - Precautions
  - Side effects
  - Contraindications
- System encourages medical consultation when necessary

---

## Explainable AI (XAI)
A **Hybrid Post-hoc Explainable AI** strategy is integrated:
- Declarative explanations (why a drug was identified)
- Counterfactual explanations (what would change the outcome)
- Enhances transparency, reliability, and trustworthiness

---

## Evaluation Strategy
- **LLM-as-a-Judge** framework used to assess:
  - Medical correctness
  - Safety
  - Clarity
  - Grounding in verified data

---

## Disclaimer
This system is designed as a **medical decision-support tool**.
It does **not replace professional medical advice**.
Users are always encouraged to consult healthcare professionals.

---

## Technologies Used
- PaddleOCR
- Large Language Models (LLaMA-3.1-70B-Instruct)
- FAISS
- Sentence Transformers
- Retrieval-Augmented Generation (RAG)
- Explainable AI (XAI)

---

## License
This project is intended for academic and research purposes.
