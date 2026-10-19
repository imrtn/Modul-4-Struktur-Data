# <h1 align="center">Laporan Praktikum Modul 4 - SINGLY LINKED LIST </h1>

<p align="center">Imroatun Sholikha - 109082500111</p>

Dasar Teori
Singly Linked List merupakan salah satu bentuk struktur data yang terdiri dari serangkaian elemen data yang saling terhubung dan bersifat fleksibel karena dapat bertambah atau berkurang sesuai kebutuhan. Setiap elemen memiliki bagian data dan pointer yang berfungsi sebagai penghubung ke elemen berikutnya. [1]

Singly Linked List hanya menggunakan satu arah pointer untuk menghubungkan setiap elemen. Struktur ini memiliki beberapa komponen, seperti First sebagai penunjuk elemen pertama, next sebagai penunjuk elemen berikutnya, serta Nil yang menunjukkan bahwa pointer tidak mengacu ke elemen mana pun. [1]

Penerapan Singly Linked List dalam C++ dilakukan dengan menggunakan struct, pointer, dan fungsi untuk mengelola elemen data. Implementasinya dapat dipisahkan ke dalam file header berekstensi .h, file implementasi .cpp, serta program utama main.cpp untuk menjalankan dan menguji operasi linked list. [1]

A. Singly Linked List

Singly Linked List merupakan model ADT Linked List yang hanya memiliki satu arah pointer. Setiap elemen atau node terdiri dari bagian info untuk menyimpan data dan next untuk menunjukkan alamat elemen berikutnya. Node terakhir menunjuk ke Nil, sedangkan First menunjuk alamat elemen pertama dalam list.

B. Header File dan Implementasi

File .h digunakan untuk mendeklarasikan tipe data, struktur elemen, struktur list, dan prototipe fungsi. File .cpp berisi implementasi fungsi-fungsi ADT, sedangkan main.cpp digunakan sebagai program utama untuk menguji operasi Singly Linked List.

C. Operasi Dasar Singly Linked List

Operasi dasar Singly Linked List meliputi CreateList() untuk membuat list kosong, alokasi() untuk menyediakan memori bagi elemen baru, dealokasi() untuk membebaskan memori, insertFirst() untuk menambahkan elemen pada awal list, dan printInfo() untuk menampilkan seluruh data yang tersimpan dalam list. [1]


## Guided

### 1. 


## list.h

```C++
#ifndef List.h
#define List .h
#define Nil NULL
#include <iostream>
using namespace std;
struct mahasiswa
{
    string nama, nim;
    int umur;
};
typedef mahasiswa dataMahasiswa;
typedef struct node *address;
struct node
{
    dataMahasiswa isidata;
    address next;
};
struct linkedlist
{
    address first;
};

bool isEmpty(linkedlist list);
void createList(linkedlist &list);
address alokasi(string nama, string nim, int umur);
void dealokasi (address &node);
void printList(linkedlist list);
void insertFirst (linkedlist &list, address nodeBaru);
void insertAfter(linkedlist &list, address nodeBaru, address prev);
void insertLast(linkedlist &list, address nodeBaru);

void delFirst(linkedlist &list);
void delLast (linkedlist &list);
void delAfter (linkedlist &list, address nodeHapus, address nodePrev);
int nbList(linkedlist list);
void deletelist (linkedlist &list);
#endif
```
Berisi deklarasi struktur data mahasiswa, node, linked list, dan fungsi-fungsi untuk mengelola data.

## list.cpp

