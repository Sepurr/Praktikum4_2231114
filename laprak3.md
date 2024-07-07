
# LINE DETECTION
#### import library

```bash
import numpy as np 
import cv2 
import matplotlib.pyplot as plt
%matplotlib inline

import skimage
```
- import numpy as np :Mengimpor library NumPy dengan alias np. NumPy digunakan untuk operasi numerik dan manipulasi array, yang sering digunakan dalam pemrosesan gambar untuk representasi dan manipulasi data gambar.
- import cv2 :Mengimpor library OpenCV (Open Source Computer Vision Library). OpenCV adalah library populer untuk pemrosesan gambar komputer, penglihatan komputer, dan analisis video.
- import matplotlib.pyplot as plt :Mengimpor modul pyplot dari library Matplotlib dengan alias plt. Matplotlib adalah library untuk visualisasi data di Python
- import skimage :Mengimpor library scikit-image. Scikit-image adalah library untuk pemrosesan gambar yang dibangun di atas NumPy, SciPy, dan matplotlib.

```bash
image=cv2.imread("2.jpg")
```
- cv2.imread("2.jpg"): Ini adalah pemanggilan fungsi imread dari OpenCV untuk membaca gambar dari file "2.jpg"

```bash
cv2.imshow("gambar parkir", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
- cv2.imshow("gambar parkir", image): Fungsi imshow() dari OpenCV digunakan untuk menampilkan gambar ke jendela GUI dengan judul "gambar parkir". Parameter pertama adalah judul jendela yang akan ditampilkan, dan parameter kedua (image) adalah variabel yang berisi gambar yang ingin ditampilkan.
- cv2.waitKey(0): Fungsi waitKey() akan menunggu penggunaan tombol keyboard untuk menutup jendela gambar. Angka 0 dalam waitKey(0) berarti menunggu tanpa batas waktu sampai pengguna menekan tombol keyboard. Jika angka positif diberikan (misalnya cv2.waitKey(100)), itu akan menunggu untuk waktu tertentu (dalam milidetik) sebelum melanjutkan.
-cv2.destroyAllWindows(): Setelah pengguna menekan tombol keyboard (dengan waitKey(0)), fungsi destroyAllWindows() akan menutup semua jendela yang dibuat oleh OpenCV.

```bash
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
edges= cv2.Canny(image,100,150)
```
-gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY): Baris ini mengonversi gambar yang sudah dibaca (image) dari format warna BGR (Blue, Green, Red) ke skala abu-abu (grayscale). Fungsi cv2.cvtColor() digunakan untuk konversi warna dalam OpenCV. Parameter kedua, cv2.COLOR_BGR2GRAY, menentukan bahwa saya ingin mengubah gambar ke skala abu-abu. Hasil dari konversi ini disimpan dalam variabel gray.
-edges = cv2.Canny(image, 100, 150): Baris ini melakukan deteksi tepi pada gambar asli (image) yang sudah dibaca. Deteksi tepi adalah teknik yang umum digunakan dalam pengolahan gambar untuk menemukan tepi objek. Fungsi cv2.Canny() dari OpenCV digunakan di sini

```bash
cv2.imshow("gambar parkir", edges)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
- cv2.imshow("gambar parkir", edges): Fungsi imshow() dari OpenCV digunakan untuk menampilkan gambar deteksi tepi ke jendela GUI dengan judul "gambar parkir". Parameter pertama adalah judul jendela yang akan ditampilkan ("gambar parkir" dalam hal ini), dan parameter kedua (edges) adalah variabel yang berisi hasil deteksi tepi dari gambar yang telah diproses sebelumnya.
- cv2.waitKey(0): Fungsi waitKey() akan menunggu penggunaan tombol keyboard untuk menutup jendela gambar. Angka 0 dalam waitKey(0) berarti menunggu tanpa batas waktu sampai pengguna menekan tombol keyboard.
- cv2.destroyAllWindows(): Setelah pengguna menekan tombol keyboard (dengan waitKey(0)), fungsi destroyAllWindows() akan menutup semua jendela yang dibuat oleh OpenCV.

