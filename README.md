# LAPORAN TUGAS BESAR: Eksplorasi Struktur Data Tree

**Matakuliah:** ET234203 Struktur Data dan Pemrograman Berorientasi Objek
**Nama / ID Kelompok:** Kelompok 2
**Bahasa Pemrograman:** Java
**Jenis Tree Dasar:** AVL Tree
**Variasi Modifikasi:** Height-Relaxed AVL Tree (HR-AVL)

**Daftar Sitasi / Referensi Ilmiah Paper Kajian:** 
1. *Paper Kajian 1 (Algoritma Standar Dasar)*: "Analysis of Self-Balancing Trees Algorithm Constraints in Main Memory Systems", *IEEE Transactions on Knowledge and Data Engineering*, Terbit 2018. 
2. *Paper Kajian 2 (Kajian Variasi Modifikasi / Paralel Relaksasi)*: "High-Performance Concurrent Height-Relaxed Trees for In-Memory Systems" (Penerapan performa penyeimbangan sistem asinkron berbasis *Concurrent Tree Threading* varian kelompok algoritma H-Relaxation), *ACM Symposium on Principles of Distributed Computing*, 2021.

---

## BAGIAN A: EKSPLORASI REFERENSI DAN LAPORAN (80%)

### 1. Problem Statement / Permasalahan
Secara fundamental matematis, struktur pohon AVL memiliki ketetapan hukum seimbang yang absolut dan kaku; batasan margin toleransi pada pembedaan *ketinggian / Balance factor (Bf)* setiap komponen akar simpul/node antara dahan sisi sebelah kiri dengan sebelahnya sama sekali tak pernah dizinkan melepasi atau lebih dari hitungan rentang margin ($\pm 1$). Perancangan pembatasan rigid ini memberikan kemurnian kecekatan proses pelacakan *(Search & Retrieving/Read query memory operation)*, dijamin optimal konstan pada pergerakan struktur kedalaman rasio laju kecepatan O($\log N$). Namun ironisnya, sifat superior matematis murni AVL normal memancarkan bencana terselubung tatkala ia dijadikan pondasi implementatif memori sentral di lingkungan nyata basis peladen / sistem *Servers High Load Multi Core - Pararell - Threading Operation Writes*, yakni problem keterbatasan kelumpuhan (*Bottle Necks system concurrent access - memory Blocking!*). 

Dalam realita transaksi ribuan tulis masukan Node *Key Values*, seketika Tree mendapati tambahan node di bawah daun yang menyalahi kestabilan rumus struktur rentang ($\Delta h \geq 1$) – Thread komputer segera mensyaratkan kuncian hak prioritas utuh terhadap Tree (*locking resources / Thread System Mem lock exclusivities*) untuk tidak dilanggar eksekutor pengiriman manapun! Masalah diperkeruh tatkala siklus Lock menyebar menjulur berentetiian dari Sub *node root* bersangkutan mengejar proses reposisi dan matematika Putaran Struktur ke sub titik asal muasal ter-atras/Top Level Branch di memory! Skema menyeimbangkan pada-saat-tersebut-pula (*Synchronus re-Balacing Nodes Constraints Updates Level Limits Tasks*) menciptakan durasi antrian *Lock/Blok Thread Request API Tulis Baru/Inserstion writes delays Operations System server* klien.

### 2. Penjelasan Struktur Tree Dasar dan Variasi Modifikasi Pohon  (Secara Logika Struktural/Algoritmiknya)
Varietas *Tree Tinggi Termodulsi Tolerasi Level Asinkrone* (Seri WAvls mapun jenis H-Relaxation Trees Termodifikasi / HR Avl) secara langsung mengekslusifkan logika "Dekupling", menjauhkan peran rutinitias Pengeditan Data berbentrok dengan Ekseksusi Rotasional: 

*   **Standard Klasik Pohon Normative Base: AVL Basis Tree Sinkrons (Immediate Maintenance Updates Rules):** Mekanika berjalan berkoloni secara pararel padu saat menyatu dengan Metode Pemrograman `Updates Insertion/Deletes keys val Node()`. Modul seketika memeriksa secara " *Bottom checks Validities*" serentetan Level ketingganya; Bilamana terjadi satu kekacauan Elevasi level melampuai rasio aman  limit-nya di cabang mananapun, Perangkat *Threading CPU Codes Processor Memory Eksekustive Node Root Tree Structure*, Segera melaksanakan putaran koreksionis. Kuncian terfokus terhadap sistem untuk operasi-penyelematan sebarisan putar (*Rotation Single L, Right atau double*)- ini terjadi detik itu pula sebelum akhirnya operasi peletakan dikirim ke luar. (Mengutamakan Keidealan Level dari-pada melonggarkan permsisikan Antiran Write masif yang mengular / Cost throughput Penuruan Sangat Sigfnifikn - Delay Kuncian!  )

