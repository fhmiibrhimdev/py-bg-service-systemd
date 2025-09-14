# Python Background Service (Systemd)

### 1. Install Python 3 LTS (misalnya Python 3.10 atau 3.12)
Ubuntu/Debian-based systems:
```bash
sudo apt update
sudo apt install -y python3 python3-pip
```
Verifikasi versi:
```bash
python3 --version
```

### 2. Install Library Python
Buat virtual environment (opsional tapi disarankan):
```bash
python3 -m venv /path/your/folder/venv
source /path/your/folder/venv/bin/activate
pip install requests paho-mqtt
```

### 3. File systemd (Update)
Edit atau buat file baru:
```bash
sudo nano /etc/systemd/system/project-name.service
```
Isi dengan:
```bash
[Unit]
Description=RFID Automation Service
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/var/www/projects/python/
ExecStart=/path/your/folder/venv/bin/python /path/your/folder/project-name.py
Restart=always
RestartSec=5
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
```

### 4. Reload dan Jalankan Service
```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable rfid-automation.service
sudo systemctl start rfid-automation.service
```

### 5. Cek Service
```bash
sudo systemctl status rfid-automation.service
```
Log output (real-time):
```bash
journalctl -u rfid-automation.service -f
```
Kalau kamu tidak ingin pakai virtualenv, cukup ganti ExecStart= jadi:
```bash
ExecStart=/usr/bin/python3 /path/your/folder/project-name.py
```
