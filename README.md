# eljeka

`eljeka` adalah _template_ untuk  [OMRChecker](https://github.com/Udayraj123/OMRChecker) dengan model LJK (Lembar Jawaban Komputer) seperti dalam map [eljeka](samples/community/eljeka).

## Cara Pemasangan

Berikut dicontohkan pemasangan `eljeka` dalam sistem Debian dan turunannya.

### 1. Gandakan `eljeka`

   ```
   git clone https://github.com/rizaumami/eljeka
   cd eljeka
   ```

### 2. Pasang paket dan pustaka yang diperlukan

#### 2.1. Memasang pustaka secara global
```bash
sudo apt install build-essential cmake unzip pkg-config libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libatlas-base-dev gfortran python3-opencv python3-deepmerge python3-dotmap python3-jsonschema python3-matplotlib python3-numpy python3-pandas python3-rich python3-screeninfo
```

Karena `opencv-contrib-python` tidak ada dalam lumbung paket Debian, maka kita pasang menggunakan `pip`:

```bash
python3 -m venv .venv
.venv/bin/pip3 install opencv-contrib-python
```

#### 2.2. Memasang pustaka secara lokal

```bash
sudo apt install build-essential cmake unzip pkg-config libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libatlas-base-dev gfortran
```

```bash
python3 -m venv .venv
.venv/bin/pip3 install opencv-python
.venv/bin/pip3 install opencv-contrib-python
.venv/bin/pip3 install -r requirements.txt
```

## Cara Penggunaan

```
~$ python3 main.py -h

usage: main.py [-h] [-i [INPUT_PATHS ...]] [-d] [-o OUTPUT_DIR] [-a] [-l]

options:
  -h, --help            show this help message and exit
  -i, --inputDir [INPUT_PATHS ...]
                        Specify an input directory.
  -d, --debug           Enables debugging mode for showing detailed errors
  -o, --outputDir OUTPUT_DIR
                        Specify an output directory.
  -a, --autoAlign       (experimental) Enables automatic template alignment - use if the scans show slight
                        misalignments.
  -l, --setLayout       Set up OMR template layout - modify your json file and run again until the template is set.
```

Jika dijalankan tanpa memberikan argumen `-i` atau `-o` maka secara asali akan menggunakan:
- `-i` di map `inputs`
- `-o` di map `outputs`

### Contoh Penggunaan:

- Melakukan OMR pada berkas hasil pemindaian yang terletak dalam /tmp/IPAS:

	```
	~$ python3 main.py -i /tmp/IPAS
	```

-  Menyimpan hasil OMR ke dalam map /tmp/NILAI_IPAS:

	```
    ~$ python3 main.py -o /tmp/NILAI_IPAS
	```

- Melakukan OMR pada berkas hasil pemindaian yang terletak dalam /tmp/IPAS dan menyimpan hasilnya ke dalam map /tmp/NILAI_IPAS:

	```
	~$ python3 main.py -i /tmp/IPAS -o /tmp/NILAI_IPAS
	```

## Catatan

- Karena OMRChecker belum mendukung _auto alignment_ untuk _marker_ yang digunakan (berbentuk persegi), maka LJK harus dipindai menggunakan pemindai (_scanner_) khusus dan tidak bisa menggunakan cara lain seperti kamera telepon genggam.
- LJK dipindai ke dalam berkas JPEG berukuran 1240 x 1754 px dengan kerapatan 200 dpi.
- _Template_ harus ada di direktori teratas (_root directory_) input. Jika input terdiri dari banyak _sub folder_ namun memiliki bentuk LJK yang sama, maka _template_ bisa hanya satu di _root directory_. Namun jika _sub folder-sub folder_ tersebut berbeda bentuk, maka _template_ harus ada dalam tiap _sub folder_ tersebut.