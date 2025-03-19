## MODULE 6

Nama: Freia Arianti Zulaika
NPM: 2306152254

### Commit 1 Reflection

Fungsi `handle_connection` bertugas membaca dan mencetak HTTP request yang masuk melalui `TcpStream`. Dengan menggunakan `BufReader`, setiap baris dalam permintaan diproses sebagai iterable. Baris-baris tersebut dipisahkan berdasarkan newline atau CRLF, lalu di-unwrap untuk mengambil nilainya. Hanya baris non-kosong yang dikumpulkan ke dalam `Vector`, memastikan hanya bagian penting dari request yang diproses. Pendekatan ini memanfaatkan ownership dan iterator di Rust untuk efisiensi dalam menangani koneksi TCP.

### Commit 2 Reflection

Dalam fungsi `handle_connection`, server HTTP menerima setiap koneksi yang masuk melalui TCP dan mengirimkan respons mentah dengan status `200 OK`, sehingga browser langsung menampilkan halaman HTML yang diminta. Fungsi ini dimulai dengan membaca permintaan HTTP menggunakan `BufReader`, yang mengumpulkan semua baris request dan berhenti ketika menemukan baris kosong (menggunakan `.take_while(|line| !line.is_empty())`) sebagai penanda akhir header HTTP. Setelah itu, server mengambil isi file `hello.html` menggunakan `fs::read_to_string()`, lalu menghitung panjang kontennya untuk ditetapkan sebagai nilai header `Content-Length` (memberi tahu browser ukuran body respons yang akan diterima). Selanjutnya, server membentuk HTTP response dalam format standar, mencakup status line, header, dan isi file HTML. Terakhir, server mengirimkan HTTP response ke browser menggunakan perintah `write_all()`.

Screenshot:
![Commit 2 screen capture](/assets/images/commit2.png)

### Commit 3 Reflection

Sebelumnya, web server selalu menampilkan halaman `hello.html`. Setelah dimodifikasi, fungsi `handle_connection` kini mengirimkan raw HTTP Response berdasarkan status HTTP Request yang diterima. Proses ini menggunakan `BufReader` untuk membaca raw HTTP Request, dengan mengambil baris pertama menggunakan `.lines().next().unwrap().unwrap()` untuk mendapatkan request line, lalu diperiksa apakah sesuai dengan GET / HTTP/1.1. Jika ya, server mengembalikan halaman `hello.html`. Jika tidak, server menampilkan `404.html`. Dengan pendekatan ini, fungsi `handle_connection` sekarang menyerupai _routing_, di mana server akan mengembalikan halaman HTML berdasarkan permintaan yang diterima. Selain itu, awalnya terdapat duplikasi kode pada bagian conditional untuk menentukan apakah permintaan akan mengembalikan halaman `hello.html` atau tidak. Oleh karena itu, saya menerapkan _refactoring_ dengan mengekstrak `status_line` dan nama file HTML ke dalam variabel yang nilainya ditentukan berdasarkan request yang diterima.

Screenshot:
![Commit 3 screen capture](/assets/images/commit3.png)