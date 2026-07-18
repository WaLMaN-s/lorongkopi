# Penjelasan Tampilan Antarmuka — Sistem Informasi Pemesanan Menu Lorong Kopi

Gaya penulisan sudah disesuaikan untuk BAB IV (Implementasi Sistem). Tinggal salin di bawah masing-masing screenshot.

---

## A. Tampilan Pelanggan

### 1. Halaman Scan QR Code Meja
Halaman ini merupakan pintu masuk pelanggan ke dalam sistem. Pelanggan cukup memindai QR Code yang tertempel pada meja menggunakan kamera ponsel, kemudian sistem akan memvalidasi kode meja tersebut ke basis data. Apabila kode meja valid dan berstatus aktif, sistem secara otomatis membuat sesi pemesanan yang terikat pada nomor meja tersebut, sehingga pelanggan dapat langsung memesan tanpa perlu melakukan registrasi maupun login terlebih dahulu.

### 2. Halaman Beranda (Daftar Menu)
Halaman beranda menampilkan seluruh menu yang tersedia di kedai, dilengkapi dengan foto, nama, deskripsi singkat, dan harga. Pelanggan dapat menyaring menu berdasarkan kategori (Coffee, Non Coffee, Tea, dan Snack) serta mencari menu melalui kolom pencarian. Ketika salah satu menu dipilih, sistem menampilkan lembar opsi pemesanan berupa ukuran (Regular/Large), cara penyajian (Dingin/Panas), dan tingkat gula (Normal/Less/No Sugar); khusus menu kopi tanpa gula seperti Espresso dan Americano, opsi gula tidak ditampilkan sesuai pengaturan pada data menu.

### 3. Halaman Keranjang
Halaman keranjang menampilkan rekapitulasi seluruh item yang telah dipilih pelanggan beserta opsi, jumlah, dan subtotal harganya. Pada halaman ini pelanggan dapat menambah atau mengurangi jumlah item, menghapus item yang tidak jadi dipesan, serta melihat total keseluruhan pesanan secara real-time. Tombol Checkout akan mengarahkan pelanggan ke halaman pembayaran apabila keranjang tidak kosong.

### 4. Halaman Checkout
Halaman checkout menampilkan ringkasan akhir pesanan beserta total yang harus dibayar. Pelanggan diminta memilih metode pembayaran yang tersedia, yaitu Cash (bayar tunai di kasir) atau QRIS (memindai kode QR kedai), serta dapat menambahkan catatan khusus untuk pesanannya. Setelah tombol Buat Pesanan ditekan, sistem menyimpan data pesanan, item pesanan, dan data pembayaran ke basis data dalam satu transaksi, kemudian mengirimkan notifikasi kepada kasir dan admin.

### 5. Halaman Pesanan Saya
Halaman ini menampilkan daftar seluruh pesanan yang pernah dibuat pelanggan selama sesi meja berlangsung, lengkap dengan nomor antrian, waktu pemesanan, total, status pesanan, dan status pembayaran. Daftar pesanan diperbarui secara otomatis (real-time) melalui mekanisme polling, sehingga perubahan status yang dilakukan kasir langsung terlihat tanpa pelanggan perlu menyegarkan halaman secara manual.

### 6. Halaman Detail Pesanan
Halaman detail pesanan menampilkan nomor antrian, indikator progres status pesanan (Menunggu, Diproses, Siap Diambil, Selesai), rincian item, serta informasi pembayaran. Apabila pelanggan memilih metode QRIS dan pembayaran belum diterima, halaman ini menampilkan gambar QRIS milik kedai beserta nominal yang harus diketik pelanggan pada aplikasi pembayarannya. Setelah pembayaran diverifikasi kasir, halaman secara otomatis memperbarui status dan menampilkan informasi WiFi kedai sebagai fasilitas bagi pelanggan; pelanggan juga dapat membatalkan pesanan selama statusnya masih Menunggu.

### 7. Halaman Akun / Info Meja
Halaman ini menampilkan informasi sesi pelanggan yang sedang aktif, meliputi nama pelanggan dan nomor meja yang sedang digunakan. Pada halaman ini pelanggan juga dapat mengakhiri sesi meja apabila telah selesai berkunjung, sehingga meja dapat digunakan kembali oleh pelanggan berikutnya.

