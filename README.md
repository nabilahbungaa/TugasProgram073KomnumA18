# Tugas Program KOMPUTASI NUMERIK #

## Kelompok A18 ##

Anggota Kelompok : 
1. ##### Umi Lailatul Khotimah (5025241062)
2. ##### Nashwa Aulia Putri Diansyah (5025241064)
3. ##### Nabilah Bunga Sulistia (5025241073)
4. ##### Rhea Debora Sianturi (5025241095)
5. ##### Mahirah Yasmin Aulia Mawahib (5025241095)

Soal Nomor 28

![Foto 1000101663](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/1000101663.jpg)

Tabel Nomor 28

![Foto 1000101664](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/1000101664.jpg)


### Penjelasan Kode Program ###

```
import numpy as np
from sympy import Rational, factorial, simplify
```
Mengimpor pustaka:
- ```numpy``` digunakan untuk manipulasi array numerik.
- ```sympy``` digunakan untuk perhitungan simbolik seperti faktorial dan rasionalisasi jika dibutuhkan. Namun dalam kode ini hanya factorial dan simplify yang digunakan.

#### Fungsi compute_diff_table ####
Fungsi compute_diff_table digunakan untuk membentuk dan menghitung tabel selisih hingga berdasarkan nilai-nilai fungsi (y) dari data tabel yang diberikan, sampai ke orde tertentu (maksimal sampai ∆⁴ dalam soal ini).

```
def compute_diff_table(y_vals):
```
```y_vals``` → List atau array satu dimensi yang berisi nilai-nilai fungsi f(x) dari tabel (misal: [634575, 1673874, ...]).

##### Proses di Dalam Fungsi #####

*1. Menentukan panjang data*
```
n = len(y_vals) 
```
Menyimpan jumlah data (banyaknya titik) dalam variabel n

*2. Membuat tabel kosong untuk selisih*
```
diff = np.zeros((n, n))
```
→ Membuat matriks diff berukuran n x n dengan semua elemen nol. Tabel ini akan menyimpan hasil perhitungan ∆, ∆², ∆³, dst.

*3. Mengisi kolom pertama dengan nilai fungsi asli*
```
diff[:, 0] = y_vals
```
→ Kolom pertama (kolom indeks ke-0) berisi nilai f(x) atau y, sesuai tabel.

*4. Menghitung selisih bertingkat (finite differences)*
```
for j in range(1, n):
    for i in range(n - j):
        diff[i, j] = diff[i + 1, j - 1] - diff[i, j - 1]
        if j <= 4:
            print(f"diff[{i}, {j}] = {round(diff[i, j], 2)}")
```
Perulangan menghitung selisih-selisih tingkat ke-1 (∆), ke-2 (∆²), dst hingga ke-n.

Baris diff[i + 1, j - 1] - diff[i, j - 1] adalah rumus umum:
![Screenshot](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20171607.png)
Cetakan print(...) hanya untuk menampilkan hasil sampai ∆⁴ sebagai referensi.

*5. Mengembalikan hasil tabel*
```
return diff
```
→ Tabel lengkap berisi nilai ∆ dari orde ke-0 sampai ke-n.

#### Fungsi: stirling_interpolation(x_vals, y_vals, x0_val, x_target_val) ####

Fungsi ini bertujuan untuk menghitung nilai pendekatan f(x) menggunakan metode interpolasi Stirling berdasarkan nilai-nilai fungsi pada titik-titik tertentu dalam tabel.

Fungsi ini menerima data:
- ```x_vals``` → array nilai-nilai x dari tabel.
- ```y_vals``` → array nilai-nilai y=f(x).
- ```x0_val``` → nilai tengah (titik pusat interpolasi).
- ```x_target_val``` → nilai x yang akan dihitung interpolasinya.

##### Proses dalam Fungsi #####

```
x_vals = np.array(x_vals, dtype=float)
y_vals = np.array(y_vals, dtype=float)
```
Mengubah daftar nilai x dan y menjadi array NumPy bertipe float. Hal ini mempermudah operasi matematis selanjutnya karena NumPy mendukung vektor dan matriks.

