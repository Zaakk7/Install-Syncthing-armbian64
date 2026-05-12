# Install Syncthing on Armbian STB HG680P

Install dan setup Syncthing pada STB HG680P / B860H dengan Armbian 64-bit.

## Install

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install syncthing -y
```

---

## Edit GUI Address

Edit config:

```bash
nano /root/.config/syncthing/config.xml
```

Cari:

```xml
<address>127.0.0.1:8384</address>
```

Ganti menjadi:

```xml
<address>0.0.0.0:8384</address>
```

---

## Buat Auto Run Service

```bash
sudo nano /etc/systemd/system/syncthing.service
```

Isi:

```ini
[Unit]
Description=Syncthing
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/bin/syncthing --no-browser --gui-address=0.0.0.0:8384
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

---

## Enable Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable syncthing
sudo systemctl start syncthing
```

Cek status:

```bash
sudo systemctl status syncthing
```

---

## Akses Web GUI

Cari IP device:

```bash
ip addr
```

Buka di browser:

```text
http://IP-STB:8384
```

Contoh:

```text
http://192.168.1.10:8384
```

---

## Notes

- Tested on Armbian 64-bit
- RAM 2GB works fine
- Compatible with CasaOS
- Can be accessed via LAN or mobile hotspot network