*   **Arsitektur Sistem Modifikatis Asynkrone Relaxses (Variatif Kelompok HR / HR-Avl  Logic - Phase Separations / Delegasi Tasks Asynchroned Decoulings Levels Limit Constraints H). :** Dalam kerangkan Algortma Terelasaski , fase Mutalis (*Penyarangan nilai masuk Nodes Write*), dengan Sistem Rehabilitais Pohon *(Maintenance Task Re-Balance Tree Structures Sweep System / Rotators*), diekstarksir menjadi elemen Ekseksusi berbeda ! Disini terdapat "fasa *Kelonggaran Batasan Height Relax Tolerance *", ketika nilai nodes keys masuk mengurakan nilai Tinggi hingga sangat membedaki (*jauh melawati Nilain Absoult 1; sepeseti differenisal tingakt > = \2* ) . Operasi Node Modifikaite insrets menolak/mendeklerer tidak dilakunana perturan di waktu itu- operasi berjalan ssingkatan layaktnta perisislap tree Linear / BTS Normail O Linear murnia , meleepskak kembali antiras dan Locks kuncu , Memberkan flag Status Memsan / "Meta tag Garbage : Butuh Reablance". Pada Titik Intervensia Interval diam  (Idle cycles/ Pekerjana Pekerj Thread Bakgruond Cleaner Memory Allocators Process Server Cloud Engine ) di aktkian meyingirkatn  *flags rebalansia tading *, sehingga sistem writes throughput ber-keceptn berlibat lipal di Banding Sistem Awwlas sinkrontan/Normal Base Clasikes !!

### 3. Diagram / Visualisasi Struktur Konsep Konkurensi

Bagian ini mengilustrasikan perbedaan drastis pada siklus "Waktu Tahan Sistem" ( *System Lock Contention*) antara pendekatan arsitektur Pohon AVL konvensional berhadapan dengan rancangan Asinkron HR-AVL modifikasi ketika menerima penambahan entri sub-node ekstrem yang merusak fondasi keseimbangan batas rasio $\pm1$.

**Visualisasi Model A: Standar Strict AVL (Fase Rotasi Seketika Memblokir Thread Node)**
Ketika node baru memecahkan keseimbangan level tinggi pada dahan Tree (Unbalanced), proses penyisipan langsung dikerjakan seketika. Tree memanggil *System Memory* memberlakukan Kuncian / Akses "Tahan Paksa" (Lock) guna mencegah klien API multithread masuk hingga matematika iterasi penataulangan (*rebalancing rotasi Node sub*) tuntas terevaluasi oleh unit inti pemroses/CPU!

```mermaid
graph TD;
    A((Root Terkunci / Lock Root Sync!)):::lock --> B[Sub-Cabang L: Terblokir State Tahan];
    A --> C((Sub-Kanan - Titik Kunci Mutlak)):::lock;
    C --> D(Level Penahanan: Validasi Re-Height...);
    C --> E[Data Pushed - Insertion Costly Time!];
    classDef lock fill:#ffcccc,stroke:#ff0000,stroke-width:2px,color:#000;
```

**Visualisasi Model B: Modifikasi HR-AVL (Konsep Delegasi Tahap Rileks / Thread Bypass Sinkronisasional Cepat) :** Ketika beban insersi yang sangat merusak (ekstrem Over-height 
Δ
H
≥
2
ΔH≥2
) menyakiti kestabilan, ia diberikan "Izin" atau relaksasi (Tolerance State) oleh mesin moduler Phase Tahap Insersi ini. Modifikasi arsitektur menghindari paksaan penyamaan siklus di Thread Pertama—operasi membalas eksekusi dengan keutamaan Linearitas O
(
1
)
(1)
/O
(
h
L
i
n
e
a
r
)
(h 
Linear
​
 )
. Sebuah Metadata (Relax Tag Needs Repair) ditinggalkan terpatri di alamat Memori Node; ini dirancang untuk segera dihapus secara kolektif di interval ekseksusi terpencil pada waktu siklus senyap background system bekerja (Cleaner sweeper thread). Sistem melepas (release) "kuncian"-nya seper-sekian mili detik seketika node terkait ditempel ke Memori Bawah agar antrean ratusan insersi Thread Node klien server sistem paralel merespons berentet sigap & amat mulus, Tanpa Intervensi Hitungan Root atas.

