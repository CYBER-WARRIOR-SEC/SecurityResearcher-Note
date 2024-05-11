# Hari 2 - APT29, Midnight Blizzard (NOBELIUM), Laboratorium Evaluasi

📢 18 April 2023 - Microsoft telah mengubah taksonomi penamaan untuk pelaku ancaman, beralih dari menggunakan simbol unsur ke penggunaan [nama terkait cuaca](https://www.microsoft.com/en-us/security/blog/2023/04/18/microsoft-shifts-to-a-new-threat-actor-naming-taxonomy/). Serangan APT29 dinamai Midnight Blizzard dalam taksonomi penamaan baru Microsoft untuk pelaku ancaman. Dalam blog ini, saya akan menggunakan nama "NOBELIUM" sebagai gantinya daripada Midnight Blizzard.

Pada [Laboratorium Evaluasi Microsoft Defender for Endpoint (MDE)](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/evaluation-lab?view=o365-worldwid), simulasi serangan Solorigate (NOBELIUM) dicakup. Selama waktu ini, saya akan terutama fokus pada menunjukkan kemampuan deteksi MDE dan bagaimana MDE menangkap serangan sebagai EDR, XDR. Selain itu, kemampuan respons yang tersedia dari produk akan disajikan.

![image](https://user-images.githubusercontent.com/120234772/231689408-6805a007-69c2-46db-a834-f11e7a5d1870.png)
> Solorigate di Laboratorium Evaluasi MDE

## Respons Insiden dengan Microsoft 365 Defender
Selama respons insiden, ada berbagai pendekatan dan skenario, dan Microsoft menawarkan dokumentasi komprehensif tentang respons insiden untuk Microsoft 365 Defender. Pada saat ini, saya ingin fokus pada **penahanan** dan **investigasi**, seperti yang disorot dalam garis biru di bawah ini:
![image](https://user-images.githubusercontent.com/120234772/231698357-8ba1ef53-4c19-4ca8-9eba-0aba46681b06.png)
> alur kerja respons insiden, [Respons Insiden dengan Microsoft 365 Defender](https://learn.microsoft.com/en-us/microsoft-365/security/defender/incidents-overview?view=o365-worldwide)

## Respons Insiden, Investigasi

### Mari kita teliti detail insiden tersebut

Berikut adalah beberapa poin penting yang perlu dipertimbangkan selama [investigasi](https://learn.microsoft.com/en-us/microsoft-365/security/defender/incidents-overview?view=o365-worldwide).

1. Di mana serangan dimulai.
2. Taktik apa yang digunakan.
3. Seberapa jauh serangan masuk ke dalam penyewa Anda.
4. Ruang lingkup serangan, seperti berapa banyak perangkat, pengguna, dan kotak surat yang terdampak.
5. Semua data yang terkait dengan serangan.

>**Catatan**: Saat memulai investigasi, penting untuk menavigasi ke **halaman insiden** daripada halaman peringatan. Hal ini karena bisa ada volume peringatan yang besar dan orang mungkin menjadi bingung atau tidak yakin dengan apa yang perlu mereka temukan.

| [Ringkasan] | Titik periksa |
|:---|:---|
| Taktik MITRE ATT&CK | Analisis cakupan penuh serangan menggunakan kerangka kerja MITRE ATT&CK. |
| Ruang lingkup | Periksa aset yang terdampak seperti perangkat, pengguna, kotak surat, dan aplikasi.|
| Bukti | Pastikan bahwa semua aktivitas mencurigakan terkait dengan insiden diidentifikasi. |
| Peringatan | Periksa timeline dari peringatan-peringatan tersebut. |

contoh: 
Pada saat insiden terjadi, saya bisa melihat bahwa 23 peringatan terkait dengannya dan [testmachine8] adalah perangkat yang terdampak yang memerlukan tindakan (penahanan) untuk diambil dalam respons insiden. Dalam hal aktivitas mencurigakan, MDE telah mendeteksi 31 entitas.

![image](https://user-images.githubusercontent.com/120234772/231705669-82ce321d-d4c2-41df-ada8-43662ddf604d.png)
> Ringkasan, Halaman Insiden

| [Kisah Serangan] | Titik periksa |
|:----|:----|
| Grafik Insiden | Periksa bagaimana aset Anda terkait dengan entitas dan aktivitas mencurigakan menggunakan grafik.  |
| Peringatan (Timeline) | Periksa berapa banyak peringatan yang terkait dengan insiden, serta timeline dari peringatan-peringatan tersebut. | 

contoh: 
Dalam timeline serangan, sejak peringatan dimulai dari "layanan mencurigakan diluncurkan," mungkin layanan tersebut telah membuat file-file berbahaya tambahan atau bahkan membentuk koneksi C2C. Juga, saat saya memeriksa grafik insiden, saya bisa melihat bahwa testmachine8 terhubung ke 'panhardware.com' dan file serta proses terkait.

![image](https://user-images.githubusercontent.com/120234772/231706242-4623984f-8853-48e5-8e02-6e71c4ad3f91.png)
> Kisah Serangan, Halaman Insiden

### Mari kita teliti lebih dalam peringatan tersebut
Ini adalah salah satu peringatan dalam insiden. Serangan dimulai dari sbsimulator.exe dan sbsimulation_sb_340461_bs_293713.exe membuat file bdata.bin yang terdeteksi sebagai aktivitas berbahaya.

![image](https://user-images.githubusercontent.com/120234772/231714249-885594bd-be8b-439a-a2e1-863dffd3b04a.png)
> Kisah Peringatan, Halaman Peringatan

Setelah menganalisis timeline peringatan, ditemukan bahwa semua aktivitas mencurigakan terkait dengan APT29 tertangkap di perangkat oleh MDE. Saya telah merangkum apa yang memberitahu kita timeline tersebut.

![image](https://user-images.githubusercontent.com/120234772/233934128-8bb8670b-bccd-484e-90ce-6d4acf8fb79a.png)

## Respons Insiden, Penahanan
Terkait penahanan ***perangkat yang terdampak***, MDE memiliki kemampuan untuk secara remote mengisolasi jaringan dari perangkat.
- [Isolasikan perangkat dari jaringan](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/respond-machine-alerts?view=o365-worldwide#isolate-dev

ices-from-the-network)
- [Batasan perangkat dari jaringan](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/respond-machine-alerts?view=o365-worldwide#contain-devices-from-the-network)

Juga, jika ***akun pengguna*** berdampak pada pelanggaran, maka opsi respons lainnya tersedia.
- [Setel ulang kata sandi akun pengguna](https://learn.microsoft.com/en-us/defender-for-identity/remediation-actions)
- [Nonaktifkan pengguna AD / pengguna Azure AD](https://learn.microsoft.com/en-us/defender-for-identity/remediation-actions)

![image](https://user-images.githubusercontent.com/120234772/231706957-6b6e2e71-ed9c-4d02-afbf-06a59f9c9825.png)
> contoh: Isolasikan perangkat dari jaringan 

#### Penafian
Pandangan dan pendapat yang dinyatakan di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
