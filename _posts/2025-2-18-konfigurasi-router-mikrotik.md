---
title: 'Konfigurasi Dasar Mikrotik OS'
author: sparkle-commit
layout: post
permalink: /basic-config-mikrotik-os/
dsq_thread_id:
  - 1204965956
categories:
  - Network
  - Mikrotik
---

<img src="{{ site.baseurl }}/images/conf0.jpg" width="300" height="168" alt="Configuration Image">

<!--more-->
# Konfigurasi Dasar Mikrotik RouterOS

MikroTik RouterOS adalah sistem operasi berbasis Linux yang banyak digunakan untuk manajemen jaringan, baik dalam skala kecil maupun besar. Agar dapat berfungsi optimal, router MikroTik memerlukan konfigurasi dasar yang mencakup pengaturan alamat IP, gateway, NAT, firewall, dan manajemen pengguna. Dokumentasi ini bertujuan untuk memberikan panduan langkah demi langkah dalam melakukan konfigurasi dasar pada router MikroTik, baik untuk keperluan jaringan SOHO maupun skala lebih besar. Dengan mengikuti panduan ini, pengguna diharapkan dapat memahami konsep dasar konfigurasi jaringan dan mengoptimalkan fungsi router MikroTik sesuai kebutuhan.

### Konfigurasi dengan VM pada Virtual Box
Untuk Mikrotik OS yang belum di konfigurasi kita bisa login terlebih dahulu dengan memasukan user admin dan tekan enter di bagian input password.

![conf1]({{ site.baseurl }}/images/conf1.png)

Setelah itu kita diminta untuk memasukkan password baru untuk user admin (contoh: admin)

![conf2]({{ site.baseurl }}/images/conf2.png)

Selanjutnya kita bisa merubah identitas atau nama router dengan perintah: 

    system identity set name=RouterAlFahri

![conf3]({{ site.baseurl }}/images/conf3.png)

Lalu tambah ip dhcp-client dengan perintah berikut:

    ip dhcp-client add interface=ether1 disabled=no

Lihat hasilnya dengan perintah:

    ip address print

![conf4]({{ site.baseurl }}/images/conf4.png)

Apabila ingin menambah ether 2 & 3 kita bisa menggunakan perintah yang sama.

    ip address add interface=ether2 address=192.168.10.1/24 disable=no
    ip address add interface=ether3 address=192.168.20.1/24 disable=no
    ip address print
    
kita bisa membuat jaringan semau kita (192.168.x.1, x dibuat semau kita)

Apabila kita ingin menghapus suatu ether tertentu kita bisa menggunakan perintah: 

    ip address remove number=2

![conf5]({{ site.baseurl }}/images/conf5.png)

Selain ip, kita juga bisa mengatur dns dengan perintah berikut:

    ip dns set servers=8.8.8.8
    ip dns print

 ![conf6]({{ site.baseurl }}/images/conf6.png)

Selain dengan user admin, kita juga bisa membuat user lain semau kita. Adapun untuk izin akses user ada 3:

full --> admin

read --> cuma bisa melihat konfigurasi

write --> cuma bisa menkonfigurasi

Gunakan perintah berikut:

    user add name=riza group=full password=alfahri

Setelah membuat user baru kembalilah ke mode login dengan klik ctrl + D lalu masuk sebagai user yang telah dibuat tadi. 

![conf7]({{ site.baseurl }}/images/conf7.png)

Apabila ingin menghapus user yang telah kita buat masukan perintah : 

    user remove riza

Maka user akan terhapus.

### Setting DHCP-Server

Selanjutnya kita akan mencoba setting dhcp-server dengan slax OS sebagai client. Sebelumnya kita buat terlebih dahulu ether2 yang akan menjadi gateway dari jaringan dhcp server. 

    ip address add interface=ether2 address=192.168.10.1/24 disable=no

![conf8]({{ site.baseurl }}/images/conf8.png)

Ketikan perintah berikut untuk setting dhcp server:

    ip dhcp-server setup

![conf9]({{ site.baseurl }}/images/conf9.png)

Atur dhcp semau kita mulai dari ether, pool dll 

Apabila setting selesai kita bisa lihat pada slax os yang telah di setting networknya menjadi internal network apakah mendapat ip dari dhcp atau tidak.

![conf10]({{ site.baseurl }}/images/conf10.png)

Coba ping ke gateway dengan perintah:

    ping 192.168.10.1

![conf11]({{ site.baseurl }}/images/conf11.png)

Slax telah bisa ping ke gateway, lalu coba untuk ping ke dns atau 8.8.8.8

![conf12]({{ site.baseurl }}/images/conf12.png)

Ternyata slax belum bisa ping ke DNS, ini berarti kita harus setting firewall atau sharing internet nya. Gunakan perintah berikut:

    ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

![conf13]({{ site.baseurl }}/images/conf13.png)

Coba ping 8.8.8.8 kembali di slax dan slax sukses untuk mendapat dhcp ip dari router mikrotik.

![conf14]({{ site.baseurl }}/images/conf14.png)

Selain konfigurasi Mikrotik RouterOS dengan VM di virtual box kita juga bisa konfigurasi dengan webfig dengan mengakses ip dari mikrotik yang terdapat pada ether1

![conf15]({{ site.baseurl }}/images/conf15.png)

Atau menggunakan Tellnet pada terminal dengan perintah:

    telnet 192.168.4.183

 ![conf16]({{ site.baseurl }}/images/conf16.png)   