```mermaid
graph TD;
    80((80 - Sistem Level Tetap Dapat Diakses Klien Kapanpun!)):::ok --> 50;
    80 --> 90;
    50((50 - Ketinggian Rusak/Ekstrem Margin )):::relax --> 40;
    50 --> 60;
    40((40 - 'MetaTaging Needs Sweep Cycle Iterative Balance!')):::relax --> 30((30 - Linear O. Instan / Langsung di Eksekusi Terselip));
    
    classDef relax fill:#ffe599,stroke:#e69138,stroke-width:2px,stroke-dasharray: 5 5,color:#000;
    classDef ok fill:#b6d7a8,stroke:#38761d,stroke-width:2px,color:#000;
```

### 4. Aplikasi dan Lingkup Ranah Implementasinya Di Ranah IT Perusahaan
Pengadaptasian fundamental Modul algoritma pohon yang "Membagi/Merelaksasikan Atribut Ketetapan Level Constraint", layaknya tipe varian HR-Trees (Height Relaxed) W-AVL / R-B Mod Tree menjadi struktur dominan dalam membenahi problematika bottlenecking locking node concurrency. Hal itu terimplementasikan erat di fondasi lingkungan Industri TI bersistem "Skalabel Pararel Intens":

* Platform Cloud Database In-Memory Multi-core (Mesin Server Redis Modulasi & NoSQL Lock-Free System Tables): Infrastruktur Mesin tabel virtual Database, terkhusus pemuatan memori bertensi pararel ekstrim. Dimana alokasi jutaan antrean mutasi penulisan memori (Pushing Massive write/Insertion data load request Server Throughputs Threads logs Arrays Key=val memory engine) berlangsung dalam kisaran order puluhan nano detik. Mereka amat rakus mengakses simpul indeks/struktur memori bawah dengan kebutuhan mendesain model kunci thread halus bersudut isolasi lokal minimum. (Skala lock micro local / fine grained rebalance node decoupling).

* Virtual Core Cache Tabel Router Peralatan Sistem Distribusi Basis Protokol TCP/Jaringan Skala Inti/Periphery Internet ISP Backbone :
Jutaan aliran masukan baru log penugasan entry Address ip jaringan dipusatkan melintas kedalam log memori tanpa mampu menunggu komputasi Penyeimbangan Rumit. Operasinya mewajibkan Tree Index berskala log O
(
log
⁡
N
)
(logN)
, untuk prosesi Query Pencarain super nge-but instans seiring berbarengannya pemindahan pencatatan insersi Routing log paralel secara bersama tanpa tersumbat blok antrean !


### 5. Keunggulan HR-AVL (Modifikasi Tree Terelaksasi)
Berdasarkan pendekatan pemisahan ( *decoupling* ) logika antara operasi manipulasi data dan operasi pemeliharaan arsitektur pohon, modifikasi HR-AVL menawarkan serangkaian keuntungan absolut dalam ekosistem sistem memori berkecepatan masif:

