# Reflection Tutorial Modul 10

**Zufar Romli Amri**  
**NPM**: 2306202694  
**Kelas**: A

---

### 2.1 Original code and how to run it.

Gambar 1:

![/original-code-and-how-to-run-it](./images/server-broadcast-chat.jpg)

Gambar 2:

![/original-code-and-how-to-run-it](./images/client-1-broadcast-chat.jpg)

Gambar 3:

![/original-code-and-how-to-run-it](./images/client-2-broadcast-chat.jpg)

Gambar 4:

![/original-code-and-how-to-run-it](./images/client-3-broadcast-chat.jpg)

Program yang dijalankan merupakan implementasi sistem chat sederhana menggunakan WebSocket di Rust. Program ini terdiri dari dua bagian utama: server yang menangani koneksi dan menyebarkan pesan antar klien, dan klien yang memungkinkan pengguna untuk mengirim dan menerima pesan.

Ketika program dijalankan sesuai urutan gambar di atas, dan saat kita mengetikkan teks di klien sesuai urutan pada gambar di atas, terjadi beberapa hal berikut:

- Server dimulai dan mendengarkan koneksi pada port 2000 (terlihat pada gambar 1)

- Setiap klien yang terhubung akan menerima pesan sambutan "Welcome to chat! Type a message"

- Ketika pengguna mengetikkan pesan di salah satu klien:

a. Pesan dikirim ke server melalui WebSocket

b. Server menerima pesan dan menyebarkannya ke semua klien yang terhubung (broadcasting)

c. Semua klien, termasuk pengirim, menerima pesan tersebut dengan format "From server: [pesan]"

Pada gambar di atas:

- Klien pertama mengirim pesan "Hello!" (gambar 2)

- Klien kedua mengirim pesan "Good morning!" (gambar 3)

- Klien ketiga mengirim pesan "My name is Zufar!" (gambar 4)

Setiap pesan yang dikirim oleh satu klien diterima oleh semua klien yang terhubung. Ini terlihat dari gambar 2 di mana klien pertama menerima semua pesan, baik yang dikirimnya sendiri maupun yang dikirim oleh klien lain.

Program ini menggunakan fitur konkuren dari Rust dengan bantuan Tokio untuk menangani koneksi secara asinkron. Pada bagian server, fungsi handle_connection menggunakan tokio::select! untuk secara bersamaan menangani pesan masuk dari klien dan menyebarkan pesan ke semua klien yang terhubung melalui saluran broadcast. Sementara pada klien, program juga menggunakan tokio::select! untuk secara bersamaan menangani input dari keyboard dan menerima pesan dari server.
Dengan implementasi ini, sistem chat dapat menangani banyak koneksi secara bersamaan tanpa memblokir proses utama, yang merupakan contoh baik tentang bagaimana asynchronous programming di Rust dapat digunakan untuk membangun aplikasi jaringan yang efisien.

---