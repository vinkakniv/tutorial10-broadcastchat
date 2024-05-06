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