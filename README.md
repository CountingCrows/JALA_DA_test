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
