# setup-ujikom
langkah langkah setup ujikom

// 172.16.51.199 (access browser jeng bahan bahan na)

-- setup user di Debian 
adduser nama (buat user baru)

-- ssh cmd
ssh user@ip Debian (ssh via cmd windows)
ssh-keygen -R (kalo error jalankan ini + ssh ulang)

-- setup webmin
1. wget (install via link website)
2. dpkg -i (unpackinh file)
3. apt install -f (mun error)
4. access browser ip Debian:10000

- setup server
1. apt install apache2 MariaDB-server php-fpm -y (install paket)
2. a2enmod proxy_fcgi (aktifkan modul proxy)
3. a2enconf php8.4-fpm (aktifkan modul php-fpm)

-- setup ssl (meh bisa https)
1. a2enmod ssl (aktifkan modul ssl)
2. mkdir ssl (buat folder ssl)
3. cd ssl (masuk ke folder ssl)
4. openssl req -x509 -nodes -days 90 -newkey rsa:2048 -keyout self.key -out self.crt (setup key ssl)
5. ls (cek isi directory yang kita masuki / cd, kalo ada file self.key dan self.crt berati di sana si key ssl nya)
6. nano /etc/apache2/sites-available/000-default-ssl.conf (edit file ssl.conf)
	- di 000_default-ssl.conf
	cari dan edit ini sesuai directory dimana kita tadi setup key ssl (contoh karna tadi kita setup nya di file /root/ssl di no 3 dan 4)
	    SSLCertificateFile /etc/apache2/ssl/selfsigned.crt     // ubah ke directory dimana kita setup key ssl (no 3 dan 4) /root/ssl/self.crt
    	    SSLCertificateKeyFile /etc/apache2/ssl/selfsigned.key  // ubah ke direcroty dimana kita setup key ssl (no 3 dan 4) /root/ssl/self.key


7. a2ensite default-ssl.conf (aktifkan modul ssl.conf)
8. systemctl reload apache2 (ngereload apache)
	- Lamun error te bisa di reload
	1. systemctl start apache2

-- setup prometheus
1. apt install Prometheus prometheus-node-exporter (install paket)
2. access browser ip debian:9090

-- setup Grafana
1. wget (download Grafana via link)
2. dpkg -i (unpacking Grafana)
3. systemctl enable grafana-server (membolehkan Grafana aktif)
4. systemctl restart Grafana-server  (merestart Grafana)
5. access browser ip Debian:3000