```
h = x_vals[1] - x_vals[0]
print(f"\nAll h are equal: h = {h}")
```
Menghitung jarak antar titik ℎ dari data tabel. Karena data disusun teratur, cukup dihitung dari dua titik awal. Hasilnya akan sama untuk semua titik (asumsi Stirling memerlukan data dengan interval tetap).

```
idx = np.where(x_vals == x0_val)[0][0]
```
Mencari indeks (letak baris) dari titik pusat 𝑥0 dalam array ```x_vals```. Nilai idx akan digunakan untuk mengambil selisih-selisih yang simetris di sekitar 𝑥0.

```
S = round((x_target_val - x0_val) / h, 2)
print(f"S = {S}")
```
Menghitung nilai 𝑆 sebagai parameter utama interpolasi:
​![Hasil Screenshot](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20181947.png)

```
diff = compute_diff_table(y_vals)
```
Memanggil fungsi compute_diff_table(...) untuk menghasilkan tabel selisih hingga dari data 𝑦. Tabel ini berisi nilai ∆, ∆², ∆³, dst.

```
print("\nCalculating Stirling Interpolation")
result = y_vals[idx]
print(f"f0 = {result}")
```
Menyimpan nilai awal 𝑓(𝑥0) sebagai nilai dasar hasil interpolasi. Dicetak ke layar untuk pelacakan proses.

*Term 1*
```
delta1 = (diff[idx][1] + diff[idx - 1][1]) / 2
term1 = round(S * delta1, 2)
print(f"Term i=1: {term1}")
result += term1
```
Menghitung suku pertama dari Stirling:
![Screenshot Hasil Program](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20183255.png)
Disimpan di term1 dan ditambahkan ke result.

*Term 2*\
```
delta2 = diff[idx - 1][2]
term2 = round((round((S * (S - 1))/2, 2) * delta2), 2)
print(f"Term i=2: {term2}")
result += term2
```
Menghitung suku kedua dari Stirling:
![Screenshot 8](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20190329.png)

*Term 3*
```
delta3 = (diff[idx - 1][3] + diff[idx - 2][3]) / 2
term3 = round((round((S * (S - 1) * (S - 2))/6, 2) * delta3), 2)
print(f"Term i=3: {term3}")
result += term3
```
Menghitung suku ketiga dari Stirling:
![Screenshot Tambahan](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20184459.png)

*Term 4*
```
delta4 = diff[idx - 2][4]
term4 = round(((x_target_val / 4) * round((S * (S - 1) * (S - 2))/6, 2) * delta4), 2)
print(f"Term i=4: {term4}")
result += term4
```
Menghitung suku keempat dari Stirling. Catatan:
Biasanya term ini berbentuk:
![Screenshot Terbaru](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20184926.png)

#### Menghasilkan nilai interpolasi akhir #####
```
y_interp = round(result, 2)
return y_interp
```
Membulatkan hasil akhir interpolasi menjadi 2 angka desimal, lalu mengembalikan hasil tersebut.

##### Pemanggilan Fungsi #####
```
x_vals = [3, 6, 9, 12, 15, 18, 21, 24, 27]
y_vals = [-741, -186, 32121, 184956, 634575, 1673874, 3741549, 7451256, 13620771]
x0 = 15
xt = 16
yt = 897104

hasil = stirling_interpolation(x_vals, y_vals, x0, xt)
```
Mengatur data input dari tabel dan memanggil fungsi interpolasi.

```
print(f"\nf({xt}) = {hasil}")
print(f"Et = {abs((yt - hasil)/yt) * 100 : .2f}")
```
Menampilkan hasil akhir 𝑓(𝑥) dan menghitung galat relatif persentase:
![Screenshot Terakhir](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20185545.png)

## OUTPUTNYA SEBAGAI BERIKUT

![Screenshot 9](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/main/Screenshot%202025-06-08%20192222.png)

 
! [b415524](https://raw.githubusercontent.com/nabilahbungaa/TugasProgram073KomnumA18/commit/b41552422bf6ce2d28cf88afa98dd0e0a660ccf6)







 .









