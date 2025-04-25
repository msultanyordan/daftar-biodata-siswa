# Laporan Proyek Machine Learning - A251YBM353_M.SULTAN YORDANIA

## Domain Proyek (Keuangan)

Solana (SOL) adalah salah satu cryptocurrency yang populer karena kecepatan dan skalabilitasnya dalam ekosistem blockchain. Mengingat volatilitas harga yang tinggi, prediksi harga Solana menjadi penting bagi investor dan trader untuk membuat keputusan yang lebih informasional. Dalam proyek ini, kami menggunakan model Gated Recurrent Unit (GRU) untuk memprediksi harga Solana berdasarkan data historisnya. Model GRU dipilih karena kemampuannya dalam menangani data time-series secara efisien, memungkinkan peramalan harga yang lebih akurat untuk membantu strategi investasi dan trading di pasar kripto.


## Business Understanding

## **Problem Statements**

1. **Volatilitas Harga Solana**  
   Harga Solana (SOL) sangat fluktuatif, yang membuat investor kesulitan merencanakan strategi investasi yang tepat.

2. **Prediksi Harga yang Kurang Akurat**  
   Metode prediksi tradisional sering kali tidak efektif dalam menangani fluktuasi harga kripto yang tajam dan tidak stabil.

---

## **Goals**

1. **Meningkatkan Akurasi Prediksi**  
   Menggunakan model GRU untuk memberikan prediksi harga Solana yang lebih akurat dan dapat diandalkan.

2. **Membantu Pengambilan Keputusan Investasi**  
   Memberikan wawasan yang lebih baik bagi investor dalam merencanakan strategi investasi dan mengurangi risiko.


## Data Understanding

Dalam proyek ini, data yang digunakan untuk memprediksi harga **Solana (SOL)** diambil dari **Yahoo Finance**. Data ini mencakup informasi historis harga Solana mulai dari Januari 2020 hingga April 2025. Anda dapat mengunduh dataset harga Solana dengan menggunakan pustaka **yfinance** atau mengaksesnya langsung dari situs Yahoo Finance.

### **Variabel-variabel pada Solana (SOL) dataset adalah sebagai berikut:**

- **Date**: Merupakan tanggal data harga tercatat.
- **Close**: Harga penutupan Solana pada hari tersebut. Ini adalah harga utama yang digunakan dalam analisis prediksi harga.

Fitur yang digunakan dalam proyek ini adalah **Date** untuk melihat harga Solana pada setiap tanggal, dan **Close** yang dipilih sebagai fitur utama untuk memprediksi harga Solana di masa depan.


## Data Preparation
Pada tahap ini, saya melakukan normalisasi minmax pada seluruh dan kemudian melakukan windowing data untuk mendapat variabel x dan y dengan ukuran window atau sequnce length nya 30. Selanjutnya data saya split untuk train 80% dan test 20%.

## Modeling
Pada tahap pemodelan ini, digunakan model GRU (Gated Recurrent Unit) untuk memprediksi harga Solana di masa depan berdasarkan data historis harga penutupan (**Close**). Model ini dipilih karena kemampuannya dalam menangani data time-series dengan efisien dan memberikan hasil yang lebih baik dibandingkan model RNN tradisional.

Berikut adalah tahapan dan parameter yang digunakan dalam pembuatan model:

1. **Input Layer**:
   - **`model.add(Input(shape=(x_train.shape[1], 1)))`**: Menambahkan layer input yang menerima data dengan bentuk `(sequence_length, 1)` yang sesuai dengan data yang sudah disiapkan dalam bentuk sequence.
   
2. **First GRU Layer**:
   - **`model.add(GRU(units=50, return_sequences=True))`**: Menambahkan layer GRU pertama dengan 50 unit dan parameter `return_sequences=True` yang mengembalikan output untuk setiap langkah waktu (sequence), yang diperlukan untuk layer GRU berikutnya.

3. **Dropout Layer**:
   - **`model.add(Dropout(0.2))`**: Dropout dengan tingkat dropout 20% digunakan untuk mengurangi overfitting selama pelatihan model. Dropout menghilangkan secara acak unit di dalam layer selama pelatihan.

4. **Second GRU Layer**:
   - **`model.add(GRU(units=50, return_sequences=False))`**: Menambahkan layer GRU kedua dengan 50 unit dan `return_sequences=False` karena ini adalah layer terakhir yang menghasilkan satu nilai output untuk prediksi harga di masa depan.

5. **Second Dropout Layer**:
   - **`model.add(Dropout(0.2))`**: Dropout dengan tingkat 20% untuk layer ini juga untuk mengurangi risiko overfitting.

6. **Dense Layer**:
   - **`model.add(Dense(units=25))`**: Layer Dense dengan 25 unit untuk menghubungkan output dari layer GRU sebelumnya dengan layer output.
   
7. **Output Layer**:
   - **`model.add(Dense(units=1))`**: Layer output yang menghasilkan satu nilai output, yaitu harga Solana yang diprediksi pada waktu tertentu.

8. **Compile Model**:
   - **`model.compile(optimizer='adam', loss='mean_squared_error')`**: Model dikompilasi dengan optimizer **Adam** yang populer karena efisiensinya dalam menangani masalah optimasi. Untuk fungsi loss, digunakan **mean squared error (MSE)** karena ini adalah tugas regresi yang memprediksi nilai kontinu.

## Evaluation
Untuk mengevaluasi model, kami menggunakan **Mean Squared Error (MSE)** karena tugas ini adalah regresi untuk memprediksi harga. MSE mengukur rata-rata kesalahan kuadrat antara nilai yang diprediksi dan nilai yang sebenarnya. Semakin rendah nilai MSE, semakin akurat model.

Hasil MSE pada model ini adalah **83.60**, yang menunjukkan bahwa model memiliki kesalahan rata-rata sebesar 83.60 dalam memprediksi harga Solana. Mengingat fluktuasi harga Solana yang tinggi, nilai MSE ini bisa dianggap cukup baik dan pada visualisasi pun dapat dilihat bahwa harga prediksi dan aktual tidak terlalu jomplang, walaupun masih ada ruang untuk perbaikan agar meningkatkan akurasi nilai prediski.





