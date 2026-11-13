# 📊 Analisis Sentimen Ulasan Pengguna Aplikasi Shopee pada Google Play Store dengan Pendekatan Leksikon & Machine Learning

## 📌 Deskripsi Proyek

Proyek penelitian ini bertujuan untuk menganalisis persepsi konsumen terhadap aplikasi Shopee Indonesia berdasarkan **242.682 ulasan pengguna** yang dikumpulkan dari Google Play Store (`com.shopee.id`).

Penelitian menggunakan pendekatan hibrid yang menggabungkan metode *Lexicon-Based Sentiment Analysis* dengan algoritma *Machine Learning*. Pelabelan sentimen dilakukan secara otomatis menggunakan kamus leksikon **InSet (Indonesian Sentiment Lexicon)**, kemudian dilanjutkan dengan pemodelan klasifikasi menggunakan tiga algoritma, yaitu Decision Tree, Random Forest, dan Support Vector Machine (SVM Linear).

Analisis dilakukan untuk mengidentifikasi distribusi sentimen positif dan negatif, menemukan pola kata dominan yang merepresentasikan pengalaman pengguna, serta membandingkan performa dan stabilitas model klasifikasi berdasarkan dua skenario pembagian data (*train-test split*), yaitu 70:30 dan 80:20.

## 🎯 Latar Belakang

Sebagai salah satu platform e-commerce dengan jumlah pengguna yang besar di Indonesia, Shopee menghasilkan volume ulasan pengguna yang dapat merepresentasikan berbagai pengalaman konsumen, mulai dari kepuasan terhadap kemudahan transaksi hingga keluhan mengenai permasalahan teknis dan layanan aplikasi.

Dalam perspektif sosiofisika dan ekonofisika berbasis data, kumpulan ulasan tersebut dapat dipandang sebagai representasi interaksi banyak agen (*multi-agent system*) yang membentuk distribusi opini publik.

Melalui pendekatan analisis sentimen, kumpulan data tersebut dapat diolah untuk memperoleh gambaran kuantitatif mengenai persepsi konsumen sekaligus mengidentifikasi aspek layanan yang perlu dipertahankan maupun ditingkatkan.

## ❓ Rumusan Masalah

1. Bagaimana distribusi sentimen positif dan negatif pada ulasan pengguna aplikasi Shopee di Google Play Store?
2. Kata-kata atau topik apa saja yang paling dominan muncul pada ulasan positif dan negatif, serta bagaimana keterkaitannya dengan pengalaman pengguna?
3. Bagaimana perbandingan akurasi dan stabilitas algoritma Decision Tree, Random Forest, dan SVM Linear pada skenario pembagian data 70:30 dan 80:20?

## 🎯 Tujuan Penelitian

1. Mengidentifikasi distribusi sentimen pengguna Shopee menggunakan metode pelabelan otomatis berbasis leksikon InSet.
2. Mengeksplorasi dan memvisualisasikan kata-kata dominan yang merepresentasikan kepuasan dan keluhan pengguna.
3. Membandingkan performa algoritma Decision Tree, Random Forest, dan SVM Linear berdasarkan akurasi data latih dan data uji.
4. Menentukan algoritma dengan performa klasifikasi paling akurat dan stabil berdasarkan hasil evaluasi model.

---

# 📂 Data Understanding

## 1. Sumber Data

Data penelitian diperoleh dari halaman ulasan aplikasi Shopee Indonesia pada Google Play Store.

| Keterangan | Deskripsi |
|---|---|
| Platform | Google Play Store |
| Aplikasi | Shopee Indonesia |
| Package ID | `com.shopee.id` |
| Data mentah | 243.000 ulasan |
| Data setelah preprocessing awal | 242.682 ulasan |
| Bahasa | Indonesia |
| Atribut utama | `content` dan `score` |

### Data Cleaning

Dari 243.000 ulasan yang dikumpulkan, dilakukan beberapa tahapan pembersihan data untuk memperoleh dataset yang siap dianalisis:

- Menghapus sembilan kolom metadata yang tidak relevan, seperti `reviewId`, `userName`, `userImage`, dan `thumbsUpCount`.
- Menghapus 318 baris yang mengandung nilai kosong (*missing values*).
- Melakukan deduplikasi data ulasan.
- Mempertahankan dua atribut utama untuk analisis, yaitu:
  - `content`: Teks ulasan yang ditulis oleh pengguna.
  - `score`: Rating aplikasi yang diberikan pengguna dengan skala 1–5.

