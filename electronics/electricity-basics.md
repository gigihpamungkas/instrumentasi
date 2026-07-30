---
layout: default
title: L1&#58; Voltage, Current, and Resistance
description: "Master the three foundational concepts behind every circuit—voltage, current, and resistance—using an intuitive water (hydraulic) analogy, SI units, and a circuit simulator."
image: /electronics/assets/images/OhmsLawCartoon_ShowingRelationshipBetweenVoltsAmpsAndResistance.png
nav_order: 1
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

<video autoplay loop muted playsinline aria-label="Animation of a water tank analogy for electrical circuits. As the water level rises, more water flows out of a hole at the bottom, illustrating how higher voltage produces more current.">
  <source src="assets/videos/WaterCircuitAnalogy_Trimmed_ByJonFroehlich.mp4" type="video/mp4" />
</video>
**Video.** Arah tujuan kita: pembelajaran ini menggunakan analogi air yang intuitif—seperti tangki air ini, di mana tingkat air yang lebih tinggi (tegangan) mendorong lebih banyak air (arus) keluar dari bagian bawah—untuk membangun tiga konsep dasar dari tegangan, arus, dan hambatan.
{: .fs-1 }

Dalam pembelajaran ini, kita akan mempelajari tiga konsep utama kelistrikan, yaitu **arus** (*current*), **tegangan** (*voltage*), dan **hambatan** (*resistance*), yang menjadi fondasi dari elektronika dan rangkaian listrik. Kita juga akan menggunakan simulator rangkaian online untuk mempraktikkan komponen dasar dan memperdalam pemahaman.

