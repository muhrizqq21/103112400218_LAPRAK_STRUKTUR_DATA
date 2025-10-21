# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 5 Singly Linked List (Bagian Kedua) </h1>
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

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

// Fungsi untuk insert di depan
void insertDepan(int data) {
    Node* newNode = createNode(data);
    newNode->next = head;
    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
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

// ========== SEARCH FUNCTION ==========
void searchNode(int dataCari) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    int posisi = 1;
    bool ditemukan = false;

    while (temp != nullptr) {
        if (temp->data == dataCari) {
            cout << "Data " << dataCari << " ditemukan di posisi " << posisi << ".\n";
            ditemukan = true;
            break;
        }
        temp = temp->next;
        posisi++;
    }

    if (!ditemukan) {
        cout << "Data " << dataCari << " tidak ditemukan dalam list.\n";
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
        cout << "6. Cari Data\n";
        cout << "7. Tampilkan List\n";
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
                cout << "Masukkan data yang ingin dicari: ";
                cin >> data;
                searchNode(data);
                break;
            case 7:
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
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/ed25817c-457a-4218-88f3-79b974f2229d" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang mengimplementasikan operasi dasar pada Singly Linked List yang dapat digunakan pengguna untuk mengelola daftar data integer melalui menu interaktif. Program ini juga menyediakan fungsionalitas untuk menambah data (di depan, di belakang, atau setelah data tertentu), menghapus, memperbarui, dan menampilkan seluruh isi list. Namun, inti dari fungsionalitas pencariannya terdapat pada fungsi searchNode, yang bertugas menelusuri list mulai dari node head atau posisi satu. Fungsi ini akan membandingkan data yang dicari dengan data pada setiap node secara berurutan sambil menghitung posisinya, yang kemudian akan mencetak posisi node jika data ditemukan atau melaporkan bahwa data tidak ada jika pencarian mencapai akhir list (NULL) tanpa menemukan kecocokan. </p>

## Unguided

### Soal 1

Buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya.

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

void cariNamaPembeli(string namapembeli) {
    dataPembeli* temp = head;
    bool found = false;

    while (temp != nullptr) {
        if (temp->namapembeli == namapembeli) {
            cout << "\nPembeli ditemukan: " << temp->namapembeli << " (Pesanan: " << temp->pesanan << ")\n";
            found = true;
            break;
        }
        temp = temp->next;
    }

    if (!found) {
        cout << "\nPembeli dengan nama " << namapembeli << " tidak ditemukan dalam antrian.\n";
    }
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
    cout << "\nMelayani pembeli: " << temp->namapembeli << " (Pesanan: " << temp->pesanan << ")\n";
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
        cout << nomor++ << ". " << temp->namapembeli << " - " << temp->pesanan << endl;
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
        cout << "2. Cari Nama Pembeli\n";
        cout << "3. Layani Antrian\n";
        cout << "4. Tampilkan Antrian\n";
        cout << "5. Hapus Semua Antrian\n";
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
            cout << "Masukkan Nama Pembeli yang Dicari: ";
            getline(cin, namapembeli);
            cariNamaPembeli(namapembeli);
            break;

            case 3: 
            layaniAntrian();
            break;

            case 4: 
            tampilkanAntrian(); 
            break;

            case 5: 
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
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/5b49ed4f-9400-45c2-886e-f268676932e1" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program antrian pembeli yang mengimplementasikan struktur data dinamis yang berfungsi untuk mengatur proses antrian dengan prinsip FIFO (First In First Out), di mana pembeli yang datang terlebih dahulu akan dilayani terlebih dahulu. Kemudian, program akan menggunakan struktur dataPembeli yang menyimpan data berupa nama pembeli dan pesanan, serta pointer next untuk menghubungkan setiap node dalam list. Pointer head juga digunakan untuk menunjuk ke pembeli pertama dalam antrian. Lalu, program juga menyediakan beberapa fitur utama, yaitu menambah antrian (menambahkan node baru di akhir list), mencari nama pembeli, melayani antrian (menghapus node pertama), menampilkan seluruh antrian (menelusuri list dari awal hingga akhir), dan menghapus semua antrian. </p>

### Soal 2

Gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN. 

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Buku {
    string ISBN;
    string judulBuku;
    string penulisBuku;
    Buku* next;
};

Buku* head = nullptr;

void tambahBuku() {
    Buku* baru = new Buku;
    cout << "Masukkan ISBN: ";
    getline(cin, baru->ISBN);
    cout << "Masukkan Judul: ";
    getline(cin, baru->judulBuku);
    cout << "Masukkan Penulis: ";
    getline(cin, baru->penulisBuku);
    baru->next = nullptr;

    if (!head) {
        head = baru;
    } else {
        Buku* temp = head;
        while (temp->next) temp = temp->next;
        temp->next = baru;
    }

    cout << "\nBuku " << "'" << baru->judulBuku << "'" << " berhasil masuk ke antrian.\n";
}

void hapusBuku() {
    string isbn;

    cout << "Masukkan ISBN buku yang akan dihapus: ";
    getline(cin, isbn);

    Buku* temp = head;
    Buku* prev = nullptr;
    while (temp && temp->ISBN != isbn) {
        prev = temp;
        temp = temp->next;
    }
    if (!temp) {
        cout << "\nBuku tidak ditemukan.\n";
        return;
    }
    if (!prev) {
        head = temp->next;
    } else {
        prev->next = temp->next;
    }
    delete temp;
    cout << "\nBuku berhasil dihapus.\n";
}

void updateBuku() {
    string judul;

    cout << "Masukkan judul buku yang akan diperbarui: ";
    getline(cin, judul);

    Buku* temp = head;
    while (temp && temp->ISBN != judul) temp = temp->next;
    if (!temp) {
        cout << "\nBuku tidak ditemukan.\n";
        return;
    }

    cout << "Masukkan Judul baru: ";
    getline(cin, temp->judulBuku);
    cout << "Masukkan Penulis baru: ";
    getline(cin, temp->penulisBuku);
    cout << "\nBuku berhasil diperbarui.\n";
}

void lihatBuku() {
    if (!head) {
        cout << "\nBelum ada data buku.\n";
        return;
    }
    Buku* temp = head;
    cout << "\n======== Daftar Buku ========\n";
    while (temp) {
        cout << "\nISBN   : " << temp->ISBN << "\n";
        cout << "Judul  : " << temp->judulBuku << "\n";
        cout << "Penulis: " << temp->penulisBuku << "\n";
        temp = temp->next;
    }
}

void cariBerdasarISBN() {
    string isbnCari;

    cout << "Masukkan ISBN yang dicari: ";
    getline(cin, isbnCari);

    Buku* temp = head;
    bool found = false;
    while (temp) {
        if (temp->ISBN == isbnCari) {
            cout << "\nBuku ditemukan!\n";
            cout << "\nISBN   : " << temp->ISBN << "\n";
            cout << "Judul  : " << temp->judulBuku << "\n";
            cout << "Penulis: " << temp->penulisBuku << "\n";
            found = true;
            break;
        }
        temp = temp->next;
    }

    if (!found) cout << "Buku dengan ISBN " << isbnCari << " tidak ditemukan.\n";
}

void cariBerdasarJudul() {
    string judulCari;

    cout << "Masukkan Judul yang dicari: ";
    getline(cin, judulCari);

    Buku* temp = head;
    bool found = false;
    while (temp) {
        if (temp->judulBuku == judulCari) {
            cout << "\nBuku ditemukan!\n";
            cout << "\nISBN   : " << temp->ISBN << "\n";
            cout << "Judul  : " << temp->judulBuku << "\n";
            cout << "Penulis: " << temp->penulisBuku << "\n";
            found = true;
        }
        temp = temp->next;
    }

    if (!found) cout << "Buku dengan judul " << judulCari << " tidak ditemukan.\n";
}

void cariBerdasarPenulis() {
    string penulisCari;

    cout << "Masukkan nama Penulis yang dicari: ";
    getline(cin, penulisCari);

    Buku* temp = head;
    bool found = false;
    while (temp) {
        if (temp->penulisBuku == penulisCari) {
            cout << "\nBuku ditemukan!\n";
            cout << "\nISBN   : " << temp->ISBN << "\n";
            cout << "Judul  : " << temp->judulBuku << "\n";
            cout << "Penulis: " << temp->penulisBuku << "\n";
            found = true;
        }
        temp = temp->next;
    }

    if (!found) cout << "Tidak ada buku karya " << penulisCari << ".\n";
}

void menuPencarian() {
    int pilih;
    string dummy;

    cout << "\n======== Menu Pencarian Buku ========\n";
    cout << "1. Cari berdasarkan ISBN\n";
    cout << "2. Cari berdasarkan Judul\n";
    cout << "3. Cari berdasarkan Penulis\n";
    cout << "Pilih: ";
    cin >> pilih;
    getline(cin, dummy);

    switch (pilih) {
        case 1: 
        cariBerdasarISBN(); 
        break;

        case 2: 
        cariBerdasarJudul(); 
        break;

        case 3: 
        cariBerdasarPenulis(); 
        break;

        default: cout << "Pilihan tidak valid.\n";
    }
}

int main() {
    int pilihan;
    string dummy;

    do {
        cout << "\n======== MENU UTAMA ========\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku\n";
        cout << "3. Update Buku\n";
        cout << "4. Lihat Buku\n";
        cout << "5. Cari Buku\n";
        cout << "0. Keluar\n";
        cout << "Pilih Menu: ";
        cin >> pilihan;
        getline(cin, dummy);

        switch (pilihan) {
            case 1: 
            tambahBuku(); 
            break;

            case 2: 
            hapusBuku(); 
            break;

            case 3: 
            updateBuku(); 
            break;

            case 4: 
            lihatBuku(); 
            break;

            case 5: 
            menuPencarian(); 
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
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/42d1e274-21d4-4ce1-92f3-f033aa0c8650" />
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/e1128458-0078-4622-8478-2f8238bb8e37" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang me-manajemen data buku dengan menggunakan Singly Linked List yang digunakan untuk menyimpan informasi ISBN, judul buku, dan penulis buku. Kemudian, program ini juga dilengkapi menu utama untuk operasi dasar (Tambah, Hapus, Update, Lihat) serta menu khusus untuk pencarian atau searching.Fungsionalitas searching terbagi menjadi tiga fungsi terpisah yaitu cariBerdasarISBN, cariBerdasarJudul, dan cariBerdasarPenulis. Setiap fungsi pencarian ini akan bekerja dengan cara menelusuri list dari node head, membandingkan input pengguna dengan data yang relevan di setiap node. Fungsi pencarian berdasarkan ISBN akan berhenti setelah menemukan kecocokan pertama, sedangkan pencarian berdasarkan judul dan penulis akan terus menelusuri seluruh list untuk menampilkan semua buku yang memenuhi kriteria. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
