# Nama: Clara Sista Widhiastuti </br> NPM: 2206825782 </br> Kelas: Adpro-A

# Reflection
1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) 
methods, and in what scenarios would each be most suitable? </br>
* **Unary RPC**: salah satu tipe protokol komunikasi yang membolehkan interaksi antara client-server dimana client akan mengirimkan
single request kepada server dan menerima single response kembali. Unary baik digunakan ketika ingin mengambil satu item 
dari database, mengautentikasi pengguna, atau ingin melakukan perhitungan dan mendapatkan hasilnya. </br>
* **Server Streaming RPC**: client mengirim single request ke server, dan mendapat banyak respon dalam aliran data berkelanjutan.
Server Streaming RPC baik digunakan saat ingin melakukan transmisi data dalam jumlah besar secara berurutan, dengan server 
mengirim pesan secara terus menerus hingga streamnya habis.
* **Bi-directional RPC**: Menggambarkan mekanisme streaming 2 arah, dimana client dan server dapat mengirim dan menerima 
pesan secara independen. Cocok digunakan untuk aplikasi yang membutuhkan komunikasi dua arah seperti chat, game interaktif
atau aplikasi yang memerlukan interaksi real-time dan responsif. 

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly 
regarding authentication, authorization, and data encryption?</br>
Untuk proses autentikasi dapat menggunakan token. Client akan mengirimkan token ini dalam header request, dan server 
akan memverifikasi token tersebut sebelum memberikan akses. Setelah autentikasi, otorisasi menentukan apa yang bisa 
dilakukan pengguna atau sistem tersebut setelah mereka terautentikasi dapat menggunakan otorisasi berbasi peran. Enkripsi 
data sangat penting untuk melindungi data yang dikirimkan antara client dengan server.


3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, 
especially in scenarios like chat applications? </br>
Dalam bidirectional streaming, server dan client akan mengirim dan menerima pesan secara terus-menerus. Hal tersebut membuat 
pengelolaan state (keadaan) menjadi kompleks karena server perlu menangani multiple connections dan masing-masing state 
secara efisien. Permasalahan terputusnya koneksi menyebabkan pesan tidak terkirim atau diterima. 


4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses 
in Rust gRPC services? </br>
Kelebihannya adalah terintegrasi dengan tokio ecosystem serta kemudahan dalam penggunaanya untuk mengubah stream kemudian
digunkan untuk streaming respons. 
Kekurangannya tidak mendukung backpressure yang dapat menyebabkan masalah kinerja jika sender mengirim pesan lebih cepat
daripada reciever mengelolanya, potensi bottleneck karena bukan cara yang paling efisien untuk menangani skenario streaming
dengan throughput tinggi.


5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability 
and extensibility over time?</br>
Penggunaan traits untuk abstraksi memungkinkan untuk mennyediakan implementasi code reuse. Mengorganisir kode ke dalam 
modul dan crate yang berbeda untuk memisahkan tanggung jawab dan memudahkan pengelolaan dependensi.Menerapkan design pattern
seperti Factory, Singleton, dan Observer untuk memecahkan masalah umum. Mengimplementasikan middleware atau interceptors 
untuk menangani aspek cross-cutting seperti logging, authentication, dan error handling.


6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment 
processing logic?</br>
Sebelum memproses sebuah pembayaran, perlu untuk memvalidasi input yang diterima dalam PaymentRequest. Pengololaan kegagalan
atau kesalahan saat melakukan transaksi. Mencatat setiap detail dari transaksi dan otorisasi transaksi


7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design 
of distributed systems, particularly in terms of interoperability with other technologies and platforms?</br>
Penggunaan Protocol Buffers (Protobuf) sebagai format pertukaran data membuat menjadi ringan dan efisien. mendefinisikan 
API yang jelas melalui file IDL (Interface Definition Language) sehingga membantu standardisasi komunikasi antar layanan.
gRPC juga mendukung streaming dua arah yang memungkinkan komunikasi realtime antar layanan.


8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to 
HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?</br>
HTTP/2 merupakan evolusi dari protokol HTTP/1.1 yang menawarkan sejumlah peningkatan dalam hal efisiensi, kecepatan, dan 
kinerja. HTTP/2 juga HTTP/2 memungkinkan beberapa request dan response untuk berinteraksi secara simultan melalui satu 
koneksi TCP, dan menyediakan mekanisme untuk menetapkan prioritas pada request yang berbeda.
Namun HTTP/2 memiliki kekurangan yaitu HTTP/2 lebih kompleks untuk diimplementasikan dibandingkan dengan HTTP/1.1, tidak 
semua server web dan infrastruktur internet sudah mendukung HTTP/2.


9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of 
gRPC in terms of real-time communication and responsiveness?</br>
Perbedaan yang paling mendasar adalah REST API biasanya menggunakan model stateless di mana setiap permintaan dibuat 
melalui koneksi HTTP/1.1 yang baru, sehingga setiap permintaan harus mencakup semua informasi yang diperlukan untuk diproses.
Sedangkan, gRPC menggunakan HTTP/2 yang mendukung koneksi multiplexing, yang memungkinkan melakukan pengiriman dan 
penerimaan banyak pesan pada satu koneksi yang sama. Dalam REST, setiap permintaan yang dikirimkan ke server menerima 
satu respons, pada grpc client dan server dapat mengirim dan menerima pesan secara berkelanjutan.


10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more 
flexible, schema-less nature of JSON in REST API payloads?</br>
gRPC menggunakan Protocol Buffers harus mendefinisikan struktur data terlebih dahulu dalam skema. Ini memastikan bahwa 
data yang dikirim dan diterima sesuai dengan struktur yang telah ditentukan, sehingga mengurangi kemungkinan kesalahan 
data. Protobuf dirancang untuk serialisasi data yang efisien, baik dalam ukuran maupun kecepatan, yang berkontribusi 
pada performa yang lebih baik dibandingkan dengan JSON. Sebaliknya, JSON dalam REST API menawarkan fleksibilitas yang 
lebih besar karena tidak memerlukan skema yang ketat. Ini memungkinkan pengembang untuk mengirim dan menerima data yang 
lebih dinamis dan beradaptasi dengan perubahan dengan lebih cepat tanpa perlu memperbarui skema atau kode. Namun, ini juga bisa menyebabkan ketidaksesuaian dan kesalahan data jika tidak ditangani dengan hati-hati.
