# Laporan Proyek Machine Learning - Analisis Prediktif Kehilangan Tutupan Pohon (2001-2020)

## Domain Proyek

Deforestasi dan kehilangan tutupan pohon merupakan masalah lingkungan global yang memiliki dampak signifikan terhadap perubahan iklim, keanekaragaman hayati, dan ekosistem. Menurut laporan Global Forest Watch, dunia kehilangan lebih dari 4,2 juta hektar hutan primer tropis pada tahun 2020 saja \[1]. Kehilangan tutupan pohon secara langsung berkaitan dengan peningkatan emisi karbon, karena hutan berfungsi sebagai penyerap karbon alami terbesar di Bumi.

Analisis pola kehilangan tutupan pohon (tree cover loss) dan hubungannya dengan emisi karbon menjadi sangat penting untuk memahami dampak perubahan lingkungan. Melalui analisis prediktif, kita dapat mengembangkan model untuk memperkirakan emisi CO₂ berdasarkan data kehilangan tutupan pohon, yang dapat membantu pengambilan keputusan kebijakan lingkungan dan strategi mitigasi perubahan iklim.

Proyek ini bertujuan untuk menganalisis data kehilangan tutupan pohon dan emisi CO₂ dari tahun 2001 hingga 2020 di berbagai wilayah global, serta mengembangkan model prediktif untuk memperkirakan emisi karbon berdasarkan data kehilangan tutupan pohon. Pemahaman yang lebih baik tentang hubungan ini dapat mendukung upaya konservasi hutan dan pengurangan emisi karbon global.

## Business Understanding

### Problem Statements

Beberapa permasalahan yang diangkat dalam proyek ini:

1. Bagaimana pola dan tren kehilangan tutupan pohon (tree cover loss) dan emisi CO₂ selama periode 2001-2020?
2. Apakah terdapat korelasi yang signifikan antara kehilangan tutupan pohon dan emisi karbon?
3. Seberapa akurat model machine learning dapat memprediksi emisi CO₂ berdasarkan data kehilangan tutupan pohon?

### Goals

Tujuan dari proyek ini adalah:

1. Mengidentifikasi dan menganalisis pola serta tren kehilangan tutupan pohon dan emisi CO₂ selama periode 20 tahun (2001-2020)
2. Menganalisis korelasi antara kehilangan tutupan pohon dan emisi karbon
3. Mengembangkan model prediktif yang akurat untuk memperkirakan emisi CO₂ berdasarkan data kehilangan tutupan pohon

### Solution Statements

Solusi yang diajukan untuk mencapai tujuan proyek:

1. Melakukan analisis eksplorasi data (EDA) untuk mengidentifikasi pola dan tren kehilangan tutupan pohon dan emisi CO₂
2. Menganalisis korelasi antara variabel-variabel utama menggunakan visualisasi dan analisis statistik
3. Mengembangkan tiga model regresi berbeda (Linear Regression, Random Forest, dan XGBoost) untuk memprediksi emisi CO₂ berdasarkan data kehilangan tutupan pohon
4. Membandingkan performa ketiga model berdasarkan metrik evaluasi MAE, RMSE, dan R² Score untuk memilih model terbaik

## Data Understanding

### **Sumber Data**

