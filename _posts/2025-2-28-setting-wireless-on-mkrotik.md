---
title: 'Membuat Wireless di Mikrotik'
author: sparkle-commit
layout: post
permalink: /make-a wireless-on mikrotik/
dsq_thread_id:
  - 1204965956
categories:
  - Network
  - Mikrotik
---

<img src="{{ site.baseurl }}/images/wire0.jpg" width="300" height="168" alt="Wireless Image">

<!--more-->

MikroTik adalah salah satu perangkat jaringan yang banyak digunakan untuk mengelola koneksi internet, baik dalam skala kecil maupun besar. Salah satu fitur unggulan yang dimiliki oleh MikroTik adalah kemampuannya untuk berfungsi sebagai access point (AP) dalam jaringan wireless. Dengan menggunakan perangkat MikroTik yang dilengkapi dengan modul Wi-Fi, kita dapat membangun jaringan nirkabel yang handal dan efisien.

Dalam tutorial ini, kita akan membahas langkah-langkah untuk membuat jaringan wireless menggunakan MikroTik. Tujuan utama dari konfigurasi ini adalah untuk memberikan akses jaringan kepada pengguna melalui koneksi nirkabel dengan keamanan yang terjamin.

Manfaat Membuat Wireless di MikroTik

- Fleksibilitas Jaringan – Pengguna dapat mengakses internet tanpa perlu kabel fisik, sehingga lebih praktis.

- Efisiensi Biaya – Tidak perlu menarik kabel LAN ke setiap perangkat pengguna.

- Kemudahan Manajemen – MikroTik memiliki fitur yang memudahkan administrator dalam mengelola pengguna dan bandwidth.

- Keamanan Terjamin – Dapat menerapkan berbagai metode keamanan seperti WPA2, MAC Filtering, dan isolasi klien.

Perangkat yang Dibutuhkan:

Sebelum memulai konfigurasi, pastikan Anda memiliki perangkat berikut:

1. Router MikroTik dengan interface wireless (misalnya RB951Ui-2HnD, hAP Lite, atau sejenisnya)

2. Koneksi internet (optional, untuk konfigurasi hotspot)

3. Akses ke WinBox atau terminal MikroTik

4. Gambaran Konfigurasi

Beberapa hal yang akan kita lakukan dalam konfigurasi jaringan wireless ini meliputi:

- Mengaktifkan interface wireless pada MikroTik.

- Mengonfigurasi SSID dan mode wireless.

- Mengatur enkripsi dan keamanan jaringan.

- Menetapkan DHCP server agar klien mendapatkan IP otomatis.

- Menguji koneksi untuk memastikan jaringan berjalan dengan baik.

Dengan mengikuti tutorial ini, diharapkan Anda dapat memahami bagaimana cara membangun dan mengelola jaringan wireless menggunakan MikroTik secara efektif. Mari kita mulai dengan langkah pertama!

### Langkah-langkah:

Pertama kita aktifkan terlebih dahulu interface wlan yang akan kita gunakan dengan klik icon ceklist.

![wire1]({{ site.baseurl }}/images/wire1.png)

Selain dari menu Interface kita juga bisa setting wireless dari menu Wireless.

![wire2]({{ site.baseurl }}/images/wire2.png)

Selanjutnya klik 2 kali interface yang akan kita atur. Lalu pilih wireless. Atur mode, SSID, dan frekuensinya. 

![wire3]({{ site.baseurl }}/images/wire3.png)

Untuk frekuensi kita bisa pilih frekuensi yang paling tinggi dengan melihatnya di freq.usage.Klik start untuk memulainya.

![wire4]({{ site.baseurl }}/images/wire4.png)

Apabila kita ingin memilih frekuensi secara otomatis maka pilih auto.

Klik apply lalu Ok. Interface untuk wlan1 telah berhasil dibuat. 

![wire5]({{ site.baseurl }}/images/wire5.png)

Langkah selanjutnya adalah berikan ip pada interface wlan kita dengan pilih menu IP lalu Addresses lalu klik icon +. Buat Ip dan network nya lalu pilih interface nya yaitu wlan1. KLik apply lalu OK dan interface untuk wireless kita telah memiliki ip. 

![wire6]({{ site.baseurl }}/images/wire6.png)

![wire7]({{ site.baseurl }}/images/wire7.png)

Langkah selanjutnya adalah membuat DHCP server agar wireless dapat diakses oleh client. Klik menu ip lalu dhcp server lalu dhcp setup. Buat dengan ketentuan sebagai berikut:

1. Interface: wlan1

2. DHCP Address Space: 10.10.10.0/24

3. Gateway: 10.10.10.1

4. DHCP pool: 10.10.10.2/24-10.10.10.254/24

5. DHCP relay: 10 menit

Klik finish dan dhcp server untuk interface wlan1 telah dibuat. Tes dengan klien apakah mendapatkan ip di jaringan 10.10.10.0/24 atau tidak.

![wire8]({{ site.baseurl }}/images/wire8.png)

Kita bisa saja menambahkan security atau password ke wireless kita. Caranya yang pertama kita harus membuat security profile terlebih dahulu. Klik wireless lalu security profile. 

Klik icon + lalu setting dengan:

Nama: verguso

Mode: dynamic keys

Authentication type: WPA PSK & WPA2 PSK

lalu buat passwordnya juga. Klik apply lalu OK. Security profile telah dibuat.

![wire9]({{ site.baseurl }}/images/wire9.png)

Kita bisa menggunakan security yang kita buat dengan mengaturnya di konfigurasi wireless tadi. Atur security nya menjadi security profile yang kita buat.  

![wire10]({{ site.baseurl }}/images/wire10.png)
