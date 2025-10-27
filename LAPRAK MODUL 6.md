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
<p> Program C++ di atas adalah program yang mengimplementasikan struktur data Doubly Linked List yang akan menggunakan pointer global head dan tail untuk mengelola list. Kemudian, program ini menyediakan fungsionalitas yang lengkap untuk memanipulasi data, termasuk operasi penambahan seperti penambahan di depan, di belakang, dan setelah data tertentu, juga operasi penghapusan seperti hapus dari depan, dari belakang, dan data spesifik, serta fungsi untuk memperbarui nilai data. Lalu, untuk keunggulan dari Doubly Linked List didemonstrasikan melalui dua fungsi tampilan yang dapat mencetak isi list dari dua arah, yaitu dari depan (tampilDepan) dan dari belakang (tampilBelakang). Seluruh fungsionalitas ini dirangkum dalam sebuah menu interaktif berbasis teks di dalam fungsi main, yang memungkinkan pengguna untuk memilih operasi yang diinginkan secara dinamis. </p>

## Unguided

### Soal 1

Buatlah ADT Doubly Linked list sebagai berikut di dalam file “Doublylist.h”:
```
Type infotype : kendaraan <
nopol : string
warna : string
thnBuat : integer
>
Type address : pointer to ElmList
Type ElmList <
info : infotype
next :address
prev : address
>
Type List <
First : address
Last : address
>
procedure CreateList( input/output L : List )
function alokasi( x : infotype ) → address
procedure dealokasi(input/output P : address )
procedure printInfo( input L : List )
procedure insertLast(input/output L : List,
input P : address )
```
Buatlah implementasi ADT Doubly Linked list pada file “Doublylist.cpp” dan coba hasil implementasi ADT pada file “main.cpp”.
<p> Contoh Output: </p>
<img width="327" height="530" alt="image" src="https://github.com/user-attachments/assets/a185362e-053a-4236-8eb8-bf201768798a" />

doublylist.h
```h
#ifndef DOUBLYLIST_H_INCLUDED
#define DOUBLYLIST_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct infotype {
    string nopol;
    string warna;
    int thnBuat;
};

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);

address alokasi(infotype x);

void dealokasi(address &P);

void printInfo(List L);

void insertLast(List &L, address P);

#endif
```

doublylist.cpp
```cpp
#include "doublylist.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        L.Last->next = P;
        P->prev = L.Last;
        L.Last = P;
    }
}

void printInfo(List L) {
    address P = L.Last; 
    if (P == NULL) {
        cout << "List kosong" << endl;
        return;
    }
    while (P != NULL) {
        cout << "\nno polisi : " << P->info.nopol << endl;
        cout << "warna     : " << P->info.warna << endl;
        cout << "tahun     : " << P->info.thnBuat << endl;
        P = P->prev; 
    }
}
```

main.cpp
```cpp
#include <iostream>
#include "doublylist.h"

using namespace std;

int main() {
    List L;
    infotype dataIn;
    address P;

    CreateList(L);

    for (int i = 0; i < 4; i++) {
        cout << "\nmasukkan nomor polisi: ";
        cin >> dataIn.nopol;
        cout << "masukkan warna kendaraan: ";
        cin >> dataIn.warna;
        cout << "masukkan tahun kendaraan: ";
        cin >> dataIn.thnBuat;

        P = alokasi(dataIn);
        insertLast(L, P);
    }

    cout << endl;
    cout << "DATA LIST 1\n" << endl;
    printInfo(L);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/246ec48a-d212-43de-b0ae-9e9d94f93bb9" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program implementasi Abstract Data Type (ADT) untuk Doubly Linked List dalam C++ yang akan dirancang khusus untuk mengelola data kendaraan. Kemudian, untuk struktur infotype didefinisikan sebagai record kendaraan yang menyimpan nopol (string), warna (string), dan thnBuat (integer). Deklarasi ADT, termasuk struktur List (dengan pointer First dan Last) ditempatkan di file doublylist.h. Kemudian, implementasi fungsi-fungsi seperti CreateList, alokasi, dealokasi, printInfo, dan insertLast dibuat di file doublylist.cpp. Lalu, program utama di main.cpp akan meminta pengguna memasukkan data kendaraan baru secara berulang. Logika program akan menggunakan prosedur insertLast untuk menambahkan data, setelahnya program akan menampilkan seluruh data kendaraan yang tersimpan di dalam list menggunakan prosedur printInfo. </p>

### Soal 2

Carilah elemen dengan nomor polisi D001 dengan membuat fungsi baru. 
fungsi findElm( L : List, x : infotype ) : address
<p> Contoh Output: </p>
<img width="417" height="134" alt="image" src="https://github.com/user-attachments/assets/40bc8624-8366-487f-ace9-5137a2cf5525" />

doublylist.h
```h
#ifndef DOUBLYLIST_H_INCLUDED
#define DOUBLYLIST_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct infotype {
    string nopol;
    string warna;
    int thnBuat;
};

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);

