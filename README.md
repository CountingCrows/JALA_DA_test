# JALA_Data Analyst Test_Lanang Bagaskara

## Soal Assignment Test
Tujuan assignment test ini adalah untuk mengolah dan menganalisis data kualitas air dan budidaya udang dari beberapa kolam budidaya di daerah yang berbeda. Data budidaya udang ini disediakan oleh JALA dan berasal dari data siklus budidaya yang berlangsung pada waktu yang berbeda dan lama budidaya yang juga berbeda.

Dari data yang ada, kita akan menganalisis;
1. Apakah ada perbedaan performa budidaya (**SR, ADG, FCR**) yang signifikan antar:
   - Kolam
   - Tambak
   - Waktu budidaya
2. Apa yang menyebabkan perbedaan tersebut?
3. Apa faktor dan kondisi yang mendukung hasil budidaya optimal? Anda dapat membandingkan kondisi kualitas air di masing-masing siklus budidaya dan lakukan analisis kondisi kualitas air seperti apa yang dapat mendorong hasil budidaya yang baik.

## Dataset
Terdapat 8 dataset yang disediakan untuk dilakukan analisis, diantaranya:
- farms = berisi tentang data lokasi provinsi dan regency tambak udang berada.
- cycles = memiliki informasi mengenai siklus panen tiap kolam.
- ponds = memiliki informasi tentang ukuran dan kedalaman kolam.
- feeds = berisi tentang data jumlah pangan yang diberikan masing-masing kolam berdasarkan tanggal tertentu.
- harvests = berisi tentang data panen tiap kolam pada tanggal tertentu dengan keterangan status panen.
- fasting = berisi tentang data puasa siklus budidaya udang pada tanggal tertentu. 
- samplings = memiliki data berat udang pada tanggal tertentu pada tiap siklus untuk masing-masing kolam.
- measurements = berisi data untuk menunjukkan faktor apa saja yang mempengaruhi kualitas air.

## Exploratory Data Analysis

### NaN Values
Sebelum menjawab pertanyaan yang ada di atas, kita akan mencari apakah data-data yang disediakan memiliki NaN values, terutama untuk data _farms, cycles, ponds, feeds, harvests, fasting, dan sampling_. 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/2af25554-5b33-4c9a-88cf-5e98a9e476da)

- farms

  ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/2078f825-ed94-44dc-b007-774cd9f32904)

- cycles
  
  ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/99c8273d-8615-4c65-9166-7886395177f3)

- ponds

   ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/85726983-c8a8-4531-9cd2-23a5df84d92e)

- harvests

  ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/ac9528ff-9583-44a0-a687-960301becded)


- fasting

   ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/e3e136ab-7643-431c-8fd0-1b0099677661)

- feeds

   ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/b695cbe2-3c6e-4994-9fba-d3aa65a37099)

- samplings

   ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/8b88e91c-2f19-43a6-9a32-281b33d73eab)

Adanya beberapa kolom yang mengandung NaN value di masing-masing dataset, maka kita akan menangani nilai yang hilang dengan fungsi drop sehingga data bisa segera diolah untuk analisis.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/95362e93-709d-487e-9907-19d2ddcb547d)

Kami ingin mendapatkan wawasan dari kumpulan data dengan mengetahui Tingkat Kelangsungan Hidup (SR), Pertambahan Rata-Rata Harian (ADG), dan Tingkat Konversi Makanan (FCR) untuk membedakan apakah ada perbedaan kinerja budidaya berdasarkan siklus, kolam, dan tambak.

### cycles dataset

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/2c07d8cf-7a1a-4d50-8473-40d1df156731)

Kita ingin mengetahui berapa hari dalam satu siklus penuh untuk tiap _id_, maka kita harus menghitungnya terlebih dahulu.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/0b54b7d5-269a-4e8d-b6c9-b364fb0346e8)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/6dda215e-832d-46bb-895f-7d0ed55b8068)

Setelah mengubah _data type_ kolom _started_at & finished_at_ ke _datetime_, kita bisa mengurangi kolom _finished_at dan started_at_ untuk mendapatkan jumlah hari dalam masing-masing id.

