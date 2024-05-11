# Insight Detonasi dan Analisis Mendalam pada File MDO

Halo para pembela dan pemburu ancaman! Terima kasih telah mengunjungi catatan penelitian produk saya. Salah satu pertanyaan yang sering saya terima mengenai Microsoft Defender for Office 365 (MDO) berkaitan dengan analisis sandbox, khususnya, apa yang kami sebut sebagai ***'Detonasi File & Analisis Mendalam'***. Misalnya, ada rasa ingin tahu tentang apakah MDO benar-benar menguji lampiran dalam lingkungan sandbox, dan apakah detonasi benar-benar terjadi. Selain itu, ada pertanyaan umum tentang bagaimana cara menguji dan memvalidasi bahwa proses ini berfungsi sebagaimana yang dimaksud. Oleh karena itu, hari ini, saya senang untuk berbagi wawasan tentang Detonasi File & Analisis Mendalam, dengan fokus khusus pada Lampiran Aman di MDO.

## Contoh File HTML
Untuk memvalidasi Detonasi File & Analisis Mendalam secara awal, saya membuat [beberapa lampiran berbasis HTML yang sederhana](https://github.com/LearningKijo/ResearchDev/tree/main/DEV01-RedirectAttachment). Ada tiga jenis lampiran yang berbeda, semua berfungsi dengan cara yang sama — mengalihkan ke situs unduhan berbahaya setelah dibuka selama 5 detik. Perbedaannya terletak pada penampilan HTML masing-masing.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/8d72c037-b3bf-4409-82ab-f7804ef0998d)

> Templat file HTML

Pada titik ini, saya menggunakan [DEV01-Attachment-Type1.html](https://github.com/LearningKijo/ResearchDev/blob/main/DEV01-RedirectAttachment/DEV01-HTML/DEV01-Attachment-Type1.html) dan mengirimkan email ke pengguna yang ditargetkan dengan lampiran tersebut.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/181c09a7-d0d4-476b-95cc-11449c9dc5ea)

## Hasil - Halaman Entitas Email MDO
Setelah beberapa menit, MDO berhasil mendeteksi email tersebut sebagai mencurigakan dan memindahkannya ke karantina. Ketika Anda memeriksa bagian "Teknologi Deteksi", Anda dapat melihat ***"Detonasi File"***, mengkonfirmasi bahwa email tersebut ditandai sebagai hasil dari "Detonasi File". Saya juga ingin berbagi dokumen resmi di sini untuk memberikan definisi "Detonasi File".

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/0b1279d2-dba4-4abd-bb98-006e3467d015)

> [!Note]
> ***Detonasi file : Lampiran Aman mendeteksi lampiran berbahaya selama detonasi dalam sandbox*** <br>
> [Memahami teknologi deteksi dalam halaman entitas email Microsoft Defender for Office 365](https://learn.microsoft.com/en-us/microsoft-365/security/office-365-security/step-by-step-guides/understand-detection-technology-in-email-entity?view=o365-worldwide)

Selanjutnya, saat memeriksa tab Lampiran di halaman Entitas Email, Anda akan menemukan informasi terperinci tentang lampiran, termasuk detail umum seperti Verdict, Hash/File IoC, Ukuran, Waktu Analisis, dan lainnya. Selain itu, Anda juga dapat mengakses 'Analisis Mendalam,' memberikan wawasan tentang bagaimana file HTML tersebut muncul setelah pengguna akhir mengkliknya, termasuk tangkapan layar UI yang diambil.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/bcb2ece6-7754-49b1-bf3f-2f82b3e49182)

Setelah menggulir ke bawah halaman Analisis Mendalam, Anda akan menemukan daftar terperinci dari semua URL, IP, dan Hash yang terkait dengan lampiran tersebut. Perlu dicatat bahwa meskipun tidak semua observasi mungkin ditandai sebagai mencurigakan, mirip dengan fitur Analisis Mendalam di MDE, file awalnya diperlakukan sebagai berpotensi mencurigakan. Oleh karena itu, kita dapat menganalisis bagaimana kemungkinan perilaku file tersebut dengan memeriksa wawasan berharga yang dikumpulkan.

![image](https://github.com/LearningKijo/SecurityResearcher-Note/assets/120234772/49fbf701-f984-413f-a306-e50e9523f22c)

#### Disclaimer
Pandangan dan pendapat yang terungkap di sini adalah milik penulis dan tidak selalu mencerminkan pandangan perusahaan.
