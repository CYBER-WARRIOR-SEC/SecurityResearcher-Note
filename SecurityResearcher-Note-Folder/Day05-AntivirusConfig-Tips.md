# Hari 5 - Rekomendasi & Tips Microsoft Defender Antivirus

Pertama-tama, Microsoft Defender Antivirus bukan hanya EPP yang dirancang untuk mencegah ancaman yang diketahui saja. Ini termasuk berbagai mesin fitur untuk mendeteksi dan melindungi terhadap ancaman baik pada tahap **pra-eksekusi maupun pasca-eksekusi**.

Dalam blog ini, saya ingin berbagi konfigurasi yang direkomendasikan dan tips untuk Microsoft Defender Antivirus. Saya berharap wawasan ini akan membantu dalam mengkonfigurasi antivirus di masa mendatang.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/da052b9d-cf65-47da-9727-eff144aff868)
> Mesin Antivirus Defender - [Dalam mengejar ancaman yang sulit ditemukan: Pemblokiran berbasis perilaku AI menghentikan serangan di jalur mereka](https://www.microsoft.com/en-us/security/blog/2019/10/08/in-hot-pursuit-of-elusive-threats-ai-driven-behavior-based-blocking-stops-attacks-in-their-tracks/) 

## Rekomendasi & Tips (pertimbangan)
Terkait konfigurasi Microsoft Defender Antivirus (MDAV), tidak ada rekomendasi yang cocok untuk semua karena sifat berkembangnya serangan cyber. Namun, ada beberapa fitur yang ***sebaiknya Anda aktifkan dan pertimbangkan saat menerapkan solusi MDAV.***

Ini adalah contoh cerita yang saya terima dari rekan senior yang saya sangat hormati. Ketika AC dinyalakan, setiap orang memiliki tingkat kenyamanan yang berbeda dalam hal suhu. Ini berarti bahwa suhu yang diinginkan dapat bervariasi di antara individu, mulai dari 18°C hingga 28°C, atau bahkan lebih tinggi. Oleh karena itu, dalam konteks konfigurasi antivirus, sementara ada beberapa fitur yang umumnya disarankan untuk diaktifkan untuk MDAV, pengaturan spesifik, seperti waktu pemindaian, hari, frekuensi pembaruan, dan lain-lain, dapat bervariasi tergantung pada kebutuhan organisasi dan persyaratan bisnis.

#### Rekomendasi
| # | Nama Konfigurasi | Komentar |
| :-- | :-- | :-- | 
| 1 | Perlindungan waktu nyata | Disarankan untuk mengaktifkan perlindungan waktu nyata. |
| 2 | Perlindungan cloud | Disarankan untuk mengaktifkan perlindungan cloud.<br> - [Blokir pada Pandangan Pertama (BAFS)](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-block-at-first-sight-microsoft-defender-antivirus?view=o365-worldwide) |
| 3 | Pengiriman sampel | Disarankan untuk mengaktifkan persetujuan pengiriman sampel. <br>  Karena ini merupakan prasyarat untuk menggunakan BAFS, Anda perlu memilih salah satu opsi di bawah ini: <br> - ***Kirim sampel aman secara otomatis (default)*** <br> - Selalu Minta Persetujuan  <br> - Kirim semua sampel secara otomatis|
| 4 | Perlindungan PUA | Disarankan untuk mengaktifkan Perlindungan PUA.
| 5 | Perlindungan Tamper | Sangat disarankan untuk mengaktifkan Perlindungan Tamper dan berikut adalah beberapa blog yang membahas fitur ini. <br> - [Pastikan Perlindungan Tamper diaktifkan](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/make-sure-tamper-protection-is-turned-on/ba-p/2695568) <br> - [Mengejar serangan LemonDuck dan LemonCat](https://www.microsoft.com/en-us/security/blog/2021/07/29/when-coin-miners-evolve-part-2-hunting-down-lemonduck-and-lemoncat-attacks/) |

#### Tips (pertimbangan)
| # | Nama Konfigurasi | Komentar |
| :-- | :-- | :-- | 
| 6 | Jenis Pemindaian  | Dalam kebanyakan kasus, **pemindaian cepat** sudah cukup dan merupakan opsi yang direkomendasikan untuk pemindaian terjadwal. <br> - [Jadwalkan pemindaian cepat dan penuh secara reguler dengan Microsoft Defender Antivirus](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/schedule-antivirus-scans?view=o365-worldwide)|
| 7 | Pembaruan perlindungan antivirus | Menjaga perlindungan antivirus Anda tetap terbaru sangat penting - Urutan fallback. <br> - [Kelola sumber untuk pembaruan perlindungan Microsoft Defender Antivirus](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/manage-protection-updates-microsoft-defender-antivirus?view=o365-worldwide)<br> - [Pembaruan Microsoft Defender Antivirus - Versi sebelumnya untuk dukungan upgrade teknis](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/msda-updates-previous-versions-technical-upgrade-support?view=o365-worldwide) |
| 8 | Koneksi jaringan antivirus | Untuk memastikan perlindungan yang disampaikan oleh cloud Microsoft Defender Antivirus berfungsi dengan baik, tim keamanan Anda harus mengkonfigurasi jaringan Anda untuk mengizinkan koneksi antara endpoint Anda dan beberapa server Microsoft tertentu. <br> - [Konfigurasi dan validasi koneksi jaringan Microsoft Defender Antivirus](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-network-connections-microsoft-defender-antivirus?view=o365-worldwide) | 

#### Konfigurasi antivirus yang salah dan konfigurasi yang rentan
Dengan menyaring antivirus dalam Manajemen Kerentanan Microsoft Defender, MDE, Anda dapat mengidentifikasi setiap konfigurasi antivirus yang salah dan konfigurasi yang rentan dalam tenant Anda. 
Dengan menggunakan KQL dengan Advanced Hunting, Anda juga dapat mengidentifikasi konfigurasi-konfigurasi ini dengan menggunakan kueri KQL berikut.

```kql
DeviceTvmSecureConfigurationAssessmentKB
| where ConfigurationSubcategory == "Antivirus"
```

- [Apa itu Manajemen Kerentanan Microsoft Defender](https://learn.microsoft.com/en-us/microsoft-365/security/defender-vulnerability-management/defender-vulnerability-management?view=o

365-worldwide)
- [Tabel DeviceTvmSecureConfigurationAssessmentKB dalam skema advanced hunting](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-devicetvmsecureconfigurationassessmentkb-table?view=o365-worldwide)


## Catatan
#### Periode waktu blokir cloud
Menurut [dokumen Microsoft](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-cloud-block-timeout-period-microsoft-defender-antivirus?view=o365-worldwide), ketika Microsoft Defender Antivirus menemukan file yang mencurigakan, itu dapat mencegah file tersebut dari dijalankan sementara itu meminta layanan cloud Microsoft Defender Antivirus. Periode default bahwa file tersebut diblokir adalah 10 detik. Itu terdengar bagus tetapi periode waktu blokir cloud dapat berpotensi memengaruhi file atau program yang membutuhkan lebih banyak waktu untuk menyelesaikan operasinya. Dalam kasus seperti itu, jika file atau program melebihi waktu maksimum 60 detik, itu dapat terganggu atau dicegah dari menjalankan, yang dapat menyebabkan masalah fungsionalitas. Oleh karena itu, secara umum, ***dianjurkan 10 detik timeout***.

#### Kinerja CPU
Jika Anda memiliki kekhawatiran tentang kinerja CPU, silakan periksa parameter berikut:
 
1. ***Batas penggunaan CPU per pemindaian (CSP: AvgCPULoadFactor)*** <br>
Pengaturan kebijakan ini memungkinkan Anda mengkonfigurasi persentase penggunaan CPU maksimum yang diperbolehkan selama pemindaian. Nilai default adalah 50.
2. ***Gunakan prioritas CPU rendah untuk pemindaian terjadwal (CSP: EnableLowCPUPriority)***<br>
Pengaturan kebijakan ini memungkinkan Anda mengaktifkan atau menonaktifkan prioritas CPU rendah untuk pemindaian terjadwal.

#### Pengecualian
Jika Anda memiliki kekhawatiran terkait Windows Server atau konfigurasi yang rentan terkait pengecualian, dokumen-dokumen ini dapat membantu. Secara khusus, mereka memberikan panduan yang ditulis dengan baik tentang path, ekstensi, dan proses yang ***Tidak disarankan untuk dikecualikan karena potensi serangan.***
1. [Konfigurasi pengecualian Microsoft Defender Antivirus pada Windows Server](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-server-exclusions-microsoft-defender-antivirus?view=o365-worldwide)
2. [Kesalahan umum yang harus dihindari saat menentukan pengecualian](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/common-exclusion-mistakes-microsoft-defender-antivirus?view=o365-worldwide)



## Referensi
1. [Defender Policy CSP - Manajemen Klien Windows](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx)
2. [Pengaturan kebijakan Antivirus Windows untuk Microsoft Defender Antivirus untuk Intune](https://learn.microsoft.com/en-us/mem/intune/protect/antivirus-microsoft-defender-settings-windows)
3. [Kesalahan Konfigurasi Antivirus MDE dan Praktik Terbaik](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/mde-antivirus-configuration-common-mistakes-and-best-practice/ba-p/2127405)
4. [Dalam mengejar ancaman yang sulit ditemukan: Pemblokiran berbasis perilaku AI menghentikan serangan di jalur mereka](https://www.microsoft.com/en-us/security/blog/2019/10/08/in-hot-pursuit-of-elusive-threats-ai-driven-behavior-based-blocking-stops-attacks-in-their-tracks/)
5. [Dari dalam: Kenali teknologi canggih di inti proteksi generasi berikutnya Microsoft Defender ATP](https://www.microsoft.com/en-us/security/blog/2019/06/24/inside-out-get-to-know-the-advanced-technologies-at-the-core-of-microsoft-defender-atp-next-generation-protection/)
6. [Bagaimana kecerdasan buatan menghentikan wabah Emotet](https://www.microsoft.com/en-us/security/blog/2018/02/14/how-artificial-intelligence-stopped-an-emotet-outbreak/)
7. [Tidak terlihat tetapi tidak tak terlihat: Mengalahkan malware tanpa file dengan pemantauan perilaku, AMSI, dan AV generasi berikutnya](https://www.microsoft.com/en-us/security/blog/2018/09/27/out-of-sight-but-not-invisible-defeating-fileless-malware-with-behavior-monitoring-amsi-and-next-gen-av/)

#### Penyangkalan
Pandangan dan pendapat yang terungkap di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
