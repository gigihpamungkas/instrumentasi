---
layout: default
title: L4&#58; Series and Parallel Resistors
description: "Extend Ohm's Law to series and parallel resistor circuits: series resistors divide voltage, parallel resistors divide current, with equivalent-resistance formulas and CircuitJS."
image: /electronics/assets/images/OhmsLaw_IntroToSeriesVsParallelResistorCircuits_ByJonFroehlich.png
nav_order: 4
parent: Intro to Electronics
has_toc: false # on by default
usemathjax: true
comments: true
usetocbot: true
---
# {{ page.title | replace_first:'L','Lesson '}}
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

Di pelajaran Hukum Ohm sebelumnya, kita sudah menganalisis rangkaian yang relatif sederhana dengan satu resistor. Rangkaian tersebut membantu kita membangun fondasi dan pemahaman konseptual tentang Hukum Ohm serta cara menerapkannya. Namun, sebagian besar rangkaian di dunia nyata tidak sesederhana itu.

Di pelajaran kali ini, kita akan mengembangkan penerapan Hukum Ohm ke rangkaian yang lebih kompleks: resistor dalam rangkaian **seri** dan resistor dalam rangkaian **paralel**. Singkatnya:
* Resistor seri **membagi tegangan** dan merupakan salah satu konfigurasi rangkaian yang paling umum (dan berguna) saat bekerja dengan mikrokontroler dan sensor resistif seperti [potensiometer](../arduino/potentiometers.md), [force-sensitive resistor (sensor tekanan)](../arduino/force-sensitive-resistors.md), dan [fotosel (LDR)](../sensors/photoresistors.md).
* Resistor paralel **membagi arus** (dan arus yang lebih besar akan mengalir ke jalur dengan hambatan yang lebih kecil). Rangkaian paralel ini sangat berguna, contohnya saat kita ingin menyalakan beberapa LED sekaligus.

![Two circuit diagrams side by side: on the left, a series resistor circuit with R1 and R2 connected end-to-end in a single loop with a battery; on the right, a parallel resistor circuit with R1 and R2 on separate branches sharing the same two nodes.](assets/images/OhmsLaw_IntroToSeriesVsParallelResistorCircuits_ByJonFroehlich.png)
**Gambar.** Contoh resistor **seri** (kiri) dan resistor **paralel** (kanan). Gambar dibuat di PowerPoint.
{: .fs-1 }

## Hambatan pengganti (Ekuivalen)

