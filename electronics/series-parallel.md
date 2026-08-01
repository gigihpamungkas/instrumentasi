---
layout: default
title: L4&#58; Resistor Seri dan Paralel
description: "Kembangkan Hukum Ohm ke rangkaian resistor seri dan paralel: resistor seri membagi tegangan, resistor paralel membagi arus, lengkap dengan rumus hambatan pengganti dan CircuitJS."
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

## Daftar Isi
{: .no_toc .text-delta }

1. TOC
{:toc}
---

Dalam pelajaran Hukum Ohm, kita telah menganalisis rangkaian yang relatif sederhana dengan satu resistor. Rangkaian tersebut membantu kita membangun fondasi dan pemahaman konseptual tentang Hukum Ohm serta cara menerapkannya; namun, sebagian besar rangkaian tidak sesederhana itu.

Dalam pelajaran ini, kita akan mengembangkan Hukum Ohm ke rangkaian yang lebih rumit: resistor dalam hubungan **seri** dan resistor dalam hubungan **paralel**. Singkatnya:
* Resistor seri **membagi tegangan** dan merupakan salah satu konfigurasi rangkaian yang paling umum (dan berguna) saat bekerja dengan mikrokontroler dan sensor resistif seperti [potensiometer](../arduino/potentiometers.md), [resistor sensor tekanan (FSR)](../arduino/force-sensitive-resistors.md), dan [fotocell/LDR](../sensors/photoresistors.md).
* Resistor paralel **membagi arus** (dan arus yang lebih besar akan mengalir melalui jalur dengan hambatan yang lebih kecil). Rangkaian paralel berguna, misalnya, untuk memberi daya pada beberapa LED sekaligus.

![Two circuit diagrams side by side: on the left, a series resistor circuit with R1 and R2 connected end-to-end in a single loop with a battery; on the right, a parallel resistor circuit with R1 and R2 on separate branches sharing the same two nodes.](assets/images/OhmsLaw_IntroToSeriesVsParallelResistorCircuits_ByJonFroehlich.png)
**Gambar.** Contoh resistor **seri** (kiri) dan resistor **paralel** (kanan). Gambar dibuat di PowerPoint.
{: .fs-1 }

## Hambatan pengganti

