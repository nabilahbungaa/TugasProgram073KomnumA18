# Tugas Program KOMPUTASI NUMERIK #

## Kelompok A18 ##

Anggota Kelompok : 
1. ##### Umi Lailatul Khotimah (5025241062)
2. ##### Nashwa Aulia Putri Diansyah (5025241064)
3. ##### Nabilah Bunga Sulistia (5025241073)
4. ##### Rhea Debora Sianturi (5025241095)
5. ##### Mahirah Yasmin Aulia Mawahib (5025241095)

### Penjelasan Kode Program ###

```
import numpy as np
from sympy import Rational, factorial, simplify
```
Mengimpor pustaka:
- ```numpy``` digunakan untuk manipulasi array numerik.
- ```sympy``` digunakan untuk perhitungan simbolik seperti faktorial dan rasionalisasi jika dibutuhkan. Namun dalam kode ini hanya factorial dan simplify yang digunakan.

#### Fungsi compute_diff_table ####
Fungsi compute_diff_table digunakan untuk membentuk Membentuk dan menghitung tabel selisih hingga berdasarkan nilai-nilai fungsi (y) dari data tabel yang diberikan, sampai ke orde tertentu (maksimal sampai ∆⁴ dalam soal ini).

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
! [Screenshot 2025-06-08 171607.png] (https://github.com/nabilahbungaa/TugasProgram073KomnumA18/blob/b107129ee9e71b98bc7f88516d8e671a127e727e/Screenshot%202025-06-08%20171607.png)


 Cetakan print(...) hanya untuk menampilkan hasil sampai ∆⁴ sebagai referensi.





