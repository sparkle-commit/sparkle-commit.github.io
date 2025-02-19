---
title: 'Install Mikrotik OS'
author: sparkle-commit
layout: post
permalink: /install-mikrotik-os/
dsq_thread_id:
  - 1204965956
categories:
  - Network
  - Mikrotik
---

<img src="{{ site.baseurl }}/images/mikrotik0.jpg" width="300" height="168" alt="Mikrotik Image">

<!--more-->
# MikroTik RouterOS di VirtualBox

MikroTik RouterOS merupakan sistem operasi berbasis Linux yang berfungsi sebagai router, firewall, dan manajemen jaringan. Salah satu cara untuk menguji dan mengonfigurasi RouterOS tanpa perangkat fisik adalah dengan menjalankannya di lingkungan virtual menggunakan VirtualBox. Dokumentasi ini bertujuan untuk memberikan panduan langkah demi langkah dalam menginstal dan mengonfigurasi MikroTik RouterOS di VirtualBox, mulai dari persiapan perangkat lunak, pembuatan mesin virtual, hingga konfigurasi dasar jaringan. Dengan pendekatan ini, pengguna dapat mempelajari dan menguji fitur-fitur RouterOS secara praktis sebelum diterapkan pada perangkat fisik.

### Instalasi MikroTik OS pada Virtual box 

 Download ISO mikrotik OS di mikrotik.com dengan memilih type x86 untuk instalasi di PC.

 Buat VM baru dengan type dan versi berikut.

![mikrotik1]({{ site.baseurl }}/images/mikrotik1.png)

 Atur RAM nya sebesar 128 MB (opsional).

![mikrotik2]({{ site.baseurl }}/images/mikrotik2.png)

4. Atur kapasitas virtual hardisknya (opsional).

![mikrotik3]({{ site.baseurl }}/images/mikrotik3.png)

Jika semua sudah sesuai kebutuhan klik finish untuk membuat VM.

![mikrotik4]({{ site.baseurl }}/images/mikrotik4.png)

Tampilan VM MikroTikOS setelah dibuat akan seperti ini.

![mikrotik5]({{ site.baseurl }}/images/mikrotik5.png)

Lalu atur Network Adapter 1-4 pada bagian setting. Buat network adapter 1 jadi bridge adapter.

![mikrotik6]({{ site.baseurl }}/images/mikrotik6.png)

Buat network adapter 2 jadi internal network.

![mikrotik7]({{ site.baseurl }}/images/mikrotik7.png)

Buat network adapter 3 jadi internal network.

![mikrotik8]({{ site.baseurl }}/images/mikrotik8.png)

Buat network adapter 4 jadi internal network.

![mikrotik9]({{ site.baseurl }}/images/mikrotik9.png)

Langkah selanjutnya adalah memasang ISO ke bagian storage dari VM.

![mikrotik10]({{ site.baseurl }}/images/mikrotik10.png)

Klik ok lalu jalankan VM dengan klik start.

Di bagian instalasi ceklis pilihan system & dhcp.

![mikrotik12]({{ site.baseurl }}/images/mikrotik12.png)

Ketik y di setiap pilihan lanjutan perintah dari VM sampai kita disuruh tekan enter untuk reboot vm.

![mikrotik13]({{ site.baseurl }}/images/mikrotik13.png)

Setelah reboot kita matikan terlebih dahulu VM nya agar tidak mengulangi langkah langkah tadi.

![mikrotik14]({{ site.baseurl }}/images/mikrotik14.png)

Sebelum dinyalakan kembali, beralih lah ke bagian system lalu pindahkan hardisk ke bagian paling atas pada boot order.

![mikrotik15]({{ site.baseurl }}/images/mikrotik15.png)

Jalankan lagi VM mikrotik dan login dengan user admin lalu tekan enter saja saat ada perintah memasukkan password. Mikrotik telah selesai di install dan siap di konfigurasi. 

![mikrotik16]({{ site.baseurl }}/images/mikrotik16.png)

