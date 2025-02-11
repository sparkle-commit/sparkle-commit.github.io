---
title: 'Install Kubectl'
author: sparkle-commit
layout: post
permalink: /install-kubectl/
dsq_thread_id:
  - 1204965956
categories:
  - Devops
  - Kubernetes
---

![kubectl1]({{ site.baseurl }}/images/kubectl1.png)

<!--more-->
kubectl adalah command-line tool untuk berinteraksi dengan Kubernetes. Dengan kubectl, kamu bisa melakukan berbagai operasi seperti deploy aplikasi, mengelola resource cluster, dan melakukan debugging.

## Menginstal kubectl Binary dengan curl di Linux

## 1. Unduh rilis terbaru dengan perintah:

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io
    /release/stable.txt)/bin/linux/amd64/kubectl"

![kubectl2]({{ site.baseurl }}/images/kubectl2.png)

 Catatan:   
Untuk mengunduh versi tertentu, ganti bagian $(curl -L -s https://dl.k8s.io/release/stable.txt) pada perintah dengan versi spesifik.

Sebagai contoh, untuk mengunduh versi 1.32.0 di Linux x86-64, ketik:

    curl -LO https://dl.k8s.io/release/v1.32.0/bin/linux/amd64/kubectl

## 2. Validasi Binary (Opsional)

Unduh file checksum untuk memverifikasi integritas binary kubectl:   

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io
    /release/stable.txt)/bin/linux/amd64/kubectl.sha256"

![kubectl3]({{ site.baseurl }}/images/kubectl3.png)

Validasi binary kubectl terhadap file checksum dengan perintah berikut:

    echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

![kubectl4]({{ site.baseurl }}/images/kubectl4.png)

Jika valid, outputnya akan menampilkan:

    kubectl: OK

Jika pemeriksaan gagal, sha256sum akan keluar dengan status nonzero dan mencetak output seperti berikut:

    kubectl: FAILED
    sha256sum: WARNING: 1 computed checksum did NOT match

Unduh versi yang sama dari binary kubectl dan file checksum. 

## 3. Install kubectl

    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

![kubectl5]({{ site.baseurl }}/images/kubectl5.png)

Jika Anda tidak memiliki akses root pada sistem target, Anda masih bisa menginstal kubectl ke direktori ~/.local/bin dengan perintah berikut:

    chmod +x kubectl
    mkdir -p ~/.local/bin
    mv ./kubectl ~/.local/bin/kubectl
    Tambahkan ~/.local/bin ke dalam variabel PATH

Jika ~/.local/bin belum ada di dalam PATH, kamu bisa menambahkannya dengan perintah berikut:

-Menambahkan di akhir PATH:
    
    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

-Menambahkan di awal PATH (untuk memastikan prioritas lebih tinggi):

    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

Untuk menguji dan memastikan bahwa versi kubectl yang telah Anda instal adalah versi terbaru, jalankan perintah berikut:

    kubectl version --client

![kubectl6]({{ site.baseurl }}/images/kubectl6.png)

Untuk mendapatkan tampilan lebih rinci mengenai versi kubectl yang terinstal, Anda dapat menggunakan perintah berikut:

    kubectl version --client --output=yaml

![kubectl7]({{ site.baseurl }}/images/kubectl7.png)
