Nama  : Shaney Zoya Fiandi
NPM   : 2306215923
Kelas : PBP A

# Tugas 9

## Model untuk Pengambilan atau Pengiriman Data JSON

### Struktur Data yang Terdefinisi
Model membantu mendefinisikan struktur data yang diterima atau dikirim, sehingga data lebih mudah dikelola dan dimanipulasi. Misalnya, sebuah model dapat memiliki properti seperti `id`, `name`, dan `price`, sehingga data dapat diakses dengan cara yang lebih terorganisir, seperti `product.name`.

### Type Safety (Keamanan Tipe Data)
Dengan model, tipe data setiap properti dapat ditentukan. Hal ini mencegah kesalahan runtime akibat tipe data yang tidak sesuai, seperti mencoba melakukan operasi matematika pada data bertipe `string`.

### Kemudahan Parsing
Model mempermudah proses konversi data dari/ke JSON (serialization dan deserialization). Dalam Flutter, biasanya digunakan metode `fromJson` untuk membaca JSON menjadi objek, dan `toJson` untuk mengubah objek kembali ke JSON.

### Apakah Terjadi Error?
Tidak akan terjadi error, tetapi kode akan lebih sulit dikelola tanpa adanya type safety, karena sulit mengetahui data yang masuk atau dikirim.

## Fungsi dari Library `http`
Library `http` dalam Flutter digunakan untuk melakukan permintaan HTTP ke server (API) untuk mengirim atau mengambil data. Pada tugas ini, saya mengimplementasikan:

- **GET** untuk menampilkan daftar produk.
- **POST** untuk menambahkan produk baru.
- **GET dan POST** untuk autentikasi (login dan register).

Permintaan HTTP ini diintegrasikan dengan aplikasi web Django.

## Fungsi dari `CookieRequest`
`CookieRequest` mempermudah aplikasi dalam mengakses cookie. Fungsinya mencakup:

- Menyimpan header, cookie, dan `jsonData` setelah login.
- Mengecek apakah pengguna sedang login.
- Dibagikan ke seluruh aplikasi Flutter untuk memastikan user tetap terautentikasi di setiap halaman.

## Mekanisme Pengiriman Data pada Flutter
1. **Pengguna mengisi data** melalui widget seperti `TextField` atau `Form`, misalnya nama dan deskripsi produk.
2. **Validasi lokal** dilakukan untuk memastikan data tidak kosong atau sesuai format.
3. **Pengiriman data** ke backend menggunakan HTTP (dengan library `http`).
4. **Django menerima data** melalui endpoint POST (misalnya `/create-flutter/`) dan memvalidasi data dengan serializer sebelum menyimpannya ke database.
5. **Pengambilan data** kembali menggunakan GET, data JSON diubah menjadi model Dart (deserialization), lalu ditampilkan dengan widget seperti `ListView`.

## Mekanisme Autentikasi

### Register
1. Pengguna memasukkan nama, email, dan password.
2. Data dikirim dengan HTTP POST ke Django.
3. Django memvalidasi data dengan serializer, lalu menyimpan password yang sudah di-hash.
4. Django mengembalikan respons berhasil atau error ke Flutter.

### Login
1. Pengguna memasukkan email dan password.
2. Data dikirim dengan HTTP POST ke Django.
3. Django memeriksa kecocokan data dengan database.
4. Jika berhasil, Django mengembalikan token autentikasi yang disimpan dalam cookies.

### Logout
1. Pengguna menekan tombol Logout.
2. Flutter mengirim permintaan logout ke Django.
3. Django menghapus session ID user.

## Step by Step Tugas 9

### Pada Django
1. Membuat endpoint untuk Flutter.
2. Membuat app `authentication` dengan perintah:
  ```bash
  py manage.py startapp authentication
  ```
3. Menyambungkan endpoint di views dan urls untuk login, logout, dan register menggunakan library django.contrib.auth.
4. Membuat endpoint POST untuk menambahkan produk, contohnya:
  ```python
  return JsonResponse(
      {
          "status": "success",
          "message": "Product has been created successfully!",
      },
      status=201,
  )
  ```
atau jika gagal:
  ```python
  return JsonResponse(
      {
          "status": False,
          "message": "Failed.",
      },
      status=400,
  )
  ```
5. Menambahkan endpoint GET untuk mengambil produk milik user tertentu dengan memanfaatkan params id.

## Pada Flutter
1. Menambahkan halaman login dan register menggunakan library http dan pbp_django_auth.
2. Menginisiasi CookieRequest() untuk menyimpan cookies user.
3. Membuat model: Product.
4. Mengubah form menjadi POST request yang divalidasi di Django sebelum data disimpan.
5. Melakukan GET request untuk semua produk dan produk milik user tertentu.
6. Menambahkan fitur detail produk, misalnya:
```dart
class DetailProductPage extends StatelessWidget {
  final ProductEntry productEntry;
  const DetailProductPage({
    super.key,
    required this.productEntry
  });

  @override
  Widget build(BuildContext context) {
    // Widget untuk menampilkan detail produk
  }
}
```

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

- **TextFormField**: Digunakan untuk menerima input berupa teks. Form ini dilengkapi dengan validasi untuk memastikan input tidak kosong. Untuk input angka, saya menambahkan productType: TextInputType.number agar hanya angka yang dapat diinput, serta melakukan validasi untuk angka negatif.

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