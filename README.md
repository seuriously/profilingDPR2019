# Profiling Anggota DPR-RI 2019-2024
## Introduction
An attempt to profile Indonesian legislative members using the data given in dpr.go.id, inspired by House of Cards.  
Complete method and raw data can be found [here](https://nbviewer.jupyter.org/github/seuriously/profilingDPR2019/blob/master/dpr_profiling.ipynb?flush_cache=true).

Saat ini website dpr.go.id menampilkan data-data profil anggota DPR RI yang mencakup nama, ttl, dapil, agama, riwayat pendidikan, riwayat pekerjaan dan riwayat organisasi. Data lainnya hingga saat ini masih kosong.  

Contoh halaman profil dari salah satu anggota DPR-RI, [source](http://www.dpr.go.id/blog/profil/id/1320).  
![dpr](https://i.ibb.co/GQLGnRM/Image.png)  


Akan lebih baik lagi jika website DPR-RI dapat mentrack kegiatan anggotanya dalam aktivitas legislasi seperti yang dilakukan oleh parlemen Amerika demi Indonesia yang lebih transparan.


Contoh halaman profil dari anggota kongres Amerika, [source](https://www.congress.gov/member/ralph-abraham/A000374?searchResultViewType=expanded).  
![congress](https://i.ibb.co/WpKQP9Q/image.png)  

Pada contoh anggota kongres Amerika diatas, terlihat peraturan apa saja yang anggota kongres tersebut dukung dan sudah sampai mana peraturan (bill) tersebut progresnya saat ini. Pastinya ini akan membantu masyarakat Indonesia dalam memilih anggota DPR dikemudian hari berdasarkan progres kerjanya.  

## Approach on Columns:
Ada beberapa kolom yang kita derive berdasarkan kolom yang ada di website DPR. Berikut kolom-kolom tersebut beserta tujuannya:
* is_dewan: pendekatan untuk mengetahui apakah seorang anggota DPR sebelumnya pernah menjabat menjadi anggota dewan, baik di DPR, MPR, DPD maupun di DPRD. Data ini derive dari kolom pekerjaan dari masing-masing anggota DPR.
* pendidikan_terakhir: pendekatan yg diambil berdasarkan biodata pendidikan yang ada di website DPR dari masing-masing anggota. Selanjutnya diambil pendidikan terakhir yang ada di kolom pendidikan.
* is_kader: diderive dari kolom organisasi. Tujuannya untuk mengetahui apakah anggota DPR dari suatu partai sebelumnya sudah pernah memegang jabatan dalam partai.
* usia_kategori: usia per tahun 2020 (saat script ini di run). Selanjutnya dibuat binning berdasarkan quintile (5 bin sama besar) agar sebaran usia tidak lagi numerical.

## Univariate Findings:
1. Partai tua nasionalis masih menjadi favorit. PDIP di urutan pertama diikuti golkar di urutan kedua. Partai islamis anjlok menempati posisi 3 terbawah.
2. 5 agama terbesar di Indonesia memiliki wakil di DPR, dengan jumlah proporsi yang hampir mirip (https://id.wikipedia.org/wiki/Agama_di_Indonesia)
3. Lebih dari 50% anggota DPR berpendidikan minimal S2.
4. Lebih dari 50% anggota DPR saat ini memiliki pengalaman menjabat sebagai anggota dewan sebelumnya.
5. Mayoritas anggota DPR tidak pernah memegang jabatan partai di partai yang mengusung mereka.
6. Rata-rata usia anggota DPR ialah 51.75 tahun. Anggota termuda berumur 24 tahun dari partai Nasdem dapil SULUT dan anggota tertua berumur 81 tahun dari partai Demokrat dapil SUMUT 1. 
7. Seorang anggota DPR dapat ditempatkan pada satu atau lebih Alat Kelengkapan Dewan (AKD). Badan Anggaran dan Badan Legislasi menjadi badan yang paling vital. Sebaliknya, komisi 2 menjadi komisi yang tidak difavoritkan. (http://www.dpr.go.id/akd/komisi).

## Bivariate Findings
P(A) adalah probabilitas dari kolom yang dipanggil dalam fungsi bivariate_analysis.  
P(B) adalah probabilitas dari partai.

1. Sebaran AKD pada tiap partai hampir sama. Hanya saja, ada beberapa partai yang condong terhadap komisi-komisi tertentu terlihat dari jumlah penempatan anggotanya. Badan Anggaran dan Badan Legislasi menjadi vital dari semua partai. Terdapat pencilan pada partai PKB dimana mayoritas anggotanya masuk dalam panitia khusus. Pimpinan diambil 1 dari masing-masing 5 partai teratas. 
2. PDIP dan PPP adalah partai veteran dimana mayoritas anggotanya melanjutkan tugasnya sebagai anggota dewan. Bisa jadi ini menandakan PDIP sangat baik dalam menjaga suaranya di tingkat masyarakat sedangkan PPP memiliki kantung-kantung suara yang loyal. Dilain hal, Gerindra adalah partai pembaruan. Hal ini menjadi wajar mengingat Prabowo menjadi ikon pembaruan di pemilu kemarin. Mayoritas (72%) anggota Gerindra belum memiliki pengalaman menjadi anggota legislatif sebelumnya.
3. Hanya PDIP dan Golkar yang mewakili 5 agama mayoritas di Indonesia. Hal ini selaras dengan ideologi nasionalis yang mereka usung. Seorang caleg yang beragama non-islam lebih besar kemungkinannya terpilih via PDIP (metric P(B|A) terbesar). PKS dan PPP menjadi partai yang anggotanya 100% muslim.
4. PKS memiliki rerata usia anggota tertua dengan 54,67 tahun sedangkan Nasdem menjadi partai termuda dengan rerata usia 49,56. PDIP dan Golkar memiliki sebaran umur_kategorical yang cukup rata dimana selisih max dan min P(A|B) nya serupa, 0.09.
5. PKS mengokohkan dirinya menjadi partai terdidik dengan memiliki porsi S3 terbesar dalam partainya. PKB untuk S2, PDIP untuk S1, dan PPP untuk SMA. SMP adalah data outlier mengingat syarat minimum untuk menjadi anggota DPR ialah SMA.
6. Golkar, PKB, PKS dan PPP adalah partai kaderisasi. Minimal 60% wakil di DPR-nya pernah menjabat di internal partai.

## Trivia
* Anggota DPR yang disukai masyarakat: islam, pernah menjadi anggota dewan, kader partai, pendidikan minimal S2.  
* Partai mana yang paling besar memungkinkan saya (<44 tahun, islam, non-dewan, eksternal, S2) lolos menjadi anggota DPR: Gerindra (33.3%).
* Probabilitas saya terpilih menjadi anggota DPR: 2.7%. Small but its actually joint second largest segment over all segments.
* Karakteristik yang disukai masyarakat: islam, pernah menjabat sebagai anggota dewan, pendidikan minimal s2.

## To do:
Join data caleg dengan aleg DPR untuk melakukan klasifikasi.  
Data caleg: https://github.com/seuriously/caleg_dpr_2019
