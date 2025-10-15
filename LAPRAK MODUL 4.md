# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 4 Singly Linked List (Bagian Pertama) </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang di dalamnya terdiri dari rangkaian node yang sudah saling terhubung melalui pointer, yang di mana setiap node berisi data dan penunjuk ke node berikutnya, sementara node yang terakhir akan menunjuk ke NULL sebagai tanda akhir dari list. Struktur data ini bersifat fleksibel karena ukurannya juga dapat berubah sesuai kebutuhan dan hanya dapat diakses secara sekuensial dari awal hingga akhir. Singly Linked List ini digunakan untuk membentuk sistem dengan prinsip FIFO (First In First Out).  

## Guided

### Contoh 1

```cpp
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk insert di depan
void insertDepan(int data) {
    Node* newNode = createNode(data);
    newNode->next = head;
    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}


void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
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
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/5d7fbd3c-3625-4f00-8311-fed44f0fd79c" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang mengimplementasikan struktur data single linked list yang memungkinkan pengguna bisa melakukan berbagai operasi dasar. Program di atas mendefinisikan sebuah struct bernama Node yang memiliki dua komponen yaitu data yang akan digunakan untuk menyimpan nilai integer dan pointer next yang akan digunakan untuk menunjuk ke node berikutnya. Kemudian, terdapat juga fungsi-fungsi untuk memodifikasi linked list, seperti menambah data di depan (insertDepan), menambah data di belakang (insertBelakang), dan menambah data setelah data tertentu (insertSetelah). Selain itu, program di atas juga menyediakan fungsi untuk menghapus (hapusNode) dan fungsi untuk memperbarui (updateNode) data yang sudah ada di dalam list. Lalu, fungsi tampilkanList akan digunakan untuk mencetak seluruh isi dari linked list ke layar. Semua operasi ini dikelola melalui sebuah menu interaktif di dalam fungsi main, yang di mana pengguna bisa memilih tindakan yang pengguna inginkan dengan memasukkan angka, dan program akan terus berjalan sampai pengguna memilih opsi untuk keluar. </p>

## Unguided

### Soal 1

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani

```cpp
#include <iostream>
#include <string>
using namespace std;

struct dataPembeli {
    string namapembeli;
    string pesanan;
    dataPembeli* next;
};

dataPembeli* head = nullptr;

dataPembeli* createNode(string namapembeli, string pesanan) {
    dataPembeli* newNode = new dataPembeli();
    newNode->namapembeli = namapembeli;
    newNode->pesanan = pesanan;
    newNode->next = nullptr;
    return newNode;
}

void tambahAntrian(string namapembeli, string pesanan) {
    dataPembeli* newNode = createNode(namapembeli, pesanan);
    if (head == nullptr) {
        head = newNode;
    } else {
        dataPembeli* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "\nPembeli " << namapembeli << " berhasil masuk ke antrian.\n";
}

void layaniAntrian() {
    if (head == nullptr) {
        cout << "\nAntrian kosong, tidak ada yang dilayani.\n";
        return;
    }

    dataPembeli* temp = head;
    cout << "Melayani pembeli: " << temp->namapembeli 
         << " (Pesanan: " << temp->pesanan << ")\n";
    head = head->next;
    delete temp;
}

void tampilkanAntrian() {
    if (head == nullptr) {
        cout << "\nAntrian sudah kosong.\n";
        return;
    }

    dataPembeli* temp = head;
    cout << "\n===== DAFTAR ANTRIAN PEMBELI =====\n";
    int nomor = 1;
    while (temp != nullptr) {
        cout << nomor++ << ". " << temp->namapembeli 
             << " - " << temp->pesanan << endl;
        temp = temp->next;
    }
}

void hapusSemuaAntrian() {
    while (head != nullptr) {
        dataPembeli* temp = head;
        head = head->next;
        delete temp;
    }
    cout << "\nSemua antrian berhasil dihapus.\n";
}

int main() {
    int pilihan;
    string namapembeli, pesanan;

    do {
        cout << "\n===== MENU ANTRIAN PEMBELI =====\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Hapus Semua Antrian\n";
        cout << "0. Keluar\n";
        cout << "Pilih Menu: ";
        cin >> pilihan;
        cin.ignore();
        switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Pembeli: ";
                getline(cin, namapembeli);
                cout << "Masukkan Pesanan Yang Akan Dibeli: ";
                getline(cin, pesanan);
                tambahAntrian(namapembeli, pesanan);
                break;

            case 2:
                layaniAntrian();
                break;

            case 3:
                tampilkanAntrian();
                break;

            case 4:
                hapusSemuaAntrian();
                break;

            case 0:
                cout << "Program selesai.\n";
                break;

            default:
                cout << "Pilihan tidak valid!\n";
        }

    } while (pilihan != 0);
    
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/3c881c90-6ed2-46e3-80b8-26f7b26d0b69" />
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/e6d05033-2d18-4669-a0fe-2ba1dd91b3c0" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program antrian pembeli yang mengimplementasikan struktur data dinamis yang berfungsi untuk mengatur proses antrian dengan prinsip FIFO (First In First Out), di mana pembeli yang datang terlebih dahulu akan dilayani terlebih dahulu. Kemudian, program akan menggunakan struktur dataPembeli yang menyimpan data berupa nama pembeli dan pesanan, serta pointer next untuk menghubungkan setiap node dalam list. Pointer head juga digunakan untuk menunjuk ke pembeli pertama dalam antrian. Lalu, program juga menyediakan beberapa fitur utama, yaitu menambah antrian (menambahkan node baru di akhir list), melayani antrian (menghapus node pertama), menampilkan seluruh antrian (menelusuri list dari awal hingga akhir), dan menghapus semua antrian. </p>

### Soal 2

buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1). 

```cpp
#include <iostream>
using namespace std;

struct Node {
    int angka;
    Node* next;
};

Node* head = nullptr;

Node* createNode(int angka) {
    Node* newNode = new Node();
    newNode->angka = angka;
    newNode->next = nullptr;
    return newNode;
}

void insertBelakang(int angka) {
    Node* newNode = createNode(angka);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void tampilkanList() {
    if (head == nullptr) {
        cout << "\nList Kosong!\n";
        return;
    }

    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->angka << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

void reverseList() {
    Node* prev = nullptr;
    Node* current = head;
    Node* next = nullptr;

    while (current != nullptr) {
        next = current->next;   
        current->next = prev;   
        prev = current;         
        current = next;         
    }
    head = prev;
}

int main() {
    int n, angka;
    cout << "Masukkan Jumlah Angka (Min. 2): ";
    cin >> n;

    for (int i = 0; i < n; i++) {
        cout << "Angka ke-" << i + 1 << ": ";
        cin >> angka;
        insertBelakang(angka);
    }

    cout << "\nList Sebelum Direverse (Dibalik): \n";
    tampilkanList();

    reverseList();

    cout << "\nList Setelah Direverse (Dibalik): \n";
    tampilkanList();

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/7195a982-7395-4e73-aa74-83ab80b68861" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program membalik atau reverse yang menerapkan konsep dasar struktur data dinamis yang menggunakan node dan pointer sebagaimana yang sudah dijelaskan dalam materi modul. Setiap node berisikan data berupa angka dan pointer yang menunjuk ke node berikutnya, sedangkan pointer head menunjuk ke elemen pertama dalam list. Kemudian, proses pembalikan atau reverse akan dilakukan dengan memanfaatkan tiga pointer, yaitu prev, current, dan next, yang secara berurutan digunakan untuk membalik arah hubungan antar node sehingga urutan data berubah dari awal ke akhir menjadi sebaliknya. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
