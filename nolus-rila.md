# <h1 align="center"> Nolus Rila Node Guide Turkish </h1>
![nolus](https://user-images.githubusercontent.com/91866065/229474610-4d176205-3fdb-494c-8ba5-4e53d21f9db8.png)

## Linkler:
 * [Nolus Resmi Twitter](https://twitter.com/NolusProtocol)
 * [Nolus Resmi Discord](https://discord.gg/nolus-protocol)
 * [Nolus Explorer](https://explorer-rila.nolus.io/nolus-rila)
 
## Minimum sistem gereksinimleri

* 2+ vCPU

* 4+ GB RAM

* 120+ GB SSD

## Başlangıç
```
sudo su

cd

sudo apt update && sudo apt upgrade -y

sudo apt install make git screen -y

sudo apt-get install build-essential -y

screen -S nolus
```

#### * İşimiz bittiğinde screen'den çıkmak için CTRL+A+D tuş kombinasyonlarını kullanın. Screen'e tekrar girmek için `screen -r nolus` kodunu kullanın.

## Go'yu yükleyin
```
wget https://golang.org/dl/go1.19.4.linux-amd64.tar.gz

sudo tar -C /usr/local -xzf go1.19.4.linux-amd64.tar.gz

rm go1.19.4.linux-amd64.tar.gz

export GOROOT=/usr/local/go

export GOPATH=$HOME/go

export GO111MODULE=on

export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

#### * Go versiyonunu kontrol edin. (Çıktı:`go version go1.19.4 linux/amd64`)
```
go version
```

## Nolus'u yükleyin
```
git clone https://github.com/Nolus-Protocol/nolus-core && cd nolus-core

git checkout v0.2.2

make install
```

#### * Nolus'un versiyonunu kontrol edin. (Çıktı:`v0.2.2`)
```
nolusd version
```

## Node'u başlatmak için gerekli adımlar

#### * <> işaretlerini kaldırın.
```
nolusd init <NODEADI> --chain-id nolus-rila
```

#### * Yeni cüzdan oluşturun veya eski cüzdanınızı kurtarın.
```
nolusd keys add <CUZDANADI>

nolusd keys add <CUZDANADI> --recover
```

#### * Genesis dosyasını yükleyin ve ikinci komut ile çıktıyı kontrol edin. (Çıktı:`d22ea6488afe58478c54afeb2d6b5a45622c797dfd75c91a8653eb1f094173c5`)
```
wget https://raw.githubusercontent.com/Nolus-Protocol/nolus-networks/main/testnet/nolus-rila/genesis.json

mv ./genesis.json ~/.nolus/config/genesis.json

shasum -a 256 $HOME/.nolus/config/genesis.json
```

#### * Minimum gas değerini ayarlayın.
```
sed -i 's/minimum-gas-prices =.*/minimum-gas-prices = "0.025unls"/g' $HOME/.nolus/config/app.toml
```

#### * Eşleşme için:
```
PEERS="$(curl -s "https://raw.githubusercontent.com/Nolus-Protocol/nolus-networks/main/testnet/nolus-rila/persistent_peers.txt")"

sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.nolus/config/config.toml
```

#### * Servis dosyasını oluşturalım.
```
sudo tee  /etc/systemd/system/nolus.service /dev/null <<EOF
[Unit]
Description=Nolus Service
After=network.target
[Service]
Type=simple
User=$USER
WorkingDirectory=$HOME
ExecStart=$HOME/go/bin/nolusd start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```

#### * Node'u başlatın. journalctl ekranından çıkmak için CTRL+C basın.
```
sudo systemctl daemon-reload && systemctl enable nolus.service && sudo systemctl start nolus.service && journalctl -o cat -fu nolus.service
```

#### * Senkronize durumunu kontrol edin. `"catching_up": false` çıktısını alana kadar diğer adıma geçmeyin.
```
nolusd status 2>&1 | jq .SyncInfo.catching_up
```

#### * Faucet'ten token talep edin.
```

```

#### * Validator'u oluşturun. (Validator'u oluşturmadan önce cüzdanınızda NOLUS bulunmalı)
```
nolusd tx staking create-validator \
--amount 100000unls \
--commission-max-change-rate "0.1" \
--commission-max-rate "0.20" \
--commission-rate "0.0" \
--min-self-delegation "1" \
--website="https://github.com/mulosbron/BlockchainNodeRehberleri/blob/main/nolus-rila.md" \
--pubkey=$(nolusd tendermint show-validator) \
--moniker <NODEADI> \
--chain-id nolus-rila \
--from <CUZDANADI> \
-y
```

#### * Son olarak yukarıdaki komutun verdiği hash'i explorer'da aratın. Sonuç `success` ise olmuştur.
![Ekran görüntüsü 2022-12-21 202905](https://user-images.githubusercontent.com/91866065/208967689-1f8b360e-885f-40a5-af22-1338f323b327.png)

# <h1 align="center">[Mulosbron's Validator](https://testnet-2.nibiru.fi/validators/nibivaloper1ns372uy5fdy94mzny56dph7l30706lhkkctyme) </h1>
