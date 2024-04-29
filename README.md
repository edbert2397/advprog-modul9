1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

Terdapat beberapa perbedaan kunci antara metode RPC (Remote Procedure Call) unary, server streaming, dan bi-directional streaming, serta skenario yang paling cocok untuk masing-masing metode tersebut:

- Unary RPC: Metode ini paling sesuai untuk situasi di mana klien hanya perlu mengirimkan sejumlah data yang kecil dan dalam satu kesempatan saja ke server. Ini biasanya digunakan dalam sistem seperti autentikasi atau pengiriman form. Dalam unary RPC, komunikasi terjadi secara satu arah dari klien ke server dengan sebuah permintaan yang diikuti oleh satu respons.

- Server Streaming RPC: Metode ini berbeda karena memungkinkan server untuk mengirimkan data secara berkelanjutan melalui satu aliran (stream) tanpa perlu menginisiasi koneksi baru setiap kali. Ini mengurangi overhead dan cocok untuk situasi di mana server perlu mengirimkan data yang besar atau streaming data secara terus-menerus seperti data harga saham, berita terkini, atau set data besar yang terbagi dalam beberapa bagian.

- Bi-directional Streaming RPC: Metode ini mirip dengan server streaming, tetapi di sini baik klien dan server dapat mengirim dan menerima data secara berkelanjutan melalui aliran yang sama. Ini sangat berguna dalam aplikasi yang memerlukan pertukaran data yang intensif dan kontinu antara klien dan server, seperti dalam aplikasi pengeditan kolaboratif atau permainan waktu nyata.

2. 
What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Dalam implementasi gRPC, setiap potongan data yang dikirim memerlukan validasi otentikasi dan otorisasi untuk memastikan keamanannya. Berbeda dengan REST yang hanya memerlukan satu kali validasi per request, gRPC membutuhkan validasi berkali-kali untuk satu stream request. Untuk enkripsi, setiap potongan data yang dikirim oleh server maupun klien harus dienkripsi secara terpisah untuk menjaga kerahasiaan data.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Dalam pengimplementasian streaming bi-directional menggunakan gRPC di Rust, tantangan utama adalah menghindari race condition dan memastikan sinkronisasi data yang akurat. Selain itu, koneksi yang berlangsung lama bisa menyulitkan load balancing karena banyak koneksi yang tidak dapat diputus, memberatkan server.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

Keuntungan :
Asynchronous yang mempercepat pengolahan data
Integrasi yang mudah dengan modul-modul tokio lain 

Kerugian :
Kompleks akibat pemrograman asinkronous
Untuk autentikasi dan autorisasi perlu dilakukan untuk tiap data

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

Rust gRPC meningkatkan kemampuan untuk memaintain dan mengextend kode karena perubahan dan penambahan fitur dapat dilakukan lebih mudah. Melalui penggunaan protokol buffer, interface yang konsisten dibuat, yang memfasilitasi ekstensibilitas dan pemeliharaan kode.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Untuk memproses pembayaran yang lebih kompleks, MyPaymentService bisa dikembangkan menjadi server streaming dari unary untuk mempercepat pengiriman data yang kompleks dan mengurangi overhead pembuatan koneksi baru antara klien dan server.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Penggunaan gRPC memungkinkan integrasi yang lebih mudah antara berbagai teknologi dan platform karena gRPC secara otomatis menghubungkan pemanggilan metode yang ditentukan melalui file proto, memudahkan konektivitas dan operasi antar sistem yang terdistribusi.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

HTTP/2 memungkinkan banyak request dan response dalam satu koneksi, yang meningkatkan efisiensi untuk data yang banyak. Namun, kerugiannya adalah biaya overhead yang lebih tinggi, baik dalam hal performa maupun memori, terutama jika data yang dikirim kecil.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

gRPC menawarkan respons yang lebih cepat dan komunikasi real-time yang lebih baik dibandingkan REST API karena hanya memerlukan satu koneksi untuk semua request dan response, sedangkan REST API membutuhkan pembuatan koneksi baru untuk setiap request.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

Pendekatan gRPC dengan protocol buffers mengurangi risiko kesalahan data karena memastikan bahwa data yang dikirim dan diterima telah sesuai dengan skema yang ditetapkan, berbeda dengan JSON dalam REST API yang lebih fleksibel tetapi berpotensi menghasilkan masalah tipe data.