![haproxy1]({{ site.baseurl }}/images/haproxy1.png)

<!--more-->
HAProxy digunakan untuk membagi beban trafik antara beberapa server backend yang berjalan di belakangnya. Hal ini berfungsi untuk meningkatkan ketersediaan, skalabilitas, performa, dan keamanan aplikasi ketika diakses.

Pada Tutorial ini, Saya akan memberikan panduan cara install HAProxy sebagai load balancer di Ubuntu. Namun membahas cara install dan konfigurasinya, terlebih dahulu pastikan bahwa kita telah mempersiapkan sistem berikut.

## Persiapan Sistem

Untuk menjalankan metode Load Balancing kali ini, kita akan menggunakan 4 node server atau VPS. 1 server (frontend) bertindak sebagai server load balancer, dan 3 server (backend) berfungsi untuk melayani request atau menampilkan konten permintaan dari client.

Pada tutorial ini, saya menggunakan 4 server dalam virtual box. Berikut persiapan sistem yang akan digunakan:

- OS Linux Ubuntu 24.04 LTS
- 1 Server HAProxy dengan RAM 2 GB : 192.168.4.240 (Load balancer)
- 1 Server Backend1 dengan RAM 2 GB : 192.168.4.241
- 1 Server Backend2 dengan RAM 4 GB : 192.168.4.242
- 1 Server Backend2 dengan RAM 6 GB : 192.168.4.243

## Install dan Konfigurasi HAProxy

Berikut step by step install dan konfigurasi HAProxy yang digunakan sebagai load balancer.
### Step 1. Install Server Backend

Pada tutorial kali ini, kita akan menggunakan apache web server sebagai server backend yang bertugas merespon permintaan client melalui server HAProxy. Berikut langkah instalasi web servernya.

1. Update package pada sistem di masing masing server backend.
 
        apt update && apt-get upgrade -y

2. Install Web Server pada ketiga node dengan perintah:

        sudo apt install apache2

![hp1]({{ site.baseurl }}/images/hp1.png)

![hp2]({{ site.baseurl }}/images/hp2.png)

![hp3]({{ site.baseurl }}/images/hp3.png)

3. Setelah melakukan instalasi, pastikan bahwa web server telah running atau belum dengan perintah berikut.

        sudo systemctl status apache2

![hp4]({{ site.baseurl }}/images/hp4.png)

![hp5]({{ site.baseurl }}/images/hp5.png)

![hp6]({{ site.baseurl }}/images/hp6.png)

4. Modifikasi file websit
e pada masing-masing backend, dengan melakukan edit pada direktori /var/www/html.

#### Server backend1

        sudo nano /var/www/html/index.html

![hp7]({{ site.baseurl }}/images/hp7.png)

#### Server backend2

        sudo nano /var/www/html/index.html

![hp8]({{ site.baseurl }}/images/hp8.png)

#### Server backend3

        sudo nano /var/www/html/index.html

![hp9]({{ site.baseurl }}/images/hp9.png)

5. Setelah melakukan modifikasi pada konten, maka kita akan lakukan restart untuk service web servernya dengan perintah berikut.

        sudo systemctl restart apache2
        sudo systemctl status apache2
        
6. Jika layanan web server telah berjalan dengan baik, maka kita dapat melakukan tes akses pada server backend. Pastikan menampilkan konten masing masing sesuai servernya.

- Akses ke webserver 1 dengan IP 192.168.4.241

![hp10]({{ site.baseurl }}/images/hp10.png)

- Akses ke webserver 2 dengan IP 192.168.4.242

![hp11]({{ site.baseurl }}/images/hp11.png)

- Akses ke webserver 3 dengan IP 192.168.4.243

![hp12]({{ site.baseurl }}/images/hp12.png)

### Step 2. Install HAProxy sebagai Load Balancer

Berikut adalah cara install HAProxy sebagai server load balancer di Ubuntu 24.04.

1. Instalasi HAProxy 

        sudo apt install haproxy -y

![hp13]({{ site.baseurl }}/images/hp13.png)

2. Konfigurasi awal untuk HAProxy

Haproxy memiliki file konfigurasi default pada file /etc/haproxy/haproxy.cfg.

- Pada section global berikut berisi tentang konfigurasi untuk SSL, informasi akses log, dan grup user untuk menjalankan HAProxy.

        global
                log /dev/log    local0
                log /dev/log    local1 notice
                chroot /var/lib/haproxy
                stats socket /run/haproxy/admin.sock
                 mode 660 level admin expose-fd listeners
                stats timeout 17s

        # user dan group Haproxy
            user haproxy
              group haproxy
              daemon               

        # Lokasi ssl yang dimiliki, diatur sesuai path
             ca-base /etc/ssl/certs
             crt-base /etc/ssl/private

        # Bagian ssl cipher untuk enkripsi
                 ssl-default-bind-ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:!aNULL:!MD5:!DSS
                ssl-default-bind-options no-sslv3

