Sentiment Analysis Project - Kelompok NaLapPro (NLP B)

📋 Informasi Kelompok

Nama Kelompok	NaLapPro
Materi :	Fundamental NLP
Tutor  : Fadilah Nur Imani

Anggota Kelompok:

No	Nama
1	Yasmin Kamila	
2	Eko Erwis Wandoko	
3	M Dhimas Agung Sugiharto (Pemilik akun github ini)	
4	Muh. Idris
5 Wahid Setio Darmadi

Struktur Proyek

Sentiment-analysis/
├── data/                           # Dataset mentah dan terproses
├── document/                       # Dokumentasi proyek (ppt)
├── model_terbaik/                   # Model final yang sudah dilatih
├── notebooks/                       # Semua notebook eksperimen
│   ├── 1_Preprocessing/            # Notebook preprocessing data
│   ├── 2_Feature_Engineering/       # Notebook feature engineering
│   ├── 3_Kelompok/                  # Notebook eksperimen kelompok
│   │   ├── LSTM/                    # 4 versi LSTM (v01-v04)
│   │   └── RandomForest/             # 6 versi Random Forest (v01-v06)
│   └── 4_Individu/                   # Notebook eksperimen individu
│       ├── LogisticRegression/       # 6 percobaan LR
│       ├── NaiveBayes/               # 3 percobaan NB
│       └── Ensemble/                 # Ensemble Methods
├── requirements.txt                 # Dependencies proyek
└── README.md                        # Dokumentasi proyek


Ringkasan Hasil Eksperimen

Model	                            Akurasi	                  Keterangan
Naive Bayes (MultinomialNB)	      (62.8%	MODEL TERBAIK)- Stabil & optimal
Ensemble Sederhana (NB + LR)	    62.8%	                  Bobot [0.3:0.7]
Logistic Regression	              61.4% - 62.3%	          C=0.1, class_weight='balanced'
Voting Classifier	                62.26% - 62.53%	        Hard & Soft voting
Linear SVM	                      61.2%	                  C=1.0
Random Forest	                    57.0% - 58.1%	          Overfitting
LSTM	                            56% - 59%	              Overfitting parah
XGBoost	                          52.3%	                  Kurang cocok
Gradient Boosting	                54.3%	                  Kurang cocok
AdaBoost	                        44.9%	                  Tidak cocok

Model Terbaik: Naive Bayes (MultinomialNB)
📊 Detail Model Terbaik:
   • Algoritma      : Multinomial Naive Bayes
   • Alpha optimal  : 1.0 (dari grid search)
   • TF-IDF         : Optimal (max_features=3000, ngram_range=(1,3))
   • Akurasi        : 62.8%
   • Precision      : 64% (macro avg)
   • Recall         : 63% (macro avg)
   • F1-Score       : 63% (macro avg)

Confusion Matrix
              Predicted
              Negatif  Netral  Positif
  Actual
  Negatif       80       12       23
  Netral        23       73       22
  Positif       33       24       73


Perbandingan Semua Model
    RANKING MODEL:
────────────────────────────────────────────────────
 1. Naive Bayes          ████████████████░░░░  62.8%
 2. Ensemble Sederhana   ████████████████░░░░  62.8%
 3. Voting Classifier    ███████████████░░░░░  62.5%
 4. Logistic Regression  ███████████████░░░░░  62.3%
 5. Bagging + SVM       ███████████████░░░░░  62.3%
 6. Linear SVM          ██████████████░░░░░░  61.2%
 7. Stacking            ████████████░░░░░░░░  59.5%
 8. Random Forest       ███████████░░░░░░░░░  58.1%
 9. LSTM                ███████████░░░░░░░░░  58.0%
10. Gradient Boosting   ██████████░░░░░░░░░░  54.3%
11. XGBoost             ██████████░░░░░░░░░░  52.3%
12. AdaBoost            ████████░░░░░░░░░░░░  44.9%

Detail Eksperimen

1. Logistic Regression (6 Percobaan)

Percobaan	    Parameter	                    Akurasi
LR_1	      TF-IDF Default + LR Default	    61.43%
LR_2	      TF-IDF Optimal + LR Default	    60.88%
LR_3	      C=0.1	                          61.98%
LR_4	      Grid Search (C=0.1, balanced)	  62.26%
LR_5	      Variasi C (C optimal=0.1)	      61.98%
LR_6	      Variasi Solver (newton-cg)	    61.16%

2. Naive Bayes (3 Percobaan)

Percobaan	     Parameter	            Akurasi
NB_1	     TF-IDF Default	            62.81%
NB_2	     TF-IDF Optimal	            62.81%
NB_3	     Grid Search Alpha (α=1.0)	62.81%

3. Ensemble Methods

Metode	                  Akurasi
Voting Hard (4 model)	    62.26%
Voting Soft (3 model)	    62.53%
Stacking Classifier	      59.50%
Bagging + LR	            61.98%
Bagging + SVM	            62.26%
Ensemble Sederhana NB+LR	62.81%

4. Deep Learning (LSTM)

Model	Akurasi	  Parameter	                                      Catatan
v01	  58.95%	  max_len=100, dropout=0.5	                      Overfitting
v02	  56%	      Preprocessing eksternal	                        Performa turun
v03	  56%	      max_len=50	                                    Tidak membantu
v04	  58%	      Grid search (units=32, dropout=0.4, lr=0.0005)	Val 63.57%

--------------------------------------------------------------------------------
Analisis dan Kesimpulan

1. Mengapa Naive Bayes Menjadi Terbaik?

