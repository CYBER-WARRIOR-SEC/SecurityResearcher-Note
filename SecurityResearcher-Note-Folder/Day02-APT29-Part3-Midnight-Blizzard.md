# Hari 2 - APT29, Midnight Blizzard (NOBELIUM)
> 📢 18 April 2023 - Microsoft telah mengubah taksonomi penamaannya untuk pelaku ancaman, beralih dari menggunakan simbol unsur menjadi menggunakan [nama yang terkait dengan cuaca](https://www.microsoft.com/en-us/security/blog/2023/04/18/microsoft-shifts-to-a-new-threat-actor-naming-taxonomy/). Serangan APT29 diberi nama Midnight Blizzard dalam taksonomi penamaan baru Microsoft untuk pelaku ancaman. Dalam blog ini, saya akan menggunakan nama "NOBELIUM" sebagai gantinya daripada Midnight Blizzard.


## Apa itu NOBELIUM?
NOBELIUM adalah kelompok peretasan yang disponsori oleh negara Rusia yang melakukan spionase cyber dan serangan terhadap berbagai target. Sebelumnya dikenal sebagai APT29 atau Cozy Bear dan bertanggung jawab atas serangan berprofil tinggi seperti **serangan SolarWinds**. 

Menurut ***update blog Keamanan Microsoft***,
> Microsoft terus bekerja dengan mitra dan pelanggan untuk memperluas pengetahuan kami tentang pelaku di balik serangan siber negara yang mengorbankan rantai pasokan SolarWinds dan memengaruhi banyak organisasi lain. Microsoft sebelumnya menggunakan **‘Solorigate’ sebagai penunjukan utama untuk pelaku**, tetapi ke depannya, kami ingin menempatkan fokus yang sesuai pada pelaku di balik serangan canggih, daripada salah satu contoh perangkat lunak berbahaya yang digunakan oleh para pelaku. **Microsoft Threat Intelligence Center (MSTIC) telah menamai pelaku di balik serangan terhadap SolarWinds, backdoor SUNBURST, malware TEARDROP, dan komponen terkait sebagai NOBELIUM.** Saat kami merilis konten dan analisis baru, kami akan menggunakan NOBELIUM untuk merujuk pada pelaku dan kampanye serangan.

#### Kata kunci NOBELIUM
SolarWinds, backdoor SUNBURST, malware TEARDROP, serangan rantai pasokan, Solorigate 

## Rantai Serangan NOBELIUM
Para penyerang menambahkan kode berbahaya ke file DLL Platform SolarWinds Orion, yang didistribusikan sebagai bagian dari pembaruan perangkat lunak. Berkas DLL tersebut ditandatangani secara digital, menunjukkan bahwa para penyerang memiliki akses ke jalur pengembangan dan distribusi perangkat lunak perusahaan. Kode berbahaya menciptakan backdoor, yang memungkinkan para penyerang beroperasi di jaringan yang tercompromi tanpa terdeteksi. Backdoor dirancang untuk menyatu dengan bagian lain dari kode, sehingga sulit untuk ditemukan. Para penyerang menggunakan daftar panjang fungsi dan kemampuan untuk melakukan berbagai tindakan, termasuk rekognisi, eskalasi keistimewaan, dan pergerakan lateral. Para penyerang melakukan banyak langkah untuk menjaga profil rendah, seperti menggunakan subdomain unik untuk setiap domain yang terpengaruh untuk menghindari deteksi.

![image](https://user-images.githubusercontent.com/120234772/230338300-734224cb-f248-47df-8472-18aaa4f0c662.png)
> [Blog Keamanan Microsoft](https://www.microsoft.com/en-us/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect/), Rantai infeksi NOBELIUM

#### Proses awal
1. Berkas SolarWinds.BusinessLayerHost.exe adalah berkas yang sah yang digunakan oleh perangkat lunak manajemen IT SolarWinds Orion.
2. Aktivitas berbahaya tidak disebabkan langsung oleh berkas eksekutif, tetapi oleh file DLL yang terpengaruh yang dimuat ke dalam eksekutif.
3. Para penyerang dapat menyisipkan kode berbahaya ke dalam file DLL pada tahap awal pembangunan perangkat lunak, sebelum tahap akhir yang akan mencakup penandatanganan digital kode yang dikompilasi.
4. Berkas DLL yang terpengaruh ditandatangani secara digital, yang meningkatkan kemampuannya untuk menjalankan tindakan berkeistimewaan dan menghindari deteksi.
5. Kode berbahaya dirancang agar ringan dan berjalan di latar belakang, sehingga tidak mengganggu operasi normal perangkat lunak SolarWinds.
6. Begitu kode berbahaya dimuat, itu memungkinkan para penyerang untuk melakukan berbagai tindakan dan bergerak lateral di seluruh jaringan, dengan tujuan akhir mencapai tujuan mereka, yang mungkin termasuk spionase cyber atau keuntungan finansial.

## Respons Insiden, Penyekatan


### Apa yang harus dilakukan jika lingkungan Anda disusupi oleh APT29 (Nobelium)?
Jika lingkungan Anda telah disusupi oleh serangan Nobelium, langkah pertama yang harus Anda ambil adalah **"Penyekatan"**.
Tentang "Penyekatan", jika Anda menggunakan solusi Keamanan Microsoft seperti Microsoft Defender for Endpoint (MDE) atau Microsoft Defender for Identity (MDI), maka ambil tindakan berikut:
- [Isolasikan perangkat dari jaringan](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/respond-machine-alerts?view=o365-worldwide#isolate-devices-from-the-network)
- [Menyekat perangkat dari jaringan](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/respond-machine-alerts?view=o365-worldwide#contain-devices-from-the-network)
- [Atur ulang kata sandi akun pengguna](https://learn.microsoft.com/en-us/defender-for-identity/remediation-actions)
- [Nonaktifkan pengguna AD / pengguna Azure AD](https://learn.microsoft.com/en-us/defender-for-identity/remediation-actions)
 
Jika Anda tidak menggunakan solusi Keamanan Microsoft, maka ambil tindakan berikut:
- Segera isolasikan perangkat yang terpengaruh
- Atur ulang kata sandi atau nonaktifkan akun

![image](https://user-images.githubusercontent.com/120234772/230063443-8b3f59d1-d3b5-4e69-b667-c7b8e7c2ea21.png)
> Tahap manajemen respons NIST 800-61
Setelah penyekatan, beralih ke penyelidikan dan pemulihan.

## Menyiapkan untuk NOBELIUM 
Ini adalah **pesan kunci** dari Microsoft Defenders.

#### Prioritaskan kebersihan siber
- Manajemen kerentanan & Pembaruan
- Implementasi Zero Trust
- Lindungi identitas Anda, mis. Aktifkan MFA
- Gunakan perangkat yang aman untuk tugas-tugas kritis

#### Amanatkan kekayaan tersebar Anda
- Implementasi Zero Trust
- Butuh alat sistem monitoring canggih seperti SIEM, XDR dan EDR

#### Rencanakan respons Anda
- Kumpulkan data untuk investigasi lebih lanjut
- Manfaatkan Intelijen Ancaman untuk penyelidikan
- Butuh praktik/latihan yang baik dalam respons insiden khusus untuk serangan APT29
- Pikirkan tentang rencana respons insiden 
- Pikirkan tentang rencana pemulihan


### Video Decoding NOBELIUM: 
1. [Membongkar NOBELIUM: Ketika negara-negara menyerang (Episode 1)](https://www.youtube.com/watch?v=VVKT8NehO_c)
2. [Membongkar NOBELIUM: Pengejaran ancaman global (Episode 2)](https://www.youtube.com/watch?v=VVbSYr1cPEE)
3. [Membongkar NOBELIUM: Tindakan Pencegahan (Episode 3)](https://www.youtube.com/watch?v=fS97PC4FLCc)
4. [Membongkar NOBELIUM: Laporan Tindakan Setelah (Episode 4)](https://www.youtube.com/watch?v=wFtGD7p58cQ)


## Referensi
### Blog Keamanan Microsoft - NOBELIUM :
15 Desember 2020, [Memastikan pelanggan dilindungi dari Solorigate](https://www.microsoft.com/en-us/security/blog/2020/12/15/ensuring-customers-are-protected-from-solorigate/)<br>
18 Desember 2020, [Menganalisis Solorigate, file DLL yang terpengaruh yang memulai serangan siber canggih....](https://www.microsoft.com/en-us/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect/)<br>
28 Desember 2020, [Menggunakan Microsoft 365 Defender untuk melindungi dari Solorigate](https://www.microsoft.com/en-us/security/blog/2020/12/28/using-microsoft-365-defender-to-coordinate-protection-against-solorigate/)<br>
20 Januari 2021, [Peleburan kedua Solorigate: Dari SUNBURST hingga TEARDROP dan Raindrop](https://www.microsoft.com/en-us/security/blog/2021/01/20/deep-dive-into-the-solorigate-second-stage-activation-from-sunburst-to-teardrop-and-raindrop/)<br>
4 Maret 2021, [GoldMax, GoldFinder, dan Sibot: Menganalisis persistensi lapisan NOBELIUM](https://www.microsoft.com/en-us/security/blog/2021/03/04/goldmax-goldfinder-sibot-analyzing-nobelium-malware/)<br>
27 Mei 2021, [Serangan email baru yang canggih dari NOBELIUM](https://www.microsoft.com/en-us/security/blog/2021/05/27/new-sophisticated-email-based-attack-from-nobelium/)<br>
28 Mei 2021, [Membongkar kumpulan alat tahap awal terbaru NOBELIUM](https://www.microsoft.com/en-us/security/blog/2021/05/28/breaking-down-nobeliums-latest-early-stage-toolset/)<br>
27 September 2021, [FoggyWeb: Malware NOBELIUM yang ditargetkan menyebabkan backdoor yang persisten](https://www.microsoft.com/en-us/security/blog/2021/09/27/foggyweb-targeted-nobelium-malware-leads-to-persistent-backdoor/)<br>
25 Oktober 2021, [NOBELIUM menargetkan hak administratif yang didelegasikan untuk memfasilitasi serangan yang lebih luas](https://www.microsoft.com/en-us/security/blog/2021/10/25/nobelium-targeting-delegated-administrative-privileges-to-facilitate-broader-attacks/)<br>
8 Februari 2023, [Memecahkan salah satu serangan NOBELIUM yang paling baru: Seri Serangan Siber](https://www.microsoft.com/en-us/security/blog/2023/02/08/solving-one-of-nobeliums-most-novel-attacks-cyberattack-series/)


### Blog Decoding NOBELIUM :
1. [Bagaimana penyerang negara seperti NOBELIUM mengubah keamanan siber](https://www.microsoft.com

/en-us/security/blog/2021/09/28/how-nation-state-attackers-like-nobelium-are-changing-cybersecurity/)
2. [Pengejaran NOBELIUM, serangan negara paling canggih dalam sejarah](https://www.microsoft.com/en-us/security/blog/2021/11/10/the-hunt-for-nobelium-the-most-sophisticated-nation-state-attack-in-history/)
3. [Di balik upaya luar biasa untuk melindungi pelanggan dari serangan negara NOBELIUM](https://www.microsoft.com/en-us/security/blog/2021/12/02/behind-the-unprecedented-effort-to-protect-customers-against-the-nobelium-nation-state-attack/)
4. [Laporan terakhir tentang serangan negara NOBELIUM yang belum pernah terjadi sebelumnya](https://www.microsoft.com/en-us/security/blog/2021/12/15/the-final-report-on-nobeliums-unprecedented-nation-state-attack/)

#### Penyangkalan
Pandangan dan pendapat yang terdapat di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
