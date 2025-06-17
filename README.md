---
title: "Eksplorasi Iterasi dan Looping di R"
author: "Sri Wahyuni, Fahma Zuaf Zarir, Arya Dirgantara Alfiqhri, Larasati Oktarani"
date: "`r Sys.Date()`"
output: html_document
---

## Pendahuluan

Pada dokumen ini, kita akan mengeksplorasi materi **Iterasi dan Looping** menggunakan bahasa pemrograman R. Iterasi dan looping sangat penting dalam pemrograman untuk melakukan eksekusi perintah secara berulang.

## Definisi

Iterasi adalah proses eksekusi berulang pada suatu blok kode dalam pemrograman hingga kondisi tertentu dipenuhi. Dengan menggunakan iterasi, pengembang dapat mengotomatisasi proses yang memerlukan eksekusi berulang tanpa harus menulis kode yang sama secara manual. Iterasi sangat erat kaitannya dengan perulangan (loop). Ada 3 tipe struktur loop, yaitu:

1. for loops
2. while loops
3. repeat-until loops

Sumber : [Unikom](https://medium.com/codelabs-unikom/algoritma-perulangan-iteration-looping-apa-itu-df8007239f9c)

---

## Contoh Looping

### For Loop

```{r}
# Contoh penggunaan for loop
for (i in 1:5) {
    print(paste("Iterasi ke-", i))
}
```

#### Flowchart For Loop

Berikut adalah flowchart sederhana yang menggambarkan alur kerja **for loop**:

```{r, echo=FALSE, message=FALSE}
# Pastikan DiagrammeR sudah terpasang: install.packages("DiagrammeR")
library(DiagrammeR)
grViz("
digraph for_loop {
    graph [rankdir=TB, bgcolor=white]
    node [fontname='Arial', fontsize=12, style=filled, fillcolor='#E3F2FD', color='#1976D2', shape=box]

    Mulai [label='Mulai', shape=oval, fillcolor='#A5D6A7', color='#388E3C']
    Inisialisasi [label='Inisialisasi: i = 1']
    Kondisi [label='i <= 5?', shape=diamond, fillcolor='#FFF9C4', color='#FBC02D']
    Eksekusi [label='Eksekusi blok kode']
    Increment [label='i = i + 1']
    Selesai [label='Selesai', shape=oval, fillcolor='#EF9A9A', color='#C62828']

    Mulai -> Inisialisasi
    Inisialisasi -> Kondisi
    Kondisi -> Eksekusi [label='Ya', color='#388E3C']
    Eksekusi -> Increment
    Increment -> Kondisi
    Kondisi -> Selesai [label='Tidak', color='#C62828']
}
")
```

### While Loop

```{r}
# Contoh penggunaan while loop
i <- 1
while (i <= 5) {
    print(paste("Iterasi ke-", i))
    i <- i + 1
}
```

#### Flowchart While Loop

Berikut adalah flowchart sederhana yang menggambarkan alur kerja **while loop**:

```{r, echo=FALSE, message=FALSE}
library(DiagrammeR)
grViz("
digraph while_loop {
    graph [rankdir=TB, bgcolor=white]
    node [fontname='Arial', fontsize=12, style=filled, fillcolor='#E3F2FD', color='#1976D2', shape=box]

    Mulai [label='Mulai', shape=oval, fillcolor='#A5D6A7', color='#388E3C']
    Inisialisasi [label='Inisialisasi: i = 1']
    Kondisi [label='i <= 5?', shape=diamond, fillcolor='#FFF9C4', color='#FBC02D']
    Selesai [label='Selesai', shape=oval, fillcolor='#EF9A9A', color='#C62828']
    Eksekusi [label='Eksekusi blok kode & i = i + 1']

    Mulai -> Inisialisasi
    Inisialisasi -> Kondisi
    Kondisi -> Eksekusi [label='Ya', color='#388E3C']
    Eksekusi -> Kondisi
    Kondisi -> Selesai [label='Tidak', color='#C62828']
}
")
```

> **Catatan:**  
> Flowchart for dan while loop memang tampak mirip karena keduanya melakukan proses iterasi dengan pengecekan kondisi sebelum eksekusi blok kode. Perbedaannya, pada for loop inisialisasi, kondisi, dan increment biasanya ditulis dalam satu baris, sedangkan pada while loop increment dilakukan di dalam blok kode secara eksplisit. Namun, secara alur logika, keduanya serupa sehingga flowchart-nya hampir sama.

### Repeat Loop

```{r}
# Contoh penggunaan repeat loop
i <- 1
repeat {
    print(paste("Iterasi ke-", i))
    i <- i + 1
    if (i > 5) {
        break
    }
}
```

#### Flowchart Repeat Loop

Berikut adalah flowchart sederhana yang menggambarkan alur kerja **repeat loop**:

```{r, echo=FALSE, message=FALSE}
library(DiagrammeR)
grViz("
digraph repeat_loop {
    graph [rankdir=TB, bgcolor=white]
    node [fontname='Arial', fontsize=12, style=filled, fillcolor='#E3F2FD', color='#1976D2', shape=box]

    Mulai [label='Mulai', shape=oval, fillcolor='#A5D6A7', color='#388E3C']
    Inisialisasi [label='Inisialisasi: i = 1']
    Eksekusi [label='Eksekusi blok kode']
    Increment [label='i = i + 1']
    Kondisi [label='i > 5?', shape=diamond, fillcolor='#FFF9C4', color='#FBC02D']
    Selesai [label='Selesai', shape=oval, fillcolor='#EF9A9A', color='#C62828']

    Mulai -> Inisialisasi
    Inisialisasi -> Eksekusi
    Eksekusi -> Increment
    Increment -> Kondisi
    Kondisi -> Eksekusi [label='Tidak', color='#388E3C']
    Kondisi -> Selesai [label='Ya', color='#C62828']
}
")
```

# Studi Kasus: Pemantauan Suhu Tubuh Pasien oleh Dokter dan Staff IT Rumah Sakit

Di sebuah rumah sakit umum, seorang dokter spesialis penyakit dalam bertugas memantau suhu tubuh 30 pasien rawat inap setiap hari selama 7 hari berturut-turut. Pemantauan ini penting untuk mendeteksi gejala demam atau tanda awal infeksi, khususnya pada pasien pascaoperasi dan pasien rentan.

Untuk mengolah dan menganalisis data suhu harian tersebut secara efisien, dokter meminta bantuan kepada staff IT rumah sakit. Staff IT diminta menggunakan bahasa pemrograman R untuk melakukan berbagai analisis berbasis data suhu tubuh tersebut.

Secara khusus, staff IT diminta untuk:

1. Menghitung rata-rata suhu tubuh setiap pasien selama 7 hari menggunakan loop.
2. Menemukan pasien pertama yang mengalami demam ringan (≥37.5°C) selama 4 hari atau lebih.
3. Menghitung jumlah pasien yang tidak pernah demam selama seminggu, dan menghentikan pencarian setelah menemukan minimal 10 pasien

## Simulasi Data Suhu

```{r}

# Set seed agar data reproducible (hasil sama saat diulang)

set.seed(123)

# Simulasi suhu berdistribusi normal (mean = 36.9, sd = 0.4) sebanyak 7 hari

suhu <- matrix(round(rnorm(30 * 7, mean = 36.9, sd = 0.4), 2), nrow = 30, ncol = 7)
colnames(suhu) <- paste("Hari", 1:7)
rownames(suhu) <- paste("Pasien", 1:30)

# Tampilkan data suhu mingguan
suhu
```

## Uji Normalitas Data Suhu Pasien

Untuk memastikan bahwa data suhu tubuh pasien mengikuti distribusi normal, dilakukan uji normalitas. Pada studi kasus ini, data suhu berbentuk numerik kontinu dan jumlah sampel cukup besar (30 pasien × 7 hari = 210 data). Uji normalitas yang paling cocok digunakan adalah **Shapiro-Wilk test**, karena uji ini sensitif dan umum digunakan untuk data dengan ukuran sampel kecil hingga sedang (biasanya hingga sekitar 50–500 data).

### Implementasi di R

```{r}
suhu_vector <- as.vector(suhu)
shapiro.test(suhu_vector)
```

> **Catatan:**  
> Jika p-value hasil uji > 0.05, maka data suhu dapat dianggap berdistribusi normal. Jika p-value ≤ 0.05, data tidak berdistribusi normal.

## Visualisasi Distribusi Data

```{r}
hist(suhu_vector, breaks=15, probability=TRUE, col="skyblue",
     main="Distribusi Suhu Tubuh Pasien", xlab="Suhu (°C)")
lines(density(suhu_vector), col="darkblue", lwd=2)
abline(v=mean(suhu_vector), col="red", lty=2)
```

> Grafik ini menyajikan distribusi suhu tubuh pasien, menampilkan bagaimana nilai suhu tersebar di antara kelompok pasien yang diamati. Bentuk histogram yang diikuti oleh kurva densitas berwarna biru tua jelas menunjukkan bahwa data suhu tubuh pasien cenderung berdistribusi normal (bell-shaped).

```{r}
qqnorm(suhu_vector, main="Q-Q Plot Suhu Tubuh")
qqline(suhu_vector, col="red", lwd=2)
```

> Berdasarkan plot Q-Q Suhu Tubuh,sebagian besar titik-titik data cukup mendekati garis lurus. Ini menunjukkan bahwa distribusi data suhu tubuh menyerupai distribusi normal. Namun, ada sedikit penyimpangan di kedua ujungnya, terutama di bagian atas (sekitar 38.0), di mana beberapa titik data berada sedikit di atas garis. Ini bisa mengindikasikan adanya beberapa individu dengan suhu tubuh yang sedikit lebih tinggi atau bahwa distribusi memiliki ekor kanan yang sedikit lebih berat dibandingkan dengan distribusi normal yang sempurna.

## Rata-rata Suhu Tiap Pasien Menggunakan For Loop

```{r}
rata_suhu <- numeric(nrow(suhu))
for (i in 1:nrow(suhu)) {
    rata_suhu[i] <- mean(suhu[i, ])
}
# Tampilkan rata-rata suhu tiap pasien dalam bentuk data frame
data.frame(Pasien = rownames(suhu), Rata_Suhu = rata_suhu)
```

## Menemukan Pasien Pertama yang Mengalami Demam ≥ 4 Hari dengan While Loop

Pada bagian ini, kita akan mencari pasien pertama yang mengalami demam ringan (suhu ≥ 37.5°C) selama minimal 4 hari dalam seminggu. Proses pencarian dilakukan menggunakan struktur perulangan **while loop**. Loop akan memeriksa setiap pasien satu per satu hingga menemukan pasien yang memenuhi kriteria tersebut, lalu proses pencarian dihentikan.

```{r}
i <- 1
hasil <- NULL
while (i <= nrow(suhu)) {
    if (sum(suhu[i, ] >= 37.5) >= 4) {
        hasil <- paste("Pasien", i, "mengalami demam ≥ 4 hari")
        break
    }
    i <- i + 1
}
if (is.null(hasil)) {
    cat("Tidak ada pasien yang mengalami demam ≥ 4 hari\n")
} else {
    cat(hasil, "\n")
}
```

## Mencari Lebih dari 10 Pasien yang Tidak Pernah Demam Menggunakan Repeat Loop

Pada bagian ini, kita akan mencari pasien yang tidak pernah mengalami demam (suhu ≤ 37.5°C) selama seminggu penuh. Proses pencarian dilakukan menggunakan struktur perulangan **repeat loop** dan akan berhenti setelah ditemukan minimal 10 pasien tanpa demam.

```{r}
i <- 1
tanpa_demam <- 0
pasien_tanpa_demam <- c()
repeat {
    if (sum(suhu[i, ] > 37.5) == 0) {
        tanpa_demam <- tanpa_demam + 1
        pasien_tanpa_demam <- c(pasien_tanpa_demam, i)
    }
    if (tanpa_demam >= 10 || i >= nrow(suhu)) {
        break
    }
    i <- i + 1
}
cat("Jumlah pasien tanpa demam ditemukan:", tanpa_demam, "\n")
cat("Pasien tanpa demam ditemukan pada pasien ke:", pasien_tanpa_demam, "\n")
```

## Kesimpulan
Terdapat berbagai jenis struktur perulangan dalam bahasa pemrograman R, yakni  for loop, while loop, dan repeat loop. Setiap tipe loop ini memiliki fungsi khusus dan metode penerapan yang berbeda.
Pada studi kasus pengukuran suhu tubuh pasien di rumah sakit, iterasi digunakan untuk menganalisis data temperatur pasien secara efektif, seperti melakukan perhitungan rata-rata suhu tubuh setiap pasien, mengidentifikasi pasien yang mengalami demam lebih dari 4 hari, dan menemukan pasien yang tidak mengalami demam dalam satu minggu penuh.
Pemahaman tentang struktur pengulangan di R adalah kunci dalam menyelesaikan masalah analisis data yang memerlukan pengulangan dan evaluasi berulang. Dengan memanfaatkan for loop, while loop, dan repeat loop, proses analisis data dapat dilakukan secara otomatis dengan lebih efisien dan sistematis.

## Penutup
Dalam dokumen ini, kita telah mengeksplorasi berbagai jenis iterasi dan looping di R, termasuk **for loop**, **while loop**, dan **repeat loop**. Masing-masing memiliki kegunaan dan cara kerja yang berbeda, namun semuanya berguna untuk melakukan eksekusi perintah secara berulang. Dengan memahami konsep ini, Anda dapat menulis kode yang lebih efisien dan terstruktur.
