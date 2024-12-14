- **Nama**: Dian Anggraeni Putri
- **NRP**: 5027231016

# Transport Layer

Transport Layer adalah lapisan keempat dalam model OSI (Open Systems Interconnection) yang bertanggung jawab untuk memastikan pengiriman data antara aplikasi yang berjalan di perangkat yang berbeda dalam jaringan. Di sini, data dibagi menjadi segmen-segmen dan disiapkan untuk pengiriman serta pengelolaan komunikasi antara perangkat sumber dan tujuan.

---

## 1. **Segmentasi dan Reassembly**

### **Segmentasi**
**Segmentasi** adalah proses memecah data yang besar menjadi bagian-bagian kecil yang disebut **segmen**, yang kemudian dapat dikirim melalui jaringan. Segmentasi penting karena:
- Setiap jaringan memiliki batasan ukuran paket data yang dapat diterima, dikenal dengan **Maximum Transmission Unit (MTU)**. 
- Data yang lebih besar daripada MTU harus dipecah agar dapat dikirimkan.
- **Transmission Control Protocol (TCP)** memecah data aplikasi menjadi segmen yang lebih kecil agar sesuai dengan batasan jaringan, dan setiap segmen dikirim dengan nomor urut yang unik untuk melacak urutan pengiriman.

### **Reassembly**
Setelah segmen-segmen data mencapai perangkat tujuan, mereka harus **disatukan kembali** dalam urutan yang benar melalui proses **reassembly**. Setiap segmen berisi informasi penting, seperti:
- **Nomor urut** untuk memastikan segmen-segmen disusun kembali dengan benar.
- **Checksum** untuk memverifikasi bahwa data tidak rusak saat transit.

Reassembly memastikan bahwa data yang diterima oleh penerima utuh dan dalam urutan yang benar.

---

## 2. **Connection Control**

### **Connection-Oriented (Berbasis Koneksi)**
Pada protokol **Connection-Oriented** seperti TCP, sebelum pengiriman data dimulai, koneksi harus dibentuk terlebih dahulu antara pengirim dan penerima melalui prosedur yang disebut **handshaking**. Handshaking adalah tahap awal yang memastikan bahwa kedua perangkat siap untuk berkomunikasi.
- **Three-way Handshake**: Proses tiga langkah yang melibatkan pengiriman sinyal antara pengirim dan penerima untuk memastikan koneksi siap:
  1. **SYN**: Pengirim mengirim sinyal permintaan koneksi.
  2. **SYN-ACK**: Penerima merespons dengan sinyal persetujuan.
  3. **ACK**: Pengirim mengkonfirmasi bahwa koneksi sudah siap.

Keuntungan utama dari koneksi berbasis ini adalah bahwa data dikirim dengan jaminan **reliabilitas**, **urutan**, dan **integritas**.

### **Connectionless (Tanpa Koneksi)**
Pada protokol **Connectionless** seperti **User Datagram Protocol (UDP)**, data dikirim tanpa membangun koneksi terlebih dahulu. 
- Pengirim langsung mengirimkan data (dalam bentuk **datagram**) ke penerima, tanpa perlu melakukan **handshaking**.
- Tidak ada mekanisme untuk memastikan data sampai dengan benar atau dalam urutan yang tepat.
- UDP lebih cepat karena tidak ada overhead untuk pembentukan koneksi, tetapi data mungkin hilang atau sampai dengan urutan yang salah.

UDP sering digunakan untuk aplikasi yang memerlukan **kecepatan tinggi** dan bisa mentolerir kehilangan data, seperti streaming video atau voice over IP (VoIP).

---

## 3. **Flow Control**

**Flow Control** adalah mekanisme yang digunakan untuk mengontrol laju pengiriman data antara pengirim dan penerima agar penerima tidak kewalahan dalam memproses data yang diterima. Jika penerima tidak dapat memproses data secepat yang dikirimkan, pengirim perlu menunggu hingga penerima siap untuk menerima lebih banyak data.