Hasil akhir menghasilkan **242.682 ulasan** yang digunakan sebagai dataset penelitian.

## 2. Metodologi Penelitian

Penelitian ini menggunakan pendekatan hibrid melalui lima tahapan utama:

### 1. Data Scraping

Pengumpulan sebanyak 243.000 ulasan aplikasi Shopee Indonesia dari Google Play Store menggunakan pustaka `google-play-scraper`.

### 2. Text Preprocessing

Melakukan pembersihan dan normalisasi teks ulasan untuk memperoleh representasi teks yang lebih terstruktur. Tahapan ini meliputi:

- Case Folding
- Text Cleaning
- Tokenization
- Stopword Removal
- Stemming Bahasa Indonesia

Hasil preprocessing digunakan sebagai atribut teks akhir (`text_akhir`).

### 3. Pelabelan Sentimen (Lexicon-Based)

Pelabelan otomatis dilakukan menggunakan kamus leksikon positif dan negatif bahasa Indonesia, yaitu **InSet (Koto & Rahmaningtyas, 2017)**.

Setiap kata dalam ulasan dicocokkan dengan kamus leksikon, kemudian bobot sentimennya dijumlahkan untuk memperoleh skor sentimen keseluruhan.

Penelitian menggunakan klasifikasi biner tanpa kelas netral dengan aturan:

- Skor sentimen ≥ 0: Positif.
- Skor sentimen < 0: Negatif.

Dengan demikian, ulasan dengan skor sentimen 0 dimasukkan ke dalam kategori positif.

### 4. Ekstraksi Fitur dan Pembagian Data

Teks ulasan yang telah diproses dikonversi menjadi representasi numerik menggunakan metode *Term Frequency-Inverse Document Frequency* (TF-IDF).

Selanjutnya, dataset dibagi menjadi dua skenario:

- 70% data latih dan 30% data uji.
- 80% data latih dan 20% data uji.

### 5. Pemodelan dan Evaluasi

Pelatihan dan pengujian dilakukan menggunakan tiga algoritma Machine Learning:

- Decision Tree
- Random Forest
- Support Vector Machine (SVM Linear)

Evaluasi dilakukan dengan membandingkan akurasi data latih dan data uji untuk mengidentifikasi model dengan performa terbaik serta menganalisis indikasi *overfitting*.

Selain itu, visualisasi WordCloud dan frekuensi kata digunakan untuk mengeksplorasi pola kata dominan pada masing-masing kelompok sentimen.

---

# 📈 Results & Discussion

## 1. Distribusi Sentimen

Berdasarkan hasil pelabelan otomatis menggunakan leksikon InSet, diperoleh distribusi sentimen sebagai berikut:

| Kategori Sentimen | Persentase |
|---|---:|
| Positif | 59,7% |
| Negatif | 40,3% |

### Visualisasi Distribusi Sentimen

<img width="628" height="581" alt="image" src="https://github.com/user-attachments/assets/16b8692d-bb4c-4d46-96c7-568dc7f2ef1b" />

*Gambar 1. Distribusi persentase sentimen positif dan negatif pada ulasan pengguna Shopee.*

Hasil tersebut menunjukkan bahwa mayoritas ulasan pengguna Shopee memiliki kecenderungan sentimen positif sebesar 59,7%. Meskipun demikian, proporsi sentimen negatif sebesar 40,3% menunjukkan masih terdapat sejumlah aspek pengalaman pengguna yang perlu diperhatikan.

## 2. Analisis Kata Dominan (WordCloud)

Visualisasi WordCloud digunakan untuk mengidentifikasi kata-kata yang paling sering muncul dalam masing-masing kelompok sentimen. Ukuran kata merepresentasikan frekuensi kemunculannya dalam kumpulan ulasan.

### A. Sentimen Positif

<img width="1384" height="784" alt="image" src="https://github.com/user-attachments/assets/a8b86e34-2390-4054-88d5-fad87480aa0e" />

*Gambar 2. WordCloud ulasan pengguna dengan sentimen positif.*

Berdasarkan hasil visualisasi WordCloud dan analisis frekuensi kata, terdapat tiga kelompok apresiasi utama:

1. **Kemudahan Transaksi:** Kata seperti `cepat`, `mudah`, `lancar`, dan `aman` menunjukkan apresiasi terhadap kemudahan penggunaan dan proses transaksi.
2. **Layanan dan Harga:** Kata seperti `pelayanan`, `ongkirnya`, dan `biaya` merepresentasikan aspek layanan serta biaya transaksi.
3. **Respons Afektif:** Kata seperti `suka`, `puas`, `nyaman`, dan `semoga` menggambarkan respons emosional positif pengguna.