### harvests dataset
Data harvests adalah salah satu data yang memiliki banyak missing values, oleh karena itu kita ingin juga mencari _outliers_ dalam dataset tersebut dan kemudian menangani _outliers_ dengan fungsi drop. Adapun penjelasan mengenai data ini bahwa bila **size** dalam satu _cycle_id_ adalah 100, maka dalam tiap 1 kg terdapat 100 ekor udang. 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/cba39074-64b1-430c-8fd2-bd6ac1d6f2b6)

_Scatter Plot_ tersebut menunjukkan bahwa outliers dalam _size_ diatas nilai 400 dan _weight_ diatas nilai 80.000. Oleh karena itu kita ingin _drop_ outliers yang ada di kolom-kolom tersebut. Menggunakan z-score dan nilai absolut 3 untuk menentukan outlier dari tiap kolom kemudian menggunakan fungsi drop.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/b01a6499-034e-4753-ae84-350f209abdca)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/cff123d1-cee2-4654-85e6-6e591ba391b3)

Setelah menghapuskan data outlier dari kolom-kolom tersebut, kita mendapatkan data yang lebih terdistribusi.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/9b55823a-ebc7-4b3b-8f7b-d10b51440c2f)

### ponds dataset
Pada data ponds, kita ingin mencari luas dari tiap kolam berdasarkan _length & width_ masing-masing kolam. 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/f9165bd9-a683-4984-a33b-0a8677293729)

### farms dataset
Pada data farms, kita ingin merubah kolom bernama "id" menjadi "farm_id" agar saat kita merge dataset nya akan mudah untuk menunjukkan "province" masing-masing kolam. Lalu kita akan melakukan merge data farmns ke ponds berdasarkan farm_id nya sehingga mendapatkan table seperti ini

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/b4b302d4-20bd-40df-8b79-06fc76cdd267)

## Calculating Survival Rate (SR)
**Survival Rate (SR)** digunakan untuk mengetahui persentasi kelangsungan hidup benur udang yang ditebar dalam 1 siklus budidaya. Nilai Ideal Survival Rate (SR) adalah 80% -90%, meskipun pada kenyataannya banyak tambak di Indonesia mencapai SR 70%-80%.

**Rumus menghitung SR** = (populasi udang (ekor)/jumlah tebar(ekor)) * 100

- Kita akan menghitung jumlah populasi saat dipanen dengan cara
Jumlah populasi = total bobot panen (kg) / ukuran (per kg)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/584f52cd-ac49-4484-a49a-7bcd510aebc8)

sehingga kita akan mendapatkan kolom baru dalam dataset _harvests_ berupa "total_pop"

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/d4318047-37b8-48eb-9158-fce0eecf5aba)

Dari sini, kita akan menghitung jumlah populasi per "cycle_id" dan kita akan mengambil total populasi untuk setiap "cycle_id" pertama yang muncul.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/0542c66e-f391-40d1-9018-8dd52d0245e5)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/00ce5d49-111d-448b-b430-ad8fe9712743)

Kemudian kita akan menghitung **SR** tiap _cycle_id_ setelah panen dengan melakukan _merge_ pada dataset _cycles_ dengan _harvests_.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/c1ca706c-4f2c-41b6-b00b-d0b28a25e8d9)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/0c27f43d-2b13-4647-88e5-63688b0d5353)

Terlihat ada 352 baris yang menunjukkan bahwa kita mempunyai Survival Rate lebih dari 100%. Oleh karena itu, tindakan terbaik adalah mengecualikannya dari kumpulan data. dan karena kita ingin menetapkan **SR** tiap cycle_id makan kita akan menghapus duplicatnya, sehingga data nya menjadi 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/c17eac34-0826-436b-ac21-967bfaf889ed)