Cocok untuk data teks - Bekerja baik dengan fitur sparse TF-IDF
Tidak overfitting - Stabil di training (62.8%) dan testing (62.8%)
Cepat dan efisien - Training dalam hitungan detik
Grid search optimal - Alpha=1.0 memberikan hasil terbaik
Asumsi independensi fitur - Cocok untuk teks pendek seperti tweet

2. Mengapa Deep Learning (LSTM) Gagal?

Dataset terlalu kecil - Hanya 1.815 total sampel (minimal 10.000+ untuk LSTM)
Overfitting parah - Train 99% vs Test 58%
Kompleksitas berlebihan - Model tidak sesuai dengan ukuran data
Data tidak cukup bervariasi - Topik terbatas pada politik/ekonomi

3. Mengapa Ensemble Tidak Lebih Baik?

Base models sudah optimal - NB sudah mencapai 62.8%
Dataset kecil - Ensemble butuh data lebih besar untuk sinergi
Voting sederhana - Mencapai 62.8% dengan bobot [0.3:0.7] (sama dengan NB)




Cara Menggunakan Model Terbaik
# ============================================
# LOAD DAN GUNAKAN MODEL TERBAIK
# ============================================

import joblib
import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer

# Load model package
model_package = joblib.load('model_terbaik/final_sentiment_model.pkl')

# Ekstrak komponen
model = model_package['model']
encoder = model_package['encoder']
tfidf = model_package['tfidf']
metadata = model_package['metadata']

print(f"✅ Model: {metadata['model_type']}")
print(f"✅ Akurasi: {metadata['accuracy']:.2%}")
print(f"✅ Kelas: {metadata['classes']}")

# Fungsi prediksi
def predict_sentiment(text):
    # Bersihkan teks (opsional, sesuaikan dengan preprocessing)
    text_clean = text.lower().strip()
    
    # Transform ke TF-IDF
    text_tfidf = tfidf.transform([text_clean])
    
    # Prediksi
    prediction = model.predict(text_tfidf)
    sentiment = encoder.inverse_transform(prediction)[0]
    proba = model.predict_proba(text_tfidf).max()
    
    return sentiment, proba

# Contoh penggunaan
texts = [
    "Produk ini sangat bagus dan berkualitas!",
    "Barangnya jelek, tidak sesuai deskripsi",
    "Pengiriman cepat, tapi kualitas biasa saja"
]

for text in texts:
    sentiment, confidence = predict_sentiment(text)
    print(f"\n📝 Teks: {text}")
    print(f"🎯 Sentimen: {sentiment} (confidence: {confidence:.2%})")





Training Model dari Awal

# ============================================
# TRAINING MODEL TERBAIK (NAIVE BAYES)
# ============================================

import pandas as pd
import joblib
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, classification_report

# 1. Load data
data = pd.read_csv('data/tweet.csv')

# 2. Preprocessing sederhana
def clean_text(text):
    text = text.lower()
    # Tambahkan preprocessing sesuai kebutuhan
    return text

data['clean_tweet'] = data['tweet'].apply(clean_text)

# 3. Split data
X = data['clean_tweet']
y = data['sentimen']
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# 4. TF-IDF Vectorizer
tfidf = TfidfVectorizer(
    max_features=3000,
    ngram_range=(1, 3),
    min_df=2,
    sublinear_tf=True
)

X_train_tfidf = tfidf.fit_transform(X_train)
X_test_tfidf = tfidf.transform(X_test)

# 5. Label Encoding
encoder = LabelEncoder()
y_train_enc = encoder.fit_transform(y_train)
y_test_enc = encoder.transform(y_test)

# 6. Train Naive Bayes
model = MultinomialNB(alpha=1.0)
model.fit(X_train_tfidf, y_train_enc)

# 7. Evaluasi
y_pred = model.predict(X_test_tfidf)
accuracy = accuracy_score(y_test_enc, y_pred)

print(f"\n🎯 Akurasi Model: {accuracy:.2%}")
print("\n📊 Classification Report:")
print(classification_report(y_test_enc, y_pred, target_names=encoder.classes_))

# 8. Simpan model
model_package = {
    'model': model,
    'encoder': encoder,
    'tfidf': tfidf,
    'metadata': {
        'accuracy': accuracy,
        'model_type': 'MultinomialNB',
        'alpha': 1.0,
        'classes': list(encoder.classes_)
    }
}

joblib.dump(model_package, 'model_terbaik/final_sentiment_model.pkl')
print("\n✅ Model berhasil disimpan!")


==Requirements==
numpy==1.24.3
pandas==2.0.3
scikit-learn==1.3.0
matplotlib==3.7.2
seaborn==0.12.2
tensorflow==2.13.0
keras==2.13.1
xgboost==1.7.6
Sastrawi==1.0.1
joblib==1.3.1


Install semua dependencies:
pip install -r requirements.txt




Rekomendasi Pengembangan

Tambah dataset - Target minimal 10.000 sampel untuk deep learning
Coba word embeddings - Word2Vec, FastText, atau BERT Indo
Data augmentation - Back translation, synonym replacement
Hyperparameter tuning - GridSearchCV untuk semua model
Cross-validation - Stratified k-fold (k=5 atau 10)
Handle class imbalance - SMOTE atau class_weight
Coba transformer models - IndoBERT, mBERT, XLMR


Referensi

Scikit-learn Documentation: https://scikit-learn.org/
TensorFlow Documentation: https://www.tensorflow.org/
Sastrawi: https://github.com/sastrawi/sastrawi
Indonesian Twitter Sentiment Dataset: [Sumber dataset]


Lisensi

© 2026 Kelompok NaLapPro. Proyek ini dibuat untuk tujuan pembelajaran.


Kontak

Repository  : https://github.com/otrahigus/Sentiment-analysis
Email       : mdasugiharto@gmail.com
LinkedIn	  : www.linkedin.com/in/mdasugiharto
