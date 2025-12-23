# <h1 align = "center" > Laporan Praktikum Struktur Data <br> Modul 14 Graph </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

Graph merupakan sebuah struktur data yang terdiri dari himpunan tidak kosong dari node atau vertex serta garis penghubung yang disebut sebagai edge. Berdasarkan karakteristik hubungannya, graph dapat dibedakan menjadi graph berarah (directed graph) di mana tiap edge memiliki arah tertentu, serta graph tidak berarah (undirected graph). Dalam implementasi pemrograman, graph dapat direpresentasikan melalui matriks ketetanggaan menggunakan array 2 dimensi atau multi linked list yang memiliki keunggulan dalam pengelolaan data secara dinamis. Selain itu, terdapat metode penelusuran graph seperti Breadth First Search (BFS) yang mengunjungi node per level menggunakan queue dan Depth First Search (DFS) yang mengunjungi subtree secara rekursif menggunakan stack, serta konsep topological sort untuk menghasilkan urutan linear dari elemen yang memiliki keterurutan parsial.

## Guided

### Contoh 1

graf.h
```h
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif
```

graf.cpp
```h
#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}
```

main.cpp
```h
#include "graf.h"
#include "graf.cpp"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
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
