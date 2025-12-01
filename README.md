# tokokita

## RegistrasiBloc
RegistrasiBloc berfungsi untuk menangani proses registrasi pengguna. BLoC ini membuat request POST ke endpoint /registrasi dengan mengirim data nama, email, dan password. Setelah server mengembalikan response, data tersebut di-decode menjadi objek Registrasi melalui Registrasi.fromJson(). Tujuan utamanya memastikan proses registrasi terjadi pada layer logika bisnis, bukan langsung pada UI.
## LoginBloc
LoginBloc berfungsi melakukan proses login melalui endpoint /login. Data berupa email dan password dikirimkan melalui HTTP POST. Jika berhasil, server mengirimkan token serta informasi user, kemudian diubah menjadi objek Login. Token ini nantinya disimpan ke SharedPreferences untuk proses autentikasi pada halaman lain.
## ProdukBloc
ProdukBloc adalah pusat logika CRUD produk. BLoC ini menyediakan beberapa fungsi:
getProduks(), melakukan HTTP GET ke endpoint /produk untuk mengambil daftar produk, lalu mengonversi JSON menjadi list objek Produk.
addProduk(), mengirim data produk baru menggunakan POST untuk membuat produk baru.
updateProduk(), melakukan HTTP PUT untuk mengubah data produk berdasarkan ID.
deleteProduk(), menghapus produk berdasarkan ID menggunakan HTTP DELETE.
Semua proses komunikasi API dilakukan secara terpisah agar UI tetap bersih dan mudah dikelola.
## APIUrl
Kelas ini digunakan untuk menyimpan URL endpoint. Pendekatan ini membuat endpoint lebih mudah dikelola serta memudahkan perubahan jika base URL berubah karena deploy server. Terdapat method dinamis seperti updateProduk(id), showProduk(id), dan deleteProduk(id) untuk membuat URL sesuai kebutuhan.
## API Helper
Api adalah helper utama untuk melakukan request HTTP. Seluruh request (GET, POST, PUT, DELETE) melewati kelas ini. Helper ini juga otomatis menyisipkan Bearer Token ke header menggunakan token yang disimpan di SharedPreferences. Selain itu, terdapat method _returnResponse() untuk menangani berbagai kemungkinan error seperti 400 (Bad Request), 401/403 (Unauthorized), dan 500 (Server Error). Dengan demikian, error dapat ditangani secara terpusat.
## Exception Handling
Terdapat beberapa custom exception seperti:
FetchDataException
BadRequestException
UnauthorisedException
InvalidInputException
Tujuannya memudahkan debugging dan membuat error message lebih spesifik, sesuai kondisi API.
## UserInfo Helper
UserInfo menggunakan SharedPreferences untuk menyimpan:
Token
User ID
Ini memungkinkan aplikasi mengetahui apakah user sudah login atau belum ketika membuka aplikasi. Method logout() digunakan untuk menghapus semua data login sehingga user keluar dari sesi.
##Model Login, Produk, dan Registrasi
Model digunakan untuk mengubah data JSON ke objek Dart.
Login menyimpan hasil login berupa code, status, token, dan informasi user.
Produk menyimpan data produk seperti kodeProduk, namaProduk, dan hargaProduk.
Registrasi menyimpan hasil response pendaftaran user.
Struktur model ini membuat pengolahan data menjadi lebih mudah dan terstruktur.
## LoginPage (UI)
Halaman login menyediakan input email dan password, serta tombol login. Setelah validasi form berhasil, halaman memanggil LoginBloc.login(). Jika berhasil, token serta user ID disimpan, lalu user diarahkan ke halaman ProdukPage(). Jika gagal, aplikasi menampilkan dialog peringatan menggunakan WarningDialog.
## ProdukPage, ProdukForm, dan ProdukDetail
ProdukPage menampilkan daftar produk (GET).
ProdukDetail digunakan untuk menampilkan detail produk serta menampilkan tombol Edit dan Delete. Delete akan memanggil ProdukBloc.deleteProduk().
ProdukForm digunakan untuk menambah atau mengubah produk. Jika form dibuka dengan data produk, maka form menjadi mode update. Jika tidak, form menjadi mode tambah produk. Setelah sukses, user diarahkan kembali ke halaman produk.
Semua komponen UI terhubung dengan BLoC, sehingga UI tetap bersih dan logika berat berada di BLoC.


<img width="1898" height="1023" alt="image" src="https://github.com/user-attachments/assets/a85fbff5-a5cb-4c13-bdd8-03cf1383194b" />

<img width="485" height="1011" alt="image" src="https://github.com/user-attachments/assets/93064381-43c2-4f43-823b-0b5eea599288" />

<img width="494" height="880" alt="image" src="https://github.com/user-attachments/assets/1efe3cb5-406d-4593-96ea-5112b7cc843f" />

<img width="486" height="1014" alt="image" src="https://github.com/user-attachments/assets/1a80a91c-7eb0-4d49-a208-ae87423bf1dd" />

<img width="481" height="1009" alt="image" src="https://github.com/user-attachments/assets/3437e0b3-3552-4406-a4a6-b42b7ffd3f9c" />

<img width="491" height="874" alt="image" src="https://github.com/user-attachments/assets/e6305e90-aa28-4662-8c7c-90d9dcaa9dc0" />





