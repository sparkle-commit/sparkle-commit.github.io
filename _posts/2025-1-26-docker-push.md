---
title: 'Docker Push'
author: sparkle-commit
layout: post
---
![docker1]({{ site.baseurl }}/images/docker1.png)

Apa itu Docker Hub?

Docker Hub adalah layanan penyimpanan repositori image Docker yang memungkinkan Anda untuk:
1. Menyimpan image secara publik atau privat.
2. Berbagi image dengan tim atau komunitas.
3. Menggunakan image yang sudah tersedia untuk mempercepat pengembangan aplikasi.

Mengapa Perlu Push Image ke Docker Hub?
1. Distribusi: Memudahkan berbagi image dengan tim atau publik.
2. Aksesibilitas: Image dapat diakses dari mana saja selama ada koneksi internet.
3. CI/CD: Mendukung pipeline Continuous Integration/Continuous Deployment.

Jika belum memiliki akun Docker, kita bisa mendaftar terlebih dahulu ke hub.docker.com. Jika sudah memiliki username dan password, login dengan perintah docker login.

    $ docker login
