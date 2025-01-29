---
title: 'Install Minicube #1 Notes'
author: sparkle-commit
layout: post
permalink: /ins-min-notes/
dsq_thread_id:
  - 1204965956
categories:
  - Poker
---

![minikube1]({{ site.baseurl }}/images/minikube1.png)

Minikube adalah sebuah alat yang memungkinkan kita dapat menjalankan Kubernetes secara lokal. Minikube menjalankan kluster Kubernetes lokal dalam satu node atau multi-node di komputer pribadi (termasuk Windows, macOS, dan Linux) sehingga kita dapat mencoba Kubernetes atau menggunakannya untuk pengembangan sehari-hari.
Minikube adalah Kubernetes lokal yang berfokus pada kemudahan belajar dan pengembangan untuk Kubernetes.

Yang dibutuhkan hanyalah Docker (atau container yang kompatibel) atau lingkungan Virtual Machine, dan Kubernetes dapat dijalankan hanya dengan satu perintah:

    minikube start

Yang dibutuhkan (Menurut dokumentasi):
1. 2 CPU atau lebih
2. 2GB memori bebas
3. 20GB ruang penyimpanan bebas
4. Koneksi internet
5. Pengelola container atau virtual machine seperti: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, atau VMware Fusion/Workstation

### a. Instalasi Minikube 

Pada tutorial ini, kita akan mencoba mneginstal minikube dengan menggunakan binary. Jadi, kita akan menginstalnya dengan curl. Sebelumnya pastikan terlebih dahulu apakah dalam komputer local kita sudah terdapat paket curl atau belum. Jika belum kita dapat menginstallnya terlebih dahulu dengan perintah berikut:
    
    sudo apt install curl
![minikube2]({{ site.baseurl }}/images/minikube2.png)

Untuk menginstal versi stabil terbaru Minikube di Linux x86-64 menggunakan unduhan biner:

    curl -LO https://github.com/kubernetes/minikube/releases
    /latest/download/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin
    /minikube && rm minikube-linux-amd64

![minikube3]({{ site.baseurl }}/images/minikube3.png)

Tunggulah hingga proses download selesai. Apabila proses download selesai, maka minikube akan secara otomatis tersimpan dalam direktori /usr/local/bin.

![minikube4]({{ site.baseurl }}/images/minikube4.png)

### b. Memulai Cluster

Dari terminal dengan akses administrator (tetapi tidak masuk sebagai root), jalankan perintah berikut:

    minikube start

Jika Minikube gagal memulai, lihat halaman drivers untuk bantuan dalam mengatur pengelola container atau virtual machine yang kompatibel.

![minikube5]({{ site.baseurl }}/images/minikube5.png)

![minikube6]({{ site.baseurl }}/images/minikube6.png)

![minikube7]({{ site.baseurl }}/images/minikube7.png)

Proses ini akan memakan waktu beberapa saat. Tunggu hingga proses selesai. Setelah proses selesai kita jalankan sekali lagi perintah tersebut dan minikube telah berhasil di install.

![minikube8]({{ site.baseurl }}/images/minikube8.png)

Minikube yang telah terinstall dan telah di jalankan akan kelihatan running di virtual box yang ada di komputer local.

![minikube9]({{ site.baseurl }}/images/minikube9.png)