---

## B. Tampilan Kasir

### 8. Halaman Login Kasir
Halaman login kasir merupakan gerbang autentikasi bagi petugas kasir sebelum mengakses sistem. Kasir memasukkan username dan password, kemudian sistem memverifikasi kecocokan password menggunakan fungsi hashing bcrypt demi keamanan data akun. Apabila autentikasi berhasil, sistem membuat session kasir dan mengarahkan pengguna ke halaman dashboard; apabila gagal, sistem menampilkan pesan kesalahan.

### 9. Halaman Dashboard Kasir
Dashboard kasir menampilkan ringkasan operasional harian, seperti jumlah pesanan masuk, pesanan yang sedang diproses, pesanan siap diambil, dan total pendapatan hari berjalan. Halaman ini dilengkapi ikon lonceng notifikasi yang memantau pesanan baru dan pembayaran secara real-time setiap lima detik disertai suara pemberitahuan, sehingga kasir dapat segera merespons pesanan yang masuk.

### 10. Halaman Daftar Pesanan
Halaman ini menampilkan seluruh pesanan yang masuk dalam bentuk daftar yang dapat difilter berdasarkan status dan dicari berdasarkan nomor pesanan. Setiap baris menampilkan nomor antrian, asal meja, jumlah item, total, status pembayaran, dan status pesanan, sehingga kasir dapat memantau seluruh antrean pesanan dari satu layar.

### 11. Halaman Detail Pesanan (Kasir)
Halaman detail pesanan menyajikan rincian lengkap satu pesanan, meliputi identitas meja, daftar item beserta opsinya, catatan pelanggan, total, dan informasi pembayaran. Dari halaman ini kasir dapat memverifikasi pembayaran (baik tunai maupun QRIS) serta mengubah status pesanan menjadi Diproses, Siap Diambil, atau Selesai; setiap perubahan langsung diteruskan ke halaman pelanggan secara real-time.

### 12. Halaman Pesanan Baru (POS)
Halaman POS (Point of Sale) digunakan kasir untuk melayani pelanggan yang memesan langsung di kasir tanpa memindai QR meja. Kasir memilih menu melalui tombol-tombol berukuran besar yang dikelompokkan per kategori, menentukan opsi ukuran, penyajian, dan gula melalui menu pilihan, kemudian memproses pembayaran secara langsung. Perhitungan harga dilakukan ulang di sisi server untuk menjamin keakuratan total transaksi.

### 13. Tampilan Struk
Struk menampilkan identitas kedai, nomor antrian, rincian item beserta opsi, total pembayaran, metode pembayaran, serta informasi WiFi kedai. Struk dirancang dengan lebar kertas printer termal dan dapat langsung dicetak melalui fungsi cetak peramban sebagai bukti transaksi bagi pelanggan.

### 14. Halaman Pembayaran (Kasir)
Halaman ini menampilkan daftar seluruh transaksi pembayaran beserta metode dan statusnya. Kasir dapat memfilter pembayaran yang belum diverifikasi, kemudian melakukan verifikasi setelah menerima uang tunai atau memastikan dana QRIS telah masuk, sehingga status pembayaran pada halaman pelanggan ikut diperbarui.

### 15. Halaman Pendapatan
Halaman pendapatan menyajikan rekapitulasi hasil penjualan yang dapat dilihat berdasarkan rentang waktu tertentu. Informasi yang ditampilkan meliputi jumlah transaksi dan total pendapatan, sehingga kasir dapat mencocokkan uang fisik di laci kas dengan catatan sistem pada akhir shift.

### 16. Halaman Data Pelanggan (Kasir)
Halaman ini menampilkan daftar pelanggan yang pernah bertransaksi di kedai beserta riwayat jumlah pesanannya. Data ini membantu kasir mengenali pelanggan yang sedang menunggu pesanan serta menjadi arsip pelanggan bagi kedai.

---

## C. Tampilan Admin