```bash
fig,axs = plt.subplots(1,2,figsize=(10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap='gray')
ax[0].set_title("Gambar Asli")

ax[1].imshow(edges, cmap='gray')
ax[1].set_title("Gambar yang udah dideteksi")
```
-fig, axs = plt.subplots(1, 2, figsize=(10, 10)): Baris ini membuat sebuah jendela plot (figure) dengan dua subplot berdampingan (1 baris, 2 kolom). fig adalah objek yang mewakili jendela plot, dan axs adalah array yang berisi subplot-subplot tersebut
- ax = axs.ravel(): Fungsi ravel() digunakan untuk mengubah array axs menjadi array satu dimensi.
- ax[0].imshow(gray, cmap='gray'): Pada subplot pertama (ax[0]), gambar dalam skala abu-abu (gray) ditampilkan menggunakan fungsi imshow() dari Matplotlib. Parameter cmap='gray' digunakan untuk menunjukkan bahwa gambar yang ditampilkan adalah dalam format grayscale. ax[0].set_title("Gambar Asli") digunakan untuk memberi judul pada subplot pertama
- ax[1].imshow(edges, cmap='gray'): Pada subplot kedua (ax[1]), gambar deteksi tepi (edges) ditampilkan menggunakan imshow() dengan parameter cmap='gray' untuk menampilkan gambar dalam format grayscale. ax[1].set_title("Gambar yang udah dideteksi") memberi judul pada subplot kedua.

```bash
lines = cv2.HoughLinesP(edges, 1, np.pi/180,100, minLineLength=50, maxLineGap=10)
image_line = image.copy()
```
- lines = cv2.HoughLinesP(edges, 1, np.pi/180, 100, minLineLength=50, maxLineGap=10): Fungsi cv2.HoughLinesP() digunakan untuk mendeteksi garis-garis dalam gambar menggunakan metode transformasi Hough Probabilistik

```bash
for line in lines:
    x1, y1, x2, y2 = line[0]
    cv2.line(image_line, (x1, y1), (x2, y2), (100, 8, 255),1)
```
- for line in lines:: Ini adalah loop for yang iterasi melalui setiap garis dalam variabel lines. Setiap elemen dalam lines adalah array satu dimensi yang berisi koordinat dua titik (x1, y1, x2, y2) yang merepresentasikan garis.
- x1, y1, x2, y2 = line[0]: Menyimpan koordinat titik awal (x1, y1) dan titik akhir (x2, y2) dari garis yang sedang diproses dalam variabel line.
- cv2.line(image_line, (x1, y1), (x2, y2), (100, 8, 255), 1): Fungsi cv2.line() digunakan untuk menggambar garis pada gambar image_line. Parameter yang digunakan adalah:

- image_line: Gambar tempat garis akan digambar.
- (x1, y1): Koordinat titik awal garis.
- (x2, y2): Koordinat titik akhir garis.
- (100, 8, 255): Warna garis dalam format BGR (Blue, Green, Red). Di sini, (100, 8, 255) menghasilkan warna ungu (campuran biru dan merah dengan nol hijau).
- 1: Ketebalan garis dalam piksel.

```bash
fig,axs = plt.subplots(1,2,figsize=(10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap='gray')
ax[0].set_title("Gambar Asli")

ax[1].imshow(image_line, cmap='gray')
ax[1].set_title("Gambar yang udah dideteksi")
```
- fig, axs = plt.subplots(1, 2, figsize=(10, 10)): Baris ini membuat sebuah jendela plot (figure) dengan dua subplot berdampingan (1 baris, 2 kolom). fig adalah objek yang mewakili jendela plot, dan axs adalah array yang berisi subplot-subplot tersebut.
- ax = axs.ravel(): Fungsi ravel() digunakan untuk mengubah array axs menjadi array satu dimensi. Ini memudahkan kita untuk mengakses setiap subplot secara individual menggunakan indeks.
- ax[0].imshow(gray, cmap='gray'): Pada subplot pertama (ax[0]), gambar asli dalam skala abu-abu (gray) ditampilkan menggunakan fungsi imshow() dari Matplotlib. Parameter cmap='gray' digunakan untuk menunjukkan bahwa gambar yang ditampilkan adalah dalam format grayscale. ax[0].set_title("Gambar Asli") digunakan untuk memberi judul pada subplot pertama.
- ax[1].imshow(image_line, cmap='gray'): Pada subplot kedua (ax[1]), gambar image_line yang telah digambar garis-garis deteksi (dengan garis-garis yang ditambahkan) ditampilkan menggunakan imshow() dengan parameter cmap='gray' untuk menampilkan gambar dalam format grayscale. ax[1].set_title("Gambar yang udah dideteksi") memberi judul pada subplot kedua.

```bash
edges
````
- mendeteksi tepi

```bash
lines
```
- untuk mendeteksi garis

```bash
lines.shape
```
- digunakan untuk mengetahui bentuk atau dimensi dari array 
