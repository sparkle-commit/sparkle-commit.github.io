---
title: 'Membuat Bridge di Mikrotik'
author: sparkle-commit
layout: post
permalink: /make-a bridge-on mikrotik/
dsq_thread_id:
  - 1204965956
categories:
  - Network
  - Mikrotik
---

<img src="{{ site.baseurl }}/images/bridge0.png" width="300" height="168" alt="Bridge Image">

<!--more-->

## BRIDGE
● Digunakan untuk menggabungkan dua interface yang berbeda.

● Bridge bekerja pada layer data link, sehingga device tidak harus memiliki IP address.

● Bridge akan membagi jaringan menjadi beberapa segmen.

● Pembagian segmen berdasarkan MAC address jaringan yang terhubung ke setiap interface/port dari router.

● Pembagian ini berdasarkan ARP table.

### Cara membuat bridge:

Pertama kita pilih terlebih dahulu interface mana saja yang akan kita buat menjadi bridge. Ubah namanya agar mudah dikenali dengan menambahkan -bridge.

![bridge1]({{ site.baseurl }}/images/bridge1.png)

Konfigurasi bridge – Membuat Device bridge

Klik Bridge lalu tekan tombol +

![bridge2]({{ site.baseurl }}/images/bridge2.png)

Buatlah sebuah interface bridge bernama Mybridge (misalkan) lalu klik apply, maka ketentuanlain seperti MTU, mac address dll akan terisi otomatis.

![bridge3]({{ site.baseurl }}/images/bridge3.png)

Selanjutnya klik Ports lalu klik tanda + untuk memilih interface mana saja yg akan dibuat bridge. pilih ether4 dan ether 5 untuk dijadikan 1 bridge dengan nama Mybridge.

![bridge4]({{ site.baseurl }}/images/bridge4.png)

![bridge5]({{ site.baseurl }}/images/bridge5.png)

Setelah kita membuat bridge buatlah jaringan pada bridge yang kita buat.

![bridge6]({{ site.baseurl }}/images/bridge6.png)

Selanjutnya kita bisa lihat pada saat kita hendak membuat dhcp server maka pilihan interface nya sudah terdapat Mybridge.

![bridge7]({{ site.baseurl }}/images/bridge7.png)

Teruskan ketentuan membuat dhcp server. Buat pool ip nya mulai dari 20-50. Dhcp server untuk interface Mybridge pu selesai dibuat.

![bridge8]({{ site.baseurl }}/images/bridge8.png)

coba uji coba ke client dengan sambungkan ke ether4 atau ether5 maka client akan mendapatkan ip dari rentang 172.16.1.20 - 172.16.1.50. 

![bridge9]({{ site.baseurl }}/images/bridge9.png)
