# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 10 Tree </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Tree ialah struktur informasi non-linear yang ditafsirkan sebagai graf tidak berarah tersambung tanpa sirkuit, mempunyai satu simpul bawah yang disebut root, serta simpul yang lain saling berhubungan dalam hierarki parent serta child. Struktur ini kerap dikelola memakai fungsi rekursif, ialah sub program yang memanggil dirinya sendiri, spesialnya pada tipe Binary Tree yang menghalangi tiap node hanya boleh mempunyai maksimum 2 anak. Salah satu wujud pelaksanaannya merupakan Binary Search Tree (BST), yang mengendalikan penempatan informasi secara terurut di mana left child wajib lebih kecil serta right child lebih besar dari parent-nya, dan bisa ditelusuri memakai tata cara traversal semacam Pre-order, In-order, serta Post-order.

## Guided

### Contoh 1

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai) 
{
    Node *baru = new Node();
    baru->data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}
//insert (sisip data ke dalam tree)
Node *insert(Node *root, int nilai) 
{
    if (root == NULL) 
        return buatNode(nilai);
    if (nilai < root->data) 
        root->kiri = insert(root->kiri, nilai);
    else if (nilai > root->data) 
        root->kanan = insert(root->kanan, nilai);

    return root;
}

//search (mencari data dalam tree)

Node *search(Node *root, int nilai) 
{
    if (root == NULL || root->data == nilai)
        return root;
    if (nilai < root->data)
        return search(root->kiri, nilai); //cari di subtree kiri
    return search(root->kanan, nilai); //cari di subtree kanan
}

//Helper cari nilai minimum dalam tree
Node *nilaiTerkecil(Node *node) 
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;
    return current;
}

//delete (menghapus data dari tree) -- untuk update data
Node *hapus(Node *root, int nilai) 
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else {
        // jika data ditemukan
        if (root->kiri == NULL) {
            Node *temp = root->kanan;
            delete root;
            return temp;
        } else if (root->kanan == NULL) {
            Node *temp = root->kiri;
            delete root;
            return temp;
        }

        // Node dengan dua anak: dapatkan inorder successor (nilai terkecil di subtree kanan)
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data; 
        root->kanan = hapus(root->kanan, temp->data); 
    }
    return root;
}

//update (mengubah data dalam tree)
Node *update(Node *root, int lama, int baru) 
{

    if (search(root, lama) != NULL) 
    {
        root = hapus(root, lama);
        root = insert(root, baru);
        cout << "data" << lama << "berhasil diupdate menjadi" << baru << endl;
    } else {
    cout << "data" << lama << "tidak ditemukan!" << endl;
    }
    return root;
}

// traversal preorder
void preOrder(Node *root) 
{
    if (root != NULL) 
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

// traversal inorder
void inOrder(Node *root) 
{
    if (root != NULL) 
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

// traversal postorder
void postOrder(Node *root) 
{ //kiri kanan akar
    if (root != NULL) 
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main ()
{
    Node *root = NULL;
    
    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert (root, 10);
    root = insert (root, 5);
    root = insert (root, 20);
    root = insert (root, 3);
    root = insert (root, 7);
    root = insert (root, 15);
    root = insert (root, 25);
    cout << "Data berhasil dimasukkan. \n" 
        << endl;
    
    cout << "=== 2. TAMPILKAN TREE (TRAVERSAL) ===" << endl;
    cout << "Preorder: ";
    preOrder(root);
    cout << endl;
    cout << "Inorder: ";
    inOrder(root);
    cout << endl;
    cout << "Postorder: ";
    postOrder(root);
    cout << "\n" 
        << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 90;
    cout << "Cari" << cari1 << ": " << (search(root, cari1) ? "Ketemu" : "Tidak Ketemu") << endl;
    cout << "Cari" << cari2 << ": " << (search(root, cari2) ? "Ketemu" : "Tidak Ketemu") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    //mengubah 5 menjadi 8
    root = update (root, 5, 8);
    cout << "Hasil InOrder setelah update: ";
    cout << endl;
    cout << endl;

    cout << "Preorder: ";
    preOrder(root);
    cout << endl;
    cout << "Inorder: ";
    inOrder(root);
    cout << endl;
    cout << "Postorder: ";
    postOrder(root);
    cout << "\n" 
        << endl;

    cout << "=== 5. TEST DELETE ===" << endl;
    //menghapus 20 (Node  yang memiliki dua anak)
    cout << "Menghapus angka 20..." << endl;
    root = hapus (root, 20);

    cout << "Preorder: ";
    preOrder(root);
    cout << endl;
    cout << "Inorder: ";
    inOrder(root);
    cout << endl;
    cout << "Postorder: ";
    postOrder(root);
    cout << "\n" 
        << endl;

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/1be2ca92-d741-442a-8265-4d258d7c0a94" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas mengimplementasikan struktur data Binary Search Tree (BST) yang memfasilitasi operasi insert, search, update, serta delete memakai manipulasi pointer dinamis. Program mempraktikkan logika spesial pada fungsi update dengan metode menghapus data lama kemudian menyisipkan yang baru demi melindungi urutan, dan fungsi delete yang mampu menangani penghapusan node kompleks memakai metode inorder successor. Semua operasi tersebut divisualisasikan lewat 3 tata cara traversal (PreOrder, InOrder, PostOrder) yang diuji secara berentetan dalam fungsi utama buat memverifikasi struktur tree. </p>

## Unguided

### Soal 1

Buatlah ADT Binary Search Tree menggunakan Linked list sebagai berikut di dalam file "bstree.h"
> <img width="571" height="172" alt="image" src="https://github.com/user-attachments/assets/d9690f12-297d-4e13-b1a4-6e00419a90db" />

Buatlah implementasi ADT Binary Search Tree pada file "bstree.cpp" dan cobalah hasil implementasi ADT pada file "main.cpp"
> <img width="671" height="333" alt="image" src="https://github.com/user-attachments/assets/7794432a-bcd4-49f7-8817-043319b6da02" />

Output:
> <img width="507" height="138" alt="image" src="https://github.com/user-attachments/assets/a93daa82-2531-4440-887c-476adc0d0029" />

bstree.h
```h
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct Node *address;

#define Nil NULL

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void printInorder(address root);

#endif
```

bstree.cpp
```cpp
#include "bstree.h"

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil || root->info == x) {
        return root;
    }
    if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void printInorder(address root) {
    if (root != Nil) {
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}
```

main.cpp
```cpp
#include "bstree.h"

int main() {
    address root = Nil;
    
    cout << "Hello World" << endl;
    
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);
    printInorder(root);
    cout << endl;
    
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/f97abbe3-f9dd-41d3-84e8-a526b22e7ad7" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang mengimplementasikan struktur data non-linear berupa Binary Search Tree (BST) menggunakan representasi linked list dan prinsip rekursif untuk mengelola penyimpanan data secara efisien. Melalui prosedur insertNode, program secara otomatis menyusun elemen dengan aturan nilai yang lebih kecil dari parent ditempatkan pada left subtree, sedangkan nilai yang lebih besar ditempatkan pada right subtree. Selain manajemen memori melalui fungsi alokasi, program ini menerapkan metode In-order traversal untuk menelusuri dan menampilkan seluruh data secara terurut, yang membuktikan bahwa logika rekursif sangat efektif untuk menyelesaikan permasalahan dengan pola langkah yang teratur. </p>

### Soal 2

Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.

➢ fungsi hitungJumlahNode( root:address ) : integer

/* fungsi mengembalikan integer banyak node yang ada di dalam BST*/

➢ fungsi hitungTotalInfo( root:address, start:integer ) : integer

/* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/

➢ fungsi hitungKedalaman( root:address, start:integer ) : integer

/* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */
> <img width="673" height="480" alt="image" src="https://github.com/user-attachments/assets/8db7c935-d07a-4ecc-8c0a-a7a53a441df2" />

bstree.h
```h
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct Node *address;

#define Nil NULL

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void printInorder(address root);

int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root, int start);

#endif
```

bstree.cpp
```cpp
#include "bstree.h"

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil || root->info == x) {
        return root;
    }
    if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void printInorder(address root) {
    if (root != Nil) {
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}

int hitungJumlahNode(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
    }
}

int hitungTotalInfo(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
    }
}

int hitungKedalaman(address root, int start) {
    if (root == Nil) {
        return start;
    } else {
        int kiri = hitungKedalaman(root->left, start + 1);
        int kanan = hitungKedalaman(root->right, start + 1);
        return (kiri > kanan) ? kiri : kanan;
    }
}
```

main.cpp
```cpp
#include "bstree.h"

int main() {
    address root = Nil;
    
    cout << "Hello World" << endl;
    
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);
    printInorder(root);
    cout << "\n";
    cout << "kedalaman   : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah Node : " << hitungJumlahNode(root) << endl;
    cout << "total       : " << hitungTotalInfo(root) << endl;

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/5ad8c856-f28d-4ba4-b69a-c6dfff53b28d" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas menggunakan fungsi rekursif untuk menghitung statistik pada Binary Search Tree, yang meliputi perhitungan jumlah seluruh node , total akumulasi nilai informasi yang tersimpan dalam pohon , serta penentuan kedalaman atau tinggi maksimal dari struktur tree tersebut. Pendekatan ini memanfaatkan prinsip rekursif untuk menyederhanakan pemrosesan data non-linear dengan cara memanggil sub-program itu sendiri hingga mencapai kondisi khusus atau terminal. </p>

### Soal 3

Print tree secara pre-order dan post-order.

<img width="375" height="296" alt="image" src="https://github.com/user-attachments/assets/2a7a3483-a9b9-491d-be72-5655ce1b700c" />

bstree.h
```h
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct Node *address;

#define Nil NULL

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void printInorder(address root);

int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root, int start);

void PreOrder(address root);
void PostOrder(address root);

#endif
```

bstree.cpp
```cpp
#include "bstree.h"

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil || root->info == x) {
        return root;
    }
    if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void printInorder(address root) {
    if (root != Nil) {
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}

int hitungJumlahNode(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
    }
}

int hitungTotalInfo(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
    }
}

int hitungKedalaman(address root, int start) {
    if (root == Nil) {
        return start;
    } else {
        int kiri = hitungKedalaman(root->left, start + 1);
        int kanan = hitungKedalaman(root->right, start + 1);
        return (kiri > kanan) ? kiri : kanan;
    }
}

void PreOrder(address root) {
    if (root != Nil) {
        cout << root->info << " - ";
        PreOrder(root->left);
        PreOrder(root->right);
    }
}

void PostOrder(address root) {
    if (root != Nil) {
        PostOrder(root->left);
        PostOrder(root->right);
        cout << root->info << " - ";
    }
}
```

main.cpp
```cpp
#include "bstree.h"

int main() {
    address root = Nil;
    
    cout << "Hello World" << endl;
    
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);
    printInorder(root);
    cout << "\n";
    cout << "kedalaman   : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah Node : " << hitungJumlahNode(root) << endl;
    cout << "total       : " << hitungTotalInfo(root) << endl;
    cout << "\nPreOrder  : ";
    PreOrder(root);
    cout << "\nPostOrder : ";
    PostOrder(root);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c4fd4178-c6d2-4f48-9112-681c84fc0589" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program ini mengimplementasikan struktur data non-linear Binary Search Tree (BST) berbasis linked list dengan memanfaatkan prinsip rekursif untuk menyederhanakan penyelesaian masalah yang memiliki langkah-langkah terpola. Secara dinamis, sistem mengatur penempatan simpul dengan aturan nilai lebih kecil dari induknya ditempatkan di sub-pohon kiri dan nilai yang lebih besar di sub-pohon kanan. Selain manajemen penyisipan, program ini mampu menganalisis karakteristik pohon melalui perhitungan jumlah simpul, akumulasi total nilai informasi, serta kedalaman maksimal, dan menyediakan metode penelusuran Pre-order, In-order, dan Post-order untuk mengakses seluruh data secara sistematis. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