```C++
#include "list.h"
#include <iostream>
using namespace std;

bool isEmpty(linkedlist list)
{
    if (list.first == Nil)
    {
        return true;
    }
    else
    {
        return false;
    }
}

void createList(linkedlist &list)
{
    list.first = Nil;
}

address alokasi(string nama, string nim, int umur)
{
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

void dealokasi(address &node)
{
    node->next = Nil;
    delete node;
}

void insertFirst(linkedlist &list, address nodeBaru)
{
    nodeBaru->next = list.first;
    list.first = nodeBaru;
}

void insertAfter(linkedlist &list, address nodeBaru, address prev)
{
    if (prev != Nil)
    {
        nodeBaru->next = prev->next;
        prev->next = nodeBaru;
    }
    else
    {
        cout << "Node sebelumnya tidak valid." << endl;
    }
}

void insertLast(linkedlist &list, address nodeBaru)
{
    if (isEmpty(list))
    {
        list.first = nodeBaru;
    }
    else
    {
        address nodeBantu = list.first;
        while (nodeBantu->next != Nil)
        {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

void delFirst(linkedlist &list)
{
        address nodeHapus;
        if (!isEmpty(list)==false)
        {
            nodeHapus = list.first;
            list.first = list.first->next;
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        }
        else
        {
            cout << "List kosong" << endl;
        }
}

void delLast(linkedlist &list)
{
    address nodeHapus, nodePrev;
    if (!isEmpty(list)==false)
    {
        nodeHapus = list.first;
        if (nodeHapus->next == Nil)
        {
            list.first->next = Nil;
            dealokasi(nodeHapus);
        }
        else
        {
            while (nodeHapus->next != Nil)
            {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    }
    else
    {
        cout << "List kosong" << endl;
    }
}

void delAfter(linkedlist &list, address nodeHapus, address nodePrev)
{
    if (isEmpty(list) == true)
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        if (nodePrev != Nil && nodePrev->next != Nil)
        {
        nodeHapus = nodePrev->next;
        nodePrev->next = nodeHapus->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
        }
        else
        {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

void printList(linkedlist list)
{
    if (isEmpty(list) == true)
    {
        cout << "List kosong!" << endl;
    }
    else
    {
        address nodeBantu = list.first;
        while (nodeBantu != Nil)
        {
            cout << "Nama: " << nodeBantu->isidata.nama << ", NIM: " << nodeBantu->isidata.nim << ", Usia: " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

int nbList(linkedlist list)
{
    int count = 0;
    address nodeBantu = list.first;
    while (nodeBantu != Nil)
    {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

void deletelist(linkedlist &list)
{
    address nodeBantu, nodeHapus;
    nodeBantu = list.first;
    while (nodeBantu != Nil)
    {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    list.first = Nil;
    cout << "List sudah terhapus." << endl;
}
```
Berisi implementasi fungsi untuk menambah, menghapus, menampilkan, menghitung, dan memeriksa data dalam linked list.

## main.cpp

```C++
#include <iostream>
#include "list.h"
using namespace std;

int main()
{
    linkedlist list;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(list);

    nodeA = alokasi("Dhimas", "001", 20);
    nodeB = alokasi("Budi", "002", 21);
    nodeC = alokasi("Andi", "003", 22);
    nodeD = alokasi("Caca", "004", 23);
    nodeE = alokasi("Dewi", "005", 24);
}

#endif
```

Merupakan program utama yang membuat linked list kosong dan mengalokasikan lima node berisi data mahasiswa.

## Unguided

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h”

## Singilylist.h

```C++

#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#define Nil NULL

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif

```
Berisi deklarasi struktur data Singly Linked List serta fungsi-fungsi yang digunakan untuk mengelola data

## Singlylist.cpp

```C++

#include <iostream>
#include <cstdlib>
#include "Singlylist.h"

using namespace std;

void CreateList(List &L) {
    L.First = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void printInfo(List L) {
    address P = L.First;

    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }

    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}

```
Berisi implementasi fungsi untuk membuat list, mengalokasikan dan membebaskan memori, menambahkan elemen di awal list, serta menampilkan data.

## main.cpp

```C++
#include <iostream>
#include "Singlylist.h"

using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5;

    CreateList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);

    return 0;
}

```
Berfungsi sebagai program utama untuk membuat list, memasukkan lima data menggunakan insertFirst(), dan menampilkan seluruh data menggunakan printInfo().

### Output Unguided 1 :

##### Output 1

![Screenshot Output Unguided](https://github.com/imrtn/Modul-4-Struktur-Data/blob/5d03c4b46ee771f35290ee16addac444a01ee30e/Modul%204/Output/main.cpp.png)

## Kesimpulan

Berdasarkan Modul 4, Singly Linked List merupakan struktur data yang menghubungkan setiap node menggunakan pointer next. Melalui praktikum ini, dapat dipahami cara membuat list, menambahkan data menggunakan insertFirst(), serta menampilkan data menggunakan printInfo(). Penyisipan data dilakukan dari awal list sehingga urutan data yang ditampilkan menjadi terbalik dari urutan pemasukan.

## Referensi

[1] Triase. (2020). Diktat Edisi Revisi: Struktur Data. Medan: Universitas Islam Negeri Sumatera Utara Medan.

[2] Indahyati, U., & Yunianita, R. (2020). Buku Ajar Algoritma dan Pemrograman dalam Bahasa C++. Sidoarjo: Umsida Press. https://doi.org/10.21070/2020/978-623-6833-67-4
