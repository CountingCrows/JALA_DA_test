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
Sebelum menjawab pertanyaan yang ada di atas, kita akan mencari apakah data-data yang disediakan memiliki NaN values, terutama untuk data _farms, cycles, ponds, feeds, harvests, fasting, dan sampling_. 

![image](https://github.com/CountingCrows/JALA_DA_test/assets/85608120/2af25554-5b33-4c9a-88cf-5e98a9e476da)


