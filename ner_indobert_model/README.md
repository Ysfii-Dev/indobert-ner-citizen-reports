# IndoBERT NER for Citizen Reports

This project aims to build a **Named Entity Recognition (NER)** system to automatically extract key information from citizen reports related to **public infrastructure issues** in Indonesia.  
The trained NER model is designed to be integrated into a web-based reporting application, enabling automatic classification of user reports into multiple entity categories.

---

## 🚀 Key Features

- **Domain-specific NER** for public infrastructure reports
- **Entity Categories:**
  - `LOC` → Location
  - `INFRA` → Infrastructure type
  - `PROB` → Problem type
  - `TIME` → Time
  - `DESC` → Additional description
  - `SEV` → Severity level
- **Dataset preprocessing** from real citizen reports
- **Automatic annotation** using dictionary-based entity labeling
- **CoNLL dataset format** for NER training
- **Fine-tuned IndoBERT** (`taufiqdp/indonesian-sentiment`)
- **Evaluation metrics:** F1, Precision, Recall
- **Ready-to-use model** for backend integration (Flask, FastAPI, or Streamlit)

---

## 📊 Model Training

- **Base model:** IndoBERT (`taufiqdp/indonesian-sentiment`)
- **Task:** Named Entity Recognition (token classification)
- **Dataset:** Citizen reports on public infrastructure issues (preprocessed & automatically annotated)
- **Format:** CoNLL with BIO tagging scheme
- **Evaluation Results:**
  - Precision: _xx.xx%_
  - Recall: _xx.xx%_
  - F1-score: _xx.xx%_

---

## 💻 Usage

```python
from transformers import AutoTokenizer, AutoModelForTokenClassification, pipeline

# Load model
model_name = "username/indobert-ner-citizen-reports"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForTokenClassification.from_pretrained(model_name)

# Create NER pipeline
ner_pipeline = pipeline("ner", model=model, tokenizer=tokenizer, aggregation_strategy="simple")

# Example input
text = "Lampu jalan di Jl. Sudirman mati sejak malam kemarin."

# Run prediction
entities = ner_pipeline(text)
print(entities)
```

---

## 📌 Applications

- Automated extraction of structured information from unstructured citizen reports
- Public infrastructure monitoring systems
- Government service platforms for faster issue resolution

---

## 📜 License

This model is released under the MIT License.

---

## 🙌 Acknowledgements

- IndoBERT pretrained model by [taufiqdp](https://huggingface.co/taufiqdp/indonesian-sentiment)
- Hugging Face Transformers
- Citizen report datasets on public infrastructure issues
