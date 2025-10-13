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

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus (0.3 x uts) + (0.4 x uas) + (0.3 x tugas).

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

<p> Buatlah ADT pelajaran sebagai berikut di dalam file “pelajaran.h”: </p> 
<img width="873" height="154" alt="image" src="https://github.com/user-attachments/assets/6428c687-026e-46fb-81df-e33f799f5497" />
<p> Buatlah implementasi ADT pelajaran pada file “pelajaran.cpp” </p>
<p> Cobalah hasil implementasi ADT pada file “main.cpp” </p>
<img width="998" height="218" alt="image" src="https://github.com/user-attachments/assets/b4a541f9-a843-414f-9aad-24c2530ebce2" />
<p> Contoh Output Hasil: </p>
<img width="420" height="65" alt="image" src="https://github.com/user-attachments/assets/cd2f4b1c-e6cc-4129-b5df-638de4693415" />

pelajaran.h
```h
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(pelajaran pel);
#endif
```

pelajaran.cpp
```cpp
#include "pelajaran.h"
#include <iostream>
using namespace std;

pelajaran create_pelajaran(string namapel, string kodepel) {
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "Nama Mata Kuliah: " << pel.namaMapel << endl;
    cout << "Kode Mata Kuliah: " << pel.kodeMapel << endl;
}
```

main.cpp
```cpp
#include "pelajaran.h"
#include <iostream>
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";
    pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/8e47a069-5517-43a3-95db-f5dacd4702e7" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang menerapkan konsep Abstract Data Type atau ADT untuk menyimpan data pelajaran berisikan nama mata kuliah dan kode mata kuliah. Struktur data pelajaran digunakan sebagai tipe abstrak, dengan fungsi create_pelajaran() yang digunakan untuk membuat objek pelajaran baru dan prosedur tampil_pelajaran() untuk menampilkan datanya. Kemudian, program dibagi menjadi tiga file, yaitu pelajaran.h untuk mendefinisikan tipe dan mendeklarasikan fungsi, pelajaran.cpp untuk mengimplementasikan fungsi, serta main.cpp sebagai program utama yang akan menguji ADT atau program tersebut. </p>

### Soal 3



## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
