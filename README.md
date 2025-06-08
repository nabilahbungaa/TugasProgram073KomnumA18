# Tugas Program KOMPUTASI NUMERIK #

## Kelompok A18 ##

Anggota Kelompok : 
1. *Umi Lailatul Khotimah* (5025241062)
2. *Nashwa Aulia Putri Diansyah* (5025241064)
3. *Nabilah Bunga Sulistia* (5025241073)
4. *Rhea Debora Sianturi* (5025241095)
5. *Mahirah Yasmin Aulia Mawahib* (5025241095)

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


