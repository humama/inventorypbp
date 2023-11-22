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

- Buat dua direktori bernama screens dan widgets di dalam direktori lib
- Buat file baru bernama `left_drawer.dart` dan `inventory_card.dart` di direktori widgets
- Pindahkan _class_ InventoryItem dan InventoryCard dari `menu.dart` ke `inventory_card.dart` dan _import_ `inventory_card.dart` pada file `menu.dart` 
- Pindahkan file `menu.dart` ke dalam direktori screens
- Isi `left_drawer.dart` dengan kode berikut.
<pre>
import 'package:flutter/material.dart';
import 'package:inventorypbp/screens/menu.dart';
import 'package:inventorypbp/screens/inventorylist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'Inventory PBP',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text("Catat seluruh keperluan belanjamu di sini!",
                      textAlign: TextAlign.center,
                      style: TextStyle(
                        fontSize: 15,
                        color: Colors.white,
                        fontWeight: FontWeight.normal,
                      ),
                    ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Item'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => const InventoryFormPage(),
                  ));
            },
          ),
        ],
      ),
    );
  }
}
</pre>
- Isi `inventorylist_form.dart` dengan kode berikut.
<pre>
import 'package:flutter/material.dart';
import 'package:inventorypbp/widgets/left_drawer.dart';

class InventoryFormPage extends StatefulWidget {
    const InventoryFormPage({super.key});

    @override
    State<InventoryFormPage> createState() => _InventoryFormPageState();
}

class _InventoryFormPageState extends State<InventoryFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";
    @override
    Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: const Center(
              child: Text(
                'Form Tambah Item',
              ),
            ),
            backgroundColor: Colors.indigo,
            foregroundColor: Colors.white,
          ),
          drawer: const LeftDrawer(),
          body: Form(
            key: _formKey,
            child: SingleChildScrollView(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Nama Item",
                        labelText: "Nama Item",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _name = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Nama tidak boleh kosong!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Jumlah",
                        labelText: "Jumlah",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _amount = int.parse(value!);
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Jumlah tidak boleh kosong!";
                        }
                        if (int.tryParse(value) == null) {
                          return "Jumlah harus berupa angka!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Deskripsi",
                        labelText: "Deskripsi",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _description = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Deskripsi tidak boleh kosong!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: Row(
                      mainAxisAlignment: MainAxisAlignment.center,
                      children: [
                        Padding(
                          padding: const EdgeInsets.all(8.0),
                          child: Align(
                            alignment: Alignment.bottomCenter,
                            child: Padding(
                              padding: const EdgeInsets.all(8.0),
                              child: ElevatedButton(
                                style: ButtonStyle(
                                  backgroundColor:
                                      MaterialStateProperty.all(Colors.indigo),
                                ),
                                onPressed: () {
                                  if (_formKey.currentState!.validate()) {
                                    showDialog(
                                      context: context,
                                      builder: (context) {
                                        return AlertDialog(
                                          title: const Text('Item berhasil tersimpan'),
                                          content: SingleChildScrollView(
                                            child: Column(
                                              crossAxisAlignment:
                                                  CrossAxisAlignment.start,
                                              children: [
                                                Text('Nama: $_name'),
                                                Text('Jumlah: $_amount'),
                                                Text('Deskripsi: $_description'),
                                              ],
                                            ),
                                          ),
                                          actions: [
                                            TextButton(
                                              child: const Text('OK'),
                                              onPressed: () {
                                                Navigator.pop(context);
                                              },
                                            ),
                                          ],
                                        );
                                      },
                                    );
                                  _formKey.currentState!.reset();
                                  }
                                },
                                child: const Text(
                                  "Save",
                                  style: TextStyle(color: Colors.white),
                                ),
                              ),
                            ),
                          ),
                        ),
                        Padding(
                          padding: const EdgeInsets.all(8.0),
                          child: Align(
                            alignment: Alignment.bottomCenter,
                            child: Padding(
                              padding: const EdgeInsets.all(8.0),
                              child: ElevatedButton(
                                style: ButtonStyle(
                                  backgroundColor:
                                      MaterialStateProperty.all(Colors.indigo),
                                ),
                                onPressed: (){
                                  Navigator.pop(context);
                                },
                                child: const Text(
                                  "Back",
                                  style: TextStyle(color: Colors.white),
                                ),
                              )
                            )
                          )
                        )
                      ]
                    )
                  ),
                ]
              )
            ),
          ),
        );
    }
}
</pre>
- Tambahkan fungsi pada `inventory_card.dart` sehingga ketika penguna menggunakan tombol Tambah Item, pengguna akan dialihkan ke halaman Tambah Item.
<pre>
          if (item.name == "Tambah Item") {
            Navigator.push(
              context,
              MaterialPageRoute(
                builder: (context) => const InventoryFormPage()
              ),
            );
          }
