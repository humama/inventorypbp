<details>
  <summary>Tugas 7</summary>
1. Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?

Stateless Widget:

Stateless widget adalah widget yang tidak memiliki keadaan internal (state).
Setelah dibangun, widget tersebut tidak dapat diubah atau diperbarui. Oleh karena itu, widget ini cocok untuk elemen UI yang tidak perlu berubah.
Stateless widget hanya memiliki metode build() yang digunakan untuk merender elemen UI yang statis.
Stateful Widget:

Stateful widget adalah widget yang memiliki keadaan (state) yang dapat berubah selama siklus hidupnya.
Widget ini digunakan ketika elemen UI memerlukan pembaruan berdasarkan tindakan pengguna atau perubahan data.
Stateful widget memiliki dua kelas terpisah: kelas widget itu sendiri (yang bersifat immutable) dan kelas "state" terkait yang mengelola keadaan widget dan dapat diubah selama proses rendering.

2. Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.

- Container: widget ini menyediakan 'kanvas' untuk programmer membuat sebuah aplikasi Flutter.
- Column: widget ini menampilkan child dalam format vertikal.
- Text: widget ini menampilkan string dalam satu baris.
- AppBar: widget ini sama seperti toolbar pada aplikasi lain yang sering kita gunakan, yang berguna untuk menampilkan judul dan fitur-fitur utama pada aplikasi.

3. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial)

- Buka cmd di direktori yg ingin dibuat aplikasi flutternya dan jalankan command `flutter create inventorypbp` untuk membuat projek baru
- Jalankan `cd inventorypbp`
- Buat file baru bernama `menu.dart` dalam direktori lib dan tambahkan kode 
    <pre>import 'package:flutter/material.dart';</pre>
- Tambahkan kode ini di file `main.dart` agar `main.dart` bisa mengakses `menu.dart`
    <pre>import 'package:inventorypbp/menu.dart';</pre>
- Pada file `main.dart` Hapus kelas `_MyHomePageState` dan pindahkan kelas `MyHomePageState` ke file `menu.dart`.
- Ubah baris kode `home: const MyHomePage(title: 'Flutter Demo Home Page'),` pada file `main.dart` menjadi `home: MyHomePage(),`.
- Ubah baris kode `colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),` pada file `main.dart` menjadi `colorScheme: ColorScheme.fromSeed(seedColor: Colors.green),`.
- Pada file `menu.dart`, ubah sifat kelas `MyHomePage` dari *`stateful`* menjadi *`stateless`* dan ubah baris kode `MyHomePage({Key? key}) : super(key: key);` menjadi `MyHomePage({Key? key}) : super(key: key);`.
- Hapus semua kode dari baris `final String title;` sampai akhir kelas `MyHomePage` pada `menu.dart`.
- Tambahkan kelas baru bernama `InventoryItem` yang memiliki properti *`name`*, *`icon`*, dan *`color`* dengan *constructor* `InventoryItem(this.name, this.icon, this.color);`.
        <pre>
            class InventoryItem {
                final String name;
                final IconData icon;
                final MaterialColor color;

                InventoryItem(this.name, this.icon, this.color);
            }
    </pre>
- Tambahkan *widget* baru bernama `InventoryCard` bersifat *stateless* dengan properti *`item`* bertipe `InventoryItem` dengan *contructor* `const InventoryCard(this.item, {super.key});` dan fungsi `build`.
        <pre>
  class InventoryCard extends StatelessWidget {
  final InventoryItem item;

  const InventoryCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
    </pre>
- Tambahkan *list* baru dalam kelas `MyHomePage` bernama `items` yang berguna untuk menyimpan tombol-tombol yang akan ditampilkan.
        <pre>
            final List<InventoryItem> items = [
                InventoryItem("Lihat Item", Icons.checklist, Colors.red),
                InventoryItem("Tambah Item", Icons.add_shopping_cart, Colors.amber),
                InventoryItem("Logout", Icons.logout, Colors.lightBlue),
            ];
        </pre>
- Tambahkan fungsi baru dalam kelas `MyHomePage` bernama `build` seperti kode berikut.
    <pre>
      @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Inventory PBP',
          style: TextStyle(color: Colors.white),
        ),
        elevation: 5,
        backgroundColor: Colors.indigo,
        shadowColor: Colors.black,
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'Inventory',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((InventoryItem item) {
                  // Iterasi untuk setiap item
                  return InventoryCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
    </pre>

</details>
<details>
  <summary>Tugas 8</summary>
1. Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!

Navigator.push():

Digunakan untuk menambahkan route baru ke dalam tumpukan (stack) route navigator.
Memberikan kemampuan pengguna untuk kembali ke halaman sebelumnya dengan tombol "Back".
Tetap menyimpan halaman sebelumnya di dalam tumpukan route.
Contoh:

<pre>
// Navigasi ke halaman baru
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);
</pre>
Navigator.pushReplacement():

Menggantikan halaman saat ini dengan halaman baru.
Tidak menyimpan halaman sebelumnya di dalam tumpukan route.
Berguna ketika Anda ingin menggantikan halaman login dengan halaman beranda setelah login berhasil.
Contoh:

<pre>
// Navigasi dan menggantikan halaman saat ini
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => HomeScreen()),
);
</pre>
2. Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!

Beberapa layout widgets pada Flutter dan konteks penggunaannya:

Container: Widget yang digunakan untuk mengelompokkan dan mendekorasi widget lainnya. Digunakan untuk mengatur tata letak dan styling.

Row dan Column: Merepresentasikan baris dan kolom, secara berturut-turut, yang memungkinkan pengaturan widget secara horizontal (Row) atau vertikal (Column).

ListView dan GridView: Membungkus kumpulan widget secara berurutan (ListView) atau dalam bentuk grid (GridView).

Stack dan Positioned: Membantu menempatkan widget di atas atau di bawah widget lain, sering digunakan untuk mendekorasi atau menumpuk widget.

Scaffold: Merupakan kerangka utama untuk aplikasi Flutter, menyediakan struktur dasar seperti AppBar, Drawer, dan BottomNavigationBar.

3. Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!

TextFormField, karena TextFormField adalah widget praktis yang nge-wrap sebuah widget TextField di dalam sebuah FormField.

4. Bagaimana penerapan clean architecture pada aplikasi Flutter?
Penerapan Clean Architecture pada Aplikasi Flutter
Clean Architecture pada aplikasi Flutter melibatkan pembagian kode menjadi beberapa lapisan:

Domain Layer: Berisi aturan bisnis dan entitas domain.

Data Layer: Bertanggung jawab untuk berkomunikasi dengan sumber daya eksternal seperti API atau database.

Presentation Layer: Mengatur tampilan dan menerima input pengguna, bertanggung jawab untuk menghubungkan antara domain dan data.

Clean Architecture membantu memisahkan kode menjadi bagian-bagian yang independen dan dapat diuji, memungkinkan fleksibilitas dan perubahan tanpa mempengaruhi bagian lain dari aplikasi. Dengan menggunakan Dependency Injection, misalnya, kita dapat dengan mudah mengganti implementasi data tanpa mengubah kode di lapisan presentasi atau domain.

5. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial)

</details>