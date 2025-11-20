# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 8 Queue </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Queue merupakan struktur data linear yang mempraktikkan prinsip FIFO (First In First Out), di mana elemen awal yang masuk hendak diproses terlebih dulu. Pembedahan utamanya terdiri dari Enqueue (penyisipan) pada posisi Tail serta Dequeue (penghapusan) pada posisi Head. Struktur ini bisa diimplementasikan memakai Linked List ataupun Array (Tabel) dengan bermacam tata cara pengaturan indeks semacam linear ataupun circular buffer.

## Guided

### Contoh 1

```cpp
#include <iostream>
using namespace std;

#define MAX 5 // Maximum size of the queue

// Queue Structure
struct Queue {
    int data[MAX];
    int head;
    int tail;
};

// Create an empty queue
void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

// Check if the queue is empty
bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

// Check if the queue is full
bool isFull(Queue Q) {
    return (Q.tail == MAX - 1);
}

// Show the elements of the queue
void printQueue(Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue is empty!" << endl;
    } else {
        cout << "Queue: ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

// Add an element to the queue
void enqueue(Queue &Q, int x) {
    if (isFull(Q)) {
        cout << "Queue is full!" << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0; // Initialize head if queue was empty
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueued: " << x << endl;
    }
}

// Remove an element from the queue
void dequeue(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue is empty!" << endl;
    } else {
        cout << "Dequeued: " << Q.data[Q.head] << endl;
        // If only one element was present
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            // Move all elements one position to the left
            for (int i = Q.head; i < Q.tail; i++) {
                Q.data[i] = Q.data[i + 1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    createQueue(Q);

    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;
}
```
> Output Program
> 

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program yang mengimplementasikan struktur data Stack (tumpukan) yang memakai representasi pointer (linked list). Program ini mendefinisikan struct Node selaku elemen stack serta mengimplementasikan operasi-operasi dasar yaitu push buat menyisipkan elemen di top, pop buat mengambil elemen dari top, serta isEmpty buat mengecek apakah stack kosong. Fungsi main berperan selaku driver buat menguji fungsionalitas ini dengan melaksanakan tiga kali push (10, 20, 30), kemudian satu kali pop, serta menunjukkan isi stack sehabis tiap operasi memakai fungsi show. </p>

## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file "stack.h":
> <img width="700" height="709" alt="image" src="https://github.com/user-attachments/assets/a3d1e4ac-b878-459d-b6f6-cbb4262f1eaf" />

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
