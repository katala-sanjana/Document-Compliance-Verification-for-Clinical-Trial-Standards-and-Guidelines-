# Towards Explainability: Document Compliance Verification for Clinical Trial Standards and Guidelines  

Clinical trial sponsors lose time and money due to manual, inconsistent compliance checking. This project automates the verification of clinical documents against FDA/ICH guidelines using a knowledge graphs and Gemma 4 LLM.

Key outcomes:
- Identifies gaps in regulatory documents
- Provides traceable explanations (regulation citations + document evidence)
- Zero false positives on out-of-scope concepts 

### Layer 1 — Data Ingestion
- Summarizes lengthy regulatory documents using Gemma 4 due to token limits
- Converts guidelines into structured JSON file for knowledge graph construction 

### Layer 2 — Knowledge Graph Construction
- Built using NetworkX library for granular control and debugging
- Nodes: GCP, informed consent, IRB, HIPAA, etc.
- Edges: `informs`, `related_to`, `requires`, `cited_in`
- Visualized using Matplotlib; stored as pickle file for reusability

### Layer 3 — Gemma 4 Inference
We used `gemma-4-e2b-it` with 4-bit quantization due to memory constraints. 

Three sub-components:
1. Document Type Detection — Classifies if document is a SUBMISSION (protocol, ICF, IND) or GUIDANCE (FDA/ICH guideline)
2. KG-Grounded Analysis — Validates document using node-centrality analysis and identifies gaps with regulation citations
3. Reasoning— Understands regulatory boundaries (Ex: HIPAA is out of scope for ICH/CGMP documents)

### Layer 4 — Explainability & Output
- Each finding is traced through a knowledge graph edge
- Recommendation summaries generated using one-shot prompting 
- FastAPI backend exposed via ngrok for frontend consumption 

## Technologies Used  
1. LLM : Gemma 4 (4-bit quantized via Hugging Face Transformers)  
2. Backend : FastAPI, ngrok 
3. Platform : Kaggle (GPU)  

## Results 
1. False positive gap flags - Zero (correctly identifies out-of-scope concepts) 
2. Explainability - Every finding includes regulation citation + document evidence + graph trace    

## Author 
Sanjana Katala

[LinkedIn](https://www.linkedin.com/in/sanjana-katala-0171b9243/)



