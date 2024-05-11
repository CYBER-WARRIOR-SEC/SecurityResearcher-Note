# MDE + MDI lebih baik jika digunakan bersama-sama - Rekognisi
Halo para pembela dan pemburu ancaman! Terima kasih telah mengunjungi catatan penelitian produk saya. Seperti yang kami fokuskan pada menjelajahi bagaimana Microsoft Defender untuk Endpoint (MDE) dan Microsoft Defender untuk Identitas (MDI) dapat bekerja lebih baik bersama-sama, dengan menekankan [rekognisi berbasis perintah pada Bagian 1](https://github.com/LearningKijo/SecurityResearcher-Note/blob/main/ProductResearch-Note-Folder/Day01-MDE-MDI-BetterTogether-Part1.md), kali ini kami akan beralih fokus ke rekognisi AD menggunakan beberapa alat pretesting.

## Alat Pretesting
Sebelum saya mulai menampilkan deteksi MDE + MDI, saya ingin menunjukkan sebuah simulasi. Simulasi ini cukup sederhana, dan yang harus Anda lakukan adalah menginstal alat-alat pentesting dan menjalankannya pada perangkat yang telah dihubungkan dengan AD dan telah terkompromi.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/b859cdc9-fddd-4b8d-8948-105005dc070b)

> [!Important]
> Alat-alat ini digunakan untuk simulasi serangan dalam blog ini. Harap gunakan mereka di lingkungan pengujian dan hindari menggunakan mereka di lingkungan produksi.
> 1. ORADAD - https://github.com/ANSSI-FR/ORADAD 
> 2. NetSess - https://www.joeware.net/freetools/tools/netsess/ 
> 3. ADRecon - https://github.com/sense-of-security/ADRecon

## Deteksi, XDR
Setelah menjalankan tiga alat pada perangkat yang telah dihubungkan dengan AD dan terkompromi, 1 insiden (yang berkorelasi dengan 9 peringatan yang dihasilkan dari MDE & MDI) muncul pada halaman Insiden pada portal Microsoft Defender XDR.
Karena saya terutama menggunakan tiga alat, mari kita lihat bagaimana alat-alat ini akan dipetakan pada halaman peringatan dalam konteks MDE dan MDI.

```
Insiden : Insiden multi-tahap yang melibatkan Akses Kredensial & Penemuan pada satu endpoint yang dilaporkan oleh beberapa sumber
    Peringatan : Sumber deteksi, Nama peringatan
        - EDR, Kemungkinan enumerasi data Active Directory menggunakan ADRecon
        - EDR, Serangkaian aktivitas eksplorasi yang mencurigakan
        - EDR, Penemuan Akun Pengguna yang mencurigakan
        - EDR, Upaya pencurian kredensial dari Akun Layanan Terkelola Grup (gMSA)
        - EDR, Kueri LDAP yang mencurigakan
        - EDR, Aktivitas alat serangan Layanan Sertifikat Active Directory
        - MDI, Rekognisi pengguna dan alamat IP (SMB)
        - MDI, Rekognisi prinsip keamanan (LDAP)
        - Defender XDR, Enumerasi sesi SMB pada pengontrol domain
```
> Semua peringatan yang dihasilkan setelah simulasi dalam Insiden    

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/97dcd6a3-c6cb-447e-be0d-9933234f99c0)
> Halaman Insiden : Insiden multi-tahap yang melibatkan Akses Kredensial & Penemuan pada satu endpoint yang dilaporkan oleh beberapa sumber

### Deteksi alat ORADAD dalam MDE & MDI
Pertama-tama, peringatan ini dihasilkan oleh MDI ketika sensor MDI mendeteksi aktivitas mencurigakan dari Win10BB. Sensor MDI memunculkan peringatan ketika Win10BB (perangkat yang terkompromi) mengirimkan kueri LDAP yang mencurigakan ke Kontroler Domain untuk enumerasi. Perlu dicatat bahwa MDI mencakup berbagai jenis enumerasi, seperti ***"AllObjects", "AllComputers", "AllUsers", dan "AllGroupPolicies"***.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/0ff61b3a-9e7a-4de7-9f72-325a6896721c)
> Peringatan MDI, Rekognisi prinsip keamanan (LDAP)

Dalam hal deteksi MDE, saya mengamati tiga peringatan :
- [x] Kueri LDAP yang mencurigakan
- [x] Aktivitas alat serangan Layanan Sertifikat Active Directory
- [x] Upaya pencurian kredensial dari Akun Layanan Terkelola Grup (gMSA)

Peringatan-peringatan ini memberikan wawasan tentang alat yang dieksekusi pada Win10BB oleh penyerang, bahkan menangkap setiap kueri LDAP yang dilakukan oleh alat (ORADAD) seperti berikut ini.

```query
< ----- Kueri LDAP yang mencurigakan ----- >
Kueri Pencarian LDAP (objectClass=group), Nama terhormat CN=