### **Windowing**
Salah satu teknik flow control yang digunakan oleh protokol TCP adalah **windowing**. Windowing memungkinkan pengirim mengirim beberapa segmen data sekaligus, tetapi membatasi jumlah data yang dapat dikirimkan sebelum menerima konfirmasi dari penerima.
- **Sliding Window**: Pengirim mengirimkan sejumlah data yang diizinkan oleh penerima berdasarkan ukuran jendela yang ditetapkan. Ketika penerima memproses sebagian data, window bergerak untuk mengizinkan lebih banyak data dikirimkan.
- **Size of the Window**: Ukuran window bergantung pada kapasitas penerima untuk memproses data. Jika penerima tidak bisa menangani lebih banyak data, ukuran window akan dikurangi.

---

## 4. **Error Control**

**Error Control** adalah teknik untuk mendeteksi dan mengoreksi kesalahan dalam data yang dikirimkan. Dalam komunikasi jaringan, kesalahan bisa terjadi karena gangguan sinyal atau masalah perangkat keras.

### **Checksum**
Protokol seperti TCP menggunakan **checksum** untuk mendeteksi kesalahan dalam data. Setiap segmen data memiliki nilai checksum yang dihitung oleh pengirim. Penerima kemudian menghitung checksum untuk data yang diterima, dan jika kedua nilai checksum cocok, data dianggap utuh.
- Jika checksum tidak cocok, data dianggap rusak dan akan diminta untuk dikirim ulang.

### **Acknowledgements (ACK) dan Retransmission**
Selain checksum, **Acknowledgements (ACK)** digunakan untuk memberi tahu pengirim bahwa data telah diterima dengan benar. Setiap kali penerima berhasil menerima segmen data, ia mengirimkan ACK untuk memberi tahu pengirim bahwa data tersebut telah diterima.
- Jika pengirim tidak menerima ACK dalam waktu tertentu (misalnya karena segmen hilang atau rusak), pengirim akan mengirim ulang segmen yang gagal diterima.

---

## 5. **Multiplexing**

**Multiplexing** adalah teknik yang memungkinkan beberapa aplikasi atau sesi komunikasi untuk berbagi satu saluran komunikasi yang sama tanpa saling mengganggu. Di Transport Layer, ini dilakukan dengan menggunakan **port numbers**.
- **Port numbers** memungkinkan aplikasi yang berbeda pada perangkat yang sama untuk mengirimkan dan menerima data secara bersamaan tanpa campur aduk.
  
Contohnya:
- **HTTP** (untuk website) menggunakan port **80**.
- **SMTP** (untuk email) menggunakan port **25**.
- **FTP** (untuk transfer file) menggunakan port **21**.

Setiap aplikasi atau proses yang berjalan pada perangkat memiliki **port number** unik yang digunakan untuk mengidentifikasi saluran komunikasi data yang sesuai.

---

## 6. **Contoh Protokol Transport Layer**

### **Transmission Control Protocol (TCP)**
- **Connection-Oriented**: Protokol ini memerlukan pembentukan koneksi sebelum data dapat dikirimkan.
- **Reliable**: Menjamin bahwa data dikirim dengan urutan yang benar dan tanpa kesalahan.
- **Flow Control**: Memungkinkan pengendalian laju pengiriman data untuk menghindari kemacetan.
- **Error Detection**: Menggunakan checksum untuk memverifikasi integritas data dan mekanisme ACK untuk memastikan pengiriman data yang berhasil.

### **User Datagram Protocol (UDP)**
- **Connectionless**: Tidak memerlukan pembentukan koneksi sebelumnya.
- **Unreliable**: Tidak ada jaminan pengiriman data atau urutan data yang benar.
- **No Flow Control**: UDP tidak memiliki kontrol aliran atau deteksi kesalahan, sehingga pengiriman data lebih cepat namun lebih rentan terhadap kehilangan data.
- **Low Latency**: Cocok untuk aplikasi yang memerlukan kecepatan pengiriman tinggi dan toleransi terhadap kehilangan data, seperti video streaming atau komunikasi suara.

---

## 7. **Kesimpulan**

Transport Layer memainkan peran penting dalam memastikan komunikasi data antara aplikasi di perangkat yang berbeda. Beberapa konsep penting di Transport Layer adalah segmentasi, reassembly, kontrol koneksi, flow control, error control, dan multiplexing. Dengan mengimplementasikan protokol seperti TCP dan UDP, Transport Layer menyediakan dua jenis model komunikasi yang berbeda: satu yang lebih andal dan terkontrol (TCP) dan satu lagi yang lebih cepat tetapi tidak menjamin keandalan (UDP).


