Nama  : Shaney Zoya Fiandi
NPM   : 2306215923
Kelas : PBP A

# Tugas 8
## Penggunaan const di Flutter
_const_ di Flutter berfungsi untuk membuat objek atau widget menjadi konstan atau tidak berubah (immutable). Ketika objek atau widget diberi atribut _const_, Flutter mengerti bahwa objek tersebut akan tetap sama selama aplikasi berjalan, sehingga objek tersebut cukup dibuat sekali. Hal ini membantu menghemat memori dan meningkatkan performa aplikasi karena Flutter tidak perlu membuat ulang objek yang bersifat tetap.

### Keuntungan menggunakan _const_:
- **Peningkatan Performa**: Mengurangi jumlah objek yang perlu diperbarui, mempercepat rendering, dan menghemat penggunaan memori.
- **Optimasi Hot Reload**: Objek _const_ tidak perlu di-refresh saat melakukan hot reload, yang mempercepat proses pengembangan.

### Penggunaan _const_:
- Gunakan _const_ jika nilai atau widget tidak akan berubah, seperti pada warna, padding, atau teks statis.

### Kapan tidak menggunakan _const_:

- Hindari _const_ jika objek bergantung pada data yang dapat berubah, seperti nilai dari pengguna atau state dinamis.

## Widget Column dan Row di Flutter
**Column**: Widget ini digunakan untuk menyusun elemen secara vertikal, misalnya untuk menumpuk elemen dalam form atau daftar item.

**Row**: Widget ini digunakan untuk menyusun elemen secara horizontal, contohnya untuk ikon yang diletakkan bersama teks atau tombol navigasi.

## Halaman Form di Yarnzie
Dalam implementasi aplikasi Yarnzie, saya menggunakan dua jenis form field:

- **TextFormField**: Digunakan untuk menerima input berupa teks. Form ini dilengkapi dengan validasi untuk memastikan input tidak kosong. Untuk input angka, saya menambahkan keyboardType: TextInputType.number agar hanya angka yang dapat diinput, serta melakukan validasi untuk angka negatif.

- **DropdownButtonFormField**: Form field ini dibuat berdasarkan enum yang dideklarasikan di luar class. Dengan dropdown ini, pengguna dapat memilih salah satu opsi. Karena terdapat default value, maka form ini tidak memerlukan validator untuk memastikan nilai selalu terisi.

## Pengaturan Tema di Flutter
Flutter memungkinkan pengaturan tema untuk menjaga konsistensi desain. Pada widget MaterialApp, saya mengatur tema dengan properti theme, lalu memasukkan konfigurasi tema menggunakan ThemeData(). Contohnya:

```dart
theme: ThemeData(
    colorScheme: ColorScheme.fromSwatch(
        primarySwatch: Colors.pink,
    ).copyWith(
        primary: Colors.pink.shade200,
        secondary: Colors.pink.shade200,
    ),
    useMaterial3: true,
),
```
Dalam pengaturan ini, warna utama adalah pink, dan warna sekunder adalah pink muda.

## Navigasi di Flutter
Di Flutter, saya menggunakan Navigator untuk mengatur navigasi antar halaman. Saya juga membuat sidebar untuk memudahkan pengguna dalam berpindah halaman. Sidebar tersebut menggunakan class Navigator untuk mengarahkan pengguna ke halaman lain. Contoh implementasinya:

```dart
ListTile(
  leading: const Icon(Icons.mood),
  title: const Text('Tambah Item'),
  onTap: () {
      Navigator.pushReplacement(
        context,
        MaterialPageRoute(
          builder: (context) => const ProductEntryFormPage(),
        ),
      );
  },
)
```
Dengan kode di atas, saat pengguna mengetuk tombol, aplikasi akan berpindah ke halaman ProductEntryFormPage.

# Tugas 7
## Perbedaan Stateless Widget dan Stateful Widget
Stateless widget adalah widget yang tidak bisa mengubah state-nya. Karena sifatnya yang immutable dan lebih ringan, stateless widget cocok untuk elemen-elemen dengan tampilan statis. Sebaliknya, stateful widget memungkinkan perubahan state, sehingga lebih tepat untuk widget yang dinamis atau interaktif karena bersifat mutable, memudahkan pembaruan tampilan.

## Widget yang Digunakan di Yarnzie
Yarnzie menggunakan stateless widget, karena kebutuhan aplikasi ini masih bersifat statis. Dengan menggunakan stateless widget, aplikasi menjadi lebih ringan dan efisien.

## Fungsi setState()
Pada stateful widget, fungsi setState() memberitahu Flutter bahwa ada perubahan state yang perlu diperbarui di UI. Ketika setState() dipanggil, Flutter akan menjalankan ulang metode build untuk memperbarui tampilan sesuai dengan state terbaru.

## Perbedaan const dan final
const: Mendeklarasikan variabel dengan nilai yang konstan dan ditentukan saat kompilasi. Objek const tidak bisa diubah nilainya setelah kompilasi dan bersifat konstan pada waktu kompilasi.
final: Mendeklarasikan variabel yang hanya dapat diinisialisasi satu kali, namun nilainya dapat ditentukan pada waktu runtime. Jadi, variabel final bersifat konstan pada waktu runtime.

Contoh:
```dart const int myConst = 10;
final DateTime myFinalDate = DateTime.now();
```

- myConst adalah konstanta yang nilainya 10 dan tidak bisa diubah.
- myFinalDate hanya dapat diinisialisasi sekali, tetapi nilainya baru ditentukan saat runtime.

## Implementasi Tugas 7
- Inisialisasi proyek Flutter:
```bash flutter create yarnzie```
- Buka virtual machine (VM) di Android Studio dan jalankan perintah berikut:
```bash flutter run```
- Modifikasi main.dart untuk mengonfigurasi tata letak aplikasi Yarnzie.
- Halaman beranda (home) dibuat di file menu.dart, berisi dua kelas stateless widget untuk komponen layar utama dan tombol.