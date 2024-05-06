# Advanced Programming - Tutorial


------------
## Overview

This repository contains the code and reflections for Tutorial 10 in Advanced Programming course by Vinka Alrezky As (NPM: 2206820200)❄️

- [Tutorial 10 - Timer](https://github.com/vinkakniv/tutorial10-timer)
- [Tutorial 10 - Broadcast Chat](https://github.com/vinkakniv/tutorial10-broadcastchat)
- [Tutorial 10 - WebChat using yew](https://github.com/vinkakniv/tutorial10-webchatyew)

------------
# Tutorial 10 - Broadcast Chat

### _Reflection_

- _Original code of broadcast chat_

![](https://imgur.com/mii4xSt.png)

Saat server dijalankan, setiap pengguna yang membuka aplikasi akan terhubung ke server menggunakan `WebSocket`. Dalam aplikasi obrolan di atas, ketika seorang pengguna mengirim pesan, pesan tersebut akan diterima oleh server dan segera disebarkan kepada semua pengguna lain yang terhubung ke server.

Dengan demikian, setiap pesan yang dikirim oleh pengguna akan segera muncul di layar pengguna lainnya secara _real time_. Hal ini dimungkinkan oleh penggunaan `WebSocket`, yang memungkinkan komunikasi instan antara server dan pengguna tanpa adanya _delay_ yang signifikan.

- _Modifying the websocket port_

Untuk mengubah port menjadi 8080, langkah-langkah perubahan yang diperlukan adalah sebagai berikut:

Pada `src/bin/server.rs`, ubah nomor port pada panggilan fungsi `TcpListener::bind`:

``` 
    let listener = TcpListener::bind("127.0.0.1:8080").await?; 
    println!("listening on port 8000"); 
```

Pada `src/bin/client.rs`, perlu juga mengubah URI untuk terhubung ke server menggunakan port 8080:
```
    let (mut ws_stream, _) =
        ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8000"))
            .connect()
            .await?;
```

![](https://imgur.com/dHZwiel.png)
Kedua file, `server.rs` dan `client.rs`, menggunakan protokol `WebSocket`, yang diimplementasikan melalui kumpulan `tokio_websockets`. Dengan menggunakan `WebSocket`, pengguna dan server dapat berkomunikasi secara dua arah melalui satu koneksi yang panjang dan persisten. Dengan mengubah port menjadi 8080, aplikasi akan dikonfigurasi untuk menggunakan port tersebut untuk komunikasi `WebSocket`.

- _Small changes. Add some information to client_

Untuk memperbarui informasi IP dan Port dari pengirim pesan, saya melakukan beberapa perubahan pada kode. Pada bagian `server.rs`, saya melakukan dua perubahan utama. Pertama, saya memodifikasi bagian pengiriman pesan ke dalam _channel_ siaran agar mencakup informasi alamat pengirim (IP dan Port) bersama dengan teks pesan yang dikirim. Ini memungkinkan penerima pesan untuk dengan jelas mengetahui asal pesan. Perubahan ini terlihat pada kode berikut:

```
    // Sebelum perubahan
    bcast_tx.send(text.into())?;
    
    // Setelah perubahan
    bcast_tx.send(format!("{addr} : {text}"))?;
```

Kemudian, saya juga mengubah pesan log yang dicetak saat ada koneksi baru agar mencakup nama komputer pengirim, memberikan informasi tambahan tentang sumber koneksi. Perubahan ini terlihat pada kode berikut:

```
    // Sebelum perubahan
    println!("New connection from {addr:?}");
    
    // Setelah perubahan
    println!("New connection from Vinka's Computer {addr:?}");
```

Selanjutnya, pada `client.rs`, saya juga melakukan perubahan untuk meningkatkan informativitas pesan yang diterima dari server. Saya mengubah pesan log yang dicetak pada bagian pengolahan pesan yang diterima. Sebelumnya, pesan log dicetak tanpa menyertakan informasi tambahan. Setelah perubahan, saya menambahkan nama komputer pengirim (Vinka's Computer) ke dalam pesan log, sehingga menjadi lebih jelas dan informatif. Perubahan ini terlihat pada kode berikut:

```
    // Sebelum perubahan
    println!("From server: {}", text);
    
    // Setelah perubahan
    println!("Vinka's Computer - From server: {}", text);
```

Dengan demikian, perubahan ini memberikan informasi tambahan tentang sumber pesan dan meningkatkan pemahaman tentang pesan yang diterima oleh pengguna.

![](https://imgur.com/pTsdzvl.png)

