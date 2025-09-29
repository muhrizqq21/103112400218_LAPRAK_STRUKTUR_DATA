# <h1 align = "center" > Laporan Praktikum Struktur Data Modul 1 <br> Pengenalan C++ </h1>
<p align = "center" > MUHAMMAD RIZQI AR RAFI - 103112400218 </p>

## Dasar Teori

C++ bahasa pemrograman yang dikembangkan oleh Bjarne Stroustrup merupakan pengembangan dari bahasa C. Bahasa C++ banyak digunakan karena bahasa ini cukup efisien dan fleksibel, juga mendukung pemrograman yang berorientasi objek. Setiap program yang menggunakan C++ biasanya memiliki fungsi utama yaitu main() yang menjadi landasan program, dan kemudian diawali dengan perintah #include <iostream> untuk mengaktifkan fasilitas input-output. C++ juga memiliki variabel untuk menyimpan data seperti int, float, string, serta bool untuk nilai logika.  

## GUIDED

### Contoh 1

```cpp
#include <iostream>
#include <string>
using namespace std;

// Definisi struct
struct Mahasiswa {
    string nama;
    string nim;
    float ipk;
};

int main() {

    Mahasiswa mhs1;

    cout << "Masukkan Nama Mahasiswa: ";
    getline(cin, mhs1.nama);
    // cin >> mhs1.nama;
    cout << "Masukkan NIM Mahasiswa : ";
    cin >> mhs1.nim;
    cout << "Masukkan IPK Mahasiswa : ";
    cin >> mhs1.ipk;

    cout << "\n=== Data Mahasiswa ===" << endl;
    cout << "Nama : " << mhs1.nama << endl;
    cout << "NIM  : " << mhs1.nim << endl;
    cout << "IPK  : " << mhs1.ipk << endl;

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="Screenshot 2025-09-29 171220" src="https://github.com/user-attachments/assets/77358a0c-8406-4bab-9f5b-cc9c327840e5" />

### Contoh 2

```cpp
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/661ed80a-cebe-40ae-93f5-e0659e932009" />

### Contoh 3

```cpp
#include <iostream>
using namespace std;
// int main()
// {
//     double tot_pembelian, diskon;
//     cout << "total pembelian: Rp";
//     cin >> tot_pembelian;
//     diskon = 0;
//     if (tot_pembelian >= 100000)
//         diskon = 0.05 * tot_pembelian;
//     cout << "besar diskon = Rp" << diskon;
// }

// int main()
// {
//     double tot_pembelian, diskon;
//     cout << "total pembelian: Rp";
//     cin >> tot_pembelian;
//     diskon = 0;
//     if (tot_pembelian >= 100000)
//         diskon = 0.05 * tot_pembelian;
//     else
//         diskon = 0;
//     cout << "besar diskon = Rp" << diskon;
// }

int main()
{
    int kode_hari;
    cout << "Menentukan hari kerja/libur\n"<<endl;
    cout << "1=Senin 3=Rabu 5=Jumat 7=Minggu "<<endl;
    cout << "2=Selasa 4=Kamis 6=Sabtu "<<endl;
    cin >> kode_hari;
    switch (kode_hari)
    {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout<<"Hari Kerja";
        break;
    case 6:
    case 7:
        cout<<"Hari Libur";
        break;
    default:
        cout<<"Kode masukan salah!!!";
    }
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/fc5509fe-c9d2-4cce-b2cc-9d032cec36de" />

### Contoh 4

```cpp
#include <iostream>
using namespace std;
// int main()
// {
//     int jum;
//     cout << "jumlah perulangan: ";
//     cin >> jum;
//     for (int i = 0; i < jum; i++)
//     {
//         cout << "saya sahroni\n";
//     }
//     return 1;
// }