### Calculating Average Daily Gain (ADG)
**Average Daily Gain (ADG)** adalah rata-rata penambahan berat harian udang dalam periode tertentu. ADG juga merupakan salah satu parameter untuk mengukur pertumbuhan udang. Dari nilai ADG, petambak dapat mengetahui pertumbuhan berat udang dalam waktu tertentu.

**Rumus menghitung ADG** = (rata-rata berat akhir - rata-rata berat awal)/ umur udang(hari)
Dari data samplings, kita akan mengelompokkan sampel berdasarkan cycle_id-nya dan menghitung bobot rata-rata.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/e73a6de1-5535-496e-805b-99a1237629a9)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/311948de-b172-45df-adf4-7256132d6deb)

Lalu kita akan menggabungkan data siklus dengan data pengambilan sampel sehingga bisa menghitung **ADG** tiap cycle. 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/2c6928ca-d80a-4485-be73-2feec6a0f9f1)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/ac3bef69-fff6-4f18-802c-a699449c71fb)

### Calculating Feed Convertion Ratio (FCR)
**Feed Convertion Ratio (FCR)** adalah rasio konversi pakan yang menjadi indikator efisiensi manajemen pakan selain waktu, frekuensi, pola pemberian, dan kualitas pakan itu sendiri. Nilai FCR yang rendah menandakan bahwa manajemen pakan yang diterapkan dan kualitas pakan yang diberikan sudah bagus. Nilai FCR yang tinggi mengindikasikan bahwa manajemen pakan yang diterapkan buruk.

**Rumus menghitung FCR** = jumlah pakan total/biomassa

Untuk menghitung FCR, kita ingin menggunakan _feeds_ dataset untuk mengetahui jumlah pakan yang diberikan untuk tiap _cycle_id_. 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/b890160e-6f73-48c9-87c4-e3e721ef2694)

Terdapat beberapa value yang negatif pada dataset ini, oleh karena itu kita ingin menghilangkan kuantitas yang mengandung nilai negatif dan juga memeriksa outlier karena kami memiliki nilai jumlah maksimum 423 kg.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/da440a17-6311-4010-b4fc-92264a31cc64)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/c6e1d0f3-2db9-4b76-8fee-59d91e3f2b41)

Menggunakan z-score dan nilai absolut 3 untuk menentukan outlier dari kolom "quantity" lalu menggunakan fungsi drop untuk menghilangkan outliernya.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/0240043b-779d-4d8c-ad9c-51bfde9186cf)

Baru kita akan menghitung FCR dengan menentukan total_feed_per_cycle" terlebih dahulu.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/7bbd100d-7a97-4237-9255-72ee35a4dc5a)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/1a61dec1-0e9f-4c41-bc23-cb4ea46c6e7c)

Hasil table FCR akan seperti ini

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/e54c4b70-2b91-45a9-9fde-746c158c2ebf)

## Merging the dataset of SR, ADG, and FCR
Data _merged_df_ memiliki kolom-kolom 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/d516b49f-48a4-468a-9dc2-26e922a3aa8a)

Kemudian kita akan merge data ADG dan juga FCR ke dalam _merged_df_.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/d4d5ea89-4e7c-4c03-9dda-4ce342a6e0c3)

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/e4795369-4b84-44aa-8acb-428955a0c71b)

Setelah mendapatkan SR, ADG, dan FCR dalam satu tabel, kita perlu memastikan bahwa tidak ada Null values didalam dataframe tersebut lalu menggunakan _drop_ untuk menghilangkan missing values dalam dataframe tersebut sehingga kita memiliki table 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/a5043327-6cc0-4c79-b42d-d20be024da25)

Kita juga bisa menambahkan kolom "provinsi" dan "wideness" sebelum kita menganalisisnya lebih lanjut.

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/4e77cab9-f2ac-4f61-812a-aa27ea19d88a)

## Analysis
Dalam analisis ini, kita akan menggunakan uji statistik ANNOVA untuk mengetahui seberapa signifikan antara SR, ADG, dan FCR bila dilihat dari kolam, lokasi tambak, dan siklus budidayanya.

- ![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/dd2004af-6cc6-404d-b5c3-261d9357798e)

