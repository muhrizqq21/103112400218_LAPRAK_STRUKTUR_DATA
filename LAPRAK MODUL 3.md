# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 3 Abstract Data Type (ADT) </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Abstract Data Type atau ADT merupakan sebuah model yang mendefinisikan sebuah tipe data dan juga sekumpulan operasi dasar yang dapat dilakukan terhadap tipe data tersebut. Konsep ADT adalah sebuah definisi yang sifatnya statis, yang artinya ia mendefinisikan apa yang bisa dilakukan oleh sebuah tipe data, bukan bagaimana cara melakukannya. Dalam bahasa pemrograman seperti C++ ini, umumnya sebuah TYPE di dalam ADT itu diterjemahkan menjadi sebuah struct. 

## Guided

### Contoh 1

mahasiswa.h
```h
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa {
    char nim[10];
    int nilai1, nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
#endif
```

mahasiswa.cpp
```cpp
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m) {
    cout << "Input Nama = ";
    cin >> (m).nim;
    cout << "Input Nilai1 = ";
    cin >> (m).nilai1;
    cout << "Input Nilai2 = ";
    cin >> (m).nilai2;
}
float rata2(mahasiswa m) {
    return float(m.nilai1 + m.nilai2) / 2;
}
```

main.cpp
```cpp
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main() {
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "Rata - Rata = " << rata2(mhs);
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d7a9b7bf-9c4a-451a-87f0-8024e0237fd0" />

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
