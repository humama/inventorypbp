<details>
    <summary>Tugas 6</summary>
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
