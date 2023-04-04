# <h1 align="center"> Nibiru Incentivized Testnet 1 Node Guide Turkish </h1> 
![nibi-logo-on-white-pink](https://user-images.githubusercontent.com/91866065/208937132-0f1e2186-0967-4f9e-aee7-a1c9f722cad7.png)

## Linkler:
 * [Nibiru Resmi Twitter](https://twitter.com/NibiruChain)
 * [Nibiru Resmi Discord](https://discord.gg/nibiru)
 * [Nibiru Explorer](https://nibiru.explorers.guru/)
 
## Minimum sistem gereksinimleri

* 4 cores (max. clock speed possible)

* 16GB RAM

* 100+ of NVMe or SSD disk

## Başlangıç
```
sudo su

cd

sudo apt update && sudo apt upgrade -y

sudo apt-get install curl gcc make jq screen -y

screen -S nibiru
```

#### * İşimiz bittiğinde screen'den çıkmak için CTRL+A+D tuş kombinasyonlarını kullanın. Screen'e tekrar girmek için `screen -r nibiru` kodunu kullanın.

## Go'yu yükleyin
```
wget https://golang.org/dl/go1.19.3.linux-amd64.tar.gz

sudo tar -C /usr/local -xzf go1.19.3.linux-amd64.tar.gz

rm go1.19.3.linux-amd64.tar.gz

export GOROOT=/usr/local/go

export GOPATH=$HOME/go

export GO111MODULE=on

export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

#### * Go versiyonunu kontrol edin. (Çıktı:`go version go1.19.3 linux/amd64`)
```
go version
```
![goversion](https://user-images.githubusercontent.com/91866065/208239917-629f76d2-419f-4372-a933-4c8f1b63ba54.png)

## Nibiru'yu yükleyin
```
git clone https://github.com/NibiruChain/nibiru && cd nibiru

git checkout v0.19.2

make install
```

#### * Nibiru'nun versiyonunu kontrol edin. (Çıktı:`0.19.2`)
```
nibid version
```

## Node'u başlatmak için gerekli adımlar

#### * <> işaretlerini kaldırın.
```
nibid init <NODEADI> --chain-id nibiru-itn-1
```

#### * Yeni cüzdan oluşturun veya eski cüzdanınızı kurtarın.
```
nibid keys add <CUZDANADI>

nibid keys add <CUZDANADI> --recover
```

#### * Genesis dosyasını yükleyin ve ikinci komut ile çıktıyı kontrol edin. (Çıktı:`69f8c494ef1147b335d1bb6bf2102624a698dec62a984aa576784de411d6c899`)
```
curl -s https://rpc.itn-1.nibiru.fi/genesis | jq -r .result.genesis > $HOME/.nibid/config/genesis.json

shasum -a 256 $HOME/.nibid/config/genesis.json
```

#### * Gerekli ayarları yapın.
```
sed -i 's/minimum-gas-prices =.*/minimum-gas-prices = "0.025unibi"/g' $HOME/.nibid/config/app.toml

wget -O $HOME/.nibid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Nibiru/addrbook.json"
```

#### * Servis dosyasını oluşturalım.
```
sudo tee /etc/systemd/system/nibid.service > /dev/null <<EOF
[Unit]
Description=nibiru
After=network-online.target
[Service]
User=$USER
ExecStart=$(which nibid) start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```

#### * Node'u başlatın. journalctl ekranından çıkmak için CTRL+C basın.
```
sudo systemctl daemon-reload && systemctl enable nibid && sudo systemctl restart nibid && journalctl -o cat -fu nibid
```

#### * Senkronize durumunu kontrol edin. `"catching_up": false` çıktısını alana kadar diğer adıma geçmeyin.
```
nibid status 2>&1 | jq .SyncInfo
```

#### * Faucet'ten token talep edin.
```
FAUCET_URL="https://faucet.itn-1.nibiru.fi/"

ADDR=<ADRESINIZ>

curl -X POST -d '{"address": "'"$ADDR"'", "coins": ["10000000unibi"]}' $FAUCET_URL
```

#### * Validator'u oluşturun. (Validator'u oluşturmadan önce cüzdanınızda NIBI bulunmalı)
```
nibid tx staking create-validator \
--amount 10000000unibi \
--commission-max-change-rate "0.1" \
--commission-max-rate "0.20" \
--commission-rate "0.0" \
--min-self-delegation "1" \
--website="https://github.com/mulosbron/NibiruTestnetNodeTurkish" \
--pubkey=$(nibid tendermint show-validator) \
--moniker <NODEADI> \
--chain-id nibiru-itn-1 \
--from <CUZDANADI> \
-y
```

#### * Son olarak yukarıdaki komutun verdiği hash'i explorer'da aratın. Sonuç `success` ise olmuştur.

# <h1 align="center">[Mulosbron's Validator](https://nibiru.explorers.guru/validator/nibivaloper1ns372uy5fdy94mzny56dph7l30706lhkkctyme) </h1>
