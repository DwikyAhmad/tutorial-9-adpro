# tutorial-9-adpro

## Reflection

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

    Unary RPS adalah single request-response communication antara client dan server. Unary RPC cocok digunakan untuk melakukan simple operations yang dimana sebuah single request dapat langsung di proses dan di respon segera.

    Server streaming RPC adalah tipe komunikasi yang dimana client mengirim sebuah request ke server dan server memberi response berupa stream untuk membaca serangkaian pesan. Client membaca stream message sampai message tersebut habis. Server streaming RPC cocok digunakan untuk situasi dimana server perlu untuk memberikan multiple response dari waktu ke waktu, seperti mengirim data set yang besar atau melakukan real time update.

    Bi-directional streaming RPC adalah komnunikasi yang dimana client dan server memberikan serangkaian pesan menggunakana read-write stream. kedua stream beroperasi secara independen sehingga kedua pihak dapat melakukan read and write dengan urutan yang bebas. Hal ini cocok digunakan untuk skenario dimana client dan server harus memerlukan dan mengirim serangkaian pesan dari waktu ke waktu, seperti aplikasi chat atau real-time game multiplayer.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

    melakukan implementasi gRPC pada Rust memberikan pertimbangan potential security pada authentication, authorization, dan data encryption. `Authentication` pada gRPC mendukung method seperti token-based dan OAuth2. `Authorization` memerlukan granular permissions dan scopes untuk melakukan restrict access terhadap specific resources atau operasi yang berada pada gRPC service. `Data encryption` diperlukan enkripsi terhadap data sensitif untuk melindunginya dari unauthorized access.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

   - Concurrency: Ownership pada Rust dapat membuat pemrograman secara concurrent menjadi lebih kompleks
   - Error handling: Network errors atau client disconnection perlu dihandle dengan baik untuk mencegah resource leaks
   - Message Ordering: Memastikan pesan yang diproses mengikuti sesuai urutan, hal ini dapat menantang dalam situasi concurrent

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

    Kelebihan:
    - Asynchronous: Mendukung asynchronous streaming yang dapat meningkatkan performa

    Kekurangan:
    - Complexity: Dapat menambah kompleksitas pada kode
    - Error handling: Error menjadi lebih sulit untuk dihandle dalam konteks asynchronous, memerlukan strategi error handling yang rumit

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

    Cara yang dapat digunakan adalah menggunakan traits, melakukan modularisasi kode, menggunakan libraries, dan menggunakan design pattern. Traits mendefinisi shared behaviour yang meningkatkan code reuse, modularisasi meningkatkan maintainability pada kode dengan memisahkan kode menjadi modul yang independen, menggunakan design pattern seperti factory atau strategy untuk menghandle common programming challenges, meningkatkan extensibility dari waktu ke waktu.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

    Untuk menghandle payment proses yang lebih kompleks dapat digunakan step tambahan seperti:
    - Validation: untuk melakukan check terhadap detail dari proses payment
    - Asynchronous processing: dibutuhkan dalam menjalankan task yang membutuhkan waktu yang lama
    - Error handling: Diperlukan error handling yang lebih kompleks untuk mengatasi error

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

    Interoperability: gRPC mendukung banyak bahasa pemrograman, menjadikannya dapat beroperasi terhadap berbagai platform dan teknologi lainnya
    Performance: gRPC menggunakan HTTP/2 dan Protocol buffer yang memberikan performa lebih baik dibandingkan dengan HTTP/1.1
    Streaming: gRPC mendukung bidriectional streaming yang menguntungkan untuk aplikasi yang membutuhkan informasi secara real-time

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

    Kelebihan:
    - Multiplexing: HTTP/2 memungkinkan multiple reqeusts dan response dikirim dalam waktu bersamaan pada single connection, meningkatkan performa
    - Binary Protocol: HTTP/2 merupakan sebuah binary protocol, yang di mana lebih efisien untuk melakukan parsing dan error yang lebih sedikit jika dibanding text-based pada HTTP/1.1

    Kekurangan:
    - Complexity: HTTP/2 lebih kompleks untuk dilakukan implementasi dan debug karena sifat binary dan multiplexing
    - Compatibility: Tidak semua client dan server mendukung HTTP/2

9.  How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

    REST API: Mengikuti synchronous request-response model. Client mengirimkan sebuah request dan menunggu response. Hal ini dapat memunculkan latency, terutama pada real-time applications.

    gRPC: Mendukung bidirectional streaming. Client dan server dapat melakukan push data secara independen. Hal ini memungkinkan real-time communication dan meningkatkan reponseiveness, sangat berguna untuk membangun real-time applications.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

    gRPC/Protocol Buffers: Menerapkan schema menghasilkan data yang lebih predictable dan aman untuk dilakukan data handling. Akan tetapi, hal ini dapat membatasi fleksibilitas dan memerlukan desain yang lebih awal.

    JSON/REST API: Menerapkan schema-less menawarkan fleksibilitas dan kemudahan dalam penggunaan. Akan tetapi, hal ini akan menyebabkan data menjadi kurang predictable dan memberikan potensi untuk error apabila data tidak sesuai ekspektasi
