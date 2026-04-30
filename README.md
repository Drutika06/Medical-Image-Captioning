# 🏥 Entity-Aware Medical Image Captioning

## 📌 Overview
This project is an advanced **Entity-Aware Medical Image Captioning System** designed to act as a rapid triage assistant for radiologists. By combining deep visual feature extraction with the domain-specific linguistic knowledge of **PubMedBERT**, this model does not just generate generic captions; it actively identifies critical clinical entities (pathologies, anatomical structures) and synthesizes them into highly structured, medically accurate diagnostic reports.

## 🎯 Objectives
* **Precision Extraction:** Identify specific medical entities directly from radiological scans, ignoring dataset noise and artifacts.
* **Clinical Synthesis:** Automatically generate grammatically correct, professional clinical sentences from extracted entities.
* **Explainable AI (XAI):** Provide interpretability through interactive heatmaps (Jet/Inferno) and region-of-interest mapping.
* **Interactive Dashboard:** Offer a seamless user interface for medical professionals to upload scans and receive instant, patient-friendly diagnostic summaries.

## 🧠 System Architecture & Models
This project moves beyond standard CNN-RNN pipelines, utilizing a custom **Memory Fusion Bridge** architecture:
* **Visual Encoder:** A deep CNN (e.g., DenseNet) extracts high-dimensional spatial features from the medical images.
* **Semantic Knowledge Base:** **PubMedBERT** tokenizes and embeds clinical entities, ensuring the model understands complex medical terminology.
* **Entity-Aware Transformer Decoder:** A custom autoregressive transformer with strict causal masking. It utilizes a Cross-Attention mechanism where the decoder queries BOTH the visual proof (image features) and clinical knowledge (entity embeddings) simultaneously.
* **Clinical Synthesizer:** A deterministic NLP formatting engine that converts raw AI outputs into readable, human-like clinical impressions.

## 💻 Training Infrastructure & Environment
To handle the computational overhead of processing high-resolution medical images alongside a heavy Transformer decoder, the model was trained in a high-performance cloud environment:
* **Compute Environment:** Google Colab Pro
* **Hardware Accelerator:** NVIDIA T4 Tensor Core GPU (16GB VRAM)
* **Training Duration:** Trained for **60 Epochs** on the complete ROCO training split.
* **Optimization Focus:** The training loop was strictly monitored to manage loss convergence and prevent overfitting, ensuring the autoregressive decoder learned complex medical grammar without hallucinating entities not present in the visual features.  

## ⚙️ How It Works
1. **Input:** The user selects a radiological scan (X-Ray, CT, MRI, Ultrasound, etc.) via the interactive dashboard.
2. **Multi-Modal Fusion:** The deep learning model extracts visual patches from the image and aligns them with embedded clinical knowledge.
3. **Explainable Visualizations:** Alongside the original image, the dashboard instantly generates and displays:
   * **Density Analysis Heatmaps (Jet)**
   * **Focus Analysis Heatmaps (Inferno)**
   * **Anatomic Region of Interest (ROI) Mapping**
4. **Entity-Aware Captioning:** The Transformer precisely detects clinical entities and synthesizes an **AI-generated caption** that is strictly grounded in those identified entities, ensuring zero hallucinations.
5. **Report Generation:** The system outputs a comprehensive, structured radiology report featuring a Clinical Impression, detected entities with medical explanations, and a simplified patient-friendly translation.

<img width="1919" height="852" alt="image" src="https://github.com/user-attachments/assets/5c88ab8f-942e-46c4-86fa-533eb2b78dca" />


## 🗂️ Dataset
* **Dataset Name:** ROCO (Radiology Objects in COntext) Dataset
* **Link:** [Kaggle - ROCO Dataset](https://www.kaggle.com/datasets/drutikapidikiti/dataset-roco)

<img width="837" height="767" alt="image" src="https://github.com/user-attachments/assets/85bcc67d-e522-4c00-8f6b-ce6379015015" />

* **Description:** A large-scale medical dataset sourced from PubMed articles, containing diverse imaging modalities and their corresponding clinical captions/entities.
* **Focus:** Optimized for precision over recall to prioritize clinical safety and eliminate AI hallucinations.

## 🛠️ Tech Stack
* **Deep Learning Framework:** PyTorch, Hugging Face `transformers`
* **Computer Vision:** OpenCV, Pillow, TorchVision
* **Data & Math:** NumPy, Pandas
* **NLP:** SpaCy, NLTK
* **UI & Visualization:** Matplotlib, Seaborn, IPyWidgets

## 🚀 How to Run
Follow these steps to run the interactive dashboard locally or in a cloud notebook:

1. **Clone this repository:**
   ```bash
   git clone [https://github.com/yourusername/Medical-Image-Captioning.git](https://github.com/yourusername/Medical-Image-Captioning.git)
   cd Medical-Image-Captioning
   
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   
3. Install the specialized medical NLP dictionary (SciSpaCy):
   ```bash
   pip install [https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.1/en_core_sci_sm-0.5.1.tar.gz](https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.1/en_core_sci_sm-0.5.1.tar.gz)

4. Launch the Dashboard:
Open the main Jupyter Notebook containing the UI code (e.g., Entity_Aware_Captioning_Dashboard.ipynb), ensure your dataset paths are configured correctly, and run all cells. The IPyWidgets interactive dashboard will render directly at the bottom of the notebook.   
