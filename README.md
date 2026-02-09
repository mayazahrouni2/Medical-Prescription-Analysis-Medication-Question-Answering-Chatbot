# Medical Prescription Analysis & Medication Question-Answering Chatbot

## Overview
This project presents an end-to-end intelligent system for analyzing medical prescriptions provided as **text or images**, and for delivering **safe, explainable, and patient-oriented question answering** about prescribed medications.

The system is designed to handle **noisy OCR outputs**, **handwritten prescriptions**, and **ambiguous medical notation** by combining:
- Optical Character Recognition (OCR)
- Large Language Models (LLMs)
- Semantic similarity search
- Retrieval-Augmented Generation (RAG)
- Explainable Artificial Intelligence (XAI)

The primary objective is to extract **structured and validated medication information** and provide **reliable medical explanations grounded in verified drug databases**.

To support real-world usage and deployment, a **dedicated REST API** has been developed and integrated via the **`ordonnance_api` branch**, enabling seamless interaction with the prescription analysis pipeline.

---

## Key Features
- Medical prescription analysis from **images or raw text**
- Robust handling of **handwritten and noisy prescriptions**
- Structured extraction of:
  - Drug name
  - Dosage
  - Frequency
  - Treatment duration
- Context-aware correction of OCR and extraction errors
- Secure medication matching using **verified drug databases**
- Safe, patient-oriented medical chatbot
- Explainable AI mechanisms for transparency and trust
- **LLM-as-a-Judge** framework for answer validation
- **REST API for integration and deployment** (`ordonnance_api` branch)

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
- Medically grounded answers related to:
  - Usage
  - Precautions
  - Side effects
  - Contraindications

---

## System Architecture & Processing Pipeline
The system follows a **multi-stage pipeline** designed to ensure robustness, medical safety, and explainability.

### Step 1 – OCR Text Extraction
- OCR engines evaluated: **Tesseract, EasyOCR, TrOCR, PaddleOCR**
- **PaddleOCR** selected for its superior performance on noisy layouts and mixed handwritten/printed content
- OCR output is treated as **inherently noisy and uncertain**

### Step 2 – Drug Extraction using Large Language Models
- OCR text processed using an LLM accessed via the **Esprit TokenFactory API**
- Model used: **LLaMA-3.1-70B-Instruct**
- Extracted information:
  - Drug names
  - Dosage
  - Posology
  - Treatment duration
- LLM-based extraction preferred over classical NER due to:
  - Handwritten prescriptions
  - Multilingual content
  - Limited availability of open-source medical NER models

### Step 3 – Context-Aware Drug Name Correction
- Secondary LLM module corrects drug names using:
  - Dosage patterns
  - Pharmaceutical syntax
  - Treatment duration consistency

### Step 4 – Drug Matching using FAISS Embeddings
- Drug names embedded using **SentenceTransformer**
- Semantic similarity matching performed with **FAISS**
- Reference database: **CIS_bdpm dataset**
  - Maintained by **ANSM, HAS, and UNCAM**
- Dataset cleaned and normalized to enable robust matching

### Step 5 – Final Drug List Construction
- Validated medications consolidated into a **trusted and structured drug list**

### Step 6 – Retrieval-Augmented Generation (RAG)
- Medical answers generated **exclusively from validated drug records**
- Significantly reduces hallucinations and improves medical safety

### Step 7 – Medical Chat and Patient Guidance
- Patient-oriented explanations covering:
  - Medication usage
  - Precautions
  - Side effects
  - Contraindications
- The system explicitly encourages medical consultation when required

---

## API Integration (Branch: `ordonnance_api`)
A RESTful API has been developed to expose the prescription analysis and medication question-answering capabilities of the system.

The API enables:
- Integration with web or mobile applications
- Programmatic submission of prescription images or text
- Retrieval of structured medication data
- Interaction with the medical question-answering module

The API implementation, routing, and service orchestration are available in the **`ordonnance_api` branch**, allowing **independent deployment** without impacting the research-oriented codebase.

---

## Explainable AI (XAI)
A **Hybrid Post-hoc Explainable AI** strategy is integrated, combining:
- **Declarative explanations** (why a drug was identified)
- **Counterfactual explanations** (what would change the outcome)

This approach enhances **transparency, reliability, and medical trustworthiness**.

---

## Evaluation Strategy
The system is evaluated using an **LLM-as-a-Judge** framework to assess:
- Medical correctness
- Safety
- Clarity
- Grounding in verified data

---

## Disclaimer
This system is designed as a **medical decision-support tool**.  
It does **not replace professional medical advice**, diagnosis, or treatment.  
Users are always encouraged to consult qualified healthcare professionals.

---

## Technologies Used
- PaddleOCR
- Large Language Models (LLaMA-3.1-70B-Instruct)
- FAISS
- Sentence Transformers
- Retrieval-Augmented Generation (RAG)
- Explainable AI (XAI)

---
## License This project is intended for academic and research purposes.
## License
This project is intended for **academic and research purposes**.
