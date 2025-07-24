This project implements a sophisticated machine learning pipeline to create a **drug recommendation system**, designed to function as a clinical decision support tool. The primary objective is to accurately predict the specific medications a patient is likely to be prescribed during a hospital admission, based on a comprehensive view of their clinical profile.

### Methodology and Data

The project leverages the **MIMIC-IV (Medical Information Mart for Intensive Care)** dataset, a large, de-identified database containing detailed patient information from critical care units.

A key innovation of this project is its prediction target. Instead of merely predicting a drug's name, the model predicts a **composite drug label**. This granular label combines three critical pieces of information:
* **NDC (National Drug Code):** The specific drug product.
* **Dosage Strength:** The concentration of the medication.
* **Prescription Duration:** The length of the treatment course.

This approach provides a much more clinically actionable prediction compared to generic drug recommendations.

#### Feature Engineering and Modeling

The model's predictive power is built on a rich, multi-modal feature set that fuses both structured and unstructured data.

* **Structured Clinical Data:** This includes patient demographics (age, gender), admission details (type, location), insurance status, and codified clinical events like diagnoses and procedures (ICD codes), and emergency department triage data.
* **Unstructured Clinical Notes:** To capture the nuanced narrative of a patient's condition, the system performs advanced Natural Language Processing (NLP) on discharge summaries. It utilizes **Bio_ClinicalBERT**, a state-of-the-art transformer model pre-trained specifically on biomedical and clinical text, to generate powerful, context-aware embeddings.

These features are then fed into a **deep neural network** architected for multi-label classification, allowing it to predict a unique set of multiple potential medications for each patient.

To ensure the model is robust and generalizable, the data is split on a **patient-level basis**. This prevents data leakage, which occurs when information about the same patient appears in both the training and testing sets. This method results in a more realistic and reliable evaluation of the model's performance on truly unseen patients.