### B. Sentimen Negatif

<img width="1384" height="784" alt="image" src="https://github.com/user-attachments/assets/2f848b91-d630-49d3-bac7-c94cf1eb5353" />

*Gambar 3. WordCloud ulasan pengguna dengan sentimen negatif.*

Berdasarkan hasil visualisasi, terdapat tiga kelompok keluhan utama:

1. **Stabilitas Teknis:** Kata seperti `kesalahan`, `sistem`, `gagal`, dan `muncul` mengindikasikan permasalahan teknis pada aplikasi.
2. **Antarmuka dan Promosi:** Kata seperti `ribet`, `iklan`, `obrolan`, dan `susah` menunjukkan ketidaknyamanan dalam pengalaman penggunaan aplikasi.
3. **Uang dan Biaya Layanan:** Kata seperti `pay`, `uang`, `biaya`, dan `ongkirnya` menunjukkan adanya keluhan terkait aspek pembayaran dan biaya layanan.

## 3. Perbandingan Performa Model Klasifikasi

Evaluasi model dilakukan menggunakan tiga algoritma Machine Learning dengan dua skenario pembagian dataset, yaitu 70:30 dan 80:20.

### A. Hasil Evaluasi Akurasi

| Algoritma | Split | Akurasi Train | Akurasi Test |
|---|---|---:|---:|
| Decision Tree | 70:30 | 92,29% | 77,59% |
| Decision Tree | 80:20 | 92,19% | 77,65% |
| Random Forest | 70:30 | 92,29% | 80,93% |
| Random Forest | 80:20 | 92,19% | 81,02% |
| SVM Linear | 70:30 | 82,66% | 82,61% |
| SVM Linear | 80:20 | 82,65% | 82,54% |

### B. Visualisasi Perbandingan Akurasi

<img width="566" height="367" alt="image" src="https://github.com/user-attachments/assets/74b329d8-fbeb-4fe2-9531-2da1bd7a87db" />

*Gambar 4. Perbandingan akurasi data latih dan data uji pada Decision Tree, Random Forest, dan SVM Linear.*

### C. Analisis Performa Model

**1. Decision Tree**

- Memiliki akurasi data latih sebesar 92,29% pada split 70:30.
- Akurasi data uji hanya mencapai 77,59%.
- Terdapat selisih akurasi sebesar 14,70 poin persentase.
- Pola serupa juga terlihat pada skenario split 80:20 dengan selisih 14,54 poin persentase.

Hasil tersebut mengindikasikan adanya *overfitting*, yaitu kondisi ketika model memiliki performa tinggi pada data latih, tetapi kemampuan generalisasinya terhadap data baru lebih rendah.

**2. Random Forest**

- Menghasilkan akurasi pengujian sebesar 80,93% pada split 70:30 dan 81,02% pada split 80:20.
- Memiliki performa lebih stabil dibandingkan Decision Tree.
- Pendekatan *ensemble learning* membantu mengurangi varians model, meskipun masih terdapat selisih antara akurasi data latih dan data uji.

**3. Support Vector Machine (SVM Linear)**

- Menghasilkan akurasi pengujian sebesar 82,61% pada split 70:30.
- Menghasilkan akurasi pengujian sebesar 82,54% pada split 80:20.
- Memiliki selisih akurasi train-test yang sangat kecil, yaitu 0,05 dan 0,11 poin persentase.
- Menunjukkan stabilitas performa terbaik di antara ketiga algoritma yang diuji.

Berdasarkan hasil tersebut, **SVM Linear merupakan algoritma dengan performa paling stabil dan akurasi pengujian tertinggi** pada kedua skenario pembagian data.

### D. Evaluasi Model Terbaik: SVM Linear

<img width="610" height="349" alt="image" src="https://github.com/user-attachments/assets/8461ad65-7d6a-41fc-881a-9fa5c7044236" />

*Gambar 5. Confusion Matrix model SVM Linear pada data pengujian.*

Confusion Matrix digunakan untuk mengevaluasi hasil klasifikasi secara lebih mendalam dengan mengidentifikasi jumlah prediksi yang benar maupun salah pada masing-masing kategori sentimen.

Evaluasi ini mencakup:

- True Positive (TP): Ulasan positif yang berhasil diklasifikasikan sebagai positif.
- True Negative (TN): Ulasan negatif yang berhasil diklasifikasikan sebagai negatif.
- False Positive (FP): Ulasan negatif yang salah diklasifikasikan sebagai positif.
- False Negative (FN): Ulasan positif yang salah diklasifikasikan sebagai negatif.