Dataset ini diambil dari Kaggle dengan judul *"Tree Cover Loss 2001-2020 by Region"*.
Link sumber data:
[Kaggle - Tree Cover Loss 2001-2020](https://www.kaggle.com/datasets/kkhandekar/tree-cover-loss-20012020?utm_source=chatgpt.com)

Dataset disimpan pada path lokal: `/content/TreeCoverLoss_2001-2020_ByRegion.csv`

### **Jumlah Data**

Dataset terdiri dari **3967 baris** dan **4 kolom**, memberikan data kerusakan tutupan hutan dan emisi CO₂ pada berbagai tahun dan wilayah.

### **Kondisi Data**

* **Missing Value:**
  Tidak terdapat nilai kosong (missing values) pada semua kolom, sehingga data lengkap dan siap digunakan tanpa perlu imputasi.
* **Duplikasi:**
  Tidak ditemukan data duplikat, memastikan setiap baris merepresentasikan data unik.
* **Outlier:**
  Berdasarkan analisis boxplot, terdapat beberapa nilai ekstrem (outlier) terutama pada kolom `TreeCoverLoss_ha` dan `GrossEmissions_Co2_all_gases_Mg`. Nilai ini menggambarkan kejadian kehilangan tutupan hutan dan emisi gas yang sangat tinggi di beberapa tahun/region tertentu, yang merupakan fenomena nyata dan penting untuk dianalisis lebih lanjut.
* **Tipe Data:**

  * `CountryCode` : tipe objek (kategori)
  * `Year` : tipe integer
  * `TreeCoverLoss_ha` : tipe float (numerik kontinu)
  * `GrossEmissions_Co2_all_gases_Mg` : tipe float (numerik kontinu)

### **Uraian Fitur**

| Nama Kolom                        | Deskripsi                                                                                                  |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `CountryCode`                     | Kode negara atau wilayah yang merepresentasikan lokasi data tutupan hutan dan emisi CO₂.                   |
| `Year`                            | Tahun pengukuran data, dari 2001 sampai 2020.                                                              |
| `TreeCoverLoss_ha`                | Luas kehilangan tutupan pohon dalam hektar (ha) untuk tahun dan wilayah tertentu.                          |
| `GrossEmissions_Co2_all_gases_Mg` | Jumlah emisi CO₂ dari semua jenis gas dalam Megagram (Mg) yang dihasilkan akibat kehilangan tutupan hutan. |

---

Dokumentasi ini melengkapi pemahaman dasar dataset yang akan digunakan dalam analisis dan pemodelan. Dengan data yang lengkap dan kondisi yang sudah diketahui,

### Variabel-variabel dalam dataset:

* **TreeCoverLoss\_ha**: Jumlah kehilangan tutupan pohon dalam hektar
* **GrossEmissions\_Co2\_all\_gases\_Mg**: Jumlah emisi CO₂ dalam Megagram
* **CountryCode**: Kode negara atau wilayah
* **Year**: Tahun data (2001-2020)

### Exploratory Data Analysis

Berikut adalah hasil analisis eksplorasi data:

1. **Distribusi Kehilangan Tutupan Pohon per Tahun**

   ![Distribusi Kehilangan Tutupan Pohon per Tahun (2001-2020)](https://github.com/user-attachments/assets/333b7ee6-dfe2-474e-8be4-8e9cd87a51c1)

   Visualisasi ini menunjukkan distribusi kehilangan tutupan pohon di berbagai tahun dalam bentuk boxplot. Terlihat adanya variasi tinggi dalam kehilangan tutupan pohon antar tahun, dengan beberapa tahun menunjukkan nilai outlier yang signifikan.

2. **Distribusi Emisi CO₂ per Tahun**

   ![Distribusi Emisi CO₂ per Tahun (2001-2020)](https://github.com/user-attachments/assets/8ec0f81a-40c6-40cf-acd5-266024af2759)

   Boxplot ini menunjukkan distribusi emisi CO₂ di berbagai tahun. Pola distribusi emisi CO₂ terlihat mirip dengan pola kehilangan tutupan pohon, mengindikasikan adanya korelasi.

3. **Tren Kehilangan Tutupan Pohon (2001-2020)**

   ![Tren Kehilangan Tutupan Pohon per Tahun (2001-2020)](https://github.com/user-attachments/assets/d32ace29-c4a9-49d8-af4a-592b6e23ec70)

   Grafik garis ini menunjukkan tren kehilangan tutupan pohon selama periode 20 tahun. Terlihat adanya fluktuasi dengan tren peningkatan secara umum, terutama setelah tahun 2015.

4. **Tren Emisi CO₂ (2001-2020)**

   ![Tren Emisi CO₂ per Tahun (2001-2020)](https://github.com/user-attachments/assets/8dbc16fc-7d8b-47a2-b196-547c3c721947)

   Grafik ini menunjukkan tren emisi CO₂ selama periode 20 tahun, yang juga menunjukkan pola serupa dengan tren kehilangan tutupan pohon.

5. **Heatmap Korelasi Antara Variabel**

   ![Heatmap Korelasi Antara Variabel](https://github.com/user-attachments/assets/63387d0a-b2aa-44c6-bb2b-5555cc339b5f)

   Heatmap ini menunjukkan korelasi antara variabel-variabel utama. Terdapat korelasi positif yang kuat (0.97) antara kehilangan tutupan pohon (TreeCoverLoss\_ha) dan emisi CO₂ (GrossEmissions\_Co2\_all\_gases\_Mg), mengkonfirmasi hubungan yang erat antara kedua variabel.

6. **Hubungan Kehilangan Tutupan Pohon dan Emisi CO₂**

   ![Hubungan Kehilangan Tutupan Pohon dan Emisi CO₂](https://github.com/user-attachments/assets/f737138b-97de-4a26-b809-66ecdd017653)

   Scatter plot ini menggambarkan hubungan antara kehilangan tutupan pohon dan emisi CO₂, dengan warna menunjukkan tahun. Terlihat adanya hubungan linear yang jelas, yang mendukung penggunaan model regresi.

7. **Visualisasi Hubungan TreeCoverLoss\_ha dan Year dengan Tren Rata-rata**

   ![Visualisasi Hubungan TreeCoverLoss\_ha dan Year](https://github.com/user-attachments/assets/229b02f2-e36c-4e43-9997-8aaff7df710b)

   Grafik ini menunjukkan hubungan antara kehilangan tutupan pohon dan tahun, serta tren rata-rata bergerak (moving average) untuk 3 tahun. Visualisasi ini membantu mengidentifikasi tren jangka panjang dengan mengurangi fluktuasi jangka pendek.

8. **Pairwise Relationships Antar Variabel Numerik**

   ![Visualisasi Pairwise Relationships Antar Variabel Numerik](https://github.com/user-attachments/assets/e4070041-a032-4ae1-a3af-bd1566288ad3)

   Visualisasi ini menunjukkan hubungan pasangan antar variabel numerik berdasarkan periode waktu. Terlihat adanya perbedaan pola antara berbagai periode tahun.

## Data Preparation

Beberapa teknik data preparation yang diterapkan dalam proyek ini:

1. **Penanganan Missing Value**

   * Missing value pada kolom TreeCoverLoss\_ha dan GrossEmissions\_Co2\_all\_gases\_Mg diisi dengan nilai median dari kolom tersebut.

   ```python
   # Memeriksa missing values sebelum penanganan
    print("Missing Values sebelum Penanganan:")
    print(df.isnull().sum())

   # Mengisi missing value dengan median pada kolom tertentu
    df['TreeCoverLoss_ha'] = df['TreeCoverLoss_ha'].fillna(df['TreeCoverLoss_ha'].median())
    df['GrossEmissions_Co2_all_gases_Mg'] = df['GrossEmissions_Co2_all_gases_Mg'].fillna(df['GrossEmissions_Co2_all_gases_Mg'].median())

   # Memeriksa missing values setelah penanganan
    print("\nMissing Values setelah Penanganan:")
    print(df.isnull().sum())

   ```

   Penggunaan median dipilih karena lebih robust terhadap outlier dibandingkan mean, mengingat data memiliki beberapa outlier yang signifikan.

2. **Feature Engineering**

   * Membuat fitur baru `avg_tree_cover_loss_per_year` yang menghitung rata-rata kehilangan tutupan pohon per tahun.

   ```python
   # Membuat fitur baru: rata-rata kehilangan tutupan pohon per tahun
    df['avg_tree_cover_loss_per_year'] = df['TreeCoverLoss_ha'] / (2020 - df['Year'])

   # Cek beberapa baris data
    df[['TreeCoverLoss_ha', 'Year', 'avg_tree_cover_loss_per_year']].head()
   ```

   Fitur ini dapat memberikan informasi tentang laju kehilangan tutupan pohon yang dinormalisasi terhadap waktu.

3. **Encoding Fitur Kategorikal**

   * Mengubah fitur kategorikal CountryCode menjadi bentuk numerik menggunakan Label Encoding.

   ```python
   # Inisialisasi LabelEncoder
    label_encoder = LabelEncoder()

   # Membuat salinan untuk menghindari chained assignment warning
    df['CountryCode_encoded'] = label_encoder.fit_transform(df['CountryCode'])

   # Menampilkan beberapa hasil
    df[['CountryCode', 'CountryCode_encoded']].head()
   ```

   Encoding ini diperlukan agar variabel kategorikal dapat diproses oleh model machine learning.

4. **Feature Scaling**

   * Proses Menginisialisasi StandardScaler untuk menormalkan fitur sehingga memiliki rata-rata 0 dan standar deviasi 1
     Melakukan fit scaler hanya pada data latih (X_train) agar informasi skala berasal dari data pelatihan saja
     Mentransformasikan data latih dan data uji (X_test) menggunakan scaler yang sudah di-fit untuk menjaga konsistensi
     Menampilkan 5 data pertama hasil scaling pada data latih sebagai contoh
     Menampilkan statistik deskriptif hasil scaling untuk memastikan data sudah terstandarisasi.:

   ```python
   # Inisialisasi scaler
    scaler = StandardScaler()

   # Fit scaler hanya pada data train, lalu transform train dan test
    X_train_scaled = scaler.fit_transform(X_train)
    X_test_scaled = scaler.transform(X_test)

   # Verifikasi data hasil scaling
    print("5 Data Pertama setelah Scaling (Train):")
    print(pd.DataFrame(X_train_scaled, columns=features).head())

    print("\nStatistik Deskriptif setelah Scaling (Train):")
    print(pd.DataFrame(X_train_scaled, columns=features).describe().round(2))


   ```

   Data fitur pada data latih telah diskalakan dengan rata-rata mendekati 0 dan standar deviasi 1.
   Distribusi fitur pada data latih terlihat stabil dengan nilai minimum, maksimum, dan kuartil yang sesuai.
   Data siap digunakan untuk proses pelatihan model machine learning.

5. **Pembersihan Data (Handling Infinite dan Missing Values)**

   * Dua fitur utama (TreeCoverLoss_ha dan avg_tree_cover_loss_per_year) diperiksa dan dibersihkan dari nilai tak terhingga dan nilai kosong.
     Nilai inf dan -inf diganti dengan NaN, kemudian semua NaN diimputasi dengan nilai median dari masing-masing kolom.:.

   ```python
   # Tentukan fitur yang akan dipakai
    features = ['TreeCoverLoss_ha', 'avg_tree_cover_loss_per_year']

   # Ambil fitur dari df dan ganti nilai inf dengan NaN
    X = df[features].replace([np.inf, -np.inf], np.nan)

   # Imputasi nilai NaN dengan median tiap kolom
    X = X.fillna(X.median())

   # Target (asumsikan sudah bersih)
    y = df['GrossEmissions_Co2_all_gases_Mg']

   # Cek ulang missing value dan infinite values di X
    print("Missing values setelah pembersihan:")
    print(X.isnull().sum())
    print("\nApakah ada infinite values di X?:")
    print(np.isinf(X).sum())


   ```
   Tidak ada nilai NaN atau inf yang tersisa di kedua kolom.
   Dataset siap untuk dibagi menjadi data latih dan uji pada tahap berikutnya.

6. **Train-Test Split**

   * Dataset yang sudah bersih dari nilai tak terhingga dan missing value dipisahkan menjadi dua bagian:
     Data Latih (Training Set): 80% dari dataset digunakan untuk melatih model
     Data Uji (Testing Set): 20% dari dataset digunakan untuk menguji performa model
     Proses ini dilakukan menggunakan fungsi train_test_split dengan parameter random_state=42 agar hasil pembagian data dapat direproduksi

   ```python
   # Split data bersih menjadi train dan test
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
    )

   # Tampilkan ukuran data hasil split
    print(f"Data Train: {X_train.shape}")
    print(f"Data Test : {X_test.shape}")

   ```

   Data latih berukuran (3173, 2), berisi 3173 sampel dengan 2 fitur
   Data uji berukuran (794, 2), siap digunakan untuk evaluasi model

## Modeling

Dalam proyek ini, tiga model regresi dikembangkan untuk memprediksi emisi CO₂ berdasarkan data kehilangan tutupan pohon:

1. **Linear Regression**

   * Model dasar yang mengasumsikan hubungan linear antara variabel independen dan dependen.
   * Kelebihan: Sederhana, mudah diinterpretasi, cepat dilatih.
   * Kekurangan: Hanya dapat menangkap hubungan linear, kurang fleksibel untuk data kompleks.

   ```python
   # Inisialisasi model Linear Regression
    lr_model = LinearRegression()

   # Latih model dengan data train yang sudah diskalakan
    lr_model.fit(X_train_scaled, y_train)

   # Prediksi data uji
    y_pred_lr = lr_model.predict(X_test_scaled)
   ```

2. **Random Forest Regressor**

   * Model ensemble yang menggunakan multiple decision trees untuk menangkap pola non-linear dalam data.
   * Kelebihan: Dapat menangkap hubungan non-linear, robust terhadap outlier, tidak memerlukan scaling.
   * Kekurangan: Komputasi lebih berat, model "black box" yang sulit diinterpretasi.

   ```python
   # Inisialisasi model Random Forest dengan 100 estimator
    rf_model = RandomForestRegressor(n_estimators=100, random_state=42)

   # Latih model dengan data train yang sudah diskalakan
    rf_model.fit(X_train_scaled, y_train)

   # Prediksi data uji
    y_pred_rf = rf_model.predict(X_test_scaled)
   ```

3. **XGBoost Regressor**

   * Model gradient boosting yang secara iteratif memperbaiki kesalahan prediksi sebelumnya.
   * Kelebihan: Performa tinggi, efisien secara komputasi, dapat menangani missing value.
   * Kekurangan: Rawan overfitting, memerlukan fine-tuning parameter, model "black box".

   ```python
   # Inisialisasi model XGBoost
    xgb_model = XGBRegressor(objective='reg:squarederror', n_estimators=100, random_state=42)

   # Latih model dengan data train yang sudah diskalakan
    xgb_model.fit(X_train_scaled, y_train)

   # Prediksi data uji
    y_pred_xgb = xgb_model.predict(X_test_scaled)
   ```

Fitur yang digunakan dalam pemodelan:

* `TreeCoverLoss_ha` (Kehilangan tutupan pohon dalam hektar)
* `avg_tree_cover_loss_per_year` (Rata-rata kehilangan tutupan pohon per tahun)

Target prediksi:

* `GrossEmissions_Co2_all_gases_Mg` (Emisi CO₂ dalam Megagram)

## Evaluation

Untuk mengevaluasi kinerja model, tiga metrik evaluasi digunakan:

1. **Mean Absolute Error (MAE)**

   * Mengukur rata-rata kesalahan absolut antara nilai prediksi dan nilai aktual.
   * Formula: MAE = (1/n) \* Σ|y\_i - ŷ\_i|
   * Interpretasi: Semakin rendah nilai MAE, semakin baik kinerja model.

2. **Root Mean Squared Error (RMSE)**

   * Mengukur akar kuadrat dari rata-rata kesalahan kuadrat antara nilai prediksi dan nilai aktual.
   * Formula: RMSE = √\[(1/n) \* Σ(y\_i - ŷ\_i)²]
   * Interpretasi: RMSE memberikan penalti lebih besar untuk kesalahan besar, sehingga lebih sensitif terhadap outlier.

3. **R² Score (Coefficient of Determination)**

   * Mengukur proporsi variasi dalam variabel dependen yang dapat dijelaskan oleh variabel independen.
   * Formula: R² = 1 - (Σ(y\_i - ŷ\_i)² / Σ(y\_i - ȳ)²)
   * Interpretasi: Nilai berkisar dari 0 hingga 1, dengan nilai yang lebih tinggi menunjukkan model yang lebih baik.

### Hasil Evaluasi Model

Berikut hasil evaluasi ketiga model (nilai terbaru):

| Model             | MAE           | RMSE          | R² Score   |
| ----------------- | ------------- | ------------- | ---------- |
| Linear Regression | 20,048,150.37 | 85,785,222.41 | 0.7428     |
| Random Forest     | 16,088,917.41 | 81,385,115.62 | **0.7685** |
| XGBoost           | 17,472,013.16 | 93,270,812.19 | 0.6959     |


Visualisasi perbandingan metrik antar model:

* ![Perbandingan R² Score Antar Model](https://github.com/user-attachments/assets/bd9dda45-c423-4c46-92d3-158de103a45f)
  Grafik menampilkan perbandingan performa model berdasarkan kemampuan menjelaskan variansi data target. Terlihat bahwa Random Forest memiliki nilai R² tertinggi, diikuti Linear 
  Regression, dan terakhir XGBoost.
* ![Perbandingan MAE Antar Model](https://github.com/user-attachments/assets/a9c87736-8df9-4101-b85a-84c3f8d19287)
  Grafik memperlihatkan perbandingan error absolut rata-rata antar model, dimana Random Forest memiliki MAE terendah, menunjukkan performa terbaik dalam hal akurasi prediksi. Linear 
  Regression dan XGBoost memiliki MAE lebih tinggi, dengan XGBoost sedikit lebih baik dibanding Linear Regression pada grafik ini.
* ![Perbandingan RMSE Antar Model](https://github.com/user-attachments/assets/4005154d-55bb-45d2-8ee3-a11c7864e724)
  Grafik memperlihatkan perbandingan error kuadrat rata-rata antar model, di mana Random Forest menunjukkan RMSE terendah, menandakan model ini memiliki prediksi yang lebih konsisten 
  dan akurat. Model Linear Regression dan XGBoost memiliki RMSE lebih tinggi, dengan XGBoost menunjukkan error terbesar di antara ketiganya.

### Analisis Hasil

Berdasarkan hasil evaluasi terbaru, Random Forest Regressor menunjukkan performa terbaik dengan nilai MAE terendah (16,088,917.4141), RMSE terendah (81,385,115.6208), dan R² Score tertinggi (0.7685). Model ini mampu menjelaskan sekitar 76.85% variasi dalam data emisi CO₂, yang menunjukkan kemampuan baik dalam memahami hubungan antara kehilangan tutupan pohon dan emisi karbon.

Linear Regression menunjukkan performa yang cukup baik dengan R² Score 0.7428, sedangkan XGBoost, meskipun populer, menunjukkan performa yang sedikit lebih rendah pada dataset ini dengan R² Score 0.6959.

Pemilihan model terbaik disesuaikan dengan kebutuhan dan kompleksitas data; dalam kasus ini Random Forest memberikan keseimbangan terbaik antara akurasi dan kestabilan.

## Kesimpulan

Berdasarkan analisis yang dilakukan, beberapa kesimpulan dapat ditarik:

1. Terdapat korelasi positif yang sangat kuat (0.97) antara kehilangan tutupan pohon dan emisi CO₂, mengkonfirmasi bahwa deforestasi merupakan kontributor signifikan terhadap emisi karbon.

2. Tren kehilangan tutupan pohon dan emisi CO₂ menunjukkan fluktuasi selama periode 2001-2020, dengan kecenderungan peningkatan yang mengkhawatirkan terutama setelah tahun 2015.

3. Model Random Forest Regressor memberikan prediksi terbaik dengan tingkat akurasi yang memadai (R² = 0.7685) berdasarkan data kehilangan tutupan pohon, menunjukkan bahwa kehilangan tutupan pohon dapat menjadi prediktor yang efektif untuk memperkirakan emisi karbon.

4. Hasil model dapat digunakan untuk membantu pembuat kebijakan dalam merancang strategi mitigasi perubahan iklim yang efektif dengan fokus pada perlindungan dan pemulihan hutan.

## Referensi

\[1] Global Forest Watch. (2021). "Global Primary Forest Loss". World Resources Institute. [https://www.globalforestwatch.org/](https://www.globalforestwatch.org/)
