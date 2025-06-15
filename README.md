# **Praktikum Komputasi Numerik _(Numerical Computation Lab Work)_**
- **Anggota Kelompok 22 :**

|    NRP     |      Name      |
| :--------: | :------------: |
| 5025241201 | Nasyita Larasati Ertyanada |
| 5025241222 | Rahma Sakinah |

### Laporan Resmi Praktikum Komputasi Numerik _(Numerical Computation Lab Work Report)_

Laporan ini disusun sebagai bagian dari pelaksanaan Praktikum Komputasi Numerik (Numerical Computation Lab Work) pada semester genap. Tujuan dari praktikum ini adalah untuk memahami dan menerapkan metode numerik yang telah dipelajari dalam perkuliahan ke dalam bentuk implementasi program komputer.

----

### Laporan Resmi Praktikum Komputasi Numerik _(Numerical Computation Lab Work Report)_

Laporan ini disusun sebagai bagian dari pelaksanaan Praktikum Komputasi Numerik (Numerical Computation Lab Work) pada semester genap. Tujuan dari praktikum ini adalah untuk memahami dan menerapkan metode numerik yang telah dipelajari dalam perkuliahan ke dalam bentuk implementasi program komputer.

----

## **Praktikum 1**

Anda sudah mengerti algoritma pemrosesan metode Regula Falsi, dan anda sudah memahami cara kerjanya. Sekarang anda tinggal mengimplementasikan algoritma tersebut menjadi sebuah program komputer metode Regula Falsi (yang dapat menampilkan proses iteratif numerik, lengkap dengan grafik fungsinya).

----

#### **Answer:**

- **Code:**
```phyton
import matplotlib.pyplot as pilot
import numpy as np

def f(x):
    return x**3 - 4*x - 9  

def regula_falsi(a, b, tol=1e-6, max_iter=100):
    if f(a) * f(b) >= 0:
        print("f(a) dan f(b) tidak memiliki tanda yang berlawanan. Tidak dapat menjamin akar.")
        return None

    print(f"{'Iter':<5} {'a':<10} {'b':<10} {'c':<10} {'f(c)':<10}")
    for i in range(1, max_iter + 1):
        c = b - (f(b)*(a - b)) / (f(a) - f(b))
        print(f"{i:<5} {a:<10.6f} {b:<10.6f} {c:<10.6f} {f(c):<10.6f}")

        if abs(f(c)) < tol:
            print(f"\nAkar ditemukan: {c} setelah {i} iterasi.")
            return c

        if f(a) * f(c) < 0:
            b = c
        else:
            a = c

    print("Akar tidak ditemukan dalam iterasi maksimum.")
    return None

def fsPlot(a, b, root=None):
    x_vals = np.linspace(a, b, 400)
    y_vals = f(x_vals)

    pilot.figure(figsize=(8, 5))
    pilot.axhline(0, color='black', linewidth=0.5)
    pilot.plot(x_vals, y_vals, label='f(x)')
    if root is not None:
        pilot.axvline(root, color='red', linestyle='--', label=f'Akar ≈ {root:.6f}')
    pilot.title('Grafik Fungsi dan Akar ')
    pilot.xlabel('x')
    pilot.ylabel('f(x)')
    pilot.grid(True)
    pilot.legend()
    pilot.show()

a = 2
b = 3
akar = regula_falsi(a, b)
if akar:
    fsPlot(a, b, akar)
```
## penjelasan
```phyton
    import matplotlib.pyplot as pilot
    import numpy as np
```
- inisialisasi library matplotlib dan numpy

```phyton
    def f(x):
    return x**3 - 4*x - 9  
```
- fungsi non linier yang ingin dicari akarnya, dengan subtitusi nilai x ke return
```phyton
    def regula_falsi(a, b, tol=1e-6, max_iter=100):
```
- fungsi metode regula falsi
- a, b adalah batas interval awal
- tol = toleransi f(c)
- max_iter = maximal iterasi 
- 
```phyton
    if f(a) * f(b) >= 0:
    print("f(a) dan f(b) tidak memiliki tanda yang berlawanan. Tidak dapat menjamin akar.")
    return None
```
- Jika f(a) dan f(b) tidak memiliki tanda berlawanan, metode tidak bisa dijalankan karena tidak bisa menjamin akar ada di antara keduanya.
```phyton
    for i in range(1, max_iter + 1):
    c = b - (f(b)*(a - b)) / (f(a) - f(b))
```
- loop rumus utama metode regula falsi
```phyton
        print(f"{i:<5} {a:<10.6f} {b:<10.6f} {c:<10.6f} {f(c):<10.6f}")
```
- print info tiap iterasi
```phyton
        if abs(f(c)) < tol:
        print(f"\nAkar ditemukan: {c} setelah {i} iterasi.")
        return c
```
- pengecekan konvergensi
- jika c sudah mendekati 0, maka loop berhenti dan c adalah akar yang dicari
```phyton
        if f(a) * f(c) < 0:
        b = c
    else:
        a = c
```
- Setelah hitung c, program memilih sisi mana dari interval yang mengandung akar berdasarkan tanda f(c).
```phyton
    print("Akar tidak ditemukan dalam iterasi maksimum.")
    return None
```
- kondisi akar konvergen
```phyton
    def fsPlot(a, b, root=None):
```
- fungsi untuk plot fungsi dan akar
```phyton
    x_vals = np.linspace(a, b, 400)
    y_vals = f(x_vals)
```
- `x_vals` untuk array sebanyak 400 dari a ke b
- `y_vals` nilai f(x) untuk setiap titik
```phyton
    pilot.figure(figsize=(8, 5))
    pilot.axhline(0, color='black', linewidth=0.5)
    pilot.plot(x_vals, y_vals, label='f(x)')
```
- untuk membuat kanvas grafik
- membuat garis horizontal
- menggambar kurva fungsi
```phyton
    if root is not None:
    pilot.axvline(root, color='red', linestyle='--', label=f'Akar ≈ {root:.6f}')
```
- kalau akar ditemukan, akar digambar putus-putus merah
```phyton
    pilot.title('Grafik Fungsi dan Akar ')
    pilot.xlabel('x')
    pilot.ylabel('f(x)')
    pilot.grid(True)
    pilot.legend()
    pilot.show()
```
- untuk menambah judul, label sumbu, grid, legend, dan menampilkan grafik.
```phyton
    a = 2
    b = 3
    akar = regula_falsi(a, b)
    if akar:
        fsPlot(a, b, akar)
```
- input dan eksekusi program

![output hasil iterasi](https://ibb.co/1ty9HskV)
![output hasil grafik](https://ibb.co/7B8x32y)
    
----
