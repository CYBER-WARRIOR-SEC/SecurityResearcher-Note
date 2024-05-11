# Hari 2 - APT29, Midnight Blizzard (YTTRIUM) 
> 📢 18 April 2023 - Microsoft telah mengubah taksonomi penamaannya untuk pelaku ancaman, beralih dari menggunakan simbol unsur menjadi menggunakan [nama yang terkait dengan cuaca](https://www.microsoft.com/en-us/security/blog/2023/04/18/microsoft-shifts-to-a-new-threat-actor-naming-taxonomy/). Serangan APT29 diberi nama Midnight Blizzard dalam taksonomi penamaan baru Microsoft untuk pelaku ancaman. Dalam blog ini, saya akan menggunakan nama "YTTRIUM" sebagai gantinya daripada Midnight Blizzard.


## Apa itu YTTRIUM ? 
YTTRIUM adalah kode nama yang diberikan oleh Microsoft untuk kelompok aktivitas tertentu yang diyakini sebagai bagian dari APT29 atau Cozy Bear, sebuah kelompok ancaman persisten canggih yang disponsori oleh negara Rusia yang dikenal dengan aktivitas spionase cybernya. Kelompok ini dikenal karena menggunakan teknik peretasan canggih, termasuk spear phishing, eksploitasi zero-day, dan taktik rekayasa sosial untuk menargetkan lembaga pemerintah, infrastruktur kritis, dan organisasi berprofil tinggi lainnya.

> **Catatan** : Blog Keamanan Microsoft - "Pihak peneliti keamanan pihak ketiga telah mengaitkan serangan dengan aktor ancaman bernama APT29 atau CozyBear, yang sebagian besar tumpang tindih dengan kelompok aktivitas yang disebut Microsoft sebagai YTTRIUM"

### Apa perbedaan antara Yttrium dan Nobelium?
Yttrium dan Nobelium adalah dua kelompok ancaman terpisah yang telah dikaitkan dengan **APT29 (Cozy Bear) di masa lalu**, tetapi mereka bukan kelompok yang sama. Selain itu, kedua kelompok ini diyakini memiliki taktik, teknik, dan prosedur (TTP) yang berbeda dan mungkin menargetkan jenis yang berbeda.


## Rantai Serangan YTTRIUM 
APT29, juga dikenal sebagai YTTRIUM, memulai serangan cyber mereka melalui kombinasi **serangan email spear-phishing** dan **rekayasa sosial**. Tautan berbahaya dalam email, jika diklik oleh penerima, mengarah ke serangkaian eksploitasi yang pada akhirnya mengakibatkan pemasangan backdoor DLL. Backdoor ini memberikan akses jarak jauh kepada para penyerang ke mesin korban.
  
<img src="https://user-images.githubusercontent.com/120234772/228781349-a582f5e1-9721-404f-ae49-b15787592d64.png" width="70%">

> [Analisis serangan cyber terhadap lembaga pemikir AS, organisasi nirlaba, sektor publik oleh penyerang tak dikenal](https://www.microsoft.com/en-us/security/blog/2018/12/03/analysis-of-cyberattack-on-u-s-think-tanks-non-profits-public-sector-by-unidentified-attackers/)

#### Mengenai situs web yang dikompromi, apakah tautan email awalnya tidak jahat?
Ya, itu benar. Para penyerang mengompromi situs web yang sah yang pada awalnya tidak jahat. Dengan cara ini, para penyerang dapat menyimpan kode berbahaya mereka di situs web dan menyampaikannya kepada pengunjung yang tidak curiga.

#### Apakah alat keamanan email mencegah tautan awal yang jahat digunakan dalam serangan APT29?
Beberapa alat keamanan surat berhasil mengidentifikasi email spear-phishing yang digunakan dalam serangan APT29 pada saat itu, tetapi tidak semua alat keamanan dapat melakukannya. Ini tergantung pada alat tertentu yang digunakan. Saat ini, kebanyakan alat keamanan telah meningkatkan kemampuan deteksinya dan kemungkinan besar akan dapat mengidentifikasi serangan serupa.

#### Apa itu berkas LNK?
LNK adalah ekstensi berkas yang digunakan untuk Berkas Pintasan Windows. Ini adalah format berkas yang digunakan oleh Windows untuk membuat pintasan ke berkas, folder, atau program. Dalam serangan APT29, penyerang dapat membuat berkas LNK yang terlihat sah tetapi sebenarnya menunjuk pada kode atau situs web berbahaya.

#### Apa itu Cobalt Strike?
Ini adalah alat pengujian penetrasi. Dalam Cobalt Strike, pipa bernama lokal dibuat dengan format [**\\.\pipe\MSSE-<nomor>-server, di mana \<nomor>**] adalah nomor acak antara 0 dan 9897. Kemudian, penyerang terhubung ke pipa bernama dan mengirimkan data global dengan ukuran 0x3FE00. Akhirnya, penyerang menggunakan pipa bernama ini untuk mengimplementasikan backdoor, memberi mereka akses ke sistem yang tercompromi.

![image](https://user-images.githubusercontent.com/120234772/229047009-be2be785-b3c8-4759-9960-ffc14a79b1a3.png)
> Cobalt Strike, [Analisis serangan cyber terhadap lembaga pemikir AS, organisasi nirlaba, sektor publik oleh penyerang tak dikenal](https://www.microsoft.com/en-us/security/blog/2018/12/03/analysis-of-cyberattack-on-u-s-think-tanks-non-profits-public-sector-by-unidentified-attackers/)
  
## KQL : Pencarian
Di [blog Keamanan Microsoft](https://www.microsoft.com/en-us/security/blog/2018/12/03/analysis-of-cyberattack-on-u-s-think-tanks-non-profits-public-sector-by-unidentified-attackers/), mereka memberikan kueri pencarian yang sangat baik untuk APT29 (YTTRIUM). Namun, tabel yang mereka gunakan tampaknya sudah kadaluarsa. Oleh karena itu, saya memperbarui kueri-kueri ini menggunakan tabel terbaru untuk melacak mereka. Selain itu, saya menyoroti beberapa IoC yang dicakup dalam kueri-kueri out-of-the-box yang disediakan dalam blog tersebut.
  
#### IoC YTTRIUM
```kql
 SHA1 = "9858d5cb2a6614be3c48e33911bf9f7978b441bf"
 SHA1 = "cd92f19d3ad4ec50f6d19652af010fe07dca55