Menggunakan [Hukum rangkaian Kirchhoff](https://en.wikipedia.org/wiki/Kirchhoff%27s_circuit_laws), kita dapat menurunkan nilai hambatan "pengganti" (ekuivalen) untuk rangkaian seri dan paralel.

Untuk resistor seri, kita menjumlahkan nilai hambatan untuk menemukan total hambatan $$R_{equivalent}$$:

$$R_{equivalent} = R_{1} + R_{2} + ... + R_{N-1} + R_{N}$$

Untuk resistor paralel, rumusnya sedikit lebih rumit:

$$R_{equivalent} = \frac{1}{\frac{1}{R_{1}} + \frac{1}{R_{2}} + ... + \frac{1}{R_{N-1}} + \frac{1}{R_{N}}}$$

Ya, persamaan hambatan paralel ini memang terlihat agak misterius, tetapi Anda dapat menurunkannya sendiri (atau bahkan melupakannya sama sekali) jika Anda memahami Hukum Ohm dan [Hukum Kirchhoff](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/v/ee-kirchhoffs-current-law).

Bagi kita, konsep paling penting dan berguna untuk dipahami adalah bahwa **resistor seri** membagi tegangan (kita akan menggunakan ini nanti pada rangkaian mikrokontroler kita) dan bahwa **resistor paralel** membagi arus (dengan arus yang *lebih besar* mengalir melalui cabang yang memiliki hambatan lebih kecil). Gambar di bawah ini mencoba menjelaskan hal tersebut secara ringkas.

![A detailed comparison of series and parallel resistor circuits. The series circuit (left) shows that current is the same through each resistor but voltage is divided proportionally across them. The parallel circuit (right) shows that voltage is the same across each branch but current is divided, with more current flowing through the branch with lower resistance.](assets/images/OhmsLaw_IntroToSeriesVsParallelResistorCircuits_PictorialDiagram_ByJonFroehlich.png)

**Gambar.** Gambaran umum tentang cara kerja **resistor seri** (arus sama di setiap resistor tetapi *tegangan dibagi*) dan cara kerja **resistor paralel** (tegangan sama di setiap resistor tetapi *arus dibagi*). Luangkan waktu sejenak untuk mempelajari dan memahami mengapa hal ini bisa terjadi. Klik kanan pada gambar dan pilih 'Buka di tab baru' untuk memperbesar. Gambar dibuat di PowerPoint.
{: .fs-1 }

Dan, meskipun kemampuan untuk memahami dan menganalisis rangkaian secara manual itu penting dalam physical computing, jika Anda bingung, Anda selalu bisa menggunakan simulator rangkaian seperti [CircuitJS](https://www.falstad.com/circuit/circuitjs.html).

## Resistor seri

[Resistor dalam hubungan seri](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-series-resistors) terhubung secara berurutan: ujung ketemu pangkal.

![Two diagrams showing components in series: on the left, a generic representation of three components connected end-to-end in a single path; on the right, a circuit schematic with resistors arranged head-to-tail between a voltage source.](assets/images/ComponentsInSeries_KhanAcademyAndJonFroehlich.png)

**Gambar.** Komponen dikatakan seri jika mereka digabungkan ujung-ke-ujung (atau kepala-ke-ekor) secara berurutan seperti di atas. Gambar di sebelah kiri dari [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-series-resistors). Gambar dibuat di PowerPoint.
{: .fs-1 }

Dari Hukum Ohm, kita tahu bahwa resistor mengakibatkan *penurunan* tegangan (memang, penurunan tegangan $$V_{R}$$ pada sebuah resistor $$R$$ adalah $$V_{R} = I * R$$). Dengan demikian, beberapa resistor yang dipasang "berderet" (seri) masing-masing akan menyebabkan penurunan tegangan—dan besarnya penurunan ini sebanding dengan nilai resistornya (makin besar hambatan, makin besar penurunan tegangan).

Umumnya, ketika kita mencoba menganalisis rangkaian dengan beberapa konfigurasi resistor (seri, paralel, atau kombinasi), langkah pertama adalah menentukan **hambatan pengganti**. Yaitu, bagaimana kita bisa menggabungkan semua hambatan dalam rangkaian menjadi satu nilai tunggal (disebut $$R_{total}$$ atau $$R_{equivalent}$$) yang memungkinkan kita menerapkan Hukum Ohm di seluruh rangkaian. Dalam kasus mencari arus, rumusnya menjadi $$I=\frac{V}{R_{total}}$$

Jadi, mari kita coba!

### Contoh seri 1: Mencari nilai arus

Mari kita mulai dengan rangkaian resistor seri yang paling sederhana: sebuah baterai 9V dengan resistor 100Ω dan 1kΩ yang terhubung seri.

![A circuit with a 9V battery and two resistors in series: R1 = 100 ohms and R2 = 1 kilohm. The current I through the circuit is unknown.](assets/images/SeriesResistorCircuit_TwoResistorsOf100OhmAnd1kOhm_Step0.png)

**Gambar.** Rangkaian sederhana dengan dua resistor seri (100Ω dan 1kΩ) dan baterai 9V. Berapa besar arus $$I$$ yang mengalir melalui rangkaian ini?
{: .fs-1 }

#### Langkah 1: Mencari total hambatan

Langkah pertama adalah mencari total hambatan dalam rangkaian kita. Kita tahu bahwa kita menjumlahkan hambatan dalam hubungan seri, jadi: $$R_{Total} = R_{1} + R_{2} \Rightarrow 100Ω + 1000Ω \Rightarrow 1100Ω$$. Total hambatannya adalah $$1100Ω$$.

![The same two-resistor series circuit, now showing the two resistors combined into a single equivalent resistor R_Total = 1100 ohms.](assets/images/SeriesResistorCircuit_TwoResistorsOf100OhmAnd1kOhm_Step1.png)

**Gambar.** Untuk menemukan hambatan pengganti dari rangkaian ini (mari kita sebut sebagai $$R_{Total}$$), kita dapat menggabungkan resistor seri dengan cara menjumlahkannya.
{: .fs-1 }

#### Langkah 2: Mencari arus I dengan hambatan pengganti

Sekarang kita dapat menggunakan nilai hambatan pengganti $$R_{Total}$$ ini untuk mencari arus $$I$$ dengan menggunakan Hukum Ohm: $$I=9V/1100Ω \Rightarrow 0.0082A \Rightarrow 8.2mA$$

![The simplified circuit showing the equivalent resistance of 1100 ohms with the solved current I = 8.2 milliamps flowing through the circuit.](assets/images/SeriesResistorCircuit_TwoResistorsOf100OhmAnd1kOhm_Step2.png)

**Gambar.** Kita sekarang mencari arus $$I$$ secara sederhana dengan Hukum Ohm: $$I=9V/1100Ω \Rightarrow 8.2mA$$
{: .fs-1 }

Selesai. Kita berhasil! Total arusnya adalah $$I = 8.2mA$$.

### Contoh seri 2: Mencari nilai arus

Untuk memperkuat pemahaman, mari kita coba lagi tetapi dengan tiga resistor, bukan dua. Kali ini, $$R_{1}=2.2kΩ$$, $$R_{2}=1kΩ$$, dan $$R_{3}=470Ω$$.

Sekali lagi, kita mulai dengan mencari $$R_{Total}$$, yaitu:

$$R_{Total} = R_{1} + R_{2} + R_{3} \\
R_{Total} = 2200Ω + 1000Ω + 470Ω \\
R_{Total} = 3670Ω$$

Kita kemudian dapat menggunakan nilai hambatan pengganti ini untuk mencari arus $$I$$, yaitu $$I=\frac{9V}{3670Ω} \Rightarrow 0.002452A \Rightarrow 2.45mA$$.

![A series circuit with three resistors (2.2 kilohms, 1 kilohm, and 470 ohms) and a 9V battery. The resistors are combined into R_Total = 3670 ohms, and the solved current is I = 2.45 milliamps.](assets/images/SeriesResistorCircuit_ThreeResistors_Solved.png)

**Gambar.** Pada gambar di atas, kita mencari arus dengan tiga resistor seri. Pertama, jumlahkan hambatan-hambatan tersebut (karena terhubung seri) lalu gunakan total hambatan ($$R_{Total}$$) ini untuk menentukan arus dengan Hukum Ohm: $$I=\frac{V}{R_{Total}} \Rightarrow \frac{9V}{3670Ω} \Rightarrow 2.45mA$$ (dibulatkan menjadi 2.5mA pada gambar).
{: .fs-1 }

#### Memeriksa hasil kerja kita di simulator rangkaian

Kita bisa memeriksa hasil kerja kita di simulator rangkaian favorit kita, bebas apa saja yang Anda suka. :)

Saya akan menggunakan alat sumber terbuka [CircuitJS](https://www.falstad.com/circuit/circuitjs.html). Simulasi spesifiknya ada [di sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rzCEqo2lWJQpMBGwDug8CIoo8SquwBOKtWAyEdIFAgNUUaSG20JVRjLxtrsNqWHhXD2Qmse0aaqhoMSwUwHj4BXxp+cHlDYSpfPQMUON9jA3T7IzTbZwc87xyFKP9DaIFUoA).

Kita bisa mengklik kabel untuk secara ajaib menampilkan berapa banyak arus yang mengalir melaluinya atau untuk menunjukkan potensial listriknya (tegangan) terhadap ground. Dan benar saja, Anda akan melihat bahwa memang $$2.5mA$$ mengalir melalui rangkaian tersebut. Apa lagi yang Anda amati?

Nah, ingat bagaimana kita terus menekankan bahwa tegangan itu *terbagi* atau *dipecah* pada resistor-resistor yang terhubung seri. Anda dapat melihat ini dengan jelas juga! Tegangan berada pada $$9V$$ di simpul atas tetapi turun sebesar $$5.4V$$ setelah melewati resistor $$2.2kΩ$$ menjadi $$3.6V$$, yang kemudian turun lagi sebesar $$2.4V$$ setelah melewati resistor $$1kΩ$$ sehingga hanya menyisakan potensial listrik sebesar $$1.2V$$ sebelum akhirnya turun menjadi $$0V$$ atau $$GND$$ setelah melewati resistor $$470Ω$$. Kita akan membahas lebih banyak tentang ini selanjutnya!

<video autoplay loop muted playsinline aria-label="CircuitJS simulation of a three-resistor series circuit with a 9V battery, showing animated current flow of 2.5 milliamps and voltage drops across each resistor.">
  <source src="assets/videos/SeriesResistorThreeResistors9VBattery2.2k1k470_CircuitJSRecording.mp4" type="video/mp4" />
</video>

**Gambar.** Video ini menunjukkan simulasi [CircuitJS](https://www.falstad.com/circuit/circuitjs.html) dari rangkaian seri dasar tiga resistor. Anda dapat mencoba rangkaian ini [di sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rzCEqo2lWJQpMBGwDug8CIoo8SquwBOKtWAyEdIFAgNUUaSG20JVRjLxtrsNqWHhXD2Qmse0aaqhoMSwUwHj4BXxp+cHlDYSpfPQMUON9jA3T7IzTbZwc87xyFKP9DaIFUoA).
{: .fs-1 }

## Pembagi tegangan (Voltage Divider)

Gagasan bahwa **resistor seri** membagi tegangan adalah konsep yang sangat penting saat bekerja dengan mikrokontroler. Oleh karena itu, hal ini layak mendapatkan penekanan tersendiri.

Hal utama yang perlu diingat: ada *penurunan tegangan* di setiap resistor (ini selalu terjadi, tidak hanya dalam konfigurasi rangkaian seri). Jadi, di antara setiap resistor kita memiliki *potensial listrik* atau tegangan yang berbeda. Dan karena mikrokontroler "membaca" tegangan alih-alih arus, kita dapat menggunakan sifat ini untuk mengontrol input dinamis ke dalam mikrokontroler kita!

Mari kita bahas beberapa contoh.

### Contoh 1: Mencari tegangan pada VB

Dengan ide tentang tegangan yang turun di setiap resistor ini, mari kita lihat bagaimana cara menghitung tegangan pada simpul $$V_{B}$$ terhadap ground (dan ingat, simpul/node adalah titik pertemuan mana pun dengan dua atau lebih sambungan dalam sebuah rangkaian).

Sebelum melanjutkan ke contoh kita, berhenti sejenak dan tanyakan pada diri Anda: bagaimana Anda akan menghitung tegangan pada $$V_{B}$$?

![A series circuit with a 9V battery, R1 = 100 ohms, and R2 = 150 ohms. The node between the two resistors is labeled V_B, and the question asks: what is the voltage at V_B?](assets/images/VoltageDivider_100And150_ByJonFroehlich.png)

#### Langkah 1: Cari arus yang mengalir melalui rangkaian

Seperti sebelumnya, langkah pertama adalah mencari arus yang mengalir melalui rangkaian. Kita melakukan ini, sekali lagi, dengan mencari hambatan pengganti $$R_{Total}$$ dan menggunakan Hukum Ohm. Jadi, $$I=\frac{V}{R_{Total}} \Rightarrow \frac{9V}{250Ω} \Rightarrow 36mA$$.

![The same voltage divider circuit now showing R_Total = 250 ohms and the solved current I = 36 milliamps.](assets/images/VoltageDivider_100And150_Step1_ByJonFroehlich.png)

#### Langkah 2: Hitung penurunan tegangan pada masing-masing resistor

Seknow setelah kita mengetahui total arus yang mengalir melalui rangkaian kita ($$36mA$$), kita dapat menggunakannya untuk menghitung penurunan tegangan spesifik di setiap resistor. Mari kita sebut penurunan tegangan pada $$R_{1}$$ sebagai $$V_{1}$$ dan penurunan tegangan pada $$R_{2}$$ sebagai $$V_{2}$$. Dan karena kita tertarik untuk menghitung tegangan, kita akan menggunakan rumusan Hukum Ohm ini: $$V = I * R$$.

Maka:

$$
{V_1} = I * R_1 \Rightarrow 0.036A * 100Ω \Rightarrow 3.6V \\
{V_2} = I * R_2 \Rightarrow 0.036A * 150Ω \Rightarrow 5.4V
$$

Dan, sekadar memeriksa cepat hasil kerja kita (tanpa membahas terlalu detail), kita tahu dari [Hukum rangkaian Kirchhoff](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-kirchhoffs-laws), bahwa $$V_{Total} = V_1 + V_2 \Rightarrow 9V = 3.6V + 5.4V \Rightarrow 9V = 9V$$. Jadi, sejauh ini semuanya terlihat benar!

![The voltage divider circuit with annotations showing the voltage drop V1 = 3.6V across R1 and V2 = 5.4V across R2, with the current I = 36 milliamps labeled.](assets/images/VoltageDivider_100And150_Step2_ByJonFroehlich.png)

#### Langkah 3: Sekarang hitung VB

Sekarang sangat mudah untuk menghitung $$V_B$$. Kita tahu bahwa $$V_A = 9V$$ dan $$R_1$$ menyebabkan penurunan tegangan sebesar $$3.6V$$. Jadi, $$V_B$$ harus sama dengan $$9V - 3.6V$$, yaitu 5.4V.

![The completed voltage divider analysis showing V_A = 9V at the top, a 3.6V drop across R1, and V_B = 5.4V at the node between the two resistors.](assets/images/VoltageDivider_100And150_Step3_ByJonFroehlich.png)

### Pola pembagi tegangan

Kita menyebut konfigurasi dua resistor seperti ini sebagai **pembagi tegangan** (voltage divider) tepat karena, seperti yang Anda lihat, konfigurasi ini membagi tegangan. Dalam kasus ini, kita menggunakan resistor $$100Ω$$ dan $$150Ω$$ seri untuk menghasilkan output $$5.4V$$ pada $$V_B$$.

Menggunakan Hukum Ohm, kita dapat [menurunkan persamaan pembagi tegangan](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider) untuk $$V_B$$ berdasarkan tegangan input ($$V_A$$) ke dalam jaringan pembagi tegangan kita dan kedua resistor tersebut: resistor atas $$R_1$$ dan resistor bawah $$R_2$$.

Persamaan pembagi tegangan ini adalah:
$$V_{B} = V_{A} * \frac{R_2}{R_1 + R_2}$$

Atau lebih umum ditulis sebagai:
$$V_{out} = V_{in} * \frac{R_2}{R_1 + R_2}$$

![A generic voltage divider schematic showing V_in at the top, R1 and R2 in series, V_out at the node between R1 and R2, and the voltage divider equation V_out = V_in times R2 divided by (R1 + R2).](assets/images/VoltageDividerBasic_ByJonFroehlich.png)

**Gambar.** Pola dan persamaan pembagi tegangan. Gambar dibuat di PowerPoint. Lihat [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider) untuk informasi lebih lanjut.
{: .fs-1 }

Yang penting, seperti yang dapat Anda ketahui dari persamaan tersebut, bukanlah nilai hambatan absolut yang menentukan melainkan **rasio** antara $$R_1$$ dan $$R_2$$ yang mengontrol $$V_{out}$$. Oleh karena itu, untuk tujuan *membagi tegangan*, memilih $$R_1 = 100Ω$$ and $$R_2 = 100Ω$$ akan sama saja dengan $$R_1 = 2.2kΩ$$ and $$R_2 = 2.2kΩ$$, keduanya akan membagi tegangan sama rata. Jadi, $$V_{out}$$ akan sama dengan $$4.5V$$ jika $$V_{in}=9V$$.

Namun, jumlah arus di antara kedua rangkaian tersebut akan sangat berbeda, pada opsi pertama: $$I = \frac{9V}{200Ω} \Rightarrow 45mA$$ dan opsi kedua: $$I = \frac{9V}{4.4kΩ} \Rightarrow 2.0mA$$.

{: .note }
> **Toleransi di Dunia Nyata dan Pembagi Tegangan.** Dalam perhitungan matematika kita, kita mengasumsikan resistor kita benar-benar sempurna. Namun ingat bahwa resistor fisik memiliki nilai **toleransi**! 
>
> Jika Anda membuat pembagi tegangan 50/50 menggunakan dua resistor 10kΩ dengan peringkat toleransi ±5%, satu resistor mungkin sebenarnya terukur 9.5kΩ dan yang lainnya 10.5kΩ. Karena ketidakseimbangan kecil ini, tegangan output dunia nyata Anda tidak akan *tepat* setengah dari tegangan input Anda. Jika Anda mengukur rangkaian fisik Anda dengan multimeter dan angkanya sedikit melesat dari teori matematika Anda, toleransi komponen hampir pasti merupakan penyebabnya!

Bukankah akan keren jika kita bisa mengontrol salah satu nilai resistor tersebut secara dinamis untuk menghasilkan tegangan variabel pada $$V_{out}$$? Ya! Dan inilah dasar dari sebuah [potensiometer](variable-resistors.md), yang akan kita pelajari pada pelajaran selanjutnya.

### Mengapa pembagi tegangan penting untuk physical computing?

Mikrokontroler seperti Arduino hanya dapat "membaca" tingkat tegangan (melalui pengubah analog-ke-digital atau ADC mereka), bukan hambatan secara langsung. Jadi, ketika kita menggunakan sensor resistif seperti fotosel (LDR), resistor sensor tekanan (FSR), atau termistor, kita menempatkannya dalam konfigurasi pembagi tegangan. Seiring berubahnya hambatan sensor sebagai respons terhadap cahaya, tekanan, atau suhu, tegangan pada $$V_{out}$$ berubah secara proporsional—dan *itulah* yang dibaca oleh mikrokontroler. Anda akan melihat pola ini berulang kali mulai dari [pelajaran Arduino](../arduino/index.md).

#### Menurunkan persamaan pembagi tegangan

Mengingat apa yang Anda pelajari tentang rangkaian, Anda sekarang memiliki pengetahuan untuk menurunkan persamaan pembagi tegangan atau, setidaknya, memahami *how* persamaan itu diturunkan. Mari kita lihat!

![A step-by-step algebraic derivation of the voltage divider equation, starting from Ohm's Law and Kirchhoff's Voltage Law, arriving at V_out = V_in times R2 divided by (R1 + R2).](assets/images/DerivingTheVoltageDividerEquation_ByJonFroehlich.png)
**Gambar.** Penurunan persamaan pembagi tegangan. Lihat [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider) untuk informasi lebih lanjut.
{: .fs-1 }

Menggunakan gambar di atas, mari kita identifikasi dan tulis apa yang kita ketahui. Kita tahu bahwa penurunan tegangan pada $$R2$$ sama dengan $$V_{out}$$ (memang, keduanya adalah hal yang sama) dan bahwa $$V_R2=I*R2$$:

$$V_{out} = V_{R2} = I * R2$$

Kita juga tahu bahwa $$V_{in}$$ sama dengan $$V_R1 + V_R2$$ berdasarkan [Hukum Tegangan Kirchhoff](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-kirchhoffs-laws).

$$V_{in} = V_{R1} + V_{R2}$$

Menggunakan Hukum Ohm, kita dapat mengganti $$I * R1$$ untuk $$V_{R1}$$ dan $$I * R2$$ untuk $$V_{R2}$$.

$$V_{in} = I * R1 + I * R2$$

Sekarang, atur ulang persamaan $$V_{in}$$ menggunakan aljabar:

$$V_{in} = I * (R1 + R2) \Rightarrow I = \frac{V_{in}}{(R1 + R2)}$$

Kembali ke $$V_{out} = I * R2$$, kita dapat menyubstitusikan $$I$$ berdasarkan rumusan di atas:

$$V_{out} = I * R2 = \frac{V_{in}}{(R1 + R2)} * R2$$

Terakhir, atur ulang persamaan di atas untuk mendapatkan persamaan pembagi tegangan yang populer:

$$V_{out} = V_{in} * \frac{R2}{(R1 + R2)}$$

{: .note }
Agar persamaan pembagi tegangan ini tetap berlaku, arus $$I$$ yang mengalir melalui $$R_1$$ harus (secara garis besar) sama dengan arus yang mengalir melalui $$R_2$$. Artinya, jika kita menghubungkan sebuah cabang ke $$V_{out}$$, seperti yang telah kita lakukan di bawah ini, maka cabang ini harus memiliki **hambatan yang sangat tinggi** sehingga sangat sedikit arus yang "bocor" ke cabang tersebut: $$R_{Load}$$ harus beberapa kali lipat lebih besar daripada $$R1 + R2$$. Dalam kasus pin input mikrokontroler, *untungnya* hal ini terpenuhi, yang akan kita bahas kembali nanti (*misalnya*, dalam [pelajaran "Menggunakan tombol"](../arduino/buttons.md)).

![A voltage divider circuit with a load resistor R_Load connected at V_out. An annotation notes that R_Load must be much larger than R1 + R2 for the voltage divider equation to remain accurate.](assets/images/VoltageDividerWithHighResistanceLoad.png)
**Gambar.** Persamaan pembagi tegangan hanya berlaku ketika $$R_{Load}$$ bernilai besar, keadaan yang akan terpenuhi ketika kita mulai menggunakan mikrokontroler (yang membaca perubahan level tegangan dan memiliki "impedansi input tinggi").
{: .fs-1 }

<!-- TODO: Khan Academy has a nice derivation of this: https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider -->

<!-- TODO: update diagrams to make this more clear. I like the diagrams by https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider -->

<!-- TODO: add in note here about how VB needs to have no load (or a very small load) -->

<!-- Electronics for beginners has some nice voltage divider examples: https://learning.oreilly.com/library/view/electronics-for-beginners/9781484259795/html/488495_1_En_9_Chapter.xhtml -->

<!-- Another discussion of voltage dividers: https://learning.oreilly.com/library/view/practical-electronics-components/9781449373221/ch01.html  -->

## Resistor paralel

Jika **resistor seri** mengalirkan arus yang sama tetapi membagi tegangan, [**resistor paralel**](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-parallel-resistors) memiliki tegangan yang sama tetapi membagi arus. Komponen dalam hubungan paralel terlihat seperti ini:

![Two diagrams showing components in parallel: on the left, a generic representation of three components whose tops all connect at one shared node and bottoms all connect at another shared node; on the right, a circuit schematic with parallel resistors between two nodes.](assets/images/ComponentsInParallel_KhanAcademyAndJonFroehlich.png)

**Gambar.** Komponen dikatakan paralel jika kepala mereka berbagi satu simpul dan ekor mereka berbagi simpul yang lain. Gambar di sebelah kiri dari [Khan Academy](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-parallel-resistors). Gambar dibuat di PowerPoint.
{: .fs-1 }

### Contoh paralel 1: Mencari $$I_{Total}$$

Pada rangkaian di bawah ini, kita memiliki dua resistor paralel $$R_1=100Ω$$ and $$R_2=1kΩ$$. Mari kita cari total arus $$I_{Total}$$ dalam rangkaian tersebut.

![A circuit with a 9V battery and two resistors in parallel: R1 = 100 ohms and R2 = 1 kilohm. The total current I_Total is unknown.](assets/images/ParallelResistorCircuit_TwoResistors_ByJonFroehlich.png)

#### Langkah 1: Amati bahwa $$I_{Total}$$ terbagi ke dalam cabang-cabang

Hal pertama yang harus disadari adalah bahwa $$I_{Total}$$ terbagi menjadi dua cabang. Mari kita sebut arus yang turun ke kedua cabang tersebut sebagai $$I_1$$ dan $$I_2$$. Dari Hukum Kirchhoff, kita tahu bahwa $$I_{Total} = I_1 + I_2$$. Hal ini dikarenakan hukum kekekalan muatan—tidak ada muatan yang hilang dalam rangkaian kita (mereka hanya mengalir berputar terus-menerus).

![The same parallel circuit with annotations showing I_Total splitting into two branch currents: I1 flowing through R1 and I2 flowing through R2.](assets/images/ParallelResistorCircuit_TwoResistors_Step1_ByJonFroehlich.png)

#### Langkah 2: Identifikasi dan beri nama simpul (node)

Sadarilah juga bahwa hanya ada dua *simpul* di dalam rangkaian kita. Kita dapat memberi label pada mereka sebagai $$Simpul A$$ dan $$Simpul B$$.

![The parallel circuit with the two nodes labeled: Node A at the top where the branches split, and Node B at the bottom where the branches rejoin.](assets/images/ParallelResistorCircuit_TwoResistors_Step2_ByJonFroehlich.png)

#### Langkah 3: Tentukan $$V_A$$

Karena $$Simpul A$$ terhubung langsung ke terminal positif baterai, simpul ini memiliki potensial listrik sebesar 9V. Mari kita sebut ini sebagai $$V_A = 9V$$. Demikian pula, $$Simpul B$$ terhubung langsung ke terminal negatif baterai, jadi mari kita sebut ini sebagai $$GND$$ atau $$0V$$.

![The parallel circuit with Node A labeled as V_A = 9V and Node B labeled as GND (0V).](assets/images/ParallelResistorCircuit_TwoResistors_Step3_ByJonFroehlich.png)

#### Langkah 4: Cari nilai $$I_1$$ dan $$I_2$$

Menggunakan Hukum Ohm, sekarang kita dapat mencari $$I_1$$ dan $$I_2$$ di mana: $$I_1 = \frac{V_A}{R_1}$$ dan $$I_2 = \frac{V_A}{R_2}$$. Maka, $$I_1 = \frac{9V}{100Ω} \Rightarrow 90mA$$ dan $$I_2 = \frac{9V}{1000Ω} \Rightarrow 9mA$$.

![The parallel circuit with the solved branch currents: I1 = 90 milliamps through R1 (100 ohms) and I2 = 9 milliamps through R2 (1 kilohm).](assets/images/ParallelResistorCircuit_TwoResistors_Step4_ByJonFroehlich.png)

Berhenti sejenak. Pikirkan hasil-hasil ini. Apakah secara *konseptual* masuk akal?

Menggunakan Hukum Ohm, kita menemukan bahwa arus yang mengalir melalui cabang $$I_1$$ adalah **10 kali** lebih banyak daripada cabang $$I_2$$. Tentu saja, ini sangat cocok dengan rasio kedua resistor R1 dan R2: R1 bernilai 10 kali lebih kecil dari R2 dan karena itu, arus yang mengalir melalui cabang $$I_1$$ akan lebih banyak (10x lebih banyak!). Ini masuk akal: sama seperti air yang akan mengalir lebih banyak melalui cabang yang memiliki hambatan lebih kecil, begitu pula arus listrik akan mengalir lebih banyak melalui jalur yang hambatannya lebih kecil.

#### Langkah 5: Terakhir, cari nilai $$I_{Total}$$

Terakhir, kita dapat menggunakan $$I_{Total} = I_1 + I_2$$ to solve for $$I_{Total}$$. Dalam kasus ini, $$I_{Total} = 90mA + 9mA \Rightarrow 99mA$$.

![The completed parallel circuit analysis showing I1 = 90 milliamps, I2 = 9 milliamps, and I_Total = 99 milliamps.](assets/images/ParallelResistorCircuit_TwoResistors_Step5_ByJonFroehlich.png)

#### Langkah 6: Gunakan hambatan pengganti untuk memeriksa hasil kerja kita

Ingat bagaimana kita memperkenalkan persamaan untuk hambatan pengganti pada rangkaian resistor paralel? Persamaannya adalah:

$$R_{equivalent} = \frac{1}{\frac{1}{R_{1}} + \frac{1}{R_{2}} + ... + \frac{1}{R_{N-1}} + \frac{1}{R_{N}}}$$

Sebagai catatan sampingan, jika Anda penasaran dengan penurunannya, lihat [pelajaran Khan Academy ini](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-parallel-resistors)—tetapi, singkatnya, Anda dapat menurunkannya dari Hukum Ohm (dan langkah-langkah yang kita ikuti di atas).

Kita dapat menggunakan persamaan ini untuk mencari $$I_{Total}$$ secara lebih cepat, yaitu $$I_{Total} = \frac{V_A}{R_{equivalent}}$$.

Kita tahu bahwa $${R_{equivalent} = \frac{1}{\frac{1}{100Ω} + \frac{1}{1kΩ}}} \Rightarrow 90.9Ω$$

Maka, $$I_{Total} = \frac{9V}{90.91Ω} \Rightarrow 99mA$$.

#### Memeriksa hasil kerja kita di simulator rangkaian

Kita juga bisa memeriksa hasil kerja kita di simulator rangkaian. Saya membuat rangkaian yang sama di CircuitJS, yang dapat Anda lihat [di sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rxR48UMTSrExVGAjYB3QSGGjsCISPBsATiDW9s2QnvW0wxqmDg7axY4eM07Zi8muL9yzU+MqoCpRp+E14ggXYPUzDbR2DIAM8-TwctRR8vUXSUiJCXXOj4tOcacxi+AXigA).

Apakah visualisasinya sesuai dengan ekspektasi Anda?

<video autoplay loop muted playsinline aria-label="CircuitJS simulation of a two-resistor parallel circuit with a 9V battery, showing 90 milliamps through the 100 ohm resistor, 9 milliamps through the 1 kilohm resistor, and a total current of 99 milliamps.">
  <source src="assets/videos/SimpleParallelResistorCircuit_9VBattery100And1kOhmResistors_CircuitJSRecording.mp4" type="video/mp4" />
</video>

**Gambar.** Video ini menunjukkan simulasi [CircuitJS](https://www.falstad.com/circuit/circuitjs.html) dari rangkaian paralel dasar dua resistor. Anda dapat mencoba rangkaian ini [di sini](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgA3cYlWwm7rxR48UMTSrExVGAjYB3QSGGjsCISPBsATiDW9s2QnvW0wxqmDg7axY4eM07Zi8muL9yzU+MqoCpRp+E14ggXYPUzDbR2DIAM8-TwctRR8vUXSUiJCXXOj4tOcacxi+AXigA).
{: .fs-1 }

{: .note }
> **Jalur pintas dua resistor.** Ketika Anda memiliki tepat dua resistor dalam hubungan paralel, rumus hambatan pengganti menyusut menjadi rumus pintas "perkalian dibagi penjumlahan":
>
> $$R_{equivalent} = \frac{R_1 \times R_2}{R_1 + R_2}$$
>
> Untuk contoh kita: $$R_{equivalent} = \frac{100 \times 1000}{100 + 1000} = \frac{100000}{1100} = 90.9Ω$$. Ini jauh lebih mudah dihitung daripada bentuk kebalikan-dari-kebalikan, terutama di atas kertas. Perhatikan bahwa jalur pintas ini hanya berlaku untuk tepat dua resistor secara paralel.

TODO: add in strategy for simplifying: https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-simplifying-resistor-networks -->

## Aktivitas

Buatlah dua buah rangkaian resistor seri dan dua buah rangkaian resistor paralel. Dengan menggunakan apa yang telah Anda pelajari, cari nilai *arus* pada masing-masing rangkaian secara manual (baik menggunakan pensil+kertas atau secara digital). Tunjukkan pengerjaan langkah demi langkah Anda. Periksa hasil kerja Anda dengan membuat simulasi di [CircuitJS](https://www.falstad.com/circuit/circuitjs.html).

Di dalam jurnal prototyping Anda, sertakan sketsa rangkaian (bisa berupa foto smartphone dari kertas+pensil), pengerjaan manual Anda untuk mencari arus $$I$$ (sekali lagi, bisa berupa kertas+pensil), dan tangkapan layar dari rangkaian [CircuitJS](https://www.falstad.com/circuit/circuitjs.html) beserta tautan langsungnya. (Ingat, Anda dapat membuat tautan CircuitJS dengan membuka File -> Export as Link).

## Sumber Daya

* [Resistors in series and parallel](https://opentextbc.ca/universityphysicsv2openstax/chapter/resistors-in-series-and-parallel/), opentextbc.ca
* [Series and Parallel Resistors](https://www.khanacademy.org/science/ap-physics-1/ap-circuits-topic/series-circuits-ap/v/ee-series-resistors), Khan Academy
* [Voltage Divider](https://www.khanacademy.org/science/electrical-engineering/ee-circuit-analysis-topic/ee-resistor-circuits/a/ee-voltage-divider), Khan Academy
* [Circuit Analysis Shortcuts](https://courses.engr.illinois.edu/ece110/sp2021/content/courseNotes/files/?circuitAnalysisShortcuts), UIUC ECE110
* [Chapter 9.3 Voltage Divider Pattern](https://learning.oreilly.com/library/view/electronics-for-beginners/9781484259795/html/488495_1_En_9_Chapter.xhtml), Bartlett, Electronics for Beginners, APress 2020

<!-- The UIUC lab page "Module 100: The Voltage Divider" has a nice description: https://courses.engr.illinois.edu/ece110/sp2021/content/labs/Modules/M100_Voltage%20Divider.pdf -->

<!-- TODO: Engineering Mindset has a nice [animation](https://youtu.be/kcL2_D33k3o?t=858) of differences between series and parallel -->

## Pelajaran Selanjutnya

Di [pelajaran berikutnya](resistors.md), kita akan mempelajari lebih lanjut tentang resistor, bagaimana mereka dibuat, cara menggunakannya, bagaimana mereka dikarakterisasi, dan cara menghitung disipasi dayanya.

<nav class="lesson-nav" aria-label="Lesson navigation">
  <a href="ohms-law.html" class="nav-prev">
    <div class="nav-label">&larr; Pelajaran Sebelumnya</div>
    <div class="nav-title">Hukum Ohm</div>
  </a>
  <a href="resistors.html" class="nav-next">
    <div class="nav-label">Pelajaran Selanjutnya &rarr;</div>
    <div class="nav-title">Resistor</div>
  </a>
</nav>