### 17. Halaman Login Admin
Halaman login admin berfungsi sebagai autentikasi bagi pengelola sistem. Mekanismenya sama dengan login kasir, yaitu verifikasi username dan password terenkripsi bcrypt, namun session yang dibuat memberikan hak akses penuh terhadap seluruh modul pengelolaan data master, laporan, dan pengaturan toko.

### 18. Halaman Dashboard Admin
Dashboard admin menampilkan ringkasan kinerja kedai secara menyeluruh, meliputi total pendapatan, jumlah pesanan, menu terlaris, serta grafik penjualan dalam beberapa periode. Visualisasi grafik membantu admin menganalisis tren penjualan dan mengambil keputusan bisnis, misalnya menentukan menu yang perlu dipromosikan.

### 19. Halaman Kelola Menu
Halaman ini digunakan admin untuk menambah, mengubah, dan menghapus data menu, meliputi nama, kategori, harga, deskripsi, foto, dan status ketersediaan. Terdapat pula opsi "tanpa gula" yang apabila dicentang akan menyembunyikan pilihan tingkat gula pada sisi pelanggan dan kasir, sesuai karakteristik menu kopi murni seperti Espresso dan Americano.

### 20. Halaman Kelola Kategori
Halaman kelola kategori digunakan untuk mengelompokkan menu ke dalam kategori tertentu seperti Coffee, Non Coffee, Tea, dan Snack. Admin dapat menambah, mengubah, maupun menghapus kategori, dan setiap kategori menampilkan jumlah menu yang berada di dalamnya sebagai informasi pendukung.

### 21. Halaman Kelola Meja
Halaman ini digunakan untuk mengelola data meja beserta QR Code-nya. Setiap meja yang ditambahkan akan dibuatkan kode unik oleh sistem yang kemudian dibangkitkan menjadi QR Code berisi tautan pemesanan meja tersebut. Admin dapat mencetak seluruh QR Code dalam format kartu siap tempel melalui tombol cetak, serta menguji hasil pemindaian melalui fitur scan test.

### 22. Halaman Pesanan (Admin)
Halaman ini menampilkan seluruh riwayat pesanan dari sisi admin sebagai fungsi pemantauan. Admin dapat melihat detail setiap pesanan beserta status dan pembayarannya, namun pengelolaan operasional harian tetap menjadi tanggung jawab kasir sesuai pembagian hak akses sistem.

### 23. Halaman Pembayaran (Admin)
Halaman pembayaran pada sisi admin menampilkan rekapitulasi seluruh transaksi pembayaran, baik yang sudah maupun belum diverifikasi, beserta metode pembayarannya. Halaman ini berfungsi sebagai alat pengawasan arus kas kedai bagi admin.

### 24. Halaman Data Pelanggan (Admin)
Halaman ini menampilkan seluruh data pelanggan yang tersimpan dalam sistem beserta rekap jumlah transaksinya. Data tersebut dapat dimanfaatkan admin sebagai bahan analisis loyalitas pelanggan.

### 25. Halaman Kelola Akun Kasir
Halaman ini digunakan admin untuk mengelola akun petugas kasir, meliputi penambahan akun baru, pengubahan nama dan password, serta penghapusan akun. Password yang tersimpan dienkripsi menggunakan algoritma bcrypt sehingga tidak dapat dibaca dalam bentuk teks asli.

### 26. Halaman Laporan Penjualan
Halaman laporan menyajikan rekapitulasi penjualan berdasarkan rentang tanggal yang dipilih, meliputi jumlah pesanan, rincian per menu, dan total pendapatan. Laporan dapat diekspor ke dalam format Excel melalui tombol ekspor, sehingga memudahkan pemilik kedai dalam melakukan pembukuan dan pengarsipan.

### 27. Halaman Pengaturan Toko
Halaman pengaturan digunakan untuk mengelola identitas kedai, meliputi nama toko, alamat, nomor WhatsApp, jam operasional, deskripsi, logo, dan banner. Halaman ini juga menyediakan pengaturan WiFi kedai yang akan ditampilkan kepada pelanggan setelah pembayaran lunas, serta unggahan gambar QRIS statis milik kedai yang ditampilkan pada halaman pembayaran pelanggan.
