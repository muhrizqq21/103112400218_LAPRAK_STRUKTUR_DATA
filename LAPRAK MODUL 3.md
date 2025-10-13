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
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/29c17ba2-3228-4959-83ca-255f16b32c7d" />

## Unguided

### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3*uts+0.4*uas+0.3*tugas.

nilaimahasiswa.h
```h
#ifndef NILAIMAHASISWA_H_INCLUDED
#define NILAIMAHASISWA_H_INCLUDED
#include <iostream>

using namespace std;
struct dataMahasiswa {
    string namaMahasiswa;
    string nimMahasiswa;
    float nilaiUTS, nilaiUAS, nilaiTugas, nilaiAkhirMahasiswa;
};

void inputMahasiswa(dataMahasiswa &m);

float hitungNilaiAkhirMahasiswa(dataMahasiswa m);

void tampilMahasiswa(dataMahasiswa m);

#endif
```

nilaimahasiswa.cpp
```cpp
#include "nilaimahasiswa.h"
#include <iostream>
using namespace std;

void inputMahasiswa(dataMahasiswa &m) {
    cout << "Nama: ";
    cin >> m.namaMahasiswa;
    cout << "NIM: ";
    cin >> m.nimMahasiswa;
    cout << "Nilai UTS: ";
    cin >> m.nilaiUTS;
    cout << "Nilai UAS: ";
    cin >> m.nilaiUAS;
    cout << "Nilai Tugas: ";
    cin >> m.nilaiTugas;

    m.nilaiAkhirMahasiswa = hitungNilaiAkhirMahasiswa(m);
}

float hitungNilaiAkhirMahasiswa(dataMahasiswa m) {
    return (0.3 * m.nilaiUTS) + (0.4 * m.nilaiUAS) + (0.3 * m.nilaiTugas);
}

void tampilMahasiswa(dataMahasiswa m) {
    cout << "\nNama        : " << m.namaMahasiswa
         << "\nNIM         : " << m.nimMahasiswa
         << "\nUTS         : " << m.nilaiUTS
         << "\nUAS         : " << m.nilaiUAS
         << "\nTugas       : " << m.nilaiTugas
         << "\nNilai Akhir : " << m.nilaiAkhirMahasiswa
         << endl;
}
```

main.cpp
```cpp
#include "nilaimahasiswa.h"
#include <iostream>
using namespace std;

int main() {
    dataMahasiswa mhs[10];
    int jumlahMahasiswa;

    cout << "Masukkan Jumlah Mahasiswa (Maks. 10): ";
    cin >> jumlahMahasiswa;
    if (jumlahMahasiswa > 10) {
        cout << "Maksimal hanya ada 10 data! Akan disimpan 10 mahasiswa pertama saja.\n";
        jumlahMahasiswa = 10;
    }

    for (int i = 0; i < jumlahMahasiswa; i++) {
        cout << "\nData Mahasiswa ke-" << i + 1 << endl;
        inputMahasiswa(mhs[i]);
    }

    cout << "\n=== Daftar Data Mahasiswa ===\n";
    for (int i = 0; i < jumlahMahasiswa; i++) {
        cout << "\nMahasiswa ke-" << i + 1;
        tampilMahasiswa(mhs[i]);
    }
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/cf753a18-10b9-41f0-8d87-23ed27306261" />
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/00a17d78-6f9f-4062-9218-b7cad7461a72" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas digunakan untuk menyimpan data mahasiswa dengan mengimplementasikan Abstract Data Type atau ADT, menggunakan struktur data yaitu struct dataMahasiswa, yang memiliki peran sebagai tipe data abstrak yang berfungsi untuk menggabungkan semua informasi mahasiswa ke dalam satu entitas. Program ini juga menerapkan pemisahan kode sesuai prinsip Abstract Data Type atau ADT, yaitu file nilaimahasiswa.h untuk mendefinisikan tipe data dan deklarasi fungsi, file nilaimahasiswa.cpp untuk merealisasikan fungsi-fungsi ADT, serta file main.cpp sebagai program utama yang akan menggunakan fungsi dan tipe tersebut. Secara keseluruhan, program ini bekerja dengan cara meminta pengguna untuk menginputkan jumlah mahasiswa dan data setiap mahasiswa, kemudian menghitung nilai akhir menggunakan fungsi yang sudah didefinisikan. Setelah itu, program akan menampilkan kembali semua data mahasiswa beserta nilai akhirnya. </p>

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