Namun sebelum itu—apa itu rangkaian listrik? Sebuah **rangkaian listrik** (*circuit*) adalah lintasan tertutup yang menyediakan jalur bagi arus listrik untuk mengalir. Minimal, sebuah rangkaian membutuhkan sumber tegangan (misalnya baterai), jalur konduktif (misalnya kabel), dan beban (misalnya lampu bohlam atau resistor) yang melakukan kerja berguna. Jika lintasan tersebut terputus di titik mana pun, arus tidak dapat mengalir dan kita menyebutnya sebagai "rangkaian terbuka" (*open circuit*) (penjelasan lebih lanjut [nanti](#apa-itu-rangkaian-terbuka)).

<!-- TODO: Include a nice overview animation? [here](https://kaiserscience.wordpress.com/physics/electromagnetism/electric-current/) -->

{: .note }
Materi ini sangat penting. Tergantung pada latar belakang Anda sebelumnya di bidang fisika atau teknik, beberapa konsep ini mungkin terasa sangat baru dan membingungkan. Luangkan waktu Anda untuk memahami (dan membaca ulang) setiap bagian—materi ini akan membantu Anda memahami *bagaimana* rangkaian bekerja serta *bagaimana* dan *mengapa* kita menghubungkan dan menggunakan komponen elektronik dengan cara yang kita lakukan. Namun, ini juga *bukan* kursus rangkaian listrik ataupun [kursus fisika](https://youtu.be/x1-SibwIPM4), jadi saya akan sangat berfokus pada apa yang saya *pikir* paling krusial untuk *physical computing*.

## Ringkasan singkat

Jadi, apa itu tegangan, arus, dan hambatan?

Singkatnya, **tegangan** "mendorong" **elektron** melalui material konduktif (misalnya kabel). Jumlah dari **aliran elektron** tersebut disebut **arus** (diukur dalam satuan amp). Beberapa material memiliki kemampuan menghantarkan arus yang lebih baik daripada yang lain. Resistor diformulasikan secara khusus untuk *menghambat* aliran elektron (nilai **hambatan** diukur dalam satuan ohm).

![A humorous depiction of the relationship between voltage, current, and resistance. Three cartoon characters are shown: the "volt" character is trying to push the "amp" character through a wire but the "ohm" character is resisting the "amp" character by restricting the girth of the wire with a tightening rope.](assets/images/OhmsLawCartoon_ShowingRelationshipBetweenVoltsAmpsAndResistance.png)
{: .mx-auto .align-center }

**Gambar.** Gambaran jenaka namun sangat membantu mengenai hubungan antara tegangan (diukur dalam volt), arus (diukur dalam amp), dan hambatan (diukur dalam ohm). Karakter "volt" berwarna kuning mencoba mendorong karakter "amp" berwarna hijau melalui sebuah tabung (yaitu kabel), tetapi karakter "ohm" berwarna merah menghalanginya dengan membatasi ukuran tabung tersebut (dengan mengencangkan tali, memperkecil lingkarannya). Sumber gambar tidak diketahui tetapi ada banyak contoh dan alternatifnya [di internet](https://www.google.com/search?q=ohm%27s+law+cartoon&tbm=isch).
{: .fs-1 }

Apa saja satuan pengukuran untuk tegangan, arus, dan hambatan?

Sama seperti kita mengukur berat dalam kilogram dan suhu dalam Celsius, kita juga memiliki satuan pengukuran standar untuk arus, tegangan, dan hambatan (disebut [satuan SI](https://id.wikipedia.org/wiki/Sistem_Satuan_Internasional) untuk *Sistem Satuan Internasional*). Kita akan sangat sering menggunakan besaran dan pengukuran ini dalam *physical computing*, jadi luangkan waktu sejenak untuk mempelajari tabel di bawah ini.

| Besaran    | Simbol | Satuan Pengukuran     | Singkatan Satuan |
|------------|--------|-----------------------|-------------------|
| Arus       | $$I$$  | Ampere (atau Amp)     | A                 |
| Tegangan   | $$V$$  | Volt                  | V                 |
| Hambatan   | $$R$$  | Ohm                   | Ω                 |


### Analogi hidrolik (air)

Dalam rangkaian listrik, kita sering menggunakan analogi hidrolik untuk membantu pemahaman. Sebagai contoh, kita bisa menganggap *tegangan* analog dengan *tekanan air* pada sistem pipa air. Peningkatan tekanan air memberikan gaya yang lebih besar untuk mendorong molekul air melalui pipa. Air mengalir dari **tekanan tinggi** (sumber pasokan masuk) ke **tekanan rendah** (keluar dari katup yang terbuka). Demikian pula, peningkatan tegangan memberikan gaya yang lebih besar untuk "mendorong" elektron dari potensial listrik **tinggi** ke potensial listrik **rendah** melalui sebuah rangkaian.

Sama seperti pipa air yang lebih lebar dapat menampung lebih banyak air, kabel konduktif yang lebih tebal juga dapat menghantarkan lebih banyak arus. Sumbatan di dalam pipa—seperti pasir atau, yang lebih buruk, tanah liat—dapat memperlambat aliran air. Sumbatan ini mirip dengan resistor, yang dapat kita pasang ke dalam rangkaian untuk merintangi aliran arus (resistor terbuat dari material yang elektronnya lebih sulit untuk berpindah).

|            | Elektrik                       | Hidrolik                                 |
|------------|--------------------------------|------------------------------------------|
| Laju aliran| Arus, *amp (coulomb/detik)*    | Laju aliran, *GPM (galon/menit)*         |
| Potensial  | Tegangan, *volt*               | Tekanan, *psi (pound per inci persegi)*  |
| Hambatan   | Hambatan, *ohm (volt/amp)*     | Hambatan, *psi/gpm*                      |

<video autoplay loop muted playsinline aria-label="Animation of a water tank analogy for electrical circuits. As the water level rises, more water flows out of a hole at the bottom, illustrating how higher voltage produces more current.">
  <source src="assets/videos/WaterCircuitAnalogy_Trimmed_ByJonFroehlich.mp4" type="video/mp4" />
</video>
**Gambar.** Ini adalah analogi hidrolik yang sedikit berbeda dari sistem pipa air yang dijelaskan di atas. Di sini, kita memiliki sebuah tangki air yang diisi air dengan lubang di bagian bawahnya: seiring meningkatnya ketinggian air, tekanan (tegangan) pada air di bagian bawah tangki juga meningkat, yang secara sebanding meningkatkan jumlah air yang mengalir keluar dari lubang. Jika kita memperbesar ukuran lubang (memperkecil hambatan), lebih banyak air (arus) yang akan mengalir. Catatan: arah animasi menunjukkan *arus konvensional* (conventional current). Diagram air ini didasarkan pada ilustrasi dalam [buku *Make: Electronics* karya Platt](https://learning.oreilly.com/library/view/make-electronics-2nd/9781680450255/).
{: .fs-1 }

Mari kita telusuri masing-masing konsep ini secara lebih mendalam, dimulai dari arus listrik.

## Apa itu arus listrik?

<video autoplay loop muted playsinline aria-label="An animated gif showing current flowing in a simple circuit out of the positive terminal of a 9V battery through an LED and resistor and then back to the negative terminal of the 9V battery">
  <source src="assets/videos/CurrentFlow_EngineeringMindset.mp4" type="video/mp4" />
</video>
**Gambar.** **[Arus listrik](https://id.wikipedia.org/wiki/Arus_listrik)** adalah aliran partikel bermuatan—dalam hal ini, elektron—melalui sebuah konduktor. Pada animasi di atas, kita mengilustrasikan "aliran elektron" sebagai garis hijau putus-putus, yang mengalir dari terminal negatif baterai 9V, melewati LED dan resistor, lalu kembali lagi ke terminal positif baterai 9V. Perhatikan bahwa arah ini sebenarnya berlawanan dengan aliran *arus konvensional*, tetapi kita akan membahasnya di bawah. Animasi dari [The Engineering Mindset](https://youtu.be/kcL2_D33k3o).
{: .fs-1 }

*Arus* adalah aliran partikel bermuatan melalui sebuah konduktor. Dalam rangkaian listrik, partikel bermuatan ini adalah *elektron* (partikel bermuatan negatif) yang didorong oleh gaya elektromotif (tegangan) untuk bergerak dari "tekanan tinggi" ke "tekanan rendah" dalam sebuah rangkaian.

Arus listrik mirip dengan arus air yang bergerak melalui pipa. Sama seperti air di mana kita bisa mengarahkan aliran air melalui berbagai konfigurasi pipa dan memanfaatkan energi kinetiknya (misalnya untuk memutar turbin), kita juga bisa menggunakan kabel untuk mengarahkan aliran elektron dan menggunakannya untuk menyalakan lampu, memutar motor, atau melakukan kerja lainnya.

Untuk mengukur aliran air, kita bisa menghitung jumlah molekul air yang melewati potongan melintang pipa tertentu dalam waktu $$t$$. Demikian pula, kita bisa mengukur arus listrik dengan "menghitung" jumlah muatan yang mengalir melalui kabel. Faktanya, arus listrik $$I$$ didefinisikan sebagai jumlah muatan $$Q$$ yang bergerak melewati suatu titik dalam waktu $$t$$:

$$I = \frac{\Delta{Q}}{\Delta{t}}$$

Sebuah [coulomb (C)](https://id.wikipedia.org/wiki/Coulomb) adalah satuan SI untuk *muatan listrik* dan nilainya kira-kira setara dengan 6.240.000.000.000.000.000 elektron—yaitu 6,24 kuintiliun atau $$6.24 × 10^{18}$$ elektron!

Daripada terus-menerus mendeskripsikan arus sebagai jumlah coulomb/detik (atau elektron/detik) yang mengalir melalui kabel—seperti, "*Hei, kabel itu menghantarkan $$1.872 × 10^{19}$$ elektron per detik!*"—kita lebih memilih menggunakan satuan SI dari arus listrik yang disebut *ampere* atau *amp* (A), yang nilainya sama dengan 1 coulomb per detik:

$$1 A = 1 C / s$$

Meskipun Anda tidak perlu melakukan ini saat membuat prototipe rangkaian, Anda tentu saja dapat menggunakan rumusan ini untuk menghitung jumlah elektron yang melewati potongan melintang kabel selama waktu $$t$$. Kami melakukannya di bawah ini pada gambar hanya untuk tujuan ilustrasi: Berapa banyak elektron yang melewati titik tertentu dalam waktu 3 detik jika sebuah konduktor menghantarkan arus sebesar 2A? Jawabannya: $$6C$$ (6 coulomb) atau $$3.74 × 10^{19}$$ elektron.

![An illustrative diagram showing how electrons flow through a conductor and how to calculate how many electrons pass through a point using I = change in Q divided by change in t](assets/images/ElectricCurrentDefinitionAndDiagram_ScherzAndMonk4thEditionpng.png)
**Gambar.** Menggunakan rumus di atas, kita dapat menghitung jumlah elektron yang melewati potongan melintang kabel dalam tiga detik jika kabel tersebut menghantarkan arus sebesar 2A. Gambar dari [Bab 2](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml) dari buku *Practical Electronics for Inventors* karya Scherz dan Monk.
{: .fs-1 }

<!-- As electric charges move through a circuit from the high potential terminal to the low, they perform work (spin a motor, heat up electric coils, turn on a light bulb). By doing work, a charge loses its electric potential energy. For example, the conductive point just prior to a light bulb or motor is at a higher electric potential than the point just after. This loss in electric potential is referred to as a *voltage drop*, which we will explain later. -->

### Membangun intuisi tentang arus listrik

Yang terpenting, sama seperti sistem pipa di rumah Anda, di mana air langsung mengalir keluar dari keran saat Anda membuka katupnya (didorong oleh tekanan air dari menara air, misalnya), arus listrik juga langsung mengalir ketika tegangan diberikan (didorong, misalnya, oleh baterai). Dan secara krusial, molekul air yang menyentuh tangan Anda tidak mengalir dari ujung sistem pipa Anda dalam sekejap. Sebaliknya, pipa-pipa Anda sudah terisi penuh dengan air bertekanan—sama seperti kabel konduktif yang sudah terisi penuh dengan atom. Ketika Anda membuka keran, molekul air yang menyentuh tangan Anda adalah molekul yang sebelumnya mendorong katup keran tersebut (semacam antrean *first-in, first-out*).

Hal ini serupa dengan arus dalam rangkaian—atom-atom tersusun rapat di dalam suatu material dengan elektron yang mengorbit. Ketika tegangan diberikan, elektron-elektron ini mulai "melompat" dari satu atom ke atom lainnya melalui konduktor tetapi tidak langsung melesat secara instan dari titik A ke B (lihat [video](https://youtu.be/OGa_b26eK2c?t=472)).

<video autoplay loop muted playsinline aria-label="An animated gif showing electrons hopping from atom to atom propelled by an applied voltage">
  <source src="assets/videos/ElectronsFlowingFromAtomToAtomToMakeCurrent.mp4" type="video/mp4" />
</video>
{: .mx-auto .align-center }

**Gambar.** Sebuah animasi muatan (elektron) yang melompat dari atom ke atom dengan dorongan tegangan yang diberikan. Ini adalah model sederhana yang menunjukkan kabel (konduktor) dengan ketebalan hanya satu atom saja, namun membantu mengilustrasikan gerakan beruntun dari elektron dalam aliran arus. Gambar dari artikel [What is Electricity?](https://learn.sparkfun.com/tutorials/what-is-electricity) oleh [Sparkfun.com](https://www.sparkfun.com/).
{: .fs-1 }

Cara lain untuk memikirkan aliran arus adalah seperti sebuah tabung yang diisi penuh dari ujung ke ujung dengan kelereng. Jika sebuah kelereng dimasukkan dari sisi kiri, kelereng lain akan langsung keluar dari tabung di sisi kanan. Meskipun setiap kelereng hanya menempuh jarak yang pendek, transfer gerakannya terjadi hampir seketika. Pada listrik, efek keseluruhan dari satu ujung konduktor ke ujung lainnya terjadi secepat kecepatan cahaya; namun, setiap individu elektron bergerak melalui konduktor dengan kecepatan yang jauh lebih lambat. Faktanya, kecepatan rata-rata pergerakan elektron melalui kabel akibat medan listrik yang diterapkan (seperti dari baterai) adalah dalam skala sentimeter per jam (disebut [kecepatan hanyut / drift velocity](https://en.wikipedia.org/wiki/Speed_of_electricity#Electric_drift))!

![An image showing a tightly packed tube of single-file marbles. When a marble is inserted into the left side of the tube, a marble on the right side instantly exits.](assets/images/ElectronFlowMarbleTube_FromAllAboutCircuits.png)
{: .mx-auto .align-center }

**Gambar.** Anda dapat membayangkan elektron yang mengalir melalui rangkaian seperti kelereng yang tersusun rapat di dalam tabung. Sebuah kelereng tidak perlu melintasi seluruh tabung untuk menciptakan gerakan. Sebaliknya, ketika sebuah kelereng dimasukkan ke sisi kiri tabung, kelereng di sisi kanan akan langsung keluar. Gambar dari [All About Circuits](https://www.allaboutcircuits.com/textbook/direct-current/chpt-1/conductors-insulators-electron-flow/). Lihat juga, [video ini](https://youtu.be/8gvJzrjwjds?t=74) oleh Afrotechmods.
{: .fs-1 }

<!-- Another nice description of this marble analogy is from https://learning.oreilly.com/library/view/practical-electronics-components/9781449373221/ch01.html -->

### Apa bedanya arus konvensional vs. aliran elektron?

<video autoplay loop muted playsinline aria-label="Side-by-side comparison of two identical circuits: one showing electron flow from negative to positive, the other showing conventional current from positive to negative.">
  <source src="assets/videos/ElectronFlowVsConventionalCurrent_PhetSimulation_ByJonFroehlich.mp4" type="video/mp4" />
</video>
**Gambar.** Pada animasi di atas, kami menunjukkan dua rangkaian listrik yang **sama** tetapi menampilkan perbedaan antara *aliran elektron* (electron flow) dan *aliran arus* (current flow). Dalam rangkaian, partikel bermuatan negatif (elektron) bergerak dari terminal negatif baterai (atau sumber tegangan) ke terminal positif—ini disebut *aliran elektron*; namun, ketika kita membuat model rangkaian (dan menggunakan rumus rangkaian), kita menggunakan *arus konvensional* (conventional current), yang bergerak ke arah sebaliknya.
{: .fs-1 }

Dalam rangkaian listrik, kita menggunakan *arus konvensional* untuk memodelkan aliran muatan dari terminal positif sumber tegangan ke terminal negatif; namun, elektron sebenarnya bergerak ke arah *sebaliknya* (disebut *aliran elektron*). Hal ini sering memicu kebingungan besar!

Mengapa? Persoalan ini berakar dari [Benjamin Franklin](https://hackaday.com/2017/07/17/conventional-current-vs-electron-current/). Pada eksperimen awal (pertengahan tahun 1740-an), Franklin menyimpulkan bahwa listrik tampaknya "mengalir" layaknya cairan di dalam material padat. Dia berasumsi bahwa muatan yang mengalir memiliki tanda positif dan bergerak dari positif ke negatif. Baru pada tahun 1897, Sir Joseph Thomson memastikan bahwa pembawa muatan yang sebenarnya di dalam kabel adalah elektron, dan elektron bergerak dari katode (negatif) ke anode (positif).

![An image of Thomson and Franklin thinking about how charge move in a conductor with Thomson actually getting it right: electrons are negatively charged and move from the negative source to the positive source.](assets/images/ConventionalCurrentVsElectronFlow_SherzAndMonk4thEdition.png)

**Gambar.** Franklin mengira bahwa pembawa muatan positif bergerak di dalam konduktor dari positif ke negatif. Ini disebut arah *arus konvensional*, yang masih digunakan hingga saat ini. Sebaliknya, seperti yang ditemukan oleh Thomson, elektronlah yang bergerak di dalam konduktor (yang bermuatan negatif) dan mereka bergerak dari negatif ke positif. Ini disebut *aliran elektron*. Gambar dari [Bab 2](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml) dari buku *Practical Electronics for Inventors* karya Scherz dan Monk.
{: .fs-1 }

Terlepas dari kebingungan ini, ternyata selama Anda konsisten, hal itu tidak menjadi masalah: elektron negatif yang mengalir ke satu arah setara dengan memodelkan muatan positif yang mengalir ke arah sebaliknya. Oleh karena itu, kita cenderung menggunakan *arus konvensional* (memodelkan aliran muatan dari positif ke negatif) dalam elektronika (misalnya pada diagram, rumus, dll.). Perhitungan matematikanya akan tetap berfungsi dengan baik dan bahkan jembatan keledai seperti [kaidah tangan kanan](https://id.wikipedia.org/wiki/Kaidah_tangan_kanan) didasarkan pada arus konvensional (arahkan jempol ke arah arus $$I$$, maka jari lain menunjukkan arah medan magnet $$B$$).

<!-- For more, see [Chapter 2](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml) of Scherz and Monk's *Practical Electronics for Inventors* and this lovely [video](https://youtu.be/kcL2_D33k3o?t=224) by The Engineering Mindset. -->

### Arus operasional yang umum pada rangkaian listrik

Saat Anda mulai bekerja di bidang *physical computing*, Anda akan mendapatkan pemahaman yang lebih baik tentang "*Berapa nilai yang termasuk arus besar?*" vs. "*Berapa nilai yang termasuk arus kecil?*"

Pada rangkaian digital, kita biasanya bekerja dengan **amperase rendah**. Sebagai contoh, sebuah LED mungkin memerlukan tegangan 2V tetapi hanya butuh arus sekitar ~20 miliampere (miliamp atau disingkat mA) untuk menyala—itu setara dengan $$(6.24 × 10^{18}) * 0.02 = 1.3 × 10^{17}$$ elektron/detik. Demikian pula, satu pin tunggal pada Arduino mungkin dapat menyuplai arus hingga 40mA atau $$2.5 × 10^{17}$$ elektron/detik. 

Port USB standar yang lebih lama (USB 2.0) menyuplai listrik 5V dengan arus maksimum 0.5A (500 mA). Port laptop modern (USB 3.0 dan USB-C standar) biasanya menyuplai antara 0.9A hingga 3A pada tegangan 5V. Terlebih lagi, dengan hadirnya *USB Power Delivery* (USB PD), port USB-C modern dapat menegosiasikan tegangan dan arus yang jauh lebih tinggi—hingga 240W (48V pada 5A)—menjadikan USB-C sebagai standar yang andal dan universal untuk menyalakan mikrokontroler serta perangkat periferal dengan kebutuhan daya tinggi.

{: .note }
Beberapa komponen listrik, seperti [motor](https://itp.nyu.edu/physcomp/labs/motors-and-transistors/using-a-transistor-to-control-a-high-current-load/) atau [rangkaian lampu LED yang panjang](https://www.eerkmans.nl/powering-lots-of-leds-from-arduino/), membutuhkan arus yang lebih besar (disebut "*high current loads*") daripada yang dapat disuplai oleh mikrokontroler atau port USB 2.0. Dalam kasus ini, kita dapat menggunakan catu daya eksternal yang dikendalikan oleh sebuah transistor.

## Apa itu tegangan listrik?

<video autoplay loop muted playsinline aria-label="Animation showing voltage as a force that pushes electrons through a circuit, similar to water pressure in a pipe.">
  <source src="assets/videos/VoltageElectromotiveForce_EngineeringMindset.mp4" type="video/mp4" />
</video>
**Gambar.** Anda dapat membayangkan *tegangan* sebagai kekuatan yang "mendorong" elektron di sekitar rangkaian listrik. Animasi dari video [Voltage Explained](https://youtu.be/w82aSjLuD_8) oleh The Engineering Mindset.
{: .fs-1 }

Baik, jadi jika arus adalah *aliran* muatan dalam sebuah rangkaian, apa yang memaksa muatan-muatan tersebut bergerak?

Mirip seperti magnet, muatan dengan *tanda yang sama* akan saling tolak-menolak (misalnya elektron saling tolak-menolak karena semuanya bermuatan negatif) dan muatan dengan tanda berbeda akan *saling tarik-menarik* (misalnya elektron dan proton). Baterai menggunakan reaksi kimia untuk menghasilkan *penumpukan* elektron di terminal negatif—hal ini menciptakan "tekanan" atau perbedaan listrik antara kedua terminal baterai.

Ketika Anda menghubungkan terminal-terminal baterai tersebut (artinya menutup rangkaian), elektron mengalir untuk menyeimbangkan ketidakseimbangan ini dari terminal negatif ke terminal positif. Namun ingat, dengan arus konvensional, kita memodelkan pergerakan muatan ke arah sebaliknya, sehingga kita menunjukkan arus berjalan dari terminal positif ke negatif; dalam hal ini, kita menyebut muatan di terminal positif memiliki energi potensial tinggi dan muatan di terminal negatif memiliki energi potensial rendah.

Singkatnya, Anda bisa menganalogikan tegangan seperti tekanan di dalam pipa air: semakin besar tekanannya, semakin banyak air yang dipaksa mengalir melalui pipa. Begitu pula dengan meningkatkan tegangan, kita bisa "mendorong" lebih banyak elektron melalui kabel.

Bahkan, Wikipedia merujuk **[Tegangan listrik](https://id.wikipedia.org/wiki/Tegangan_listrik)** sebagai "tekanan listrik", "gaya elektromotif", dan "perbedaan potensial listrik" untuk menggambarkan efek dorongan (atau tolakan) ini. Ini adalah pendekatan konseptual yang masuk akal: Anda dapat menganggap tegangan sebagai ukuran "tekanan" yang menyebabkan arus mengalir. Di antara dua komponen, jika perbedaan potensial listriknya adalah 0V, maka tidak akan ada arus yang mengalir.

<!-- As [Scherz and Monk](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml) state, "a voltage placed across a conductor gives rise to an *electromotive force (EMF)* that is responsible for giving all free electrons within the conductor a push." -->

<!-- https://learning.oreilly.com/library/view/make-electronics-2nd/9781680450255/ch01.html
https://learning.oreilly.com/library/view/make-electronics-2nd/9781680450255/ch01.html
https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml#
https://learning.oreilly.com/library/view/practical-electronics-components/9781449373221/ch05.html
https://learning.oreilly.com/library/view/electronics-for-beginners/9781484259795/html/488495_1_En_5_Chapter.xhtml
https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-voltage-and-current -->

### Definisi yang lebih presisi

Lebih tepatnya, *tegangan* adalah usaha yang diperlukan untuk memindahkan suatu muatan dari satu lokasi ke lokasi lain di dalam medan listrik. Tegangan memberikan kita gambaran tentang seberapa besar gaya "dorong" yang dimiliki oleh medan listrik, dan didefinisikan sebagai energi potensial listrik per satuan muatan (misalnya elektron), yang diukur dalam satuan joule per coulomb (volt):

$$1\ V = 1\ joule\ (usaha) / 1\ coulomb\ (muatan)$$

Karena joule adalah satuan *energi*, tegangan memperkenalkan konsep yang sangat penting dan diperlukan: potensi untuk melakukan *usaha* (misalnya untuk menyalakan lampu, memutar motor)!

<video autoplay loop muted playsinline aria-label="Split-screen animation comparing an electrical circuit to a water wheel circuit, showing how charges gain potential energy in a battery and lose it performing work, just as water gains potential energy when pumped uphill.">
  <source src="assets/videos/VoltagePotentialWaterWheelCircuitAnalogy_TrimmedAndCropped_ByJonFroehlich.mp4" type="video/mp4" />
</video>
**Gambar.** Sebuah animasi yang menunjukkan analogi antara rangkaian listrik dan rangkaian "air". Di dalam baterai, potensial listrik dari muatan meningkat saat mereka bergerak ke terminal positif (tegangan lebih tinggi)—potensial ini turun ketika usaha dilakukan (misalnya mengalir melewati resistor). Demikian pula, molekul air yang dipompa ke tempat yang lebih tinggi memiliki *potensial lebih tinggi* untuk melakukan usaha; potensial ini berkurang saat air mengalir ke tempat yang lebih rendah atau digunakan untuk melakukan usaha (misalnya memutar turbin). Perhatikan bahwa tidak ada muatan (atau molekul air) yang hilang dalam sistem ini—tetapi energi potensial dari partikel-partikel ini diubah ke bentuk lain (misalnya kinetik, panas).
{: .fs-1 }

Dan sama seperti kita bisa menggunakan "energi" dari air yang mengalir untuk melakukan usaha—misalnya untuk memutar kincir—kita juga bisa menggunakan arus yang mengalir untuk melakukan usaha. Saat elektron bergerak melalui rangkaian dan melakukan usaha (menggerakkan motor, memanaskan kabel, menyalakan lampu), mereka mulai kehilangan "potensial listrik" mereka. Lihat animasi di atas.

<!-- ### Example problems

Let's look at some examples (inspired by [Khan Academy](https://www.khanacademy.org/science/in-in-class10th-physics/in-in-electricity/in-in-electric-potential-potential-difference/v/intro-to-potential-difference-voltage)). We use conventional current below.

If a smartphone battery does $$15J$$ of work to move a net charge of $$3.0C$$ between its negative and positive terminals, then what voltage does the battery provide? Let's define $$V_{cell}$$ as the work needed to move one unit of charge through the battery and we know $$1V = \frac{1J}{1C}$$. Thus:

$$V_{cell} = \frac{15J}{3.0C} = 5V$$

So, we say that the *charges* at the battery's positive terminal have an electric potential of 5V. The battery uses chemical reactions (work) to elevate the potential energy of these charges from 0V (from its negative terminal) to 5V (to its positive terminal).

As another example, after an exhausting journey through resistors and bulbs in a circuit, 2C of charges arrive at the negative terminal of a 9V battery with 0 electric potential (0V). How much work, in joules, does the battery need to do to push these charges back to high potential energy (its positive terminal)? Using basic algebra, we can solve for joules by:

$$9V = \frac{xJ}{2C} => xJ = 9V * 2C = 18J$$

So, it takes 18J to move 2C of charge ($$1.25 x 10^{19}$$ electrons) from the negative terminal of the battery to the positive. -->

<!-- Finally, last one: if 1C of charge exits the positive terminal of a battery with 2J of energy and passes through a resistive lamp, what is the voltage drop across the lamp? -->

<!-- TODO: insert that animation I use in lecture here of charges moving up gaining electric potential and then using that work would drops potential. See: https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-voltage-and-current -->

<!-- another fun gravity analogy: https://electronics.stackexchange.com/a/182450 -->

<!-- In a battery-powered circuit, electrons are repelled by the negative battery terminal (which has an imbalance of negative charges) and attracted to the positive battery terminal (which has an imbalance of positive charges). These charge "buildups" create an electromotive force that moves charge through the circuit. We call this movement *current*. -->

<!-- This is similar to water flow in a pipe (hydraulics) or air flow in a tube (pneumatics)—all which flow from "high pressure" to "low pressure." -->

<!-- Another nice analogy is a tube with water and angling the tube upright, which increases pressure and then increases flow -->

<!-- "Another way to think of voltage is as the electric potential difference between two points in an electric field. It is similar to the difference in the potential energy of a cannonball at the top of a ladder as opposed to one at the top of a tall tower. Both cannonballs exist in the earth's gravitational field, they both have potential energy, and it took some work to get them both into position. When they are released, the cannonball on the top of the tower will have more energy when it hits the ground than the cannonball dropped from the top of the ladder, because it had a larger potential energy due to its position." From https://learning.oreilly.com/library/view/practical-electronics-components/9781449373221/ch01.html -->

### Tegangan operasional yang umum

Dalam rangkaian digital, tegangan operasional yang umum relatif kecil—seperti 3.3V atau 5V—jika dibandingkan dengan tegangan yang disuplai oleh stopkontak dinding Anda (yang di AS sebesar 120V dan di Indonesia sebesar 220V!). Mikrokontroler populer seperti [ESP32](https://www.espressif.com/en/products/socs/esp32) beroperasi pada tegangan 3.3V sedangkan papan [Arduino Uno](https://store.arduino.cc/usa/arduino-uno-rev3) dan [Arduino Leonardo](https://www.arduino.cc/en/Main/Arduino_BoardLeonardo) beroperasi pada 5V. Pengisi daya USB-A Lightning Apple iPhone 8 saya mengeluarkan output 5V dan dapat menyuplai arus hingga 2A. Pengisi daya Apple yang lebih baru, seperti *Apple 20W USB-C Power Adapter*, dapat menyuplai 9V pada 2.2A (dapat mengisi daya cepat iPhone 17 hingga sekitar 50% dalam waktu 30 menit).

Penting untuk diperhatikan, Anda tidak boleh menyuplai tegangan melebihi batas tegangan input yang ditentukan dari suatu komponen listrik karena Anda berisiko merusak komponen tersebut. Oleh karena itu, sangat penting bagi Anda untuk membaca lembar data (*data sheet*) komponen sebelum menggunakannya (yang akan kita pelajari caranya pada pembelajaran mendatang).

<!-- **TODO: UPDATE THIS DESCRIPTION**
Some potential references:
- https://learning.oreilly.com/library/view/practical-electronics-components/9781449373221/ch01.html
- https://learning.oreilly.com/library/view/learn-electronics-with/9781680454420/#toc
- https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/12_Chapter_01.xhtml#ch01 -->

### Tegangan relatif dan ground

Berdasarkan definisinya, tegangan adalah *perbedaan* potensial listrik antara **dua titik**. Ketika kita mulai mengukur tegangan dalam sebuah rangkaian (menggunakan multimeter), Anda akan melihat bahwa kita tidak bisa hanya menempelkan satu kabel colok (*probe*) pada rangkaian. Sebaliknya, kita harus menaruh **dua probe** di lokasi berbeda untuk mengukur selisih tegangan di antara keduanya (juga disebut **tegangan jatuh** atau **voltage drop**).

Untuk menyederhanakan perhitungan, kita memilih suatu titik pada rangkaian—biasanya titik dengan potensial listrik paling rendah (misalnya kabel yang terhubung ke terminal negatif baterai)—sebagai 0 volt. Seperti yang dicatat oleh [Bartlett](https://learning.oreilly.com/library/view/electronics-for-beginners/9781484259795/) (Bab 4.3), "*'Titik nol' ini memiliki beberapa nama, yang paling populer di antaranya adalah **ground** (sering disingkat **GND**). Dinamakan ground karena secara historis, tanah fisik bumi sering digunakan sebagai tegangan acuan untuk rangkaian listrik*."

Kembali ke analogi gravitasi-tegangan, seberapa besar energi potensial yang dimiliki sebuah batu setelah menyentuh tanah? Tidak ada! Agar batu tersebut mendapatkan energi potensial, kita perlu melakukan *usaha* untuk mengangkat batu tersebut.

### Bahaya: tegangan tinggi!

Anda mungkin pernah melihat peringatan seperti: *DANGER: HIGH VOLTAGE* tetapi Anda mungkin juga pernah mendengar kalimat kontradiktif seperti "*bukan tegangan yang membunuh, melainkan arus listrik.*" Bagaimana keduanya bisa sama-sama benar?

Pada beberapa aspek: keduanya memang benar. Tegangan tinggi memiliki potensi untuk mendorong arus listrik yang lebih besar melalui tubuh Anda dibandingkan tegangan rendah—dan *arus listrik* itulah yang dapat membakar jaringan tubuh, mengganggu kendali otot, dan menyebabkan fibrilasi pada jantung Anda. Faktanya, manusia dapat merasakan arus DC sekecil 0,6–1,0mA yang mengalir melalui tubuh mereka, 40–60mA terasa menyakitkan, dan sekitar ~90mA ke atas sudah cukup untuk memicu henti jantung/pernapasan.

Tetapi—dan ini adalah poin penting—tubuh kita menawarkan hambatan yang terbilang cukup tinggi. Dan tegangan yang kita gunakan untuk praktik (biasanya 3.3V dan 5V) tidak cukup tinggi untuk "mendorong" arus melewati tubuh kita. Walau demikian, kulit yang basah dapat menurunkan hambatan tubuh Anda dan perhiasan logam dapat menyebabkan hubungan singkat yang tidak disengaja (dan kemungkinan luka bakar termal). Jadi, tetaplah berhati-hati.

Umumnya, hal kelistrikan yang paling berbahaya di rumah Anda adalah tegangan jala-jala yang keluar dari stopkontak rumah Anda (120V pada 60Hz di AS dan 220V pada 50Hz di Indonesia dan banyak negara lain). Jangan pernah membuka perangkat elektronik apa pun saat masih terhubung ke stopkontak, dan bahkan setelahnya pun tetaplah berhati-hati (kapasitor yang bermuatan masih dapat menyimpan tegangan tinggi untuk beberapa waktu).

Untuk informasi lebih lanjut tentang keselamatan listrik, lihat [tulisan di AllAboutCircuits.com](https://www.allaboutcircuits.com/textbook/direct-current/chpt-3/ohms-law-again/) atau bagian [Keselamatan (Bab 7.1) dalam Practical Electronics for Inventors](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/18_Chapter_07.xhtml).

Anda juga dapat menonton [video ini](https://youtu.be/hp97GjuULX8) oleh YouTuber populer [ElectroBOOM](https://www.youtube.com/channel/UCJ0-OtVpF0wOKEqT2Z1HEtA), yang menguji toleransi rasa sakitnya terhadap listrik AC dan DC.

<!-- Returning to the [water tank analogy](assets/videos/WaterCircuitAnalogy_Trimmed_ByJonFroehlich.mp4) from the Introduction, how much potential to do work does water have once it's flowed out of the hole and onto the ground? None! It's lost all of its energy. Likewise, when an electric charge reaches ground, it no longer has electric potential for work. -->

### Bagaimana kita bisa meningkatkan tekanan?

Baterai memiliki ketidakseimbangan muatan listrik yang terbentuk di antara kutub positif dan negatifnya. Ketika suatu rangkaian terhubung, muatan listrik (elektron) mengalir untuk "memperbaiki" ketidakseimbangan ini. Semakin besar ketidakseimbangan tersebut (yaitu semakin tinggi tegangan), semakin besar "dorongan" yang terjadi dan semakin banyak elektron yang mengalir (arus lebih tinggi).

Jika Anda menghubungkan dua baterai secara seri (artinya ditumpuk), Anda meningkatkan kemampuan mereka untuk "mendorong" elektron—secara harfiah, Anda menjumlahkan tegangan baterai tersebut bersama-sama. Jadi, dua baterai AA alkalin standar 1.5V secara seri akan memiliki perbedaan potensial sebesar 3V, yang dapat "mendorong" lebih banyak elektron di sekitar rangkaian—lihat animasi di bawah ini.

<video autoplay loop muted playsinline aria-label="Animation showing two 1.5V batteries connected in series to produce 3V total, with increased electron flow through the circuit.">
  <source src="assets/videos/VoltageBatteriesInSeries_CroppedAndTrimmed2_EngineeringMindset.mp4" type="video/mp4" />
</video>
**Gambar.** Ketika Anda menghubungkan baterai secara seri, Anda meningkatkan gaya "dorong"—secara harfiah, Anda menjumlahkan tegangan baterai bersama-sama (jadi, 1.5V + 1.5V = total 3V). Lebih banyak tegangan, lebih banyak tekanan. Lebih banyak tekanan, lebih banyak elektron yang "didorong" melalui rangkaian. Animasi dari video [Voltage Explained](https://youtu.be/w82aSjLuD_8?t=183) oleh The Engineering Mindset.
{: .fs-1 }

<!-- See https://www.physicsclassroom.com/class/circuits/Lesson-1/Electric-Potential-Difference -->

<!-- See also: http://andnowforelectronics.com/notes/voltage-and-current/ -->

{: .note }
> **Satuan dasar.** Saat Anda belajar dan mulai menganalisis rangkaian listrik, penting untuk memperhatikan *satuan*. Satuan dasar dari tegangan adalah volt (V), satuan dasar dari arus adalah ampere atau amp (A), dan satuan dasar dari hambatan adalah ohm (Ω). Seperti yang telah dicatat, pada rangkaian digital kita sering bekerja dengan tegangan antara 0–5V (dan terkadang 9V atau 12V), tetapi arus listrik sering kali berada dalam kisaran miliamp—seperti 0.02A atau 0.1A—dan hambatan yang umum digunakan meliputi 220Ω, 1.000Ω, 2.200Ω, dan bahkan 10.000Ω. Namun biasanya, Anda akan melihat nilai-nilai ini ditulis masing-masing sebagai 20mA dan 100mA serta 1kΩ, 2.2kΩ, dan 10kΩ. Oleh karena itu, penting untuk melacak satuan dengan cermat dan mengonversi nilai ke satuan dasar untuk keperluan analisis. Kita akan membahas lebih banyak tentang hal ini pada pembelajaran [Hukum Ohm](ohms-law.md).

## Apa itu hambatan listrik?

<video autoplay loop muted playsinline aria-label="Animation comparing electron flow through copper wire versus iron wire, showing more collisions and heat generation in the higher-resistance iron wire.">
  <source src="assets/videos/CopperVsIronWireResistanceElectronFlow_EngineeringMindset.mp4" type="video/mp4" />
</video>
**Gambar.** Saat elektron bergerak melalui suatu material, mereka dapat bertabrakan dengan beberapa atom atau elektron lainnya. Tabrakan ini menciptakan sebuah *hambatan* (resistance) terhadap arus listrik. Yang patut dicatat dan penting, hambatan ini memperlambat **seluruh** pergerakan muatan (arus) di dalam rangkaian, bukan hanya muatan yang melewati material resistif tersebut.
Analogi yang umum, meskipun tidak sepenuhnya sempurna, untuk hambatan listrik adalah *gesekan mekanis*; sebuah resistor mengubah energi listrik menjadi energi panas (dan menyebabkan tegangan jatuh) sama seperti gesekan mengubah energi mekanik kinetik menjadi panas. Di dalam animasi di atas, perhatikan bagaimana kawat besi memiliki lebih banyak tabrakan dibandingkan kawat tembaga. Besi memiliki tingkat konduktivitas sekitar ~17% dari tembaga. Pada suhu 20°C, besi memiliki resistivitas listrik sebesar 96,1 nanoohm-meter sedangkan tembaga memiliki resistivitas 16,8 nanoohm-meter. Perhatikan lingkaran cahaya di sekitar kawat besi: ini untuk mengilustrasikan bagaimana sebagian energi "kinetik" atau gerakan elektron diubah menjadi panas atau cahaya melalui tabrakan tersebut. Sungguh, ini adalah prinsip kerja dari lampu pijar, pemanggang roti (toaster), dan pemanas ruangan elektrik! Animasi dari video [How Electricity Works](https://youtu.be/mc979OhitAg?t=322) oleh The Engineering Mindset.
{: .fs-1 }

Saat elektron bergerak melalui suatu material, mereka dapat bertabrakan dengan beberapa atom atau elektron lainnya. Tabrakan ini menciptakan sebuah *hambatan* terhadap arus listrik. Yang patut dicatat dan penting, hambatan ini memperlambat **seluruh** pergerakan muatan (arus) di dalam rangkaian, bukan hanya muatan yang melewati material resistif tersebut.

Analogi yang umum, meskipun tidak sepenuhnya sempurna, untuk hambatan listrik adalah *gesekan mekanis*; sebuah resistor mengubah energi listrik menjadi energi panas (dan menyebabkan tegangan jatuh) sama seperti gesekan mengubah energi mekanik kinetik menjadi panas.

<!-- **TODO: think of a water [flow through a narrow pipe](https://youtu.be/F_vLWkkOETI?t=267)** -->

Tergantung pada komposisi atomnya, beberapa material memiliki hambatan yang lebih rendah daripada yang lain. Logam seperti perak, tembaga, dan emas adalah konduktor yang *baik*—mereka menawarkan hambatan yang *rendah*—karena mereka memiliki elektron yang terikat longgar di kulit terluar atom mereka. Elektron-elektron ini mudah berpindah tempat dan, dengan adanya medan listrik yang diterapkan, dapat "didorong" dari atom ke atom di dalam material untuk membentuk arus.

Satuan SI untuk hambatan listrik adalah ohm (Ω). Kebalikan langsung dari hambatan adalah *konduktansi*. Material dengan hambatan rendah disebut *konduktor*. Sebaliknya, material seperti kaca, karet, dan udara memiliki hambatan yang tinggi dan konduktivitas yang buruk ("mobilitas elektron rendah")—material ini disebut *isolator*.

![This image shows PVC insulated wire with two annotations: the annotation on the left points to the internal part of the wire, which is highly conductive and made of copper. The annotation on the right points to the insulation around the wire, which has low conductivity and is made of PVC.](assets/images/PVCWrappedWire-ConductorVsInsulator.png)
**Gambar.** Kabel tembaga berisolasi PVC. Inti tembaga (keterangan kiri) adalah **konduktor** yang baik dengan hambatan rendah, sedangkan lapisan PVC (keterangan kanan) adalah **isolator** dengan hambatan tinggi, mencegah arus bocor keluar dari kabel atau menyengat pengguna.
{: .fs-1 }

Hambatan $$R$$ dari suatu objek didefinisikan sebagai rasio tegangan $$V$$ yang melintasinya terhadap arus $$I$$ yang mengalir melaluinya, sedangkan konduktansi $$G$$ adalah kebalikannya:

$$R = \frac{V}{I}$$, $$G = \frac{1}{R}$$

Dengan tegangan (tekanan) yang cukup besar, hampir semua material dapat menghantarkan arus listrik (bahkan udara sekalipun, seperti yang terbukti pada kilat petir). Hambatan (atau konduktansi) dari sebuah kabel bukan hanya fungsi dari jenis material saja tetapi juga suhunya dan ukurannya (baik panjang maupun ketebalannya). Singkatnya, untuk kabel logam, hambatan akan menurun seiring dengan bertambahnya diameter kabel. Sebaliknya, hambatan akan meningkat seiring bertambahnya panjang kabel atau meningkatnya suhu.

[Wikipedia](https://en.wikipedia.org/wiki/Electrical_resistivity_and_conductivity) menyediakan analogi berbasis air yang bagus:

> "mengalirkan arus melalui material berhambatan tinggi adalah seperti mendorong air melalui pipa yang penuh dengan pasir. Sebaliknya, mengalirkan arus melalui material berresistivitas rendah adalah seperti mendorong air melalui pipa yang kosong. Jika pipa-pipa tersebut memiliki ukuran dan bentuk yang sama, pipa yang penuh dengan pasir memiliki hambatan aliran yang lebih tinggi. Namun, hambatan tidak hanya ditentukan oleh ada atau tidaknya pasir. Hal itu juga bergantung pada panjang dan lebar pipa: pipa yang pendek atau lebar memiliki hambatan yang lebih rendah daripada pipa yang sempit atau panjang."
{: .fs-4 }

Untuk membantu mengilustrasikan ide ini secara visual, [Profesor Squier](http://people.cs.georgetown.edu/~squier/Teaching/ComputerSystemsArchitecture/520-2013-CourseDocuments/Lec-1-electricityPrimer.pdf) membuat beberapa sketsa yang sangat membantu—lihat keterangan gambar untuk detail lebih lanjut:

![Image shows a water analogy for electricity. There are two pipes visible: one filled with gravel (less resistance) and one filled with clay (more resistance). There is an equal amount of water pressure (voltage) "pushing" water through both pipes. The pipe with less resistance (gravel) will have more water flow (current).](assets/images/ElectricityPrimer_WaterAnalogy_SquierGeorgetown.png)
**Gambar.** Melanjutkan analogi air kita: bayangkan dua pipa yang diisi dengan material resistif, satu berisi kerikil (hambatan lebih rendah) dan satu lagi diisi tanah liat (hambatan lebih tinggi). Kedua pipa memiliki jumlah tekanan air (tegangan) yang sama yang "mendorong" air melalui pipa-pipa tersebut. Pipa dengan hambatan lebih rendah (kerikil) akan memiliki aliran air (arus) yang lebih banyak. Gambar dari *Electricity Primer* milik Profesor Richard Squier.
{: .fs-1 }

{: .note}
Untuk kawat logam, **hambatan** akan **meningkat** seiring **suhu** yang **meningkat**. Mengapa? Ketika logam memanas, atom-atomnya bergetar dengan lebih kuat. Peningkatan getaran ini menyebabkan lebih banyak tabrakan dengan elektron yang mengalir, yang menghalangi pergerakan mereka dan *meningkatkan* hambatan listriknya.

### Resistivitas listrik

Karena hambatan bukan sekadar sifat intrinsik dari suatu material (misalnya berdasarkan struktur atomnya) tetapi juga didasarkan pada bentuk dan ukuran material tersebut, kita menggunakan istilah [*resistivitas listrik*](https://id.wikipedia.org/wiki/Resistivitas_listrik) $$\rho$$, yang nilainya tidak bergantung pada dimensi material (dengan asumsi suhu konstan).

Lebih spesifiknya, pada suhu konstan, resistivitas listrik $$\rho$$ dari sebuah kabel dapat dihitung dengan rumus:

$$\rho =R{\frac {A}{\ell }}$$,

di mana $$R$$ adalah hambatan listrik dari spesimen material yang seragam, $$ℓ$$ adalah panjang spesimen, dan $$A$$ adalah luas penampang melintang spesimen. Satuan SI untuk resistivitas adalah ohm-meter (Ωm).

Serupa dengan hambatan dan konduktansi, kita juga dapat mendeskripsikan *resistivitas* dalam bentuk kebalikannya, yaitu *konduktivitas* $$\sigma$$:

$$\sigma = \frac {1}{\rho }$$

Satuan SI untuk konduktivitas adalah siemens per meter (S/m).

[Scherz dan Monk](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml) melaporkan beberapa nilai resistivitas (dan konduktivitas) material yang umum, yang diambil dari *Handbook of Chemistry and Physics*.

| Material   | Klasifikasi    | Resistivitas $$\rho$$ (Ωm) | Konduktivitas $$\sigma$$ (S/m) |
|------------|----------------|--------------------------|-------------------------------|
|Aluminium   | Konductor      | $$2.82 × 10^{-8}$$       | $$3.55 × 10^{7}$$             |
|Emas        | Konductor      | $$2.44 × 10^{-8}$$       | $$4.10 × 10^{7}$$             |
|Perak       | Konductor      | $$1.59 × 10^{-8}$$       | $$6.29 × 10^{7}$$             |
|Tembaga     | Konductor      | $$1.72 × 10^{-8}$$       | $$5.81 × 10^{7}$$             |
|Kuningan    | Konductor      | $$7 × 10^{-8}$$          | $$1.4 × 10^{7}$$              |
|Karbon      | Semi-Konduktor | $$3.5 × 10^{-5}$$        | $$2.9 × 10^{4}$$              |
|Silikon     | Semi-Konduktor | $$640$$                  | $$3.5 × 10^{-3}$$             |
|Kaca        | Isolator       | $$\sim10^{10}$$          | $$10^{-10}$$                  |
|Karet       | Isolator       | $$10^{9}$$               | $$10^{-9}$$                   |
|Teflon      | Isolator       | $$10^{14}$$              | $$10^{-14}$$                  |

<!-- See also http://spiff.rit.edu/classes/phys213/lectures/resist/resist_long.html -->

### Meningkatkan konduktansi dengan memperbesar ketebalan kabel

Seperti yang telah disebutkan di atas, kita dapat *meningkatkan* konduktansi sebuah kabel dengan cara *memperbesar* diameternya (seperti membuat "pipa yang lebih besar" untuk aliran arus). Merujuk kembali ke analogi air kita: sama seperti pipa berdiameter lebih besar dapat menampung jumlah aliran air yang lebih besar, kabel yang lebih tebal juga dapat menampung aliran arus yang lebih besar.

<!-- TODO: possibly insert figure (maybe from that PDF?) -->

Karena diameter kabel sangat penting untuk kapasitas arus, terdapat sistem pengukuran yang terstandardisasi. Di AS, sistem yang digunakan adalah [American Wire Gauge](https://en.wikipedia.org/wiki/American_wire_gauge) atau sistem AWG. Kabel dengan diameter 5.2mm (AWG 4) memiliki kapasitas arus sebesar 59.6A. Sebagai perbandingan, kabel prototipe rangkaian standar (0.64mm atau AWG 22)—lihat Gambar di bawah—memiliki kapasitas arus sebesar 0.9A.

![A picture of a box of AWG circuit prototyping wire and a complementary image showing that wire being used in a breadboard](assets/images/StandardSolidCorePrototypingWireOf22AWG.png)
**Gambar.** Contoh kabel inti padat (*solid-core*) AWG yang umum digunakan dalam pembuatan prototipe rangkaian. Kotak kabel di sebelah kiri seharga $29,95 untuk sepuluh gulungan masing-masing sepanjang 25 kaki dari [Adafruit](https://www.adafruit.com/product/3174).
{: .fs-1 }

Secara berlawanan dengan intuisi, angka AWG yang *semakin besar* menunjukkan diameter kabel yang *semakin kecil* (dan anehnya, ukuran AWG selalu berupa bilangan bulat tetapi bisa kurang dari 1 dengan simbol '0', '00', atau bahkan '000' untuk kabel yang sangat tebal).

Jika kita mengalirkan arus melebihi kapasitas kabel tersebut, kabel akan mulai memanas dan pada akhirnya terbakar. Sungguh, ini adalah prinsip bagaimana sekering (*fuse*) *dirancang* untuk bekerja! Sekering berisi kabel tipis yang melindungi rangkaian Anda dari arus tinggi yang merusak dan akan "terbakar habis" untuk langsung memutuskan rangkaian Anda (menciptakan "rangkaian terbuka") jika arus yang tinggi dialirkan. Anda kemudian dapat mengganti sekering tersebut, yang mana jauh lebih murah dan mudah daripada mengganti perangkat elektronik atau peralatan rumah tangga Anda. Ada banyak video bagus tentang hal ini di internet, termasuk [di sini](https://youtu.be/V-lhVTDWjwY?t=120) dan [di sini](https://youtu.be/qgz1lskyYDU?t=70).

<video autoplay loop muted playsinline aria-label="Slow-motion video of automotive fuses burning out when excessive current is applied, demonstrating how fuses protect circuits by breaking the connection.">
  <source src="assets/videos/BlowingFuses_RobinsonsAuto.mp4" type="video/mp4" />
</video>
**Gambar.** Jika kita mencoba mendorong arus dalam jumlah besar melalui kabel dan melebihi kapasitas daya tampungnya (dengan menghubungkan pasokan tegangan yang besar, misalnya), maka kabel tersebut akan memanas dan dapat memicu kebakaran. Hal ini dapat terjadi hampir seketika, yang merupakan prinsip kerja di balik sebuah sekering (ditunjukkan di atas). Sekering *dirancang* untuk terbakar sehingga memutuskan rangkaian Anda ketika arus yang sangat besar dan merusak dialirkan. Video dari [Robinson Auto](https://youtu.be/V-lhVTDWjwY).
{: .fs-1 }

<!-- TODO: can we totally ignore wire resistance? It depends. Typically, in basic circuit analysis, we do but this can become problematic if we employ the wrong wire sizes in practice. Nice discussion of cars, 12V batteries, and thick wiring here: https://learning.oreilly.com/library/view/make-electronics-2nd/9781680450255/ch01.html -->

<!-- ### Resistance increases with wire length

TODO?

Could have posille's law here? -->

### Apa itu resistor?

<video autoplay loop muted playsinline aria-label="An animated gif showing how resistors can be placed in a circuit to resist current flow.">
  <source src="assets/videos/ResistorCurrentFlow_EngineeringMindset-Optimized.mp4" type="video/mp4" />
</video>
**Gambar.** Animasi ini menunjukkan bagaimana sebuah resistor dapat ditempatkan di antara dua kabel untuk mengurangi aliran arus. Perhatikan bagaimana elektron mengalir bebas melalui kabel tembaga. Begitu melewati resistor, elektron-elektron ini "bertabrakan" dengan atom lain dan sesamanya, yang membatasi aliran elektron (dan juga mengubah sebagian energi menjadi panas). Animasi dari [The Engineering Mindset](https://youtu.be/kcL2_D33k3o?t=891).
{: .fs-1 }

Resistor adalah komponen listrik yang diformulasikan secara khusus untuk membatasi arus pada laju tertentu berdasarkan komposisi material dan konstruksinya. Dalam rangkaian listrik, kita menempatkan resistor di antara komponen untuk menurunkan arus. Mengapa kita ingin membatasi arus? Singkatnya, untuk melindungi komponen dalam rangkaian kita yang membutuhkan arus lebih rendah (seperti LED).

Sama seperti adanya penurunan tekanan setelah selang yang tertekuk, begitu pula terdapat penurunan tegangan setelah melewati resistor. Artinya, muatan listrik sebelum resistor memiliki potensial listrik yang lebih tinggi daripada setelah melewati resistor.

{: .note }
Kita akan membahas resistor lebih mendalam pada [Pembelajaran 5: Menggunakan Resistor](resistors.md), di mana Anda akan mempelajari bagaimana komponen ini dibuat, cara membaca gelang warnanya, dan cara menghitung disipasi dayanya.

<!-- **TODO: We'll talk more about this in Lesson X.** -->

## Beberapa pertanyaan umum

Sebelum melanjutkan ke pembelajaran berikutnya, mari kita bahas beberapa pertanyaan yang sering diajukan.

### Apa itu hubungan singkat (korsleting)?

<video autoplay loop muted playsinline aria-label="Animation of a short circuit in a simulation environment, showing a wire bypassing a light bulb and creating a zero-resistance path that causes excessive current.">
  <source src="assets/videos/ShortCircuitExample_PhetScreenRecording-Cropped2_ByJonFroehlich.mp4" type="video/mp4" />
</video>
**Gambar.** Sebuah **hubungan singkat** (*short circuit* / korsleting) terjadi ketika ada jalur berhambatan nol yang langsung kembali ke sumber daya Anda (*shortcut*). Hal ini tidak pernah berdampak baik! Korsleting dapat menyebabkan arus berlebih, membakar komponen, memicu kebakaran, atau bahkan menyebabkan ledakan. Berikut adalah [video](https://youtu.be/4fj5BLo27yw?si=UWbAml8UFQ_Gx4oy) dari empat baterai AA yang mengalami korsleting, sebuah [berita](https://youtu.be/75_f6CjIcz8) tentang bagaimana kebakaran rumah bermula ketika dua baterai 9V saling korsleting, dan sebuah [kiriman Stack Exchange](https://physics.stackexchange.com/a/30596) tentang korsleting pada satu baterai alkaline AA.

Ketika kita membangun rangkaian, kita jelas tidak mencoba membuat *korsleting*, tetapi hal itu bisa saja terjadi secara tidak sengaja. Sebagai contoh, kita mungkin secara tidak sengaja menghubungkan sumber 5V langsung ke ground, menempelkan dua kabel secara tidak sengaja, atau bahkan membuat koneksi yang tidak disengaja antara dua titik dalam rangkaian menggunakan obeng atau perkakas logam lainnya. Saat bekerja pada rangkaian Anda, selalu pastikan bahwa rangkaian tersebut dalam keadaan *tidak beraliran listrik* (mati) untuk mencegah korsleting yang tidak disengaja selama perakitan.

Bagaimana Anda tahu jika ada sesuatu yang korsleting? Anda mungkin mulai mencium bau sesuatu yang terbakar atau menyentuh kabel atau komponen listrik lain yang terasa sangat panas. Jika hal ini terjadi—dan ini pada akhirnya pernah dialami oleh kita semua—segera cabut sumber daya Anda!

Perlu dicatat bahwa port USB Anda dan mikrokontroler Arduino memiliki tingkat perlindungan korsleting tertentu. Misalnya, jika Anda mulai menarik terlalu banyak arus dari USB Anda, port tersebut akan (diharapkan) otomatis terputus. Dan rumah Anda, tentu saja, memiliki "sakelar pemutus arus" (*circuit breaker* / MCB) bawaan yang terpicu secara otomatis ketika arus berlebih ditarik (seperti yang terjadi saat korsleting). Lihat bagaimana cara kerja pemutus arus dalam gerak lambat [di sini](https://youtu.be/wGFnooeA6Iw?t=116) dan [di sini](https://youtu.be/wGFnooeA6Iw?t=284).

Ketika sakelar pemutus arus terpicu, ia akan menciptakan *rangkaian terbuka*, yang akan kita jelaskan selanjutnya!

### Apa itu rangkaian terbuka?

Sementara rangkaian **tertutup** (*closed circuit*) adalah rangkaian yang lengkap (sebuah "lingkaran" penuh untuk aliran arus), rangkaian **terbuka** (*open circuit*) adalah rangkaian yang *tidak lengkap*. Sebagai contoh, ketika tidak ada jalur dari terminal positif baterai menuju ke terminal negatif. Hal ini bisa terjadi secara sengaja (misalnya karena sakelar yang dibuka) atau tidak sengaja (misalnya rangkaian mati karena sekering yang putus).

<video autoplay loop muted playsinline aria-label="Animation toggling between a closed circuit with current flowing and an open circuit where the wire is disconnected and no current flows.">
  <source src="assets/videos/ClosedVsOpenCircuit-Cropped_PhetRecording_ByJonFroehlich.mp4" type="video/mp4" />
</video>
**Gambar.** Sebuah **rangkaian terbuka** adalah kondisi ketika **tidak ada jalur** yang menghubungkan antara terminal positif dan negatif dari sumber daya Anda. Rangkaian ini merupakan rangkaian yang tidak lengkap. Animasi dibuat dalam [Lingkungan Simulasi PhET](https://phet.colorado.edu/sims/html/circuit-construction-kit-dc-virtual-lab/latest/circuit-construction-kit-dc-virtual-lab_en.html).
{: .fs-1 }

### Apa perbedaan antara AC dan DC?

Rangkaian digital menggunakan **Direct Current** (**DC** atau Arus Searah), di mana arus hanya mengalir ke satu arah—ini persis seperti apa yang dihasilkan oleh baterai. Sebaliknya, stopkontak dinding Anda menyediakan **Alternating Current** (**AC** atau Arus Bolak-balik), di mana arus listrik secara berkala berbalik arah, biasanya berosilasi membentuk gelombang sinus. AC digunakan untuk jaringan listrik karena jauh lebih efisien untuk ditransmisikan dalam jarak jauh, karena tegangannya dapat dengan mudah dinaikkan atau diturunkan menggunakan transformator (trafo).

Namun, mikrokontroler dan logika digital bergantung pada ambang batas tegangan yang stabil untuk dapat membaca biner 1 dan 0 secara andal. Karena alasan ini, hampir semua perangkat elektronik—termasuk ponsel, laptop, dan Arduino Anda—secara internal membutuhkan arus DC. "Adaptor AC" atau "kepala pengisi daya" (*power brick*) yang disertakan dengan perangkat elektronik Anda bertugas melakukan tugas berat untuk mengubah arus AC dari dinding menjadi tegangan DC yang mulus dan stabil yang dibutuhkan oleh rangkaian Anda.

Ada banyak video bagus di YouTube yang menjelaskan perbedaan antara AC dan DC, seperti [yang satu ini](https://youtu.be/vN9aR2wKv0U) oleh AddOhms dan [yang ini](https://youtu.be/Wm75XgbqHBY) oleh KEMET Electronics.

## Aktivitas

{: .note }
> **Tujuan pembelajaran.** Di akhir aktivitas ini, Anda harus mampu mengidentifikasi peringkat tegangan dan arus input serta output pada adaptor AC-to-DC yang umum, serta menghargai rentang tegangan dan arus yang digunakan oleh perangkat elektronik sehari-hari.

Untuk mendapatkan pemahaman yang lebih baik tentang tegangan/arus operasional yang umum, kami ingin Anda mendokumentasikan tegangan/arus input AC dan tegangan/arus output DC dari perangkat-perangkat yang ada di rumah Anda. Pilih lima perangkat dan ambil foto dari perangkat beserta adaptor AC-to-DC miliknya dengan informasi operasional AC/DC yang terlihat jelas (jika Anda tidak dapat menemukan stiker ini, informasi tersebut mungkin tertera pada perangkat itu sendiri, yang juga tidak masalah). Di dalam jurnal prototipe Anda, sertakan foto-foto ini beserta tabel tegangan/arus input/output operasional dan ringkasan singkat dari apa yang Anda temukan.

![Three AC-to-DC power adapters showing their input voltage and current ratings on the label, along with the DC output voltage and current specifications.](assets/images/InputOutputVoltages_ThreeDevices_ByJonFroehlich.png)

**Gambar.** Berikut adalah contoh input AC dan output DC dari tiga perangkat di rumah saya.
{: .fs-1 }

<!-- Should probably talk about watts P= V * I. But don't want to overwhelm in first lesson. https://learning.oreilly.com/library/view/make-electronics-2nd/9781680450255/ch01.html has a nice introductory description of watts -->

<!-- ## ACTIVITY Idea:
- Have them work with an online circuit simulator like Tinkercad or [Falstad](https://www.falstad.com/circuit/circuitjs.html)

- Introduce the multimeter and how to measure voltage, current, and resistance
- Engineering Mindset has a good animation of [ammeter here](https://youtu.be/kcL2_D33k3o?t=718) -->

## Sumber Daya

### Simulator Rangkaian

Kami merekomendasikan simulator rangkaian dasar berikut (ini tidak ditujukan untuk analisis tingkat lanjut):
- [Falstad's CircuitJS](https://www.falstad.com/circuit/circuitjs.html). Sebuah platform web yang sepenuhnya gratis dan open-source untuk simulasi rangkaian yang dilengkapi dengan animasi rangkaian.
- [EveryCircuit.com](https://everycircuit.com/). Mirip dengan CircuitJS dalam mendukung simulasi animasi arus tetapi lebih kuat (dan juga tidak gratis, meskipun ada masa uji coba gratis). Tidak ada komponen 'kabel'; Anda perlu mengklik satu node lalu node lainnya untuk membuat koneksi.
- [Circuitlab.com](https://www.circuitlab.com/). Simulator rangkaian yang lebih tradisional yang kurang ramah untuk pemula/maker. Anda dapat menggunakan versi uji coba tetapi jumlah rangkaian yang dapat Anda buat terbatas tanpa akun berbayar.

### Tautan teks online

- [Chapter 2: Circuit Theory](https://learning.oreilly.com/library/view/practical-electronics-for/9781259587559/xhtml/13_Chapter_02.xhtml), Scherz & Monk, Practical Electronics for Inventors, 4th Edition
- [Basic electrical quantities: current, voltage, power](https://www.khanacademy.org/science/physics/circuits-topic/circuits-resistance/a/ee-voltage-and-current)
- [Voltage, Current, Resistance, and Ohm's Law](https://learn.sparkfun.com/tutorials/voltage-current-resistance-and-ohms-law/all), Sparkfun.com
- [Electrical Resistance and Conductance](https://en.wikipedia.org/wiki/Electrical_resistance_and_conductance), Wikipedia
- [Electromotive Force](https://opentextbc.ca/universityphysicsv2openstax/chapter/electromotive-force/), opentextbc.ca

<!-- https://www.physicsclassroom.com/class/circuits/Lesson-1/Electric-Potential -->
<!-- https://www.physicsclassroom.com/class/circuits/Lesson-1/Electric-Potential-Difference -->

### Tautan video

- [Intro to potential differences and voltage](https://youtu.be/pmtmJep1xY0), [Khan Academy](https://www.khanacademy.org/science/in-in-class10th-physics/in-in-electricity/in-in-electric-potential-potential-difference/v/intro-to-potential-difference-voltage)
- [Electronics for Beginners](https://www.youtube.com/watch?v=8gvJzrjwjds&list=PLzqS33DOPhJkRn6e9_OTdQwRojO8qlusI), [afrotechmods.com](http://afrotechmods.com/tutorials/)
- [Voltage, Current, Resistance](https://youtu.be/OGa_b26eK2c), [mathandscience.com](http://mathandscience.com/)
- [What is Ohm's Law?](https://youtu.be/lf0lMDZVwTI), [mathandscience.com](http://mathandscience.com/)
- [Engineering Circuits, Volume 1](https://www.youtube.com/watch?v=OGa_b26eK2c&list=PLnVYEpTNGNtUSjEEYf01D-q4ExTO960sG), [mathandscience.com](http://mathandscience.com/)
- [What is Voltage?](https://youtu.be/OGa_b26eK2c), Sparkfun.com
- [What is Current?](https://youtu.be/kYwNj9uauJ4), Sparkfun.com

<!-- 
MIT 8.02x lecture on electric charges, forces, and coulomb's law (polarization) by Walter Lewin: https://youtu.be/x1-SibwIPM4 -->

## Pembelajaran Berikutnya

Pada [pembelajaran berikutnya](schematics.md), kita akan mempelajari tentang representasi visual dari rangkaian—yang disebut [skema rangkaian](schematics.md), yang akan mempersiapkan kita untuk beberapa analisis rangkaian dasar dan [Hukum Ohm](ohms-law.md).

<nav class="lesson-nav" aria-label="Lesson navigation">
  <a href="schematics.html" class="nav-next">
    <div class="nav-label">Next Lesson &rarr;</div>
    <div class="nav-title">Circuit Schematics</div>
  </a>
</nav>