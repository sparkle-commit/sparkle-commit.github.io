<!--more-->

Pertama kita pilih terlebih dahulu interface mana saja yang akan kita buat menjadi bridge. Ubah namanya agar mudah dikenali dengan menambahkan -bridge.

![bridge1]({{ site.baseurl }}/images/bridge1.jpg)

Konfigurasi bridge – Membuat Device bridge

Klik Bridge lalu tekan tombol +

![bridge2]({{ site.baseurl }}/images/bridge2.jpg)

Buatlah sebuah interface bridge bernama Mybridge (misalkan) lalu klik apply, maka ketentuanlain seperti MTU, mac address dll akan terisi otomatis.

![bridge3]({{ site.baseurl }}/images/bridge3.jpg)

Selanjutnya klik Ports lalu klik tanda + untuk memilih interface mana saja yg akan dibuat bridge. pilih ether4 dan ether 5 untuk dijadikan 1 bridge dengan nama Mybridge.

![bridge4]({{ site.baseurl }}/images/bridge4.jpg)

![bridge5]({{ site.baseurl }}/images/bridge5.jpg)

Setelah kita membuat bridge buatlah jaringan pada bridge yang kita buat.

![bridge6]({{ site.baseurl }}/images/bridge6.jpg)

Selanjutnya kita bisa lihat pada saat kita hendak membuat dhcp server maka pilihan interface nya sudah terdapat Mybridge.

![bridge7]({{ site.baseurl }}/images/bridge7.jpg)

Teruskan ketentuan membuat dhcp server. Buat pool ip nya mulai dari 20-50. Dhcp server untuk interface Mybridge pu selesai dibuat.

![bridge8]({{ site.baseurl }}/images/bridge8.jpg)

coba uji coba ke client dengan sambungkan ke ether4 atau ether5 maka client akan mendapatkan ip dari rentang 172.16.1.20 - 172.16.1.50. 

![bridge9]({{ site.baseurl }}/images/bridge9.jpg)
