# WebCL.ProxyCores
Для подготовки Linux-системы (например, Debian, Ubuntu, Arch, Armbian и др.) под **скачивание, сборку и установку** всех перечисленных прокси-ядер, потребуется:

---

## ✅ Универсальные шаги подготовки системы

### 1. Обновление системы

```bash
# Debian/Ubuntu/Armbian
sudo apt update && sudo apt upgrade -y

# Arch
sudo pacman -Syu --noconfirm
```

---

### 2. Установка общих зависимостей

```bash
# Debian/Ubuntu/Armbian
sudo apt install -y curl wget unzip tar git build-essential cmake pkg-config golang clang protobuf libssl-dev

# Arch Linux
sudo pacman -S --noconfirm curl wget unzip tar git base-devel cmake pkgconf go clang protobuf openssl
```

---

### 3. Создание рабочего каталога

```bash
sudo mkdir -p /opt/proxycores/cores
sudo mkdir -p /opt/proxycores/conf.d
sudo chown -R $(whoami) /opt/proxycores
```

---

## 🔧 Подготовка для каждого ядра:

---

### 1. **brook**

📦 Go-программа (можно скачать бинарник или собрать)

```bash
# Сборка вручную
git clone https://github.com/txthinking/brook.git
cd brook
go build -o brook
mv brook /opt/proxycores/cores/brook
```

📥 Или просто:

```bash
wget -O /opt/proxycores/cores/brook https://github.com/txthinking/brook/releases/latest/download/brook-linux-amd64
chmod +x /opt/proxycores/cores/brook
```

---

### 2. **hysteria2**

📦 Go-программа

```bash
wget -O hysteria https://github.com/apernet/hysteria/releases/latest/download/hysteria-linux-amd64
chmod +x hysteria && mv hysteria /opt/proxycores/cores/hysteria
```

---

### 3. **juicity**

📦 Rust-программа (server и client)

```bash
# Установка Rust
curl https://sh.rustup.rs -sSf | sh

# Сборка
git clone https://github.com/juicity/juicity.git
cd juicity
cargo build --release
cp target/release/juicity-client /opt/proxycores/cores/juicity-client
cp target/release/juicity-server /opt/proxycores/cores/juicity-server
```

📥 Или скачать:

```bash
wget https://github.com/juicity/juicity/releases/latest/download/juicity-client-linux-amd64
chmod +x juicity-client-linux-amd64
mv juicity-client-linux-amd64 /opt/proxycores/cores/juicity-client
```

---

### 4. **mihomo-core** (форк sing-box)

📦 Go-программа

```bash
wget https://github.com/MetaCubeX/mihomo/releases/latest/download/mihomo-linux-amd64
chmod +x mihomo-linux-amd64
mv mihomo-linux-amd64 /opt/proxycores/cores/mihomo
```

---

### 5. **naiveproxy**

📦 Требует Chromium toolchain и GN/Ninja

```bash
# Установка зависимостей
sudo apt install -y python3 python3-pip nodejs gn ninja-build

git clone https://github.com/klzgrad/naiveproxy.git
cd naiveproxy/src
./get_toolchain.py
./build.sh
cp out/Release/naive /opt/proxycores/cores/naiveproxy
```

📥 Альтернатива:

```bash
wget https://github.com/klzgrad/naiveproxy/releases/latest/download/naiveproxy-linux-x64.tar.xz
tar -xf naiveproxy-linux-x64.tar.xz
mv naiveproxy /opt/proxycores/cores/naiveproxy
```

---

### 6. **OverTLS**

📦 Go-программа

```bash
wget https://github.com/zhenorzz/OverTLS/releases/latest/download/overtls-linux-amd64
chmod +x overtls-linux-amd64
mv overtls-linux-amd64 /opt/proxycores/cores/overtls
```

---

### 7. **sing-box-core**

📦 Go-программа

```bash
wget https://github.com/SagerNet/sing-box/releases/latest/download/sing-box-linux-amd64
chmod +x sing-box-linux-amd64
mv sing-box-linux-amd64 /opt/proxycores/cores/sing-box
```

---

### 8. **tuic**

📦 Rust-программа (v2)

```bash
git clone https://github.com/EAimTY/tuic.git
cd tuic
cargo build --release
cp target/release/tuic-server /opt/proxycores/cores/tuic-server
cp target/release/tuic-client /opt/proxycores/cores/tuic-client
```

📥 Или скачать релиз:

```bash
wget https://github.com/EAimTY/tuic/releases/latest -O tuic.tar.gz
# ручная распаковка и перенос
```

---

### 9. **v2fly / v2ray-core**

📦 Go-программа

```bash
wget https://github.com/v2fly/v2ray-core/releases/latest/download/v2ray-linux-64.zip
unzip v2ray-linux-64.zip
mv v2ray /opt/proxycores/cores/v2ray
chmod +x /opt/proxycores/cores/v2ray
```

---

### 10. **xray-core**

📦 Go-программа

```bash
wget https://github.com/XTLS/Xray-core/releases/latest/download/Xray-linux-64.zip
unzip Xray-linux-64.zip
mv xray /opt/proxycores/cores/xray
chmod +x /opt/proxycores/cores/xray
```

---

## 📁 Результат

После всех действий в каталоге `/opt/proxycores/cores/` вы получите:

```
brook
hysteria
juicity-client
juicity-server
mihomo
naiveproxy
overtls
sing-box
tuic-server
tuic-client
v2ray
xray
```