*Catatan: Confusion Matrix ditampilkan sebagai evaluasi tambahan. Nilai-nilai di dalamnya mengikuti hasil pengujian model pada notebook penelitian.*

---

# 💡 Key Insights

Berdasarkan keseluruhan hasil analisis, diperoleh beberapa temuan utama:

**1. Dominasi Sentimen Positif**

Sebanyak 59,7% ulasan menunjukkan sentimen positif, sedangkan 40,3% lainnya menunjukkan sentimen negatif. Hal ini menggambarkan bahwa pengalaman pengguna Shopee cenderung positif, meskipun masih terdapat proporsi keluhan yang cukup besar.

**2. Aspek yang Diapresiasi Pengguna**

Kemudahan transaksi, kecepatan proses, kenyamanan, serta layanan menjadi beberapa aspek yang paling sering direpresentasikan dalam ulasan positif.

**3. Aspek yang Perlu Ditingkatkan**

Keluhan pengguna banyak berkaitan dengan stabilitas sistem, antarmuka aplikasi, intensitas iklan, serta biaya layanan dan pengiriman.

**4. Performa Algoritma**

SVM Linear menunjukkan generalisasi yang lebih baik berdasarkan kedekatan akurasi data latih dan data uji. Sebaliknya, Decision Tree menunjukkan indikasi *overfitting* yang lebih signifikan.

**5. Pengaruh Pembagian Data**

Perubahan rasio pembagian data dari 70:30 menjadi 80:20 tidak menghasilkan perubahan performa yang signifikan pada SVM Linear. Hal ini menunjukkan konsistensi performa model pada kedua skenario pengujian.

---

# 🛠️ Tools & Technologies

| Kategori | Tools / Libraries |
|---|---|
| Programming Language | Python |
| Data Scraping | google-play-scraper |
| Data Manipulation | Pandas, NumPy |
| Text Processing | NLTK, Sastrawi |
| Sentiment Analysis | InSet Lexicon |
| Feature Extraction | TF-IDF |
| Machine Learning | Scikit-learn |
| Classification Algorithms | Decision Tree, Random Forest, Linear SVM |
| Data Visualization | Matplotlib, Seaborn, WordCloud |
| Development Environment | Google Colaboratory |

---

# 📚 References

Koto, F., & Rahmaningtyas, G. (2017). InSet lexicon: Evaluation of a word list for Indonesian sentiment analysis in microblogs. *Proceedings of the 2017 International Conference on Asian Language Processing (IALP)*.

---

# 📝 Kesimpulan

Penelitian terhadap 242.682 ulasan pengguna aplikasi Shopee di Google Play Store menunjukkan bahwa sentimen positif mendominasi dengan persentase 59,7%, sedangkan sentimen negatif mencapai 40,3%.

Berdasarkan hasil perbandingan tiga algoritma Machine Learning, SVM Linear menghasilkan performa klasifikasi paling stabil dengan akurasi pengujian sebesar 82,61% pada split 70:30 dan 82,54% pada split 80:20. Kedekatan antara akurasi data latih dan data uji menunjukkan kemampuan generalisasi yang lebih baik dibandingkan Decision Tree dan Random Forest dalam skenario penelitian ini.

Secara keseluruhan, penelitian ini menunjukkan bagaimana kombinasi pendekatan leksikon, pengolahan teks, dan Machine Learning dapat digunakan untuk mengekstraksi informasi dari data ulasan berskala besar serta menghasilkan wawasan kuantitatif mengenai persepsi dan pengalaman pengguna aplikasi.

---

# 📁 Repository Structure

```text
shopee-sentiment-analysis/
│
├── README.md
│
├── notebooks/
│   └── shopee_sentiment_analysis.ipynb
│
├── data/
│   └── README.md
│
├── images/
│   ├── sentiment_distribution.png
│   ├── wordcloud_positive.png
│   ├── wordcloud_negative.png
│   ├── model_comparison.png
│   └── confusion_matrix_svm.png
│
└── requirements.txt
```

---

# 🔑 Keywords

`Sentiment Analysis` · `Natural Language Processing` · `Machine Learning` · `Lexicon-Based Sentiment Analysis` · `InSet Lexicon` · `TF-IDF` · `Decision Tree` · `Random Forest` · `Linear SVM` · `Shopee` · `Python` · `Data Analytics`