// while
int main()
{
    int i = 1;
    int jum;
    cin >> jum;
    do
    {
        cout << "bahlil ke-" << (i + 1) << endl;
        i++;
    } while (i < jum);
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/8de722f0-2869-496a-8a54-d0ceddc73266" />

### Contoh 5

```cpp
#include <iostream>
using namespace std;

// Prosedur: hanya menampilkan hasil, tidak mengembalikan nilai
void tampilkanHasil(double p, double l)
{
    cout << "\n=== Hasil Perhitungan ===" << endl;
    cout << "Panjang : " << p << endl;
    cout << "Lebar   : " << l << endl;
    cout << "Luas    : " << p * l << endl;
    cout << "Keliling: " << 2 * (p + l) << endl;
}

// Fungsi: mengembalikan nilai luas
double hitungLuas(double p, double l)
{
    return p * l;
}

// Fungsi: mengembalikan nilai keliling
double hitungKeliling(double p, double l)
{
    return 2 * (p + l);
}

int main()
{
    double panjang, lebar;

    cout << "Masukkan panjang: ";
    cin >> panjang;
    cout << "Masukkan lebar  : ";
    cin >> lebar;

    // Panggil fungsi
    double luas = hitungLuas(panjang, lebar);
    double keliling = hitungKeliling(panjang, lebar);

    cout << "\nDihitung dengan fungsi:" << endl;
    cout << "Luas      = " << luas << endl;
    cout << "Keliling  = " << keliling << endl;

    // Panggil prosedur
    tampilkanHasil(panjang, lebar);

    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/ac87b888-891c-463e-bcf8-eade2178e5df" />

### Contoh 6

```cpp
#include <iostream>
using namespace std;
int main()
{
    string ch;
    cout << "Masukkan sebuah karakter: ";
    // cin >> ch;
    ch = getchar();  //Menggunakan getchar() untuk membaca satu karakter
    cout << "Karakter yang Anda masukkan adalah: " << ch << endl;
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/38a70760-2ac3-425e-b2a3-55dacd24b920" />

## UNGUIDED

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan bertipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```cpp
#include <iostream>
using namespace std;

int main() {
    float bil1, bil2;
    cin >> bil1 >> bil2;
    cout << "Hasil Penjumlahan adalah: " << bil1 + bil2 << endl;
    cout << "Hasil Pengurangan adalah: " << bil1 - bil2 << endl;
    cout << "Hasil Perkalian adalah: " << bil1 * bil2 << endl;
    cout << "Hasil Pembagian adalah: " << bil1 / bil2 << endl;
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0da8a11b-4170-4d14-9614-708e65e1cba4" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas merupakan program kalkulator sederhana yang meminta input dua bilangan. Setelah diinputkan dua bilangan, program akan langsung menghitung dan menampilkan output hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan yang sudah diinput tadi. Seperti gambar di atas pada saat diinputkan 6 dan 3 maka akan mnedapatkan output hasil penjumlahannya yaitu 9, kemudian hasil pengurangannya yaitu 3, kemudian hasil perkaliannya yaitu 18, dan yang terakhir hasil pembagiannya yaitu 2.  </p>

### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100.

```cpp
#include <iostream>
using namespace std;

const string satu[] = {"nol", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan", "sepuluh", "sebelas", "dua belas", "tiga belas", "empat belas", "lima belas", "enam belas", "tujuh belas", "delapan belas", "sembilan belas"};
const string puluh[] = {"_", "_", "dua puluh", "tiga puluh", "empat puluh", "lima puluh", "enam puluh", "tujuh puluh", "delapan puluh", "sembilan puluh", "seratus"};

string BilangankeTeks(int bilangan) {
    if (bilangan < 20) {
        return satu[bilangan];
    }

    if (bilangan < 100) {
        int satuan = bilangan % 10;
        int puluhan = bilangan / 10;
        return puluh[puluhan] + " " + satu[satuan];
    }
    
    if (bilangan == 100) {
        return "seratus";
    }
    return 0;
} 

int main() {
    int bilangan; 
    cin >> bilangan;
    string teks = BilangankeTeks(bilangan);
    cout << bilangan << " : " << teks << endl;
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/cfd03220-c632-418f-98f1-bd9309d4a46f" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Program di atas berfungsi untuk mengubah bilangan menjadi format string atau tulisan. Program ini menggunakan array string yang dibagi menjadi dua array, satu untuk menyimpan penamaan bilangan dalam satuan, satu lagi untuk penamaan bilangan dalam puluhan, kemudian program ini juga menggunakan logika if-else untuk membantu menentukan terjemahan bilangan. Seperti gambar di atas pada saat diinputkan 79 maka akan menghasilkan output tujuh puluh sembilan. </p>

### Soal 3

Buatlah program yang dapat memberikan input dan output sbb.
> <img width="183" height="175" alt="image" src="https://github.com/user-attachments/assets/19b26e9f-2fa1-4406-8aa5-006bbb76231f" />

```cpp
#include <iostream>
using namespace std;

int main() {
    int bilangan;
    cin >> bilangan;

    for (int i = bilangan; i > 0; i--) {
        for (int spasi = 0; spasi < bilangan - i; spasi++) {
            cout << " ";
        }
        
        for (int j = i; j > 0; j--) {
            cout << j;
        }

        cout << "*";

        for (int k = 1; k <= i; k++) {
            cout << k;
        }

        cout << endl;
    }

    for (int spasi = 0; spasi < bilangan; spasi++) {
            cout << " ";
        }

    cout << "*" << endl;
    return 0;
}
```
> Output Program
> <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/54ebefbb-c90c-4784-b3b5-8cc986665eca" />

<p> <strong> Deskripsi Program </strong> </p>
<p> Proggram di atas adalah program yang berfungsi untuk menghasilkan output pola numerik segitiga simetris terbalik berdasarkan sebuah bilangan. Logika utamanya adalah nested loops atau perulangan bersarang. Seperti gambar di atas pada saat diinputkan 3 maka program akan menghasilkan output yaitu segitiga simetris terbalik dengan pola numerik. </p>

## Referensi

1. Dewi, L. J. E. (2010). Media Pembelajaran Bahasa Pemrograman C++. Jurnal Pendidikan Teknologi dan Kejuruan, 7(1).
2. Aulia, F. (2024). Mengenal bahasa pemrograman pada algoritma pemrograman. Journal Of Informatics And Busisnes, 1(4), 223-228.
3. Ramadhana, I., & Sujatmiko, B. (2018). Pengembangan Aplikasi Kamus Bahasa Pemrograman C++ Berbasis Android Untuk Meningkatkan Kompetensi Kognitif Mata Kuliah Struktur Data. IT-Edu: Jurnal Information Technology and Education, 3(1).

