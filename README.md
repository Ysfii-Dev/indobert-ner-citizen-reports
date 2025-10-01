Siap 👍, saya buatkan draft **README.md** untuk dokumentasi proyek kamu:

---

# 📌 Ekstraksi Informasi Laporan Masyarakat dengan Named Entity Recognition (NER) untuk Identifikasi Masalah Infrastruktur Publik

Proyek ini bertujuan untuk membangun sistem **Named Entity Recognition (NER)** yang dapat mengekstraksi informasi penting dari laporan masyarakat terkait **masalah infrastruktur publik**. Model NER yang dilatih kemudian akan diintegrasikan ke dalam aplikasi web pelaporan, sehingga laporan pengguna dapat secara otomatis dipisahkan menjadi beberapa kategori entitas: lokasi, jenis infrastruktur, jenis masalah, waktu, keterangan tambahan, dan tingkat kerusakan.

---

## 🚀 Fitur Utama

- **NER khusus laporan infrastruktur publik**
  - **LOC** → Lokasi
  - **INFRA** → Jenis Infrastruktur
  - **PROB** → Jenis Masalah
  - **TIME** → Waktu
  - **DESC** → Keterangan tambahan
  - **SEV** → Tingkat Kerusakan
- **Preprocessing dataset laporan masyarakat**
- **Anotasi otomatis** menggunakan kamus entitas (dictionary-based labeling)
- **Format dataset CoNLL** untuk training
- **Fine-tuning IndoBERT** (`taufiqdp/indonesian-sentiment`)
- **Evaluasi model** dengan metrik F1, precision, recall
- **Model siap digunakan** untuk integrasi ke backend (Flask/FastAPI/Streamlit)

---

## 📂 Struktur Proyek

```
ner_proyek/
│
├── data/
│ ├── LOC.csv
│ ├── ner_dataset_convertedV3.conll
│ ├── preprocessed_data.csv
│
├── ner_indobert_model/  # folder untuk menyimpan model NER
│
├── ner-indobert-train/  # folder training (misal checkpoint)
│
├── notebook/
│ ├── crawl_NLP_copy.ipynb
│ ├── ner_bio_tagging.ipynb
│ ├── train_ner.ipynb
│
└── README.md

```

---

## ⚙️ Instalasi

Clone repo ini dan install dependensi:

```bash
git clone https://github.com/username/ner-infra-proyek.git
cd ner-infra-proyek
pip install -r requirements.txt
```

---

## 📊 Dataset

Dataset awal (`preprocessed_data.csv`) diperoleh dari hasil crawling data laporan masyarakat di platform X (Twitter/X) dengan kata kunci seputar laporan infrastruktur publik, seperti:

- Jalan Rusak
- Lampu Jalan Padam
- Sampah
- Banjir
- Pohon Tumbang

Data hasil crawling kemudian melalui tahap pembersihan (`preprocessing`) untuk menghapus noise seperti emoji, URL, mention, hashtag, dan karakter khusus.

Selanjutnya dataset ini digunakan sebagai bahan dasar anotasi entitas (NER). Dataset kemudian **dianotasi otomatis** menggunakan **kamus entitas** (dictionary) → dikonversi ke **format CoNLL**.

**📌 Apa itu Anotasi BIO?**

Anotasi **BIO (Begin, Inside, Outside)** adalah salah satu skema pelabelan yang paling umum dipakai dalam Named Entity Recognition (NER).
Setiap token (kata) dalam teks diberi label sesuai dengan perannya terhadap suatu entitas.

- B-XXX (Begin) → menandai awal dari sebuah entitas dengan tipe XXX
- I-XXX (Inside) → menandai kata lanjutan (di dalam) dari entitas bertipe XXX
- O (Outside) → menandai token yang bukan bagian dari entitas manapun

Contoh anotasi BIO:

```
Di      O
Jalan   B-INFRA
Ahmad   I-LOC
Yani    I-LOC
Bandung B-LOC
lampu   B-INFRA
jalan   I-INFRA
rusak   B-PROB
parah   B-SEV
```

---

## 🧠 Training Model NER

Model dasar: **IndoBERT (taufiqdp/indonesian-sentiment)**

Langkah utama di notebook:

1. **Parse dataset CoNLL**
2. **Split train/validation/test (80/10/10)**
3. **Encode labels**
4. **Tokenisasi & align label**
5. **Load model IndoBERT**
6. **Training dengan HuggingFace `Trainer`**
7. **Evaluasi metrik NER**
8. **Save model ke `ner_indobert_model/`**

---

## 📈 Evaluasi

Model dievaluasi dengan metrik:

- **Precision**
- **Recall**
- **F1-score**

Hasil Traning:

```
Precision: 0.88
Recall:    0.91
F1-score:  0.89
```

---

## 💾 Penyimpanan Model

Model hasil training disimpan dalam folder `ner_indobert_model/`.
Format: HuggingFace Transformers → bisa langsung `from_pretrained`.

```python
from transformers import AutoTokenizer, AutoModelForTokenClassification

model_path = "./ner_indobert_model"
tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoModelForTokenClassification.from_pretrained(model_path)
```

---

## 🌐 Integrasi ke Web

Model ini dapat diintegrasikan ke aplikasi web (Flask, FastAPI, atau Streamlit).
Alur sistem:

1. User mengunggah laporan teks di web.
2. Teks diproses oleh model NER.
3. Sistem mengekstraksi entitas → ditampilkan sebagai informasi terstruktur (lokasi, infrastruktur, masalah, waktu, keterangan, tingkat kerusakan).

---

## 📌 Contoh Laporan & Ekstraksi

**Input Laporan:**

> "Di Jalan Ahmad Yani, Bandung, sebuah pohon besar tumbang menimpa trotoar dan lampu jalan pada tadi malam, menyebabkan kondisi berbahaya karena area menjadi gelap dan sulit dilalui, dengan tingkat kerusakan cukup parah."

**Output Ekstraksi (NER):**

- **LOC**: Jalan Ahmad Yani, Bandung
- **INFRA**: trotoar, lampu jalan
- **PROB**: tumbang
- **TIME**: tadi malam
- **DESC**: berbahaya, gelap, sulit dilalui
- **SEV**: parah

---

## 📜 Lisensi

Proyek ini dilisensikan di bawah **MIT License** – bebas digunakan dengan mencantumkan atribusi.

---

## 👨‍💻 Kontributor

- **Yusfi Syawali** – Pengembang Model NER
