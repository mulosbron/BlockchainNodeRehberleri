# <h1 align="center"> Shardeum Sphinx (Betanet) Node Guide Turkish </h1> 
![shardeum](https://user-images.githubusercontent.com/91866065/229753729-5b814804-b163-4636-a070-b17061224e35.png)


## Linkler:
 * [Shardeum Resmi Twitter](https://twitter.com/shardeum)
 * [Shardeum Resmi Discord](https://discord.gg/shardeum)
 * [Shardeum Explorer](https://explorer-sphinx.shardeum.org/)
 
## Minimum sistem gereksinimleri

* 250 GB SSD storage

* Quad core CPU less than 10 years old if self hosting

* Dual core CPU works if hosted with newer Xeons / EPYC

* 16 GB of ram,  4+ GB of virtual memory recommended

* Hosting: 8 GB RAM + 8 GB Virtual Memory

## Gerekli kurulumlar
```
sudo su

cd

sudo apt update && sudo apt upgrade -y

sudo apt-get install curl screen -y

sudo apt install docker.io -y

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

screen -S shardeum
```

#### * İşimiz bittiğinde screen'den çıkmak için CTRL+A+D tuş kombinasyonlarını kullanın. Screen'e tekrar girmek için `screen -r shardeum` kodunu kullanın.

#### * docker versiyonunu kontrol edin. `20.10.12` veya daha yüksek bir sürüm olmalı.  (Çıktı:`Docker version 20.10.21, build 20.10.21-0ubuntu1~20.04.1`)
```
docker --version
```

#### * docker-compose versiyonunu kontrol edin. `1.29.2` veya daha yüksek bir sürüm olmalı.  (Çıktı:`docker-compose version 1.29.2, build 5becea4c`)
```
docker-compose --version
```

## Shardeum kurulumu
```
curl -O https://gitlab.com/shardeum/validator/dashboard/-/raw/main/installer.sh && chmod +x installer.sh && ./installer.sh
```
![sifrebelirle](https://user-images.githubusercontent.com/91866065/229762518-18fae0de-ea2f-49f9-8784-24c3f4def8ad.png)

#### * Çıkan sorulara `y` yazıp enterlayın. Şifrenizi girin. Daha sonra sorduğu şeyler için direkt enterlayın.

```
$HOME/.shardeum/shell.sh

operator-cli gui start
```
