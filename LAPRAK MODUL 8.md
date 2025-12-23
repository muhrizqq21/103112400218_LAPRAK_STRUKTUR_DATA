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
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d2130554-4857-4616-9004-e5e93d97feb5" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program yang mengimplementasikan struktur data Queue memakai array statis dengan operasi enqueue serta dequeue yang mempraktikkan tata cara perpindahan elemen (shifting) dikala penghapusan data. Program ini dilengkapi fitur inisialisasi, validasi status antrean, serta pencetakan data buat mengelola antrean integer secara FIFO. </p>

## Unguided

### Soal 1

Buatlah ADT Queue menggunakan ARRAY sebagai berikut di dalam file "queue.h":
> <img width="595" height="197" alt="image" src="https://github.com/user-attachments/assets/50d55d23-f4e8-4e5d-aee8-e3971d8255be" />

Buatlah implementasi ADT Queue pada file "queue.cpp" dengan menerapkan mekanisme
queue Alternatif 1 (head diam, tail bergerak).
> <img width="689" height="353" alt="image" src="https://github.com/user-attachments/assets/9e0938ef-c4f0-4b60-991c-fdfd77aa8d0b" />

queue.h
```h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

typedef int infotype;

struct Queue {
    infotype info[5];
    int head;
    int tail;
};

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```

queue.cpp
```cpp
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == 4);
}

void enqueue(Queue &Q, infotype x) {
    if (!isFullQueue(Q)) {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    } else {
        cout << "Antrean Penuh" << endl;
    }
}

infotype dequeue(Queue &Q) {
    infotype x = -1;
    if (!isEmptyQueue(Q)) {
        x = Q.info[Q.head];
        if (Q.head == Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        } else {
            for (int i = 0; i < Q.tail; i++) {
                Q.info[i] = Q.info[i + 1];
            }
            Q.tail--;
        }
    }
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " \t | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = 0; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```

main.cpp
```cpp
#include "queue.h"

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);

    cout << "-----------------------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "-----------------------------------" << endl;

    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    
    dequeue(Q); printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/65043213-b63b-4a55-97e1-7a4b75af2254" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas mengimplementasikan ADT Queue berbasis array menggunakan mekanisme Alternatif 1, di mana posisi HEAD tetap statis sementara TAIL bergerak maju saat penambahan elemen. Setiap penghapusan elemen dilakukan dengan mengambil nilai pada HEAD yang kemudian diikuti dengan pergeseran seluruh sisa elemen ke depan untuk mengisi kekosongan, sehingga mensimulasikan pergerakan antrean fisik secara nyata. Program ini mencakup fungsi standar seperti inisialisasi antrean, pengecekan status kosong atau penuh, serta penampilan informasi elemen secara sistematis. </p>

### Soal 2

Buatlah implementasi ADT Queue pada file "queue.cpp" dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

queue.h
```h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

typedef int infotype;

struct Queue {
    infotype info[5];
    int head;
    int tail;
};

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```

queue.cpp
```cpp
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.head == 0 && Q.tail == 4);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Antrean benar-benar penuh!" << endl;
    } else {
        if (Q.tail == 4 && Q.head > 0) {
            int j = 0;
            for (int i = Q.head; i <= Q.tail; i++) {
                Q.info[j] = Q.info[i];
                j++;
            }
            Q.tail = j - 1;
            Q.head = 0;
        }

        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x = -1;
    if (!isEmptyQueue(Q)) {
        x = Q.info[Q.head];
        if (Q.head == Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        } else {
            Q.head++;
        }
    }
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " \t | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```

main.cpp
```cpp
#include "queue.h"

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);

    cout << "-----------------------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "-----------------------------------" << endl;

    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    
    dequeue(Q); printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d9977ec3-bf21-422e-ac79-c8e3cf0776a5" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang mengimplementasikan ADT Queue menggunakan mekanisme Alternatif 2, di mana indeks HEAD dan TAIL bergerak maju secara dinamis mengikuti operasi penghapusan dan penambahan elemen. Strategi ini dirancang agar lebih efisien karena meniadakan pergeseran elemen pada setiap operasi dequeue, namun konsekuensinya dapat muncul kondisi "penuh semu" saat TAIL mencapai batas maksimal array padahal masih terdapat ruang kosong di bagian depan. Guna mengoptimalkan penggunaan memori, program ini hanya akan melakukan pergeseran elemen secara kolektif apabila TAIL telah mencapai indeks maksimal (IdxMax) dan diperlukan ruang tambahan untuk elemen baru. </p>

### Soal 3

Buatlah implementasi ADT Queue pada file "queue.cpp" dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

queue.h
```h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

typedef int infotype;

struct Queue {
    infotype info[5];
    int head;
    int tail;
};

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```

queue.cpp
```cpp
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1);
}

bool isFullQueue(Queue Q) {
    return ((Q.tail + 1) % 5 == Q.head);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Antrean Penuh" << endl;
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail = (Q.tail + 1) % 5;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x = -1;
    if (!isEmptyQueue(Q)) {
        x = Q.info[Q.head];
        if (Q.head == Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        } else {
            Q.head = (Q.head + 1) % 5;
        }
    }
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " \t | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        int i = Q.head;
        while (true) {
            cout << Q.info[i] << " ";
            if (i == Q.tail) break;
            i = (i + 1) % 5;
        }
    }
    cout << endl;
}
```

main.cpp
```cpp
#include "queue.h"

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);

    cout << "-----------------------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "-----------------------------------" << endl;

    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    
    dequeue(Q); printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/21385f47-2044-4895-ad1e-a61072f82e47" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas adalah program yang menggunakan mekanisme Circular Buffer di mana indeks HEAD dan TAIL "berputar" kembali ke awal array setelah mencapai batas maksimal. Metode ini adalah yang paling efisien karena meniadakan kebutuhan pergeseran elemen (shifting) dan memungkinkan penggunaan seluruh slot memori secara kontinu tanpa terhalang kendala indeks maksimal. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).
