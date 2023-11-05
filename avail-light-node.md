# <h1 align="center">Avail Light Node Kurulumu</h1>
![availproject](https://github.com/mulosbron/BlockchainNodeRehberleri/assets/91866065/104abc83-017f-4214-88b8-84751cf075f4)

## Linkler:
 * [Avail Resmi Websitesi](https://www.availproject.org/)
 * [Avail Resmi Twitter](https://twitter.com/AvailProject)
 * [Avail Resmi Discord](https://discord.gg/kkHAXZCNZa)
 * [Avail Light Node Dökümantasyon](https://docs.availproject.org/operate/node/light-client/)
 * [Avail Light Node Form](https://docs.google.com/forms/d/e/1FAIpQLSeL6aXqz6vBbYEgD1cZKaQ4vwbN2o3Rxys-wKTuKySVR-oS8g/viewform)

## Minimum sistem gereksinimleri

* 4GB RAM

* 2 core CPU (amd64/x86 architecture)

* 20-40 GB SSD

## Başlangıç
```
sudo su

cd

sudo apt update && sudo apt upgrade -y

sudo apt-get install make clang pkg-config libssl-dev build-essential

screen -S avail-light-node
```

#### * İşimiz bittiğinde screen'den çıkmak için CTRL+A+D tuş kombinasyonlarını kullanın. Screen'e tekrar girmek için `screen -r avail-light-node` kodunu kullanın.

## Avail Light Client'i yükleyin
```
cd

wget https://github.com/availproject/avail-light/releases/download/v1.7.2/avail-light-linux-amd64.tar.gz

tar -xvzf avail-light-linux-amd64.tar.gz

mv avail-light-linux-amd64 avail-light

rm -rf avail-light-linux-amd64.tar.gz
```

## Node'u başlatmak için gerekli adımlar

#### * Servis dosyasını oluşturalım.
```
sudo tee /etc/systemd/system/availd.service > /dev/null <<EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart=/root/avail-light --network biryani
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
EOF
```

#### * Node'u başlatın. journalctl ekranından çıkmak için CTRL+C basın.
```
sudo systemctl daemon-reload && systemctl enable availd && sudo systemctl restart availd && journalctl -o cat -fu availd
```
![image](https://github.com/mulosbron/BlockchainNodeRehberleri/assets/91866065/a9eb0f1e-e17f-4fd8-936b-71fa5e06f80c)

## Loglar
#### * Çalışan servisten logları görüntüleyin
```
journalctl -o cat -fu availd
```

#### * Light client tarafından işlenen en son blok numarasını döndürün
```
curl "http://localhost:7000/v1/latest_block"
```
