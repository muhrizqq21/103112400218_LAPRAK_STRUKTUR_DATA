# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 13 Multi Linked List (MLL) </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Multi Linked List merupakan struktur data yang terdiri dari sekumpulan list berbeda yang saling terhubung, di mana setiap elemen di dalamnya dapat membentuk list sendiri yang umumnya terbagi ke dalam hierarki list induk dan list anak. Dalam struktur ini, list induk berfungsi sebagai penunjuk bagi list anak yang terkait dengannya. Oleh karena itu, setiap operasi penambahan (insert) maupun penghapusan (delete) pada elemen anak wajib mengetahui posisi elemen induknya terlebih dahulu. Secara teknis, pengelolaan data ini menggunakan representasi pointer (address) untuk mengacu pada elemen tertentu, serta melibatkan manajemen memori berupa alokasi untuk pembuatan elemen baru dan dealokasi untuk mengembalikan memori ke sistem, terutama saat penghapusan elemen induk yang mengharuskan seluruh elemen anak di bawahnya ikut dihapus.

## Guided

### Contoh 1

```cpp
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;
    
    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    printAll(list);
    cout << "\n";

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/48f3ac4e-2e20-41eb-add8-c05327e7e917" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan implementasi dari struktur data Multi Linked List yang menghubungkan dua jenis list berbeda, yaitu list induk (ParentNode) dan list anak (ChildNode). Dalam kode ini, setiap elemen induk memiliki sebuah pointer (childHead) yang menunjuk ke awal dari list anak yang terkait dengannya, sehingga satu induk dapat memiliki sekumpulan data anak yang spesifik. Program tersebut menyediakan fungsionalitas untuk melakukan alokasi memori node baru, menyisipkan elemen induk, serta menyisipkan elemen anak dengan cara mencari posisi induknya terlebih dahulu sebelum meletakkan data anak di akhir list tersebut. Hasil akhirnya adalah sebuah struktur hierarkis yang dapat ditelusuri untuk menampilkan hubungan antara setiap induk dan daftar anak-anaknya. </p>

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
