## Apa itu Mango Sandstorm?

Mango Sandstorm, sebelumnya dikenal sebagai MERCURY, adalah ***kelompok aktivitas cyber berbasis Iran*** yang mengkhususkan diri dalam pengumpulan data sensitif melalui serangan cyber canggih, bukan untuk keuntungan finansial. Teknik serangan mereka termasuk serangan spear-phishing, eksploitasi kerentanan, malware, dan rekayasa sosial.

Untuk mendapatkan wawasan yang lebih detail, Intelijen Ancaman Microsoft Defender juga mencakup deskripsi Mango Sandstorm, TTP, dan IOCs.

![image](https://user-images.githubusercontent.com/120234772/235598610-51723cfb-b598-43bc-ac5c-2c344a384611.png)
> Mango Sandstorm, Intelijen Ancaman Microsoft Defender

## Kronologi Mango Sandstorm
#### 25 Agustus 2022
Mango Sandstorm, sebelumnya dikenal karena menggunakan eksploitasi Log4j 2 untuk menyerang aplikasi VMware, baru-baru ini menargetkan aplikasi SysAid menggunakan teknik yang sama. Begitu mereka mendapatkan akses awal, kelompok ini mendirikan persistensi, bergerak lateral dalam jaringan menggunakan alat hacking kustom dan terkenal, dan mengambil kredensial.
> [!Note]
> [MERCURY memanfaatkan kerentanan Log4j 2 dalam sistem yang belum dipatch untuk menargetkan organisasi Israel](https://www.microsoft.com/en-us/security/blog/2022/08/25/mercury-leveraging-log4j-2-vulnerabilities-in-unpatched-systems-to-target-israeli-organizations/)


#### 7 April 2023
Mango Sandstorm, sebelumnya dikenal karena menggunakan eksploitasi Log4j 2 dan menargetkan lingkungan on-premises, sekarang telah memperluas fokusnya untuk mencakup lingkungan on-premises dan cloud. Setelah mendapatkan akses awal melalui kerentanan yang diketahui, serangan tersebut telah dikaitkan dengan Storm-1084 (sebelumnya dikenal sebagai DEV-1084).
> [!Note]
> [MERCURY dan DEV-1084: Serangan merusak pada lingkungan hibrid](https://www.microsoft.com/en-us/security/blog/2023/04/07/mercury-and-dev-1084-destructive-attack-on-hybrid-environment/)

## Kelompok yang terkait dengan Mango Sandstorm
Ada beberapa kelompok yang terkait dengan APT29, dan setiap kelompok menggunakan teknik serangan yang berbeda. 
- Earth Vetala
- Mango Sandstorm (MERCURY)
- Static Kitten
- Seedworm
- TEMP.Zagros
- MuddyWater

## Teknik Serangan Mango Sandstorm

### Teknik serangan yang paling umum
- Email spear-phishing
- Penggunaan layanan berbagi file cloud
- Penggunaan aplikasi remote access komersial
- Alat: Alat proxy Venom, tunneling terbalik Ligolo, dan program PowerShell buatan sendiri
- Eksploitasi kerentanan
- Rekayasa sosial
- Serangan tempat minum
- Instalasi pintu belakang
- Gerakan lateral

### Peta Serangan MITRE ATT&CK MuddyWater
![image](https://user-images.githubusercontent.com/120234772/236394767-4a35fec6-0897-48ae-bfa3-e22db9a5a7ca.png)
> MuddyWater, Teknik yang Digunakan, [ATT&CK® Navigator](https://mitre-attack.github.io/attack-navigator/)


## Referensi
1. 25 Agustus 2022, [MERCURY memanfaatkan kerentanan Log4j 2 dalam sistem yang belum dipatch untuk menargetkan organisasi Israel](https://www.microsoft.com/en-us/security/blog/2022/08/25/mercury-leveraging-log4j-2-vulnerabilities-in-unpatched-systems-to-target-israeli-organizations/)
2. 7 April 2023, [MERCURY dan DEV-1084: Serangan merusak pada lingkungan hibrid](https://www.microsoft.com/en-us/security/blog/2023/04/07/mercury-and-dev-1084-destructive-attack-on-hybrid-environment/)
3. [Apa itu Intelijen Ancaman Microsoft Defender (Defender TI)?](https://learn.microsoft.com/en-us/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti)

#### Penafian
Pandangan dan pendapat yang dinyatakan di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
