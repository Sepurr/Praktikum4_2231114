```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
import skimage
from skimage.feature import graycomatrix, graycoprops
```
- import cv2: Mengimpor pustaka OpenCV, yang digunakan untuk manipulasi dan analisis gambar seperti pembacaan gambar, pengolahan citra, dan deteksi objek.
- import matplotlib.pyplot as plt: Mengimpor modul matplotlib.pyplot untuk membuat plot grafik dari data yang dihasilkan, seperti gambar hasil pemrosesan citra.
- import numpy as np: Mengimpor NumPy, sebuah pustaka Python yang digunakan untuk komputasi numerik, termasuk manipulasi array dan matriks, yang sangat penting dalam pemrosesan citra.
- import skimage: Mengimpor modul utama dari pustaka scikit-image, yang menyediakan berbagai fungsi untuk pemrosesan gambar seperti transformasi, segmentasi, dan ekstraksi fitur.
- from skimage.feature import graycomatrix, graycoprops: Mengimpor spesifik fungsi graycomatrix dan graycoprops dari modul skimage.feature. Fungsi ini digunakan untuk menghitung matriks kemunculan abu-abu (Gray-Level Co-occurrence Matrix, GLCM) dari gambar dan propertinya, yang sering digunakan dalam analisis tekstur.

```bash
img_hsv = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)

fig, axs = plt.subplots(1, 2, figsize=(10,10))
ax = axs.ravel()

ax[0].imshow(img)
ax[0].set_title("RGB")

ax[1].imshow(img_hsv)
ax[1].set_title("HSV")

plt.show()
```
- img_hsv = cv2.cvtColor(img, cv2.COLOR_RGB2HSV): Baris ini mengonversi citra yang disimpan dalam variabel img dari ruang warna RGB ke HSV menggunakan fungsi cvtColor dari opencv
- fig, axs = plt.subplots(1, 2, figsize=(10,10)): Baris ini mempersiapkan sebuah plot dengan dua subplot sejajar (1, 2), yang berarti akan ada dua gambar yang akan ditampilkan secara berdampingan
- ax = axs.ravel(): Baris ini meratakan array dari subplot axs menjadi satu dimensi menggunakan ravel(), sehingga kita dapat dengan mudah mengakses masing-masing subplot.
- ax[0].imshow(img): Baris ini menampilkan citra asli (dalam ruang warna RGB) di subplot pertama (ax[0]) dengan menggunakan imshow() dari matplotlib.
- ax[0].set_title("RGB"): Baris ini memberikan judul "RGB" untuk subplot pertama.
- ax[1].imshow(img_hsv): Baris ini menampilkan citra yang sudah dikonversi ke ruang warna HSV di subplot kedua (ax[1]) dengan menggunakan imshow().
- ax[1].set_title("HSV"): Baris ini memberikan judul "HSV" untuk subplot kedua.
- plt.show(): Baris ini menampilkan plot yang sudah disiapkan.

```bash
mean = np.mean(img_hsv.ravel())
std = np.std(img_hsv.ravel())
print("rata-rata",mean)
print("standar deviasi",std)
```
- mean = np.mean(img_hsv.ravel()): Baris ini menggunakan NumPy (np) untuk menghitung rata-rata dari nilai piksel dalam citra yang sudah dikonversi (img_hsv). Fungsi ravel() digunakan untuk meratakan matriks citra menjadi satu dimensi sebelum dihitung rata-ratanya menggunakan np.mean().

- std = np.std(img_hsv.ravel()): Baris ini menggunakan NumPy untuk menghitung standar deviasi dari nilai piksel dalam citra yang sama (img_hsv). Fungsi ravel() juga digunakan di sini untuk meratakan matriks citra sebelum dihitung standar deviasinya menggunakan np.std().

- print("rata-rata", mean): Baris ini mencetak nilai rata-rata yang telah dihitung sebelumnya ke konsol, disertai dengan label "rata-rata".

- print("standar deviasi", std): Baris ini mencetak nilai standar deviasi yang telah dihitung ke konsol, dengan label "standar deviasi".

```bash
hue = img_hsv[:,:,0]
```
- hue = img_hsv[:,:,0] mengambil salinan komponen hue (hue channel) dari citra yang sudah dikonversi ke ruang warna HSV (img_hsv).

```bash
glcm = graycomatrix(hue, distances=[1], angles=[0], levels=256, symmetric=True, normed=True)
```
- glcm = graycomatrix(hue, distances=[1], angles=[0], levels=256, symmetric=True, normed=True) digunakan untuk menghitung Gray-Level Co-occurrence Matrix (GLCM) dari citra atau matriks hue

```bash
print(glcm)
```
- print(glcm) digunakan untuk mencetak hasil GLCM (Gray-Level Co-occurrence Matrix) yang sudah dihitung sebelumnya ke konsol atau output.

```bash
contrast = graycoprops(glcm, 'contrast')[0,0]
```
- graycoprops(glcm, 'contrast'): Fungsi ini menghitung kontras dari GLCM yang diberikan.
- [0,0]: Ini mengambil nilai kontras yang dihasilkan dari hasil fungsi graycoprops. Biasanya, hasil dari graycoprops adalah matriks, dan saya menggunakan indeks [0,0] untuk mengambil elemen di posisi pertama.

```bash
dissimilarity = graycoprops(glcm, 'dissimilarity')[0,0]
```
- graycoprops(glcm, 'dissimilarity'): Fungsi ini menghitung dissimilaritas dari GLCM.
- [0,0]: Sama seperti sebelumnya, ini mengambil nilai dissimilaritas dari hasil fungsi graycoprops.

```bash
homogeneity = graycoprops(glcm, 'homogeneity')[0,0]
```
- graycoprops(glcm, 'homogeneity'): Fungsi ini menghitung homogenitas dari GLCM.
- [0,0]: Mengambil nilai homogenitas dari hasil fungsi graycoprops.

```bash
energy = graycoprops(glcm, 'energy')[0,0]
```
- graycoprops(glcm, 'energy'): Fungsi ini menghitung energi dari GLCM.
- [0,0]: Mengambil nilai energi dari hasil fungsi graycoprops.
```bash
correlation = graycoprops(glcm, 'correlation')[0,0]
```
- graycoprops(glcm, 'correlation'): Fungsi ini menghitung korelasi dari GLCM.
- [0,0]: Mengambil nilai korelasi dari hasil fungsi graycoprops.

```bash
print(f'contrast : {contrast}')
```
-Ini mencetak nilai kontras yang telah dihitung sebelumnya menggunakan graycoprops. Variabel contrast mengandung nilai kontras dari GLCM.

```bash
print(f'dissimilarity : {dissimilarity}')
```
- Ini mencetak nilai dissimilaritas yang telah dihitung sebelumnya menggunakan graycoprops. Variabel dissimilarity mengandung nilai dissimilaritas dari GLCM.

```bash
print(f'homogeneity : {homogeneity}')
```
- Ini mencetak nilai homogenitas yang telah dihitung sebelumnya menggunakan graycoprops. Variabel homogeneity mengandung nilai homogenitas dari GLCM

```bash
print(f'energy : {energy}')
```
- Ini mencetak nilai energi yang telah dihitung sebelumnya menggunakan graycoprops. Variabel energy mengandung nilai energi dari GLCM.

```bash
print(f'correlation : {correlation}')
```
-ni mencetak nilai korelasi yang telah dihitung sebelumnya menggunakan graycoprops. Variabel correlation mengandung nilai korelasi dari GLCM.
