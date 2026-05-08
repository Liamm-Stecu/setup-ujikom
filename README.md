# 🚀 Debian Server Setup Guide

> Bahan bahan wget: `172.16.51.199 atau 172.16.51.99`

---

# 👤 Setup User Debian

Membuat user baru:

```bash
adduser nama_user
```

---

# 🔐 SSH via CMD Windows

Login SSH:

```bash
ssh user@IP_DEBIAN
```

Contoh:

```bash
ssh marcel@172.16.51.199
```

Jika error SSH key:

```bash
ssh-keygen -R 172.16.51.199
```

Lalu coba SSH ulang.

---

# 🌐 Setup Webmin

## 1. Download Webmin

```bash
wget LINK_WEBMIN
```

## 2. Install Package

```bash
dpkg -i nama_file.deb
```

## 3. Jika Dependency Error

```bash
apt install -f
```

## 4. Akses Webmin

Buka browser:

```txt
https://IP_DEBIAN:10000
```

Contoh:

```txt
https://172.16.51.199:10000
```

---

# 🖥️ Setup Apache + MariaDB + PHP-FPM

## Install Package

```bash
apt install apache2 mariadb-server php-fpm -y
```

## Aktifkan Module Proxy

```bash
a2enmod proxy_fcgi
```

## Aktifkan PHP-FPM

```bash
a2enconf php8.4-fpm
```

## Restart Apache

```bash
systemctl restart apache2
```

---

# 🔒 Setup SSL HTTPS Apache

## Aktifkan Module SSL

```bash
a2enmod ssl
```

## Buat Folder SSL

```bash
mkdir ssl
```

## Masuk ke Folder SSL

```bash
cd ssl
```

## Generate SSL Key & Certificate

```bash
openssl req -x509 -nodes -days 90 -newkey rsa:2048 \
-keyout self.key \
-out self.crt
```

## Cek Isi Folder

```bash
ls
```

Pastikan ada file:

```txt
self.key
self.crt
```

---

# ⚙️ Konfigurasi SSL Apache

Edit file SSL config:

```bash
nano /etc/apache2/sites-available/000-default-ssl.conf
```

Cari bagian ini:

```apache
SSLCertificateFile /etc/apache2/ssl/selfsigned.crt
SSLCertificateKeyFile /etc/apache2/ssl/selfsigned.key
```

Ubah sesuai lokasi file SSL yang tadi dibuat.

Contoh:

```apache
SSLCertificateFile /root/ssl/self.crt
SSLCertificateKeyFile /root/ssl/self.key
```

---

# ✅ Aktifkan SSL Site

```bash
a2ensite default-ssl.conf
```

Reload Apache:

```bash
systemctl reload apache2
```

Jika reload error:

```bash
systemctl start apache2
```

---

# 📊 Setup Prometheus

## Install Prometheus + Node Exporter

```bash
apt install prometheus prometheus-node-exporter -y
```

## Akses Prometheus

```txt
http://IP_DEBIAN:9090
```

Contoh:

```txt
http://172.16.51.199:9090
```

---

# 📈 Setup Grafana

## Download Grafana

```bash
wget LINK_GRAFANA
```

## Install Grafana

```bash
dpkg -i nama_file_grafana.deb
```

## Enable Grafana

```bash
systemctl enable grafana-server
```

## Restart Grafana

```bash
systemctl restart grafana-server
```

## Akses Grafana

```txt
http://IP_DEBIAN:3000
```

Contoh:

```txt
http://172.16.51.199:3000
```

---

# 🛠️ Port Service

| Service | Port |
|----------|------|
| Apache HTTP | 80 |
| Apache HTTPS | 443 |
| Webmin | 10000 |
| Prometheus | 9090 |
| Grafana | 3000 |

---