- Pada section default, berisi tentang nilai konfigurasi dari berbagai node. Kita dapat melakukan custom pada bagian nilai dan halaman error.

        defaults
                 log     global
                 mode    http
                 option  httplog
                 option  dontlognull
                 timeout connect 11s
                 timeout client  7s
                 timeout server  4s
                 timeout http-request 15s
                 errorfile 400 /etc/haproxy/errors/400.http
                 errorfile 403 /etc/haproxy/errors/403.http
                 errorfile 408 /etc/haproxy/errors/408.http
                 errorfile 500 /etc/haproxy/errors/500.http
                 errorfile 502 /etc/haproxy/errors/502.http
                 errorfile 503 /etc/haproxy/errors/503.http
                 errorfile 504 /etc/haproxy/errors/504.http

Keterangan kode:

1. Bagian mode, digunakan untuk menentukan metode load balancing, apakah kita menggunakan metode tcp atau http.
2. Bagian timeout, berisi tentang penyesuaian transfer data, bagaimana waktu koneksi antar server diatur.
3. Timeout connect : waktu yang diperlukan Haproxy untuk membuat koneksi dengan Server backend.
4. Timeout client  : delay yang diperlukan client untuk mengirim data ke server.
5. Timeout server : waktu tunggu server untuk mengirim data.
6. Timeout http-request : waktu tunggu client mengirimkan response http secara lengkap.

- Pada Section Frontend, menjelaskan bagaimana akses ke load balancer,  ketika akses maka permintaan akan diteruskan kepada server backend.

        frontend my_frontend
                bind *:80
                mode http
                default_backend my_backend 

Note : kita dapat menyesuaikan nama pada parameter load balancing, penamaan harus sesuai dengan node yang dipanggil.

- Pada section Backend, kota dapat mengatur node server yang akan menjadi target load balancing, seperti pada contoh berikut.

        backend my_backend
                mode http
                balance roundrobin
                option forwardfor
                http-request set-header X-Forwarded-Port %[dst_port]
                http-request add-header X-Forwarded-Proto https if { ssl_fc }
                option httpchk HEAD / HTTP/1.1rnHost:localhost
                server backend1 192.168.4.241:80
                server backend2 192.168.4.242:80
                server backend3 192.168.4.243:80

Keterangan kode:

1. Bagian backend, dinamai sesuai nama yang dipanggil pada frontend.
2. Balance roundrobin berarti kita akan menggunakan metode load balancing round robin, dimana setiap request dikirimkan bergantian ke seluruh server node yang ada.
3. HTTP request berarti kita akan meneruskan permintaan ke server backend.
4. Server adalah node server target load balancing, kita dapat mengisi ip address dan jumlah server yang kita miliki, pada panduan ini kita akan menggunakan 2 server sebagai backend.

Note: kita dapat mengubah algoritma loadbalancing sesuai dengan metode loadbalancing apa yang kita mau.

- Pada section selanjutnya, kita akan membuat kode untuk akses ke halaman statistik Haproxy.

        listen monitoring 
                bind  *:8080
                stats enable
                stats hide-version
                stats refresh 10s
                stats show-node
                stats auth username:password
                stats uri /monitoring

Note: kita dapat mengisi username dan password sesuai dengan yang kita inginkan.

Semua section telah selesai diinputkan, berikut adalah hasil akhir dari konfigurasi yang ada di file /etc/haproxy/haproxy.cfg.

![hp14]({{ site.baseurl }}/images/hp14.png)

![hp15]({{ site.baseurl }}/images/hp15.png)

![hp16]({{ site.baseurl }}/images/hp16.png)


Simpan file dan restart layanan HAProxy.


        systemctl start haproxy
        systemctl enable haproxy
        sudo systemctl restart haproxy


## Pengujian Load Balancer

Akses ke server load balancer dengan ip 192.168.4.240:80 maka akan menampilkan konten dari server 1,2 dan 3 secara bergantian.

![hp17]({{ site.baseurl }}/images/hp17.png)

Saat diakses menampilkan server backend 1, dan ketika di refresh pada browser akan dialihkan ke server backend ke 2 dan 3.

![hp18]({{ site.baseurl }}/images/hp18.png)

![hp19]({{ site.baseurl }}/images/hp19.png)


Untuk memastikan load balancer bekerja dengan baik, kita dapat menjalankan curl seperti berikut:

        curl -I http://192.168.4.240

![hp20]({{ site.baseurl }}/images/hp20.png)

Kita juga dapat mengakses halaman statistik HAProxy pada http://192.168.4.240:8081/stats

Login dengan username dan password yang telah dibuat sebelumnya.

![hp21]({{ site.baseurl }}/images/hp21.png)


Proses instalasi dan konfigurasi haproxy telah selesai. Selanjutnya apabila kita ingin menguji pembagian beban oleh loadbalancer dengan beban yang tinggi kita bisa gunakan tools seperti Apache Benmark dll. 
