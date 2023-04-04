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

#### * Web tarayıcınıza gidin `https://localhost:8080/` adresini yapıştırın ve localhost yerine serverinizin IP'sini yazın. Login sayfası açıldığında kurulum sırasında belirlediğiniz şifreniz istenecektir.
![login](https://user-images.githubusercontent.com/91866065/229783338-95415568-2b04-4d5d-9940-3f1efebce293.jpg)

#### * Web tarayıcınızda Shardeum Validator Panel'inin "Overview" sayfasını görmelisiniz:
![overview](https://user-images.githubusercontent.com/91866065/229783790-66ecb00e-09ee-4024-8c92-83e0100a8897.jpg)

## Validator kurulumu

#### * "Maintenance" sayfasına gidin, sonra üst sol taraftaki beyaz kutuda bulunan "Start Node" butonuna tıklayın. Daha sonra bekleyin ve sayfayı yenileyin. Eğer "Start Node" butonu yerine "Stop Node" yazıyorsa, node doğru bir şekilde çalışıyor demektir.
![maintenance](https://user-images.githubusercontent.com/91866065/229784390-75a658d5-0ca8-4623-800f-85cf25c53943.jpg)

#### * [Shardeum Betanet Faucet](https://faucet-sphinx.shardeum.org/) adresinden SHM talep edin. Son olarak sağdaki kutudan cüzdanınızı bağlayıp SHM stake edin. (Ayrıca Shardeum Discord'undan SHM talep edebilirsiniz.)
