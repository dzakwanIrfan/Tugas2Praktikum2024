# Penjelasan Passing Data di Flutter

## Deskripsi
Aplikasi ini menampilkan proses **passing data** dari satu form menuju halaman tampilan menggunakan Flutter. Pengguna memasukkan informasi berupa **nama**, **NIM**, dan **tahun lahir** pada form input, dan setelah menekan tombol **Simpan**, data tersebut dikirimkan ke halaman lain yang menampilkan informasi tersebut, termasuk usia pengguna yang dihitung dari tahun lahir.

## Alur Kerja

### 1. **Pengumpulan Data di Form Input**
Pada file `form_data.dart`, kita menyediakan beberapa `TextField` untuk mengumpulkan input dari pengguna, yaitu:
- **Nama**
- **NIM**
- **Tahun Lahir**

Masing-masing `TextField` menggunakan `TextEditingController` untuk menangani input pengguna, yang kemudian akan disimpan dalam variabel controller (_namaController_, _nimController_, _tahunController_).

```dart
final _namaController = TextEditingController();
final _nimController = TextEditingController();
final _tahunController = TextEditingController();
```

### 2. **Menangani Aksi Tombol Simpan**
Ketika tombol **Simpan** ditekan, data yang dimasukkan diambil dari controller menggunakan `text` untuk nama dan NIM, serta diubah menjadi `int` untuk tahun lahir. Setelah itu, kita menggunakan `Navigator.of(context).push()` untuk mengarahkan pengguna ke halaman baru (`TampilData`) sambil mengoper data yang telah dimasukkan.

```dart
_tombolSimpan() {
  return ElevatedButton(
      onPressed: () {
        String nama = _namaController.text;
        String nim = _nimController.text;
        int tahun = int.parse(_tahunController.text);
        Navigator.of(context).push(MaterialPageRoute(
            builder: (context) =>
                TampilData(nama: nama, nim: nim, tahun: tahun)));
      },
      child: const Text('Simpan'));
}
```

### 3. **Navigasi ke Halaman TampilData**
Pada file `tampil_data.dart`, data yang dikirimkan dari halaman form diterima melalui **constructor**. `TampilData` adalah widget yang menerima parameter `nama`, `nim`, dan `tahun` dari halaman form dan menampilkannya pada layar.

```dart
class TampilData extends StatelessWidget {
  final String nama;
  final String nim;
  final int tahun;

  const TampilData({
    Key? key,
    required this.nama,
    required this.nim,
    required this.tahun,
  }) : super(key: key);
}
```

### 4. **Menghitung Usia dan Menampilkan Data**
Di dalam halaman `TampilData`, aplikasi menghitung usia pengguna berdasarkan tahun lahir dengan mengurangi tahun saat ini dengan tahun lahir. Hasilnya, bersama dengan nama dan NIM, ditampilkan menggunakan widget `Text`.

```dart
@override
Widget build(BuildContext context) {
  final int umur = DateTime.now().year - tahun;
  return Scaffold(
    appBar: AppBar(
      title: const Text("Perkenalan"),
    ),
    body: Container(
      margin: const EdgeInsets.all(10),
      child: Column(
        children: [
          Text("Nama saya $nama, NIM $nim, dan umur saya adalah $umur tahun"),
        ],
      ),
    ),
  );
}
```

### 5. **Hasil Akhir**
Setelah pengguna menekan tombol **Simpan** pada halaman form, mereka akan diarahkan ke halaman baru yang menampilkan informasi yang telah dimasukkan:
- Nama
- NIM
- Usia (dihitung dari tahun lahir)

## Struktur Proyek

```
lib/
│
├── ui/
│   ├── form_data.dart      # Form input untuk mengumpulkan data dari pengguna
│   └── tampil_data.dart    # Halaman untuk menampilkan data yang telah diinput
│
└── main.dart               # File utama yang menjalankan aplikasi Flutter
```

## Dependencies
Tambahkan dependency berikut ke dalam `pubspec.yaml` untuk styling font futuristik:

```yaml
dependencies:
  flutter:
    sdk: flutter
  google_fonts: ^5.0.0
```

## Cara Menjalankan Aplikasi

1. Clone repository ini ke mesin lokal.
2. Install dependencies dengan menjalankan perintah:
   ```bash
   flutter pub get
   ```
3. Jalankan aplikasi dengan:
   ```bash
   flutter run
   ```

## Screen Record
https://github.com/user-attachments/assets/472bd078-d041-460c-9c22-47188e0c5abf