Dengan menggunakan [Hukum Rangkaian Kirchhoff](https://en.wikipedia.org/wiki/Kirchhoff%27s_circuit_laws), kita bisa mencari nilai hambatan "pengganti" atau ekuivalen untuk rangkaian seri dan paralel.

Untuk resistor seri, kita cukup menjumlahkan semua nilai hambatan untuk mencari total hambatan $$R_{equivalent}$$:

$$R_{equivalent} = R_{1} + R_{2} + ... + R_{N-1} + R_{N}$$

Untuk resistor paralel, rumusnya sedikit lebih menantang:

$$R_{equivalent} = \frac{1}{\frac{1}{R_{1}} + \frac{1}{R_{2}} + ... + \frac{1}{R_{N-1}} + \frac{1}{R_{N}}}$$

Ya, rumus hambatan paralel memang terlihat agak rumit, tapi kamu bisa menurunkannya sendiri (atau bahkan melupakannya sama sekali) kalau kamu sudah paham Hukum Ohm dan [Hukum Kirchhoff](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/v/ee-kirchhoffs-current-law).

Bagi kita, konsep paling penting dan berguna yang harus dipahami adalah bahwa **resistor seri** membagi tegangan (kita akan sering pakai ini nanti di rangkaian mikrokontroler) dan **resistor paralel** membagi arus (di mana arus *lebih besar* mengalir melalui cabang yang hambatannya lebih kecil). Gambar di bawah ini mencoba menjelaskan konsep tersebut secara ringkas.

![A detailed comparison of series and parallel resistor circuits. The series circuit (left) shows that current is the same through each resistor but voltage is divided proportionally across them. The parallel circuit (right) shows that voltage is the same across each branch but current is divided, with more current flowing through the branch with lower resistance.](assets/images/OhmsLaw_IntroToSeriesVsParallelResistorCircuits_PictorialDiagram_ByJonFroehlich.png)

**Gambar.** Gambaran umum tentang cara kerja **resistor seri** (arus sama di setiap resistor tetapi *tegangan dibagi*) dan cara kerja **resistor paralel** (tegangan sama di setiap resistor tetapi *arus dibagi*). Coba luangkan waktu sejenak untuk mempelajari dan memahami kenapa fenomena ini bisa terjadi. Klik kanan pada gambar dan pilih 'Open in new tab' untuk memperbesar. Gambar dibuat di PowerPoint.
{: .fs-1 }

Meskipun kemampuan menganalisis rangkaian secara manual itu penting dalam dunia physical computing, jangan khawatir kalau kamu bingung. Kamu selalu bisa menggunakan simulator rangkaian seperti [CircuitJS](https://www.falstad.com/circuit/circuitjs.html).

## Resistor seri

[Resistor dalam rangkaian seri](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-series-resistors) dihubungkan secara berurutan: ujung bertemu pangkal (head-to-tail).

![Two diagrams showing components in series: on the left, a generic representation of three components connected end-to-end in a single path; on the right, a circuit schematic with resistors arranged head-to-tail between a voltage source.](assets/images/ComponentsInSeries_KhanAcademyAndJonFroehlich.png)

**Gambar.** Komponen dikatakan seri jika digabungkan ujung-ke-ujung (atau head-to-tail) secara berurutan seperti di atas. Gambar di sebelah kiri bersumber dari [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-series-resistors). Gambar dibuat di PowerPoint.
{: .fs-1 }

Dari Hukum Ohm, kita tahu bahwa resistor *menurunkan* tegangan (tepatnya, penurunan tegangan $$V_{R}$$ pada resistor $$R$$ adalah $$V_{R} = I * R$$). Oleh karena itu, beberapa resistor yang dipasang "berjejer" (seri) *masing-masing* akan menyebabkan penurunan tegangan—dan besarnya penurunan ini sebanding dengan nilai resistornya (makin besar hambatan, makin besar juga penurunan tegangannya).

Umumnya, saat kita mencoba menganalisis rangkaian dengan beberapa konfigurasi resistor (seri, paralel, atau gabungan), langkah pertamanya adalah menentukan **hambatan pengganti (total)**. Artinya, bagaimana kita bisa menggabungkan semua hambatan dalam rangkaian menjadi satu nilai tunggal (disebut $$R_{total}$$ atau $$R_{equivalent}$$) agar kita bisa menerapkan Hukum Ohm ke seluruh rangkaian. Dalam kasus mencari total arus, rumusnya menjadi $$I=\frac{V}{R_{total}}$$

Yuk, langsung kita coba!

### Contoh Seri 1: Mencari Nilai Arus

Kita mulai dari rangkaian resistor seri yang paling simpel: sebuah baterai 9V dengan resistor 100Ω dan 1kΩ yang disusun seri.

![A circuit with a 9V battery and two resistors in series: R1 = 100 ohms and R2 = 1 kilohm. The current I through the circuit is unknown.](assets/images/SeriesResistorCircuit_TwoResistorsOf100OhmAnd1kOhm_Step0.png)

**Gambar.** Rangkaian sederhana dengan dua resistor seri (100Ω dan 1kΩ) dan baterai 9V. Berapa banyak arus $$I$$ yang mengalir melalui rangkaian ini?
{: .fs-1 }

#### Langkah 1: Cari total hambatan

Langkah pertama adalah menghitung total hambatan dalam rangkaian kita. Karena kita tahu bahwa rangkaian seri itu tinggal dijumlahkan, maka: $$R_{Total} = R_{1} + R_{2} \Rightarrow  100Ω + 1000Ω \Rightarrow 1100Ω$$. Jadi, total hambatannya adalah $$1100Ω$$.

![The same two-resistor series circuit, now showing the two resistors combined into a single equivalent resistor R_Total = 1100 ohms.](assets/images/SeriesResistorCircuit_TwoResistorsOf100OhmAnd1kOhm_Step1.png)

**Gambar.** Untuk menemukan hambatan pengganti dari rangkaian ini (kita sebut saja $$R_{Total}$$), kita bisa menggabungkan resistor seri dengan cara menjumlahkannya.
{: .fs-1 }

#### Langkah 2: Cari arus I dengan hambatan pengganti

Sekarang kita bisa menggunakan nilai hambatan pengganti $$R_{Total}$$ ini untuk mencari arus $$I$$ menggunakan Hukum Ohm: $$I=9V/1100Ω \Rightarrow 0.0082A \Rightarrow 8.2mA$$

![The simplified circuit showing the equivalent resistance of 1100 ohms with the solved current I = 8.2 milliamps flowing through the circuit.](assets/images/SeriesResistorCircuit_TwoResistorsOf100OhmAnd1kOhm_Step2.png)

**Gambar.** Sekarang kita cari arus $$I$$ dengan mudah memakai Hukum Ohm: $$I=9V/1100Ω \Rightarrow 8.2mA$$
{: .fs-1 }

Selesai! Gampang, kan? Arus totalnya adalah $$I = 8.2mA$$.

### Contoh Seri 2: Mencari Nilai Arus

Biar makin mantap pemahamannya, mari kita coba lagi tapi pakai tiga resistor. Kali ini, $$R_{1}=2.2kΩ$$, $$R_{2}=1kΩ$$, dan $$R_{3}=470Ω$$.

Sama seperti tadi, kita mulai dengan mencari $$R_{Total}$$, yaitu:

$$R_{Total} = R_{1} + R_{2} + R_{3} \\
R_{Total} = 2200Ω + 1000Ω + 470Ω \\
R_{Total} = 3670Ω$$

Setelah itu, kita gunakan nilai hambatan pengganti ini untuk mencari arus $$I$$, yaitu $$I=\frac{9V}{3670Ω} \Rightarrow 0.002452A \Rightarrow 2.45mA$$.

![A series circuit with three resistors (2.2 kilohms, 1 kilohm, and 470 ohms) and a 9V battery. The resistors are combined into R_Total = 3670 ohms, and the solved current is I = 2.45 milliamps.](assets/images/SeriesResistorCircuit_ThreeResistors_Solved.png)

**Gambar.** Pada gambar di atas, kita mencari nilai arus dengan tiga resistor seri. Pertama, jumlahkan semua hambatan (karena disusun seri) lalu gunakan total hambatan tersebut ($$R_{Total}$$) untuk menentukan arus dengan Hukum Ohm: $$I=\frac{V}{R_{Total}} \Rightarrow \frac{9V}{3670Ω} \Rightarrow 2.45mA$$ (dibulatkan menjadi 2.5mA pada gambar).
{: .fs-1 }

#### Pembuktian hasil kerja di simulator rangkaian

Kita bisa mengecek hasil perhitungan kita di simulator rangkaian favorit masing-masing. Bebas mau pakai apa saja. :)

Di sini saya akan menggunakan alat open-source bernama [CircuitJS](https://www.falstad.com/circuit/circuitjs.html). Kamu bisa langsung melihat simulasinya di [sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rzCEqo2lWJQpMBGwDug8CIoo8SquwBOKtWAyEdIFAgNUUaSG20JVRjLxtrsNqWHhXD2Qmse0aaqhoMSwUwHj4BXxp+cHlDYSpfPQMUON9jA3T7IzTbZwc87xyFKP9DaIFUoA).

Kita tinggal klik pada kabel untuk melihat secara ajaib berapa banyak arus yang mengalir di dalamnya atau melihat potensi listriknya (tegangan) terhadap ground. Dan benar saja, kamu akan melihat bahwa arus sebesar $$2.5mA$$ memang sedang mengalir melalui rangkaian tersebut. Ada hal lain yang kamu sadari?

Ingat kan kalau dari tadi kita selalu menekankan bahwa tegangan itu *terbagi* atau *terpecah* pada resistor yang disusun seri? Di simulasi ini hal itu terlihat sangat jelas! Tegangannya berada di angka $$9V$$ pada titik (node) atas, lalu turun sebesar $$5.4V$$ setelah melewati resistor $$2.2kΩ$$ menjadi $$3.6V$$. Tegangan ini turun lagi sebesar $$2.4V$$ setelah melewati resistor $$1kΩ$$ dan menyisakan potensi listrik sebesar $$1.2V$$, sebelum akhirnya turun habis menjadi $$0V$$ atau $$GND$$ setelah melewati resistor $$470Ω$$. Kita akan bahas ini lebih detail di bagian selanjutnya!

<video autoplay loop muted playsinline aria-label="CircuitJS simulation of a three-resistor series circuit with a 9V battery, showing animated current flow of 2.5 milliamps and voltage drops across each resistor.">
  <source src="assets/videos/SeriesResistorThreeResistors9VBattery2.2k1k470_CircuitJSRecording.mp4" type="video/mp4" />
</video>

**Gambar.** Video ini menunjukkan simulasi [CircuitJS](https://www.falstad.com/circuit/circuitjs.html) dari rangkaian seri tiga resistor dasar. Kamu bisa mengotak-atik rangkaiannya di [sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rzCEqo2lWJQpMBGwDug8CIoo8SquwBOKtWAyEdIFAgNUUaSG20JVRjLxtrsNqWHhXD2Qmse0aaqhoMSwUwHj4BXxp+cHlDYSpfPQMUON9jA3T7IzTbZwc87xyFKP9DaIFUoA).
{: .fs-1 }

## Pembagi Tegangan (Voltage Divider)

Konsep bahwa **resistor seri** bisa membagi tegangan adalah hal yang sangat krusial saat kita bekerja dengan mikrokontroler. Jadi, bagian ini sengaja diberi pembahasan khusus.

Hal penting yang wajib ingat: selalu ada *penurunan tegangan* di setiap resistor (ini berlaku umum ya, bukan cuma di rangkaian seri). Oleh karena itu, di antara setiap resistor kita akan mendapatkan *potensi listrik* atau tegangan yang berbeda. Dan karena mikrokontroler mendeteksi atau "membaca" tegangan (bukan arus), kita bisa memanfaatkan sifat ini untuk mengontrol input dinamis ke mikrokontroler kita!

Mari kita bedah beberapa contohnya.

### Contoh 1: Cari nilai tegangan pada titik VB

Berbekal ide penurunan tegangan di setiap resistor tadi, mari kita hitung berapa tegangan pada titik (node) $$V_{B}$$ terhadap ground (ingat, node atau titik adalah istilah untuk setiap sambungan yang menghubungkan dua atau lebih komponen dalam rangkaian).

Sebelum lanjut membaca pembahasannya, coba berhenti sejenak dan pikirkan: bagaimana caramu menghitung tegangan di titik $$V_{B}$$?

![A series circuit with a 9V battery, R1 = 100 ohms, and R2 = 150 ohms. The node between the two resistors is labeled V_B, and the question asks: what is the voltage at V_B?](assets/images/VoltageDivider_100And150_ByJonFroehlich.png)

#### Langkah 1: Cari arus yang mengalir di rangkaian

Sama seperti sebelumnya, langkah awal adalah mencari arus yang mengalir di rangkaian. Caranya, cari dulu hambatan pengganti $$R_{Total}$$ lalu gunakan Hukum Ohm. Maka, $$I=\frac{V}{R_{Total}} \Rightarrow \frac{9V}{250Ω} \Rightarrow 36mA$$.

![The same voltage divider circuit now showing R_Total = 250 ohms and the solved current I = 36 milliamps.](assets/images/VoltageDivider_100And150_Step1_ByJonFroehlich.png)

#### Langkah 2: Hitung penurunan tegangan di masing-masing resistor

Karena sekarang kita sudah tahu arus total yang mengalir ($$36mA$$), kita bisa pakai angka ini untuk menghitung penurunan tegangan spesifik di tiap resistor. Mari kita sebut penurunan tegangan pada $$R_{1}$$ sebagai $$V_{1}$$ dan penurunan tegangan pada $$R_{2}$$ sebagai $$V_{2}$$. Karena fokus kita adalah mencari tegangan, kita pakai rumus Hukum Ohm yang ini: $$V = I * R$$.

Maka hasilnya:

$$
{V_1} = I * R_1 \Rightarrow 0.036A * 100Ω \Rightarrow 3.6V \\
{V_2} = I * R_2 \Rightarrow 0.036A * 150Ω \Rightarrow 5.4V
$$

Sebagai pembuktian singkat (tanpa perlu bahas terlalu panjang), berdasarkan [Hukum Rangkaian Kirchhoff (KVL)](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-kirchhoffs-laws), kita tahu bahwa $$V_{Total} = V_1 + V_2 \Rightarrow 9V = 3.6V + 5.4V \Rightarrow 9V = 9V$$. Sip, hitungan kita sejauh ini sudah sinkron dan benar!

![The voltage divider circuit with annotations showing the voltage drop V1 = 3.6V across R1 and V2 = 5.4V across R2, with the current I = 36 milliamps labeled.](assets/images/VoltageDivider_100And150_Step2_ByJonFroehlich.png)

#### Langkah 3: Sekarang, hitung nilai VB

Sekarang menghitung $$V_B$$ jadi gampang banget. Kita tahu kalau $$V_A = 9V$$ dan $$R_1$$ menyebabkan penurunan tegangan sebesar $$3.6V$$. Otomatis, $$V_B$$ pastilah senilai $$9V - 3.6V$$, yaitu 5.4V.

![The completed voltage divider analysis showing V_A = 9V at the top, a 3.6V drop across R1, and V_B = 5.4V at the node between the two resistors.](assets/images/VoltageDivider_100And150_Step3_ByJonFroehlich.png)

### Pola pembagi tegangan

Kita menyebut konfigurasi dua resistor seperti ini sebagai **pembagi tegangan (voltage divider)** karena fungsinya yang memang membagi-bagi tegangan. Di contoh ini, kita memakai resistor $$100Ω$$ dan $$150Ω$$ secara seri untuk menghasilkan output $$5.4V$$ pada titik $$V_B$$.

Dengan menggunakan Hukum Ohm, kita bisa [menurunkan rumus pembagi tegangan](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider) untuk mencari $$V_B$$ berdasarkan tegangan input ($$V_A$$) yang masuk ke jaringan pembagi tegangan serta nilai kedua resistor: resistor atas $$R_1$$ dan resistor bawah $$R_2$$.

Rumus pembagi tegangannya adalah:
$$V_{B} = V_{A} * \frac{R_2}{R_1 + R_2}$$

Atau yang lebih sering ditulis seperti ini:
$$V_{out} = V_{in} * \frac{R_2}{R_1 + R_2}$$

![A generic voltage divider schematic showing V_in at the top, R1 and R2 in series, V_out at the node between R1 and R2, and the voltage divider equation V_out = V_in times R2 divided by (R1 + R2).](assets/images/VoltageDividerBasic_ByJonFroehlich.png)

**Gambar.** Pola dan rumus dasar pembagi tegangan. Gambar dibuat di PowerPoint. Lihat [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider) untuk info lebih lanjut.
{: .fs-1 }

Menariknya, kalau kamu perhatikan rumusnya, yang berpengaruh itu bukan nilai mutlak dari hambatannya, melainkan **perbandingan (rasio)** antara $$R_1$$ dan $$R_2$$ yang menentukan nilai $$V_{out}$$. Jadi, untuk urusan *membagi tegangan*, memasang $$R_1 = 100Ω$$ and $$R_2 = 100Ω$$ akan memberikan hasil yang sama persis dengan memasang $$R_1 = 2.2kΩ$$ and $$R_2 = 2.2kΩ$$, karena keduanya membagi tegangan sama rata. Artinya, $$V_{out}$$ akan bernilai $$4.5V$$ jika $$V_{in}=9V$$.

Bedanya, jumlah arus yang mengalir di kedua rangkaian tersebut bakal jauh berbeda. Rangkaian pertama menghasilkan arus: $$I = \frac{9V}{200Ω} \Rightarrow 45mA$$, sedangkan rangkaian kedua menghasilkan arus: $$I = \frac{9V}{4.4kΩ} \Rightarrow 2.0mA$$.

{: .note }
> **Toleransi di Dunia Nyata dan Pembagi Tegangan.** Dalam teori matematika di atas, kita menganggap semua resistor itu sempurna tanpa cacat. Tapi ingat, resistor fisik di dunia nyata punya nilai **toleransi**! 
>
> Kalau kamu membuat pembagi tegangan 50/50 pakai dua resistor 10kΩ yang punya toleransi ±5%, bisa jadi resistor pertama aslinya berukuran 9.5kΩ dan yang satunya lagi 10.5kΩ. Akibat ketidakseimbangan kecil ini, tegangan output aslimu tidak akan pas *persis* setengah dari tegangan input. Jadi, kalau nanti kamu mengukur rangkaian fisikmu pakai multimeter dan angkanya sedikit meleset dari hitungan teori, toleransi komponen inilah penyebab utamanya!

Bukannya seru ya kalau kita bisa mengubah nilai salah satu resistor itu secara dinamis agar menghasilkan tegangan $$V_{out}$$ yang bervariasi? Tentu saja! Dan konsep inilah yang menjadi dasar cara kerja [potensiometer](variable-resistors.md), yang akan kita pelajari di pelajaran berikutnya.

### Kenapa pembagi tegangan penting di physical computing?

Mikrokontroler seperti Arduino hanya bisa "membaca" level tegangan (lewat fitur Analog-to-Digital Converter atau ADC), mereka tidak bisa membaca nilai hambatan secara langsung. Makanya, saat kita ingin memakai sensor jenis resistif seperti fotosel (LDR), sensor tekanan (FSR), atau termistor (sensor suhu), kita wajib menyusunnya dalam konfigurasi pembagi tegangan. Begitu nilai hambatan sensor berubah karena pengaruh cahaya, tekanan, atau suhu, tegangan di titik $$V_{out}$$ juga ikut berubah secara proporsional—dan tegangan *itulah* yang dibaca oleh mikrokontroler. Kamu bakal sering banget melihat pola ini mulai di [pelajaran Arduino](../arduino/index.md).

#### Menurunkan rumus pembagi tegangan

Berbekal apa yang sudah kamu pelajari tentang rangkaian listrik, sekarang kamu pasti bisa menurunkan rumus pembagi tegangan sendiri, atau minimal paham *bagaimana* rumus itu tercipta. Yuk, kita bedah!

![A step-by-step algebraic derivation of the voltage divider equation, starting from Ohm's Law and Kirchhoff's Voltage Law, arriving at V_out = V_in times R2 divided by (R1 + R2).](assets/images/DerivingTheVoltageDividerEquation_ByJonFroehlich.png)
**Gambar.** Langkah-langkah menurunkan rumus pembagi tegangan. Lihat [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider) untuk ulasan lengkapnya.
{: .fs-1 }

Merujuk pada gambar di atas, mari kita kumpulkan informasi yang kita punya. Kita tahu kalau penurunan tegangan di $$R2$$ itu sama dengan $$V_{out}$$ (keduanya adalah hal yang sama) dan rumus $$V_R2=I*R2$$:

$$V_{out} = V_{R2} = I * R2$$

Kita juga tahu kalau $$V_{in}$$ itu adalah hasil penjumlahan dari $$V_R1 + V_R2$$ berdasarkan [Hukum Tegangan Kirchhoff (KVL)](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-kirchhoffs-laws).

$$V_{in} = V_{R1} + V_{R2}$$

Menggunakan Hukum Ohm, kita bisa mengganti $$V_{R1}$$ menjadi $$I * R1$$ dan $$V_{R2}$$ menjadi $$I * R2$$.

$$V_{in} = I * R1 + I * R2$$

Sekarang, kita rapikan persamaan $$V_{in}$$ tersebut menggunakan aljabar:

$$V_{in} = I * (R1 + R2) \Rightarrow I = \frac{V_{in}}{(R1 + R2)}$$

Kembali ke rumus $$V_{out} = I * R2$$, kita bisa substitusikan nilai $$I$$ yang sudah kita dapatkan dari persamaan di atas:

$$V_{out} = I * R2 = \frac{V_{in}}{(R1 + R2)} * R2$$

Terakhir, ubah susunannya agar menjadi bentuk rumus pembagi tegangan yang populer:

$$V_{out} = V_{in} * \frac{R2}{(R1 + R2)}$$

{: .note }
Agar rumus pembagi tegangan ini bisa bekerja dengan akurat, arus $$I$$ yang mengalir lewat $$R_1$$ harus (hampir) sama dengan arus yang mengalir lewat $$R_2$$. Artinya, kalau kita menghubungkan sebuah jalur baru (beban) ke titik $$V_{out}$$, seperti gambar di bawah, maka jalur baru ini harus punya **hambatan yang sangat tinggi** supaya arus tidak bocor atau "rembes" ke jalur tersebut: nilai $$R_{Load}$$ harus jauh lebih besar daripada $$R1 + R2$$. Untungnya, pada pin input mikrokontroler, kondisinya memang *selalu begitu*, yang mana bahasan ini akan kita ulas lagi nanti (contohnya di [pelajaran menggunakan tombol](../arduino/buttons.md)).

![A voltage divider circuit with a load resistor R_Load connected at V_out. An annotation notes that R_Load must be much larger than R1 + R2 for the voltage divider equation to remain accurate.](assets/images/VoltageDividerWithHighResistanceLoad.png)
**Gambar.** Rumus pembagi tegangan hanya berlaku akurat jika $$R_{Load}$$ bernilai sangat besar. Kondisi ini terpenuhi saat kita menggunakan mikrokontroler (karena mikrokontroler membaca perubahan level tegangan dan memiliki fitur bernama "high input impedance").
{: .fs-1 }

<!-- TODO: Khan Academy has a nice derivation of this: https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider -->

<!-- TODO: update diagrams to make this more clear. I like the diagrams by https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider -->

<!-- TODO: add in note here about how VB needs to have no load (or a very small load) -->

<!-- Electronics for beginners has some nice voltage divider examples: https://learning.oreilly.com/library/view/electronics-for-beginners/9781484259795/html/488495_1_En_9_Chapter.xhtml -->

<!-- Another discussion of voltage dividers: https://learning.oreilly.com/library/view/practical-electronics-components/9781449373221/ch01.html  -->

## Resistor paralel

Kalau **resistor seri** dilewati oleh arus yang sama namun tegangannya terbagi, maka [**resistor paralel**](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-parallel-resistors) kebalikannya: tegangannya sama tetapi arusnya terbagi. Bentuk komponen yang disusun paralel terlihat seperti ini:

![Two diagrams showing components in parallel: on the left, a generic representation of three components whose tops all connect at one shared node and bottoms all connect at another shared node; on the right, a circuit schematic with parallel resistors between two nodes.](assets/images/ComponentsInParallel_KhanAcademyAndJonFroehlich.png)

**Gambar.** Komponen dikatakan paralel jika semua bagian "kepala" terhubung di satu titik node yang sama dan semua bagian "ekor" terhubung di titik node bersama lainnya. Gambar kiri bersumber dari [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-parallel-resistors). Gambar dibuat di PowerPoint.
{: .fs-1 }

### Contoh Paralel 1: Cari nilai $$I_{Total}$$

Pada rangkaian di bawah ini, ada dua resistor paralel $$R_1=100Ω$$ dan $$R_2=1kΩ$$. Mari kita cari berapa total arus $$I_{Total}$$ pada rangkaian tersebut.

![A circuit with a 9V battery and two resistors in parallel: R1 = 100 ohms and R2 = 1 kilohm. The total current I_Total is unknown.](assets/images/ParallelResistorCircuit_TwoResistors_ByJonFroehlich.png)

#### Langkah 1: Perhatikan bahwa $$I_{Total}$$ terbagi ke tiap cabang

Hal pertama yang harus disadari adalah bahwa $$I_{Total}$$ akan terbagi ke dua cabang. Mari kita sebut arus yang mengalir di kedua cabang itu sebagai $$I_1$$ dan $$I_2$$. Dari Hukum Kirchhoff, kita tahu kalau $$I_{Total} = I_1 + I_2$$. Fenomena ini terjadi karena adanya hukum kekekalan muatan—tidak ada muatan yang hilang di dalam rangkaian kita (mereka hanya mengalir berputar terus menerus).

![The same parallel circuit with annotations showing I_Total splitting into two branch currents: I1 flowing through R1 and I2 flowing through R2.](assets/images/ParallelResistorCircuit_TwoResistors_Step1_ByJonFroehlich.png)

#### Langkah 2: Identifikasi dan beri nama node (titik sambungan)

Sadarilah juga bahwa hanya ada dua *node* utama di rangkaian kita. Kita bisa beri label mereka $$Node A$$ dan $$Node B$$.

![The parallel circuit with the two nodes labeled: Node A at the top where the branches split, and Node B at the bottom where the branches rejoin.](assets/images/ParallelResistorCircuit_TwoResistors_Step2_ByJonFroehlich.png)

#### Langkah 3: Tentukan Nilai $$V_A$$

Karena $$Node A$$ terhubung langsung ke kutub positif baterai, maka potensi listriknya adalah 9V. Kita sebut saja ini $$V_A = 9V$$. Sebaliknya, $$Node B$$ terhubung langsung ke kutub negatif baterai, jadi kita sebut ini sebagai $$GND$$ atau $$0V$$.

![The parallel circuit with Node A labeled as V_A = 9V and Node B labeled as GND (0V).](assets/images/ParallelResistorCircuit_TwoResistors_Step3_ByJonFroehlich.png)

#### Langkah 4: Hitung nilai $$I_1$$ dan $$I_2$$

Memakai Hukum Ohm, sekarang kita bisa menghitung nilai $$I_1$$ dan $$I_2$$ dengan rumus: $$I_1 = \frac{V_A}{R_1}$$ dan $$I_2 = \frac{V_A}{R_2}$$. Hasilnya, $$I_1 = \frac{9V}{100Ω} \Rightarrow 90mA$$ dan $$I_2 = \frac{9V}{1000Ω} \Rightarrow 9mA$$.

![The parallel circuit with the solved branch currents: I1 = 90 milliamps through R1 (100 ohms) and I2 = 9 milliamps through R2 (1 kilohm).](assets/images/ParallelResistorCircuit_TwoResistors_Step4_ByJonFroehlich.png)

Berhenti sejenak. Coba resapi hasil hitungan ini. Secara *konsep*, masuk akal tidak?

Lewat Hukum Ohm, kita menemukan fakta bahwa arus yang mengalir di cabang $$I_1$$ ukurannya **10 kali lipat** lebih besar daripada arus di cabang $$I_2$$. Dan tebak apa? Angka ini pas banget dengan perbandingan nilai kedua resistor R1 dan R2: R1 nilainya 10 kali lebih kecil dari R2, makanya arus yang mengalir lewat jalur $$I_1$$ jadi jauh lebih lancar dan besar (10x lipat!). Ini sangat logis: sama seperti air yang bakal mengalir lebih deras di pipa yang hambatannya kecil, arus listrik pun akan memilih mengalir lebih banyak ke jalur yang hambatannya minim.

#### Langkah 5: Terakhir, hitung nilai $$I_{Total}$$

Terakhir, kita gunakan rumus $$I_{Total} = I_1 + I_2$$ untuk mendapatkan nilai $$I_{Total}$$. Dalam kasus ini, $$I_{Total} = 90mA + 9mA \Rightarrow 99mA$$.

![The completed parallel circuit analysis showing I1 = 90 milliamps, I2 = 9 milliamps, and I_Total = 99 milliamps.](assets/images/ParallelResistorCircuit_TwoResistors_Step5_ByJonFroehlich.png)

#### Langkah 6: Gunakan rumus hambatan pengganti untuk pembuktian

Remember how we introduced an equation for equivalent resistance in parallel resistor circuits? The equation is:

$$R_{equivalent} = \frac{1}{\frac{1}{R_{1}} + \frac{1}{R_{2}} + ... + \frac{1}{R_{N-1}} + \frac{1}{R_{N}}}$$

Sebagai info tambahan, kalau kamu penasaran bagaimana rumus ini didapatkan, silakan cek [pelajaran Khan Academy ini](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-parallel-resistors)—tapi singkatnya, rumus ini didantikan dari Hukum Ohm (lewat langkah-langkah yang baru saja kita kerjakan di atas).

Kita bisa pakai rumus ini agar bisa mencari $$I_{Total}$$ secara lebih kilat, yaitu $$I_{Total} = \frac{V_A}{R_{equivalent}}$$.

Kita hitung dulu: $${R_{equivalent} = \frac{1}{\frac{1}{100Ω} + \frac{1}{1kΩ}}} \Rightarrow 90.9Ω$$

Maka, $$I_{Total} = \frac{9V}{90.91Ω} \Rightarrow 99mA$$. Hasilnya sama persis!

#### Pembuktian hasil kerja di simulator rangkaian

Kita juga bisa membuktikan hitungan kita lewat simulator rangkaian. Saya sudah membuat rangkaian yang sama di CircuitJS, yang bisa kamu tengok di [sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rxR48UMTSrExVGAjYB3QSGGjsCISPBsATiDW9s2QnvW0wxqmDg7axY4eM07Zi8muL9yzU+MqoCpRp+E14ggXYPUzDbR2DIAM8-TwctRR8vUXSUiJCXXOj4tOcacxi+AXigA).

Apakah visualisasinya sudah sesuai dengan ekspektasimu?

<video autoplay loop muted playsinline aria-label="CircuitJS simulation of a two-resistor parallel circuit with a 9V battery, showing 90 milliamps through the 100 ohm resistor, 9 milliamps through the 1 kilohm resistor, and a total current of 99 milliamps.">
  <source src="assets/videos/SimpleParallelResistorCircuit_9VBattery100And1kOhmResistors_CircuitJSRecording.mp4" type="video/mp4" />
</video>

**Gambar.** Video ini menampilkan simulasi [CircuitJS](https://www.falstad.com/circuit/circuitjs.html) dari rangkaian paralel dua resistor dasar. Kamu bisa mencoba memainkan simulasi rangkaiannya di [sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rxR48UMTSrExVGAjYB3QSGGjsCISPBsATiDW9s2QnvW0wxqmDg7axY4eM07Zi8muL9yzU+MqoCpRp+E14ggXYPUzDbR2DIAM8-TwctRR8vUXSUiJCXXOj4tOcacxi+AXigA).
{: .fs-1 }

{: .note }
> **Trik cepat dua resistor.** Kalau kamu punya **hanya dua** resistor yang disusun paralel, rumus hambatan penggantinya bisa disederhanakan pakai trik cepat "perkalian dibagi penjumlahan" (product over sum):
>
> $$R_{equivalent} = \frac{R_1 \times R_2}{R_1 + R_2}$$
>
> Menggunakan contoh kita tadi: $$R_{equivalent} = \frac{100 \times 1000}{100 + 1000} = \frac{100000}{1100} = 90.9Ω$$. Cara ini jauh lebih gampang dihitung daripada pakai rumus pecahan bertingkat, apalagi kalau lagi coret-coret di kertas. Ingat ya, trik instan ini *hanya* berlaku kalau jumlah resistor paralelnya pas dua biji.

TODO: add in strategy for simplifying: https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-simplifying-resistor-networks -->

## Aktivitas Mandiri

Coba buat dua rancangan rangkaian resistor seri dan dua rangkaian resistor paralel buatanmu sendiri. Berdasarkan materi yang sudah dipelajari, hitung secara manual nilai *arus* pada tiap-tiap rangkaian (boleh coret-coret di kertas atau diketik digital). Tuliskan langkah pengerjaannya tahap demi tahap. Terakhir, buktikan kebenaran hasil hitunganmu dengan membuat simulasinya di [CircuitJS](https://www.falstad.com/circuit/circuitjs.html).

Di dalam jurnal prototipe kalian, sertakan gambar sketsa rangkaian (boleh foto coretan kertas pakai HP), langkah manual kalian saat mencari nilai arus $$I$$ (sekali lagi, boleh foto coretan kertas), serta screenshot visual dari rangkaian di [CircuitJS](https://www.falstad.com/circuit/circuitjs.html) lengkap dengan link langsungnya. (Sebagai pengingat, kamu bisa menyalin link CircuitJS lewat menu File -> Export as Link).

## Sumber Belajar Tambahan

* [Resistors in series and parallel](https://opentextbc.ca/universityphysicsv2openstax/chapter/resistors-in-series-and-parallel/), opentextbc.ca
* [Series and Parallel Resistors](https://www.khanacademy.org/science/ap-physics-1/ap-circuits-topic/series-circuits-ap/v/ee-series-resistors), Khan Academy
* [Voltage Divider](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider), Khan Academy
* [Circuit Analysis Shortcuts](https://courses.engr.illinois.edu/ece110/sp2021/content/courseNotes/files/?circuitAnalysisShortcuts), UIUC ECE110
* [Chapter 9.3 Voltage Divider Pattern](https://learning.oreilly.com/library/view/electronics-for-beginners/9781484259795/html/488495_1_En_9_Chapter.xhtml), Bartlett, Electronics for Beginners, APress 2020

<!-- The UIUC lab page "Module 100: The Voltage Divider" has a nice description: https://courses.engr.illinois.edu/ece110/sp2021/content/labs/Modules/M100_Voltage%20Divider.pdf -->

<!-- TODO: Engineering Mindset has a nice [animation](https://youtu.be/kcL2_D33k3o?t=858) of differences between series and parallel -->

## Pelajaran Berikutnya

Di [pelajaran selanjutnya](resistors.md), kita akan membedah lebih dalam seputar komponen resistor, mulai dari bagaimana komponen ini diproduksi, tips pemakaiannya, cara membaca karakteristiknya, hingga rumus menghitung disipasi dayanya (power dissipation).

<nav class="lesson-nav" aria-label="Lesson navigation">
  <a href="ohms-law.html" class="nav-prev">
    <div class="nav-label">&larr; Pelajaran Sebelumnya</div>
    <div class="nav-title">Hukum Ohm</div>
  </a>
  <a href="resistors.html" class="nav-next">
    <div class="nav-label">Pelajaran Berikutnya &rarr;</div>
    <div class="nav-title">Resistor</div>
  </a>
</nav>