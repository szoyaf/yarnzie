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
```bash flutter create yarnzie
```
- Buka virtual machine (VM) di Android Studio dan jalankan perintah berikut:
```bash flutter run
```
- Modifikasi main.dart untuk mengonfigurasi tata letak aplikasi Yarnzie.
- Halaman beranda (home) dibuat di file menu.dart, berisi dua kelas stateless widget untuk komponen layar utama dan tombol.