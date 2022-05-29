# eljeka

`eljeka` adalah skrip untuk otomasi [OMRChecker](https://github.com/Udayraj123/OMRChecker) dengan model LJK seperti dalam map samples/community/eljeka.

Jika menggunakan bentuk LJK berbeda, silakan rujuk [OMRChecker](https://github.com/Udayraj123/OMRChecker) dan [wikinya](https://github.com/Udayraj123/OMRChecker/wiki).

## Cara Penggunaan

Berikut dicontohkan pemasangan `eljeka` dalam sistem Debian.

### 1. Gandakan `eljeka`

   ```
   git clone https://github.com/rizaumami/eljeka
   cd eljeka
   ```

### 2. Pasang paket dan pustaka yang diperlukan

Anda bisa memasang paket python yang ada dalam lumbung paket distro menggunakan perintah seperti `sudo apt install python3-XXX`. Namun ketika skrip `eljeka` ditulis, saya tidak menemukan paket `python3-dotmap` di lumbung paket, `pip`, dan `pipx`. Jadi, cara berikut di bawah lebih disarankan.

  ```
  ./eljeka -d
  ./eljeka -p
  ```

### 3. Jalankan `eljeka`

```
$ ./eljeka -h

  eljeka adalah skrip alat bantu OMRChecker untuk melakukan
  Optical Markup Recognition (OMR) pada kertas Lembar Jawaban Komputer (LJK).

  Penggunaan: eljeka PILIHAN

  PILIHAN:
    -d              Pasang paket yang dibutuhkan.
    -h              Tampilkan pesan ini.
    -i INPUT_DIR    Letak gambar LJK yang akan di-OMR.
    -o OUTPUT_DIR   Letak hasil OMR akan disimpan.
    -p              Pasang pustaka python yang dibutuhkan ke /home/iza/.pip.
    -r              Langsung OMR tanpa mengolah gambar terlebih dahulu.
    -v              Tampilkan versi skrip.

  Setiap direktori input harus memiliki template.json.

  Jika dijalankan tanpa argumen -i atau -o maka skrip akan menggunakan:
  -i di /tmp/eljeka/inputs
  -o di /tmp/eljeka/outputs

  Apa yang skrip ini lakukan adalah sebagai berikut:
  1. Mengubah gambar LJK menjadi hitam putih.
  2. Menebalkan bagian hitam agar lebih mudah di-OMR.
  3. Melakukan OMR.


  Contoh:
    - Melakukan OMR pada berkas hasil pemindaian yang terletak dalam ~/IPA:

      $ eljeka -i /home/iza/IPA

    - Menyimpan hasil OMR ke dalam map /home/iza/NILAI_IPA:

      $ eljeka -o /home/iza/NILAI_IPA

    - Melakukan OMR pada berkas hasil pemindaian yang terletak dalam ~/IPA
      dan menyimpan hasilnya ke dalam map /home/iza/NILAI_IPA:

      $ eljeka -i /home/iza/IPA -o /home/iza/NILAI_IPA

    - Jika ada berkas yang tidak sempurna di-OMR misal karena jawaban terdeteksi
      ganda, gunakan argumen -r untuk langsung melakukan OMR tanpa mengolah
      gambar terlebih dahulu.
      Mungkin diperlukan untuk menyunting gambar input secara manual.

      $ eljeka -i /home/iza/IPA -r

  eljeka hanyalah skrip pembantu (helper/wrapper script) untuk otomasi
  OMR model LJK seperti tampak dalam map samples/community/eljeka.

  Jika mempunyai bentuk LJK berbeda, silakan rujuk
  https://github.com/Udayraj123/OMRChecker untuk langsung menggunakan
  OMRChecker dan atau membuat template.json sendiri.

```

## Catatan

Catatan ini hanya untuk contoh LJK dalam [samples/community/eljeka](samples/community/eljeka).

- Karena OMRChecker belum mendukung _auto alignment_ untuk _marker_ yang digunakan, maka LJK harus dipindai menggunakan pemindai (_scanner_) khusus dan tidak bisa menggunakan cara lain seperti kamera telepon genggam.
- LJK dipindai ke dalam berkas JPEG berukuran 1654 x 2338 px dengan resolusi 200 dpi.
- _Template_ harus ada di direktori teratas (_root directory_) input. Jika input terdiri dari banyak _sub folder_ namun memiliki bentuk LJK yang sama, maka _template_ bisa hanya satu di _root directory_. Namun jika _sub folder-sub folder_ tersebut berbeda bentuk, maka _template harus ada dalam tiap _sub folder_ tersebut.
- Python `ENV` yang digunakan bisa disesuaikan dengan menyunting berkas [`eljeka`](eljeka) baris ke-63 (variabel `OMRCHECKER`).