*   **Peningkatan Throughput Operasi Penulisan (*Writes Throughput*):** Merupakan nilai jual paling mutlak dari modifikasi HR-AVL. Kecepatan insersi dan mutasi pada data (*Insert/Delete*) sangat tinggi hingga melesat berlipat ganda dikarenakan eksekusi algoritma pembaruan langsung memberikan status respons balik ke klien tepat saat proses alokasi node (peletakan memori lokal dahan terbawah pohon) berhasil ter-registrasi di dalam RAM tanpa diinterupsi antrean durasi pengerjaan sistem kalkulasi putaran akar Node ter-atasnya!
*   **Minimalisasi Persaingan dan Kebuntuan Siklus Sinkronasi (*Minimizes Thread-Lock Contentions/Dead-locks!*):** Sistem relaksasi ini sangat mengedepankan pendekatan wilayah eksekutorial Kunci-Berlingkup Mikro (*Fine-Grained/Lock-Free localized nodes*). Antrean benang operasi / multi-thread yang secara ekstrem bersama-sama menjebol gerbang Node API tak lagi di sandera/disumbat, membebaskan siklus sistem terhalang yang sebelumnya dikurung mutlak di sekujur badan/batang-sampai-keakar Node sentral utama pada Algoritma Normal Klasikal. Algoritma pembersih (Sweeper latar) meniadakan gejala antrean tertunda tak tertebak sistem secara total di saat puncak kepadatan penyerapan log harian.
*   **Optimalisasi Interval Pemrosesan Unit Cloud Server multi Core (Batching Optimizations Cycle CPU):** Menyerap sumber daya server core-multithread secara efektif. Pekerjaan memurnikan atau perapihan kurva arsitektur level log tree baru dipacu (dilakukan secarabongkahan masal/*Batches-tasks Queue cycle*) menumpang waktu longgar disaat core Processor idle dari trafik beban Tulis-Server!

### 6. Kekurangan & Biaya Konsekuensi Pengaplikasian H-Relaxed AVL
Konsep modifikasi fleksibel/Longgar yang dihadirkan, memaksa beberapa kelemahan arsitektural hingga kerumitan manajerial dalam hal pengelolaan logis program/sistem di level *backend memory server*, diantaranya:

*   **Degradasi Pelemahan Durasi Pembacaan / Pencarian Kurva Limit O-Search Tree Temporer:** Trade-off dari *insersi super-cepat asinkron* membuat simpul Tree bisa melenceng merusak ketinggian, pohon menjulur ekstrem tajam melebar sementara waktu. Bilamana intervensi unit pembantu sistem pemungut (*Background Sweepers Maintenance Cleaners Threads*) gagal turun lapangan/tersangkut tertunda (*Thread starvations*), performa fungsi Kueri akses lacak get nilai bacaan Nodes *(Searching Read Nodes Retrieval Ops)* melambat dan tersiksa drastis! Pohon kehilangan keunggulan konstan kurva sempurnanya ($\mathcal{O}(\log n)$ bisa sementara membusuk hingga condong ke $\mathcal{O}(H_{depth})$, sampai petugas rebalance diterjunkan kembali membersihkannya ke akar normatifnya).
*   **Melambungnya Kompleksitas Kerangka Basis Kodikasi / Beban Manajerial Rekayasa Perangkat Lunak:** Modul asinkron membebani tugas insinyur pembangun kode untuk berfikir tentang sistem *Delegators / Garbage tags* koleksi. Sistem ini dipenuhi implementasi logika alokasi bendera "Nodes flags pointers meta datas", desain Manajemen siklus perulangan utas belakang memori server multi-processor. Implementasi memicu kode kotor/rumit hingga kebingungan siklus isolator algoritma alokasi Memori C/C++ RAM mesin inti / pointer ber-eskalasi bocor memori *leaks* apabila dieksekusi koding programmer ceroboh. 
*   **Penyitaan Metrik Spasi Lebar Ruang Tambahan *(Variables overhead limits space per nodes bytes)*:** Pengorbanan alokasi metadata pada variabel ekstra bagi seluruh ratusan jutaan simpul (penitipan tag status bit *"Are Needs Clean/Balance Status "* atau variabel indikasi ter-relaksasi) memaksa pohon mensintesis muatan berat untuk dimensi memori penyokong sistem pusatnya, merubah kerangka nodes tree menjadi tak selangsing desain Klasik primitif.

### 7. Perbandingan Antara Tree Dasar dan Modifikasi (Secara Teori)

Sebagai ringkasan teoritis dari desain konseptual yang diusung oleh masing-masing pendekatan, tabel komparasi di bawah ini menjabarkan pergeseran sifat/kriteria algoritma konvensional berhadapan dengan model struktural HR-AVL (Height-Relaxed):

| Indikator Perbandingan | Tree Klasik Standar (Strict AVL) | Varian Tree Modifikasi (HR-AVL) |
| :--- | :--- | :--- |
| **Batas Aturan Tinggi (*Balance Factor / Kriteria Selisih Sub-tree*)** | Kaku & Rigorous. Secara konstan dipertahankan pada margin wajib mutlak: Maksimal **$\Delta h = \pm 1$**. | Relaks & Fleksibel (*Tolerated Level Limits*). Level penyimpangan ditolerir sementara bisa sangat melampaui **$\Delta h \geq 2$**. |
| **Pelaksanaan Manuver Rotasi / Mekanisme *Balancing*** | Disisipkan (Inline/Sinkron) di dalam modul `Insert` / `Delete`. Perputaran paksa langsung bekerja sesaat pasca insersi elemen data pada urutan operasi pengeksekusian beruntun *User/API.* | Mekanik "Desinkronisasi Terpisah" (*Deferred Rebalance Approach*). Pekerjaan rotasional dirapelkan secara parsial dalam jeda masa henti interval utas (Tertunda via perambatan unit Pekerja Latar Eksekutor Laten - *Cycle Idle Sweep Threads!*). |
| **Dampak Mekanika Ekseksui Paralel *(Conurrency Threads Lokcing Space Domain)*:** | Puncak hambatan terluas: Sifat pengunci iteratif sering membeku merantai memanjang dari nodul sisipan dasar ke Batang Level Atribut Pusat Root - menahan gerbang *Input.* (*Extensively Global lock Area-Bottleneck Path*)! | Sifat penyandraan thread operasi minimum *Local*. Algoritma cepat meninggalkan (Release pointer API seketika Data merasuk sukses tertaut!), membuka ruang masukan gerbang lebar (*Lock-Free Decouple Area*) |
| **Konvensi Habitat / Lingkungan Fokus Unggulan Sasaran** | Pustaka indeks kueri server pembaca intensif rutin (*Heavy Read-Query Orientated Environment Storage System!*). | Berkemampuan ekstream memukul traksi pencatatan gelombang lalu lintas data baru TULIS MASAL bersamaan waktu / (*Sangat memihak Super Writes Overloaded Environment Systems/Buffers Servers*). |


### 8. Analisis Kompleksitas Berdasarkan Struktur Tree (*Big-O Metric Bounds Analysis*)

Secara fundamental sistematis *(Metrik Time dan Bound Notasi Big-O - Notasi durasi/Kerapatan batas matematis maksimal sistem saat menerima beban kuantitas  ($n$) data Simpul/Nodes dalam sistem memori Tree*), Berikut merupakan pergeseran biaya dan kompleksitas diakibatkan metode Isolatif *HRAvl mod*.

| Matriks / Skenario Eksekusi Pohon (*Operation Costs Metrics*) | Strict AVL Tree Base (*Struktur Fundamental Dasar Konstan*) | Variasi Relaksasi Modifikasi: (*Asynchron HR-AVL Trees*) | Bukti Pembedaan Sifat Kompleksitas Model Asinkron *Mod-Tree HRAvls!* |
| :--- | :--- | :--- | :--- |
| **Maximum Degradable High Paths Level Limits (*Resiko Beban Panjang Cabang/ Tinggi Terdalam*)** | Stabil/Terpatok aman sebatas Tinggi konstan Rasio log : <br>**$\approx \mathcal{O}(1.44 \log n)$** | Mengalamsi sifat Temporarily-Degradable Curve Depth hingga anjlok turun melebar menuju batas setara limit pohon ekstrim sebelum rapi: <br> Maks **$\approx \mathcal{O}(2 \log n)$** | Memunculkan pelemahan elevasi *(Over heights Degradasi Node sub pointer Limits!)* untuk rentang jangka pendek menembus $\mathcal{O}$ log konvensional tatkala proses 'Petugas Cycle Cleanup Backround' sedang mengalami Tunda waktu masuk/Turun memotong Node sampah (Belum bekerja) . |
| **Query Traversals Operations (Search Get Keys Nodes /  Latensi Deteksi Unsur *Retrievals*)** | Tetap mengunci sifat absolut pada metrik rasio penulusaran optimal Tree : <br>**$\mathcal{O}(\log n)$** mutlak!. | Tersikapi dinamis dan Temporarily Labil (Kurva menanjak membeban Fluktuat) $\rightarrow$ *Berotasi Mengkikuti Besarnya Margin Kecacatan Lebar $\Delta H\_Tingkat$ / Elevasi Saat Dicari sebelum Rotated Kembali.*  | Pada Kondisi Area node yang cacat belum sempat disisir oleh thread latarnya $\rightarrow$ Pencarian memakan cost Travers level Linear memburuk memanjangkan jarak lacak ke Log. Begitu Cycle Sweep Berhasil Merotasinya$\rightarrow$ Waktu akan Sehat sempurna kembali  secepat O ($\log n$) Normal Classikal!|
| **Write API Operattion (*Inserting* / Penanaman, Hapus Menulis  Nodes Nilai Memoris)!** | Menyedot waktu lambat menyertakan iteratif rotasion path di cost :<br> **$(\mathcal{O} \log n)$** $_\to h_{depth} $ ditambah  *( $+ K$- Cost Rotasi Limits Eksekusions Seketikalitas! )* | Berfokus melibas beban Cost Lock, memutar kembali sistem  sangat pesat/Amortasi nyaris Linier-Cepat layaknya Penancapan Murni  se-Kilat sub Tree (C-BTS / Normal Branch) tanpa eksekusi Rotasi.<br> | Penanggungan Batas Hitung Perulangan Sinkron pada Node-Path/Pointer (Algoritama Penempatan Putar *Top Nodes*) di pangkas murni  menjadi pengiriman kembali "Callback Responses - Suksses-Writes/Done", Sekilat node berhasil merapat tanpa harus memvalidasikan Tinggi di sekeliling sub Tree Pohonya .|
