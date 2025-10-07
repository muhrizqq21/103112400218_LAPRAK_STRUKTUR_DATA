# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 2 Pengenalan C++ (Bagian Kedua) </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

C++ bahasa pemrograman yang dikembangkan oleh Bjarne Stroustrup merupakan pengembangan dari bahasa C. Bahasa C++ banyak digunakan karena bahasa ini cukup efisien dan fleksibel, juga mendukung pemrograman yang berorientasi objek. Setiap program yang menggunakan C++ biasanya memiliki fungsi utama yaitu main() yang menjadi landasan program, dan kemudian diawali dengan perintah #include <iostream> untuk mengaktifkan fasilitas input-output. C++ juga memiliki variabel untuk menyimpan data seperti int, float, string, serta bool untuk nilai logika.  

## Guided

### Contoh 1

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai[] = {1, 2, 3, 4, 5};
    for (int i = 0; i < 5; i++) {
        cout << "Elemen ke-" << i << " = " << nilai[i] << endl;
    }
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d7a9b7bf-9c4a-451a-87f0-8024e0237fd0" />

### Contoh 2

```cpp
#include <iostream>
using namespace std;

int main() {
    int matriks[3][3] = {
         {1, 2, 3},
         {4, 5, 6},
         {7, 8, 9}};

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        // memindah baris setelah setiap baris matriks
        cout << endl;
    }
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/26415fd8-18c7-47a2-9619-3bcbc4567cc3" />

### Contoh 3

```cpp
#include <iostream>
using namespace std;

int main() {
    int umur = 25;
    int *p_umur;
    p_umur = &umur;

    cout << "Nilai 'umur': " << umur << endl;
    cout << "Alamat memori 'umur': " << &umur << endl;
    cout << "Nilai 'p_umur' (alamat): " << p_umur << endl;
    cout << "Nilai yang diakses 'p_umur': " << *p_umur << endl;
    cout << "Alamat memori dari pointer 'p_umur' itu sendiri: " << &p_umur << endl;

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/a0491ddb-4351-44fc-a1df-8d1c17b5f980" />

### Contoh 4

```cpp
#include <iostream>
using namespace std;

void tukar(int *px, int *py);

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/99d162e9-0018-41bc-b005-63a3c6c77936" />

### Contoh 5

```cpp
#include <iostream>
using namespace std;

void tukar(int &x, int &y);

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d5d20685-7773-4e72-b06c-3e038d465794" />

## Unguided

### Soal 1

Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:
<p> 1 2 3 </p>
<p> 4 5 6 </p>
<p> 7 8 9 </p>

Matriks Hasil Transpose:
<p> 1 4 7 </p>
<p> 2 5 8 </p>
<p> 3 6 9 </p>

```cpp
#include <iostream>
using namespace std;

void cetakMatriks(int matriks[3][3], const char* judul) {
    cout << judul << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    int matriksDiberikan[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    int transposeMatriks[3][3];
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transposeMatriks[j][i] = matriksDiberikan[i][j];
        }
    }
    cetakMatriks(matriksDiberikan, "Matriks Awal:");
    cout << endl;
    cetakMatriks(transposeMatriks, "Matriks Hasil Transpose:");
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/7f980eff-1f17-4625-a19b-90a4ed042ad5" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program yang menunjukkan cara melakukan transpose matriks 3x3. Dengan membandingkan matriks asli dan hasil transpose, kita bisa dengan jelas melihat bahwa baris pertama (1 2 3) kini menjadi kolom pertama, baris kedua (4 5 6) menjadi kolom kedua, dan seterusnya. </p>

### Soal 2

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

<p> Nilai awal: 5 </p>
<p> Nilai setelah dikuadratkan: 25 </p>

```cpp
#include <iostream>
using namespace std;

void kuadrat(int &bil) {
    bil = bil * bil;
}

int main() {
    int nilai = 5;
    cout << "Nilai Awal: " << nilai << endl;
    kuadrat(nilai);
    cout << "Nilai AKhir Setelah Dikuadratkan: " << nilai << endl;
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/25b8c3c9-62dd-444e-a0d8-96715b363932" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang memodifikasi variabel nilai secara langsung melalui prosedur kuadrat. Prosedur ini menerima alamat memori variabel, bukan salinannya. Hasilnya, nilai awal 5 berhasil diubah menjadi 25 setelah pemanggilan prosedur. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).


