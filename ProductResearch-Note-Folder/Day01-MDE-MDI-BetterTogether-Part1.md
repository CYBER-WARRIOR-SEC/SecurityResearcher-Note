# MDE + MDI lebih baik bersama-sama - Rekognisi
Halo para pembela dan pemburu ancaman, terima kasih telah mengunjungi catatan penelitian produk saya. Dalam seri blog ini, saya ingin fokus pada Microsoft Defender untuk Endpoint (MDE) + Microsoft Defender untuk Identitas (MDI) lebih baik bersama-sama, memperlihatkan berbagai keuntungan dari mendeploy kedua produk tersebut bersama-sama. Mari kita mulai dengan melihat rekognisi dalam Bagian 1.

### Rekognisi ?
Rekognisi adalah tahap awal di mana penyerang mengumpulkan informasi tentang jaringan atau sistem target, mengidentifikasi kerentanan, dan mengumpulkan informasi. Data yang dikumpulkan ini akan digunakan oleh penyerang untuk membantu dalam tahap-tahap serangan lainnya, seperti akses awal dan pencurian kredensial.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/ea593e3e-d171-4101-80b6-48e80a0aa0eb)

## Deteksi, XDR

Penyerang ingin mengumpulkan informasi Active Directory (AD) lokal terlebih dahulu, dan mereka menjalankan beberapa perintah 'net' pada perangkat yang dikompromi. Aspek penting dari mendeploy MDI adalah kemampuan untuk memvisualisasikan deteksi tentang apa yang terjadi pada perangkat yang dikompromi dalam hal identitas. Namun, jika Anda memiliki MDE (perlindungan endpoint), juga mungkin untuk melihat semua perintah yang dieksekusi oleh penyerang. Pada akhirnya, Anda akan dapat melihat peringatan yang dihasilkan oleh MDI dan MDE.

Pada saat ini, saya mensimulasikan [skrip ninja.ps1](https://github.com/LearningKijo/SecurityResearcher-Note/blob/main/ProductResearch-Note-Folder/Day01-MDE-MDI-BetterTogether-Part1.md#simulation) yang mengeksekusi beberapa perintah 'net' dengan encoding base64 pada perangkat yang dikompromi, yang sudah menjadi perangkat yang tergabung dalam domain yang dikelola oleh AD di lokasi dan dilindungi oleh MDE. Setelah beberapa menit, 1 insiden (yang berkorelasi dengan 3 peringatan yang dihasilkan dari MDE & MDI) muncul pada halaman Insiden pada portal Microsoft Defender XDR dan mari kita lihat setiap poin pentingnya.

#### Insiden, Korelasi XDR
| Judul Peringatan | Sumber   | Deskripsi |
|:-----------------|:---------|:------------|
| Rekognisi keanggotaan pengguna dan grup (SAMR) | MDI | David Ninja di Win11CC mengirimkan kueri SAMR mencurigakan ke Svr2016, mencari: semua pengguna dan semua grup di mdipoc.com, dan juga 2 grup sensitif. |
| Pencarian akun yang tidak wajar | MDE | Rantai upaya mencari informasi akun pengguna yang tidak wajar telah diamati. Seorang penyerang mungkin mengumpulkan informasi tentang target potensial.| 
| Serangkaian aktivitas eksplorasi yang mencurigakan | MDE| Sebuah proses mengeksekusi serangkaian perintah windows. Perintah-perintah ini dapat digunakan oleh penyerang untuk mengidentifikasi aset yang berharga dan mengoordinasikan pergerakan lateral setelah mengompromikan sebuah mesin.| 
> Detail dari peringatan yang dihasilkan dalam insiden

Perlu dicatat, kemampuan untuk mengkorelasikan peringatan dari produk Defender yang berbeda ke dalam satu insiden adalah salah satu fitur andal dalam Microsoft Defender XDR. Berkat kemampuan ini, halaman ini memberikan informasi tentang berapa banyak peringatan yang dihasilkan dalam serangan ini dan menampilkan entitas terkait dengan grafik yang komprehensif. Selain itu, untuk mengambil tindakan lebih lanjut, Microsoft Defender XDR menangkap semua aset terkait, seperti akun dan perangkat yang terlibat dalam serangan ini.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/5c2ebf8f-09ab-4336-838c-301da379eb75)
> Halaman Insiden : Penemuan insiden pada satu endpoint dilaporkan oleh beberapa sumber

#### Peringatan MDI
Terkait dengan deteksi identitas, MDI menghasilkan peringatan terkait rekognisi, menyediakan gambaran tingkat tinggi, detail serangan, dan grafik. Penyerang (dari perangkat yang dikompromi) menjalankan kueri SAMR yang mencurigakan ke server, mencari semua pengguna, grup, Domain Admins, dan Schema Admins.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/562f108f-c254-404f-a9c7-0f51d62b0e9a)
> Peringatan MDI : Rekognisi keanggotaan pengguna dan grup (SMAR)

#### Peringatan MDE
Manfaat lain dari mendeploy MDE adalah kemampuan untuk menangkap aktivitas tingkat perangkat. Berbeda dengan peringatan MDI, peringatan MDE memberikan detail tentang perintah yang dieksekusi pada perangkat yang dikompromi. Kemampuan ini memungkinkan untuk memvisualisasikan semua aktivitas perintah secara kronologis dalam cerita peringatan dan pemetaan semua entitas terkait, seperti skrip PowerShell yang mencurigakan, seperti yang disorot dalam 'Ninja.ps1'.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/641c457c-9dd6-4dba-a921-901b2cb6d3cd)
> Peringatan MDE : Pencarian akun yang tidak wajar, perintah yang dieksekusi

MDE dapat menangkap skrip PowerShell yang dipetakan ke teknik MITRE ATT&CK™. Selama simulasi saya, khususnya difokuskan pada rekognisi, kami mengamati beberapa taktik penemuan dan beberapa eksekusi.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/189ca17a-bc7f-40c8-9cd1-464a0002cee8)
> Peringatan MDE : Serangkaian aktivitas eksplorasi yang mencurigakan
