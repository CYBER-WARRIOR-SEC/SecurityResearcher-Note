## 7 April 2023, Mango Sandstorm

#### Ringkasan Singkat

Mango Sandstorm, sebelumnya dikenal karena menggunakan eksploitasi Log4j 2 dan menargetkan lingkungan on-premise, sekarang telah memperluas fokusnya untuk termasuk kedua lingkungan on-premise dan cloud. Setelah mendapatkan akses awal melalui kerentanan yang diketahui, serangan ini dikaitkan dengan Storm-1084 (sebelumnya dikenal sebagai DEV-1084).

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/ee623697-5a31-48fe-933a-85fa360ef3c1)

> [!Note]
> [MERCURY dan DEV-1084: Serangan destruktif pada lingkungan hibrid](https://www.microsoft.com/en-us/security/blog/2023/04/07/mercury-and-dev-1084-destructive-attack-on-hybrid-environment/)


#### Bagaimana Mango Sandstorm berubah dibandingkan dengan aktivitas sebelumnya?
Sebelumnya, Mango Sandstorm terutama diamati dalam lingkungan on-premise. Namun, sekarang mereka telah memperluas aktivitas mereka untuk termasuk ***lingkungan cloud*** juga. 
Selain itu, ada kecurigaan kuat bahwa Mango Sandstorm terkait dengan ***Storm-1084***, menurut Microsoft.


#### Apa itu Storm-1084?
Menurut Microsoft, DEV-1084 secara publik mengadopsi persona DarkBit dan menyatakan diri sebagai pelaku kriminal yang tertarik pada pemerasan. 
Hal ini kemungkinan dilakukan sebagai upaya untuk menyembunyikan keterkaitan Iran dengan dan motivasi strategis untuk serangan.
> [!Note]
> DarkBit - sebuah ransomware baru

#### Apakah ada bukti yang menghubungkan Storm-1084 ke Mango Sandstorm?
- Alamat IP email (146.70.106[.]89) terhubung ke Mango Sandstorm.
- Keduanya terlihat menggunakan layanan VPN yang sama.
- Keduanya terlihat menggunakan alat yang sama seperti Rport dan Ligolo.
- vatacloud[.]com, pusat komando dan kontrol yang digunakan oleh Storm-1084, dikendalikan oleh Mango Sandstorm.

#### Bagaimana mereka melakukan serangan pada lingkungan on-premise?
Teknik akses awal dan pergerakan lateral yang digunakan dalam serangan ini mirip dengan teknik Mango Sandstorm sebelumnya. 
Para penyerang mengompromikan lingkungan on-premise dengan memanfaatkan Objek Kebijakan Grup (GPOs) untuk ***menonaktifkan alat keamanan seperti antivirus.***
Mereka juga menggunakan GPO untuk ***membuat tugas terjadwal untuk pengiriman ransomware.*** Payload ransomware ditempatkan di share NETLOGON pada pengontrol domain. 
Pada akhirnya, para penyerang mengenkripsi file pada perangkat yang ditargetkan dan meninggalkan catatan tebusan.

#### Jenis serangan apa yang dilakukan dalam lingkungan cloud?
- Pemalsuan email
- Dump email menggunakan Exchange Web Server API
- Penghapusan massa sumber daya Azure

## KQL: Pencarian Ancaman Berbasis IoCs
Berikut adalah kueri KQL yang siap pakai untuk memburu Mango SandStorm dengan Storm-1084. IoCs tersedia dari blog Microsoft - [MERCURY dan DEV-1084: Serangan destruktif pada lingkungan hibrid](https://www.microsoft.com/en-us/security/blog/2023/04/07/mercury-and-dev-1084-destructive-attack-on-hybrid-environment/).
#### File csv IoCs: [MangoSandstorm-Storm-1084-IOCs-042023.csv](https://github.com/LearningKijo/KQL/blob/main/KQL-XDR-Hunting/ThreatHunting/IOCs-Folder/MangoSandstorm-Storm-1084-IOCs-042023.csv)
```kql
// IoCs - MERCURY and DEV-1084: Destructive attack on hybrid environment
let MangoSandstorm = externaldata(Indicator:string, Type:string, Description:string)
[@'https://raw.githubusercontent.com/LearningKijo/KQL/main/KQL-XDR-Hunting/ThreatHunting/IOCs-Folder/MangoSandstorm-Storm-1084-IOCs-042023.csv'] with (format='csv', ignorefirstrecord = true);
let Domains = (MangoSandstorm | where Type == "Domain"| project Indicator);
let IPaddress = (MangoSandstorm | where Type == "IP address"| project Indicator);
let SHA256hash = (MangoSandstorm | where

 Type == "SHA-256"| project Indicator);
(union isfuzzy=true
(DeviceNetworkEvents
| where Timestamp > ago(1d)
| where RemoteUrl has_any (Domains) or RemoteIP in (IPaddress) 
| project Timestamp, DeviceId, DeviceName, ActionType, RemoteUrl, RemoteIP, RemotePort, InitiatingProcessFileName
),
(DeviceFileEvents
| where Timestamp > ago(1d)
| where SHA256 in~ (SHA256hash)
| project Timestamp, DeviceId, DeviceName, ActionType, FileName, FileSize, FolderPath, SHA256
),
(DeviceProcessEvents
| where Timestamp > ago(1d)
| where SHA256 in~ (SHA256hash)
| project Timestamp, DeviceId, DeviceName, ActionType, FileName, FileSize, FolderPath, SHA256, ProcessCommandLine, InitiatingProcessCommandLine
),
(DeviceImageLoadEvents
| where Timestamp > ago(1d)
| where SHA256 in~ (SHA256hash)
| project Timestamp, DeviceId, DeviceName, ActionType, FileName, FileSize, FolderPath, SHA256, InitiatingProcessFileName, InitiatingProcessCommandLine
)
)
```

#### Penafian
Pandangan dan pendapat yang dinyatakan di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