</pre>
- Tambahkan drawer pada file `menu.dart` dan `inventorylist_form.dart` dengan menambahkan line 
<pre>drawer: const LeftDrawer(),</pre>
di widget build sebelum body

- Tambahkan juga tombol _Back_ pada file `inventorylist_form.dart` agar pengguna bisa mudah kembali ke halaman utama
</details>
<details>
  <summary>Tugas 9</summary>

1. Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON? 

Ya, bisa. Dalam beberapa kasus, terutama untuk proyek kecil atau ketika struktur data tidak kompleks, kita dapat menggunakan tipe data dinamis (seperti Map<String, dynamic>) untuk mengambil dan memproses data JSON tanpa membuat model terlebih dahulu. Ini dapat mempermudah implementasi, tetapi memiliki kelemahan karena kehilangan keamanan tipe yang dimiliki model. Penggunaan model membantu memastikan bahwa data yang diambil sesuai dengan ekspektasi aplikasi.

2. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.

CookieRequest pada umumnya tidak merupakan bagian dari Flutter sendiri, namun, mungkin Anda berbicara tentang http.Cookie di Flutter yang digunakan untuk bekerja dengan cookie dalam permintaan HTTP. Jika begitu, instance http.Cookie dibagikan ke semua komponen dalam aplikasi untuk mempertahankan sesi atau status otentikasi antar permintaan HTTP. Ini penting untuk menjaga keadaan otentikasi dan memastikan bahwa permintaan selanjutnya dapat diotentikasi dengan benar.

3. Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.

Mekanisme umum melibatkan penggunaan paket HTTP seperti http untuk membuat permintaan ke API atau sumber data JSON. Data JSON kemudian diuraikan ke dalam model Dart menggunakan konversi JSON yang otomatis atau manual. Setelah itu, model dapat digunakan dalam struktur widget untuk membangun antarmuka pengguna.

4. Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

Mekanisme otentikasi umumnya melibatkan pengiriman informasi otentikasi (seperti nama pengguna dan kata sandi) dari Flutter ke backend Django melalui permintaan HTTP. Django akan memverifikasi informasi tersebut, dan jika valid, akan menghasilkan token akses atau memberikan sesi otentikasi. Token atau sesi ini kemudian dapat digunakan dalam permintaan berikutnya untuk mengotentikasi pengguna dan memberikan akses ke sumber daya terproteksi.

5. Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.

Container: widget ini menyediakan 'kanvas' untuk programmer membuat sebuah aplikasi Flutter.
Column: widget ini menampilkan child dalam format vertikal.
Text: widget ini menampilkan string dalam satu baris.
AppBar: widget ini sama seperti toolbar pada aplikasi lain yang sering kita gunakan, yang berguna untuk menampilkan judul dan fitur-fitur utama pada aplikasi.
Scaffold: Digunakan sebagai kerangka dasar untuk sebagian besar aplikasi Flutter.
Row: widget ini menampilkan child dalam format horizontal.
Material: Digunakan sebagai container untuk mengimplementasikan desain Material Design dalam aplikasi Flutter.
ListView: Menampilkan daftar widget dalam format scrollable. Digunakan ketika daftar item mungkin melebihi ruang layar yang tersedia.
Padding: Menambahkan ruang kosong atau margin di sekitar widget child di dalamnya. Digunakan untuk memberikan ruang antara elemen-elemen dalam tata letak.
GridView: Menampilkan daftar widget dalam format grid. Berguna ketika item perlu diatur dalam grid dengan beberapa kolom.

6. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).


</details>