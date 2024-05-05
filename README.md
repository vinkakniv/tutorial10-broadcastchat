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