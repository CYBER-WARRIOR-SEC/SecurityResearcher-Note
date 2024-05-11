# Hari 6 - Disrupsi Serangan Otomatis XDR  
Disrupsi serangan otomatis dalam Microsoft 365 Defender menggunakan sinyal XDR dari berbagai sumber (endpoint, email, identitas, data) untuk ***secara otomatis menahan aset yang kompromi dan menghentikan serangan cyber yang sedang berlangsung, meminimalkan dampaknya pada organisasi***.
#### Apa tujuan dari disrupsi serangan?
Tujuan utama fitur ini adalah untuk mencapai ***penahanan*** selama fase respons insiden. Dalam hal disrupsi otomatis, ada dua tindakan yang dapat diambil: ***"penahanan perangkat"*** oleh Microsoft Defender for Endpoint dan ***"menonaktifkan pengguna"*** oleh Microsoft Defender for Identity.

## Serangan Lanjutan vs Disrupsi Serangan XDR
Microsoft 365 Defender XDR memberikan cakupan untuk tiga serangan lanjutan berikut untuk mengganggu progres lebih lanjut.

1. Serangan musuh di tengah (AiTM)
2. Penipuan email bisnis (BEC)
3. Serangan ransomware yang dioperasikan manusia

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/4a26dc22-2a5a-4197-b000-8ceaa44f2111)
>  Disrupsi serangan otomatis, [Blog Microsoft 365 Defender](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/automatic-disruption-of-ransomware-and-bec-attacks-with/ba-p/3738294)

## Wawasan AiTM
Serangan AiTM merujuk pada teknik phishing ***"Musuh di Tengah"*** di mana penyerang menyadap komunikasi antara pengguna dan situs web sah, mencuri kata sandi dan cookie sesi untuk mendapatkan akses tanpa izin dan melakukan aktivitas penipuan.

#### Blog keamanan MS: Timeline AiTM

- 12 Juli 2022, [Dari pencurian cookie hingga BEC: Penyerang menggunakan situs phishing AiTM sebagai titik masuk untuk penipuan keuangan lebih lanjut](https://www.microsoft.com/en-us/security/blog/2022/07/12/from-cookie-theft-to-bec-attackers-use-aitm-phishing-sites-as-entry-point-to-further-financial-fraud/)
- 16 November 2022, [Taktik token: Cara mencegah, mendeteksi, dan menanggapi pencurian token cloud](https://www.microsoft.com/en-us/security/blog/2022/11/16/token-tactics-how-to-prevent-detect-and-respond-to-cloud-token-theft/)
- 13 Maret 2023, [DEV-1101 memungkinkan kampanye AiTM berkecepatan tinggi dengan kit phishing open-source](https://www.microsoft.com/en-us/security/blog/2023/03/13/dev-1101-enables-high-volume-aitm-campaigns-with-open-source-phishing-kit/)
- 8 Juni 2023, [Mendeteksi dan memitigasi kampanye phishing dan BEC multi-tahap AiTM](https://www.microsoft.com/en-us/security/blog/2023/06/08/detecting-and-mitigating-a-multi-stage-aitm-phishing-and-bec-campaign/)

## Wawasan BEC
Penipuan Email Bisnis (BEC) adalah serangan cyber di mana penyerang menipu organisasi melalui email palsu. Mereka menyamar sebagai individu terpercaya untuk menipu karyawan agar melakukan tindakan tidak sah, seperti mentransfer uang atau mengungkapkan informasi sensitif. Serangan BEC dapat menyebabkan kerugian finansial dan kerusakan reputasi bagi bisnis.

- 6 Mei 2021, [Penipuan email bisnis: Bagaimana Microsoft melawan ancaman mahal ini](https://www.microsoft.com/en-us/security/blog/2021/05/06/business-email-compromise-how-microsoft-is-combating-this-costly-threat/)

## Wawasan Serangan Ransomware yang Dioperasikan Manusia
Serangan ransomware yang dioperasikan manusia, juga dikenal sebagai serangan ***"hands-on-keyboard"***, merujuk pada jenis serangan ransomware tertentu di mana penyerang manusia terampil aktif berpartisipasi dalam berbagai tahap serangan daripada hanya mengandalkan alat otomatis atau malware.

- [Ransomware yang Dioperasikan Manusia | Microsoft Learn](https://learn.microsoft.com/en-us/security/ransomware/human-operated-ransomware)
- 5 Maret 2020, [Serangan ransomware yang dioperasikan manusia: Bencana yang bisa dicegah](https://www.microsoft.com/en-us/security/blog/2020/03/05/human-operated-ransomware-attacks-a-preventable-disaster/)

## Blog MS - disrupsi serangan otomatis  
1. [Disrupsi serangan otomatis dalam Microsoft 365 Defender](https://learn.microsoft.com/en-us/microsoft-365/security/defender/automatic-attack-disruption?view=o365-worldwide)
2. 22 Februari 2023, [Disrupsi otomatis serangan Ransomware dan BEC dengan Microsoft 365 Defender](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/automatic-disruption-of-ransomware-and-bec-attacks-with/ba-p/3738294)
3. 8 Maret 2023, [Disrupsi serangan XDR dalam tindakan - Membela diri terhadap serangan BEC terbaru](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/xdr-attack-disruption-in-action-defending-against-a-recent-bec/ba-p/3749822)
4. 17 Mei 2023, [Mengganggu secara otomatis serangan musuh di tengah (AiTM) dengan XDR](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/automatically-disrupt-adversary-in-the-middle-aitm-attacks-with/ba-p/3821751)



#### Penyangkalan
Pandangan dan pendapat yang terungkap di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
