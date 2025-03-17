## MODULE 6

Nama: Freia Arianti Zulaika
NPM: 2306152254

### Commit 1 Reflection

Fungsi `handle_connection` bertugas membaca dan mencetak HTTP request yang masuk melalui `TcpStream`. Dengan menggunakan `BufReader`, setiap baris dalam permintaan diproses sebagai iterable. Baris-baris tersebut dipisahkan berdasarkan newline atau CRLF, lalu di-unwrap untuk mengambil nilainya. Hanya baris non-kosong yang dikumpulkan ke dalam `Vector`, memastikan hanya bagian penting dari request yang diproses. Pendekatan ini memanfaatkan ownership dan iterator di Rust untuk efisiensi dalam menangani koneksi TCP.