address alokasi(infotype x);

void dealokasi(address &P);

void printInfo(List L);

void insertLast(List &L, address P);

address findElm(List L, string nopol);

#endif
```

doublylist.cpp
```cpp
#include "doublylist.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        L.Last->next = P;
        P->prev = L.Last;
        L.Last = P;
    }
}

address findElm(List L, string nopol) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.nopol == nopol) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

void printInfo(List L) {
    address P = L.Last; 
    if (P == NULL) {
        cout << "List kosong" << endl;
        return;
    }
    while (P != NULL) {
        cout << "no polisi : " << P->info.nopol << endl;
        cout << "warna     : " << P->info.warna << endl;
        cout << "tahun     : " << P->info.thnBuat << endl;
        P = P->prev;
    }
}
```

main.cpp
```cpp
#include "doublylist.h"
#include <iostream>

using namespace std;

int main() {
    List L;
    infotype dataIn;
    address P;
    string nopolCari;

    CreateList(L);
    
    for (int i = 0; i < 4; i++) {
        cout << "\nmasukkan nomor polisi: ";
        cin >> dataIn.nopol;
        cout << "masukkan warna kendaraan: ";
        cin >> dataIn.warna;
        cout << "masukkan tahun kendaraan: ";
        cin >> dataIn.thnBuat;

        P = alokasi(dataIn);
        insertLast(L, P);
    }

    cout << endl;
    cout << "DATA LIST 1\n" << endl;
    printInfo(L);
    
    cout << "\nMasukkan Nomor Polisi yang dicari : "; 
    cin >> nopolCari;
    
    P = findElm(L, nopolCari);
    
    if (P != NULL) {
        cout << "\nNomor Polisi : " << P->info.nopol << endl;
        cout << "Warna        : " << P->info.warna << endl;
        cout << "Tahun        : " << P->info.thnBuat << endl;
    } else {
        cout << "Data dengan nomor polisi " << nopolCari << " tidak ditemukan." << endl;
    }

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/b49126f2-499f-4753-857b-963f16ff8adc" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah pengembangan dari latihan 1 dengan menambahkan fungsionalitas pencarian elemen, dengan latihan utamanya adalah membuat sebuah fungsi baru bernama findElm yang memiliki parameter (L: List, x: infotype) dan mengembalikan tipe address. Kemudian, fungsi ini akan menelusuri Doubly Linked List untuk mencari elemen berdasarkan nopol (nomor polisi). Lalu, pada program utama (main.cpp), pengguna akan diminta untuk memasukkan nomor polisi yang ingin dicari. Setelah itu, program akan memanggil fungsi findElm dengan nomor polisi tersebut. Jika data ditemukan, program akan menampilkan detail lengkap dari kendaraan tersebut, yang terdiri dari nomor polisi, warna, dan tahun. </p>

### Soal 3

Hapus elemen dengan nomor polisi D003 dengan procedure delete.
- procedure deleteFirst( input/output L : List,
P : address )
- procedure deleteLast( input/output L : List,
P : address )
- procedure deleteAfter( input Prec : address,
input/output P : address )
<p> Contoh Output: </p>
<img width="536" height="208" alt="image" src="https://github.com/user-attachments/assets/bdad6be3-842e-4ba4-a6b4-c2c7fafccbb9" />

doublylist.h
```h
#ifndef DOUBLYLIST_H_INCLUDED
#define DOUBLYLIST_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct infotype {
    string nopol;
    string warna;
    int thnBuat;
};

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);

address alokasi(infotype x);

void dealokasi(address &P);

void printInfo(List L);

void insertLast(List &L, address P);

address findElm(List L, string nopol);

void deleteFirst(List &L, address &P);

void deleteLast(List &L, address &P);
  
void deleteAfter(List &L, address Prec, address &P); 

#endif
```

doublylist.cpp
```cpp
#include "doublylist.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        L.Last->next = P;
        P->prev = L.Last;
        L.Last = P;
    }
}

address findElm(List L, string nopol) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.nopol == nopol) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

void printInfo(List L) {
    address P = L.Last; 
    if (P == NULL) {
        cout << "List kosong" << endl;
        return;
    }
    while (P != NULL) {
        cout << "no polisi : " << P->info.nopol << endl;
        cout << "warna     : " << P->info.warna << endl;
        cout << "tahun     : " << P->info.thnBuat << endl;
        P = P->prev;
    }
}

void deleteFirst(List &L, address &P) {
    if (L.First == NULL) {
        cout << "List kosong, tidak ada yang bisa dihapus" << endl;
    } else {
        P = L.First;
        if (L.First == L.Last) {
            L.First = NULL;
            L.Last = NULL;
        } else {
            L.First = P->next;
            L.First->prev = NULL;
            P->next = NULL;
        }
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == NULL) {
        cout << "List kosong, tidak ada yang bisa dihapus" << endl;
    } else {
        P = L.Last;
        if (L.First == L.Last) {
            L.First = NULL;
            L.Last = NULL;
        } else {
            L.Last = P->prev;
            L.Last->next = NULL;
            P->prev = NULL;
        }
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec == NULL || Prec->next == NULL) {
        cout << "Tidak ada elemen setelah Prec" << endl;
    } else {
        P = Prec->next;
        
        if (P == L.Last) {
            deleteLast(L, P);
        } else {
            Prec->next = P->next;
            P->next->prev = Prec;
            P->next = NULL;
            P->prev = NULL;
        }
    }
}
```

main.cpp
```cpp
#include "doublylist.h"
#include <iostream>

using namespace std;

int main() {
    List L;
    infotype dataIn;
    address P;
    string nopolCari, nopolHapus;

    CreateList(L);
    
    for (int i = 0; i < 4; i++) {
        cout << "\nMasukkan nomor polisi: ";
        cin >> dataIn.nopol;
        cout << "Masukkan warna kendaraan: ";
        cin >> dataIn.warna;
        cout << "Masukkan tahun kendaraan: ";
        cin >> dataIn.thnBuat;

        P = alokasi(dataIn);
        insertLast(L, P);
    }

    cout << endl;
    cout << "DATA LIST 1\n" << endl;
    printInfo(L);
    
    cout << "\nMasukkan Nomor Polisi yang ingin dihapus : ";
    cin >> nopolHapus;

    address target = findElm(L, nopolHapus);
    if (target != NULL) {
        address prec = target->prev;
        address Q;

        if (prec == NULL) {
            deleteFirst(L, Q);
        } else {
            deleteAfter(L, prec, Q);
        }
        dealokasi(Q);
        cout << "\nData dengan nomor polisi " << nopolHapus << " telah dihapus.\n";
    } else {
        cout << "\nData dengan nomor polisi " << nopolHapus << " tidak ditemukan.\n";
    }

    cout << "\nDATA LIST 1 SETELAH PENGHAPUSAN\n" << endl;
    printInfo(L);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/ba043878-b0f0-4a34-8a8a-9bf1fd52ae3b" />
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/17b3ea4d-6c82-456e-9506-376b6b9d7266" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program yang berfungsi untuk menghapus data kendaraan dari Doubly Linked List berdasarkan nomor polisi yang dimasukkan pengguna. Setelah itu, pengguna akan menginput beberapa data kendaraan dan list akan terbentuk, lalu program meminta pengguna memasukkan nomor polisi yang ingin dihapus. Kemudian, proses penghapusan dilakukan dengan menggunakan prosedur deleteAfter jika data yang dihapus berada di tengah list, atau deleteFirst jika data tersebut berada di awal list. Setelah data berhasil dihapus, program akan menampilkan kembali isi list yang sudah diperbarui. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
