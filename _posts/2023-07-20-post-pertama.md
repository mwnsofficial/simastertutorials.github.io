---
title: Mengatur Singkron Jam
layout: post
description: Cara mengatur singkronisasi jam pada opewnrt
image: images/blog/mengatur-singkron-jam.jpg
image-alt: mengatur singkron jam
tags: [openwrt]
---
Silahkan anda hidupkan perangkat dan masuk lah ke webgui dari luci `openwrt`.

Untuk memasukkan `IP` pada search http browser silahkan periksa terlebih dahulu di alamat `address` host yang ada di pengaturan wifi anda.

Jika alamat `IP` pada wifi anda menunjukkan alamat di `192.168.1.106` (hanya contoh saja) itu berarti untuk gateway ip adalah `192.168.1.1` karena subnet mask nya adalah 24.

Jadi untuk masuk ke webgui openwrt adalah `192.168.1.1` dan setelah masuk silahkan anda untuk mengisi password luci anda.

Setelah masuk login, anda bisa menuju ke menu pojok kiri atas dan pilih lah menu `System` lalu kemudian pilih lagi `System`.

Kemudian anda mengatur zona waktu tepat di bawah nya lalu simpan.

Setelah itu masuk ke tab singkronisasi, anda bisa mengatur `ip pool` sendiri atau anda bisa mengikuti ip pool di bawah ini:

Ini no.1
```
0.id.pool.ntp.org
```
No.2
```
1.id.pool.ntp.org
```
No.3
```
2.id.pool.ntp.org
```
No.4
```
3.id.pool.ntp.org
```
Dan jikq sudah anda bisa tekan `save and apply` untuk menyipan hasil settingan.
