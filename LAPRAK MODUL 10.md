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
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

typedef int infotype;

struct Stack {
    infotype info[20];
    int top;
};

void CreateStack(Stack &S);

void push(Stack &S, infotype x);

infotype pop(Stack &S);

void printInfo(Stack S);

void balikStack(Stack &S);

#endif
```

stack.cpp
```cpp
#include "stack.h"

void CreateStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < 19) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top != -1) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    if (S.top != -1) {
        for (int i = S.top; i >= 0; i--) {
            cout << S.info[i] << " ";
        }
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack tempStack, tempStack2;
    CreateStack(tempStack);
    CreateStack(tempStack2);

    while (S.top != -1) {
        push(tempStack, pop(S));
    }

    while (tempStack.top != -1) {
        push(tempStack2, pop(tempStack));
    }

    while (tempStack2.top != -1) {
        push(S, pop(tempStack2));
    }
}
```

main.cpp
```cpp
#include <iostream>
#include "stack.h"

using namespace std;

int main() {
    cout << "Hello World!!" << endl;
    Stack S;
    CreateStack(S);
    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/f6ddc49c-e5e8-480f-91c1-e19829a32018" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program pada Latihan 1 ini bertujuan buat mengimplementasikan ADT (Abstract Data Type) Stack memakai representasi tabel, ialah array. Struktur informasi Stack ini didefinisikan buat menaruh infotype integer, dengan kapasitas array info sebanyak 20 elemen serta suatu variabel top buat menandai posisi elemen paling atas. Program ini mengimplementasikan fungsi-fungsi bawah stack semacam CreateStack (inisialisasi stack), push (menambah elemen), pop (mengambil elemen), serta printInfo (mencetak isi stack). Sebagai tambahan, program ini pula membuat prosedur balikStack yang berperan buat membalik urutan seluruh elemen di dalam stack. Program utama (main.cpp) setelah itu digunakan buat menguji fungsionalitas ADT ini dengan melaksanakan serangkaian pembedahan push serta pop, mencetak hasilnya, memanggil balikStack, serta mencetak kembali isi stack yang sudah terbalik. </p>

### Soal 2

Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)
```
int main()
{
Gambar 7-11 Output stack
STRUKTUR DATA 65
cout << "Hello world!" << endl;
Stack S;
createStack(S);
pushAscending(S,3);
pushAscending(S,4);
pushAscending(S,8);
pushAscending(S,2);
pushAscending(S,3);
pushAscending(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}
```
<p> Contoh Output: </p>
<img width="241" height="114" alt="image" src="https://github.com/user-attachments/assets/53051f33-2c4c-446d-a0e0-d1a442db121f" />

stack.h
```h
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

typedef int infotype;

struct Stack {
    infotype info[20];
    int top;
};

void CreateStack(Stack &S);

void push(Stack &S, infotype x);

infotype pop(Stack &S);

void printInfo(Stack S);

void balikStack(Stack &S);

void pushAscending(Stack &S, infotype x);

#endif
```

stack.cpp
```cpp
#include "stack.h"

void CreateStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < 19) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top != -1) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    if (S.top != -1) {
        for (int i = S.top; i >= 0; i--) {
            cout << S.info[i] << " ";
        }
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack tempStack, tempStack2;
    CreateStack(tempStack);
    CreateStack(tempStack2);

    while (S.top != -1) {
        push(tempStack, pop(S));
    }

    while (tempStack.top != -1) {
        push(tempStack2, pop(tempStack));
    }

    while (tempStack2.top != -1) {
        push(S, pop(tempStack2));
    }
}

void pushAscending(Stack &S, infotype x) {
    Stack tempStack;
    CreateStack(tempStack);

    while (S.top != -1 && S.info[S.top] > x) {
        push(tempStack, pop(S));
    }

    push(S, x);

    while (tempStack.top != -1) {
        push(S, pop(tempStack));
    }
}
```

main.cpp
```cpp
#include <iostream>
#include "stack.h"

using namespace std;

int main() {
    cout << "Hello World!!" << endl;
    Stack S;
    CreateStack(S);
    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/65709b85-70cb-4d49-81a7-3d5fb4d3251e" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program pada Latihan 2 ini ialah pengembangan dari Latihan 1 dengan meningkatkan satu prosedur baru, ialah pushAscending (in/out S: Stack, in x: integer). Prosedur ini mempunyai fungsi spesial, alih-alih cuma menambahkan elemen baru (x) di posisi Top, prosedur ini hendak menyisipkan x ke dalam stack sedemikian rupa sehingga urutan data di dalam stack senantiasa terpelihara secara ascending (terurut membesar) dari dasar stack mengarah ke Top. Program utama (main.cpp) setelah itu dimodifikasi buat memanggil pushAscending secara berurutan, mengambil alih pemanggilan push biasa, buat mendemonstrasikan kalau elemen-elemen (semacam 9, 8, 4, 3, 3, 2) tersimpan secara terurut di dalam stack. </p>

### Soal 3

Tambahkan prosedur getInputStream( in/out S : Stack ). Prosedur akan terus membaca dan
menerima input user dan memasukkan setiap input ke dalam stack hingga user menekan
tombol enter. Contoh: gunakan cin.get() untuk mendapatkan inputan user.
<img width="629" height="250" alt="image" src="https://github.com/user-attachments/assets/877496ac-8046-4284-98e3-12b1ee12d09c" />

stack.h
```h
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

typedef int infotype;

struct Stack {
    infotype info[20];
    int top;
};

void CreateStack(Stack &S);

void push(Stack &S, infotype x);

infotype pop(Stack &S);

void printInfo(Stack S);

void balikStack(Stack &S);

void pushAscending(Stack &S, infotype x);

void getInputStream(Stack &S);

#endif
```

stack.cpp
```cpp
#include "stack.h"
#include <cctype>

void CreateStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < 19) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top != -1) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    if (S.top != -1) {
        for (int i = S.top; i >= 0; i--) {
            cout << S.info[i] << " ";
        }
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack tempStack, tempStack2;
    CreateStack(tempStack);
    CreateStack(tempStack2);

    while (S.top != -1) {
        push(tempStack, pop(S));
    }

    while (tempStack.top != -1) {
        push(tempStack2, pop(tempStack));
    }

    while (tempStack2.top != -1) {
        push(S, pop(tempStack2));
    }
}

void pushAscending(Stack &S, infotype x) {
    Stack tempStack;
    CreateStack(tempStack);

    while (S.top != -1 && S.info[S.top] > x) {
        push(tempStack, pop(S));
    }

    push(S, x);

    while (tempStack.top != -1) {
        push(S, pop(tempStack));
    }
}

void getInputStream(Stack &S) {
    char c;
    
    while ((c = std::cin.get()) != '\n') {
        if (isdigit(c)) {
            infotype x = c - '0';
            push(S, x);
        }
    }
}
```

main.cpp
```cpp
#include <iostream>
#include "stack.h"

using namespace std;

int main() {
    cout << "Hello World!!" << endl;
    Stack S;
    CreateStack(S);

    getInputStream(S);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0d176e60-47f0-42a0-940a-f4ff2affc937" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program pada Latihan 3 ini akan memperkenalkan prosedur baru bernama getInputStream (in/out S: Stack). Fungsi dari prosedur ini adalah untuk secara kontinu membaca input yang dimasukkan oleh pengguna serta memasukkan tiap input tersebut ke dalam stack. Proses push input ke stack ini akan terus berlangsung sampai pengguna memencet tombol Enter, yang menunjukkan akhir dari input. Program utama (main.cpp) diganti buat memanggil getInputStream(S) selaku metode buat mengisi stack, mengambil alih pemanggilan push manual ataupun pushAscending dari latihan sebelumnya. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
