# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 6 Doubly Linked List (Bagian Pertama) </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Doubly Linked List adalah program linked list yang mana di setiap elemennya terdapat dua successor atau penunjuk, yaitu next yang akan menunjuk ke elemen sesudahnya dan prev yang akan menunjuk ke elemen sebelumnya. Struktur ini dikelola oleh dua pointer utama pada list, yaitu first (penunjuk elemen pertama) dan last (penunjuk elemen terakhir). Kemudian, di setiap elemen dalam list terdiri dari tiga komponen, yaitu info (data), next (penunjuk ke elemen depan), dan prev (penunjuk ke elemen belakang). Lalu, untuk keunggulan utama Doubly Linked List adalah kemampuannya untuk melakukan penelusuran (iterasi) secara dua arah, baik maju maupun mundur. Operasi fundamental pada Doubly Linked List meliputi penambahan elemen seperti insertFirst, insertLast, insertAfter dan penghapusan elemen seperti deleteFirst, deleteLast, deleteAfter yang semuanya akan memanfaatkan manipulasi pointer next dan prev.

## Guided

### Contoh 1

```cpp
#include <iostream>
using namespace std;

// ========
// STRUKTUR NODE
// ========
struct Node {
    int data;
    Node* prev;
    Node* next;
};

// POINTER GLOBAL
Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr) {
        head->prev = newNode;
    } else {
        tail = newNode; // Jika list kosong, tail juga menunjuk ke newNode
    }

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

// FUNGSI INSERT BELAKANG
void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr) {
        tail->next = newNode;
    } else {
        head = newNode; // Jika list kosong, head juga menunjuk ke newNode
    }

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

// FUNGSI INSERT SETELAH
void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current->data != target) {
        current = current->next;
    }

    if (current == nullptr) {
        cout << "Data target " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr) {
        current->next->prev = newNode;
    } else {
        tail = newNode; // Jika menambahkan di akhir, update tail
    }

    current->next = newNode;
    cout << "Data " << data << " berhasil ditambahkan setelah " << target << ".\n";
}

// FUNGSI HAPUS DEPAN
void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong, tidak ada yang dihapus.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr) {
        head->prev = nullptr;
    } else {
        tail = nullptr; // Jika list menjadi kosong, update tail
    }

    cout << "Data " << temp->data << " di depan berhasil dihapus.\n";
    delete temp;
}

// FUNGSI HAPUS BELAKANG
void hapusBelakang() {
    if (tail == nullptr) {
        cout << "List kosong, tidak ada yang dihapus.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr) {
        tail->next = nullptr;
    } else {
        head = nullptr; // Jika list menjadi kosong, update head
    }

    cout << "Data " << temp->data << " di belakang berhasil dihapus.\n";
    delete temp;
}

// HAPUS DATA
void hapusData(int target) {
    if (head == nullptr) {
        cout << "List kosong, tidak ada yang dihapus.\n";
        return;
    }

    Node* current = head;
    while (current != nullptr && current->data != target) {
        current = current->next;
    }

    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    if (current == head) {
        hapusDepan();
    } else if (current == tail) {
        hapusBelakang();
    } else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " berhasil dihapus.\n";
        delete current;
    }
}

// UPDATE DATA
void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}

// TAMPILKAN DARI DEPAN
void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

// ====================================
// Fungsi: Tampilkan dari belakang
// ====================================
void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/5f941a98-1ff2-4dfb-aa40-e37839bb958d" />
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0256b77c-ec87-4480-a5da-88b7dbcd100c" />
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/87424e55-4724-4b54-ba83-9a3c83d95a12" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program untuk menghitung nilai rata-rata dari mahasiswa dengan menggunakan struktur data dan fungsi yang dipisah dalam beberapa file berbeda namun tetap satu program. Terdapat file header mahasiswa.h yang digunakan untuk mendefinisikan sebuah struct bernama mahasiswa yang berisikan NIM (akan disimpan sebagai char nim[10]) dan juga dua nilai integer (nilai1, nilai2), serta mendeklarasikan dua fungsi: inputMhs untuk menginputkan data mahasiswa dan rata2 untuk menghitung rata-rata nilai mahasiswa. Kemudian, implementasi fungsi-fungsi ini terdapat dalam file mahasiswa.cpp, yang di mana inputMhs akan meminta pengguna memasukkan NIM dan kedua nilai dari mahasiswa, sementara fungsi rata2 akan menjumlahkan kedua nilai mahasiswa tersebut dan akan membaginya dua untuk mendapatkan nilai rata-rata. Lalu, program utama dalam main.cpp akan membuat sebuah variabel mahasiswa bernama mhs, dan memanggil fungsi inputMhs untuk mengisi datanya, lalu memanggil fungsi rata2 untuk menghitung dan menampilkan hasilnya ke layar. </p>

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

Buatlah program dengan ketentuan :
- 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
- fungsi/prosedur yang menampilkan isi sebuah array integer 2D
- fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu
- fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointer

```cpp
#include <iostream>
using namespace std;

void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

void tukarPosisi(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int A[3][3] = {
        {9, 8, 7},
        {6, 5, 4},
        {3, 2, 1}
    };

    int B[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    cout << "Array A:" << endl;
    tampilArray(A);

    cout << "Array B:" << endl;
    tampilArray(B);

    int baris = 2, kolom = 1; 
    tukarPosisi(A, B, baris, kolom);

    cout << "\nArray A setelah ditukar:" << endl;
    tampilArray(A);

    cout << "Array B setelah ditukar:" << endl;
    tampilArray(B);

    int x = 15, y = 5;
    int *p1 = &x;
    int *p2 = &y;

    cout << "\nSebelum ditukar:" << endl;
    cout << "x = " << x << ", y = " << y << endl;

    tukarPointer(p1, p2);

    cout << "Setelah ditukar:" << endl;
    cout << "x = " << x << ", y = " << y << endl;

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/b2f3636e-32dd-4fa4-a667-9fb9441ff813" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas menggunakan 2 array 2D berdimensi 3×3 serta 2 pointer integer yang digunakan untuk mempraktikkan konsep fungsi serta manipulasi data. Program ini mempunyai prosedur yang digunakan untuk menampilkan isi array 2D, mengubah elemen antara 2 array pada posisi tertentu, dan mengubah nilai dari 2 variabel menggunakan pointer. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
