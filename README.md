## 💻 Sistem Gereksinimleri
| Bileşenler | Minimum Gereksinimler | 
| ------------ | ------------ |
| CPU |	4|
| RAM	| 8+ GB |
| Storage	| 400 GB SSD |

### 🚧Gerekli kurulumlar
```
sudo apt update && sudo apt upgrade -y
sudo apt install curl git wget htop tmux build-essential jq make lz4 gcc unzip -y
```

### 🚧 Go kurulumu
```eğer kurulu değilse kurun
cd $HOME
VER="1.21.3"
wget "https://golang.org/dl/go$VER.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$VER.linux-amd64.tar.gz"
rm "go$VER.linux-amd64.tar.gz"
[ ! -f ~/.bash_profile ] && touch ~/.bash_profile
echo "export PATH=$PATH:/usr/local/go/bin:~/go/bin" >> ~/.bash_profile
source $HOME/.bash_profile
[ ! -d ~/go/bin ] && mkdir -p ~/go/bin
```

### 🚧 Auto İnstall
```
cd $HOME
sudo apt install curl -y && source <(curl -s https://nodesync.top/warden_auto)
```

### 🚧 Cüzdan olusturalım
```
wardend keys add cüzdan-adi

--eğer mevcut cüzdanınız varsa
wardend keys add wallet --recover

--balance kontrolü
wardend q bank balances $(wardend keys show wallet -a)
```
### 🚧 Faucet
Not: altaki kodu çalıştırdıktan sonra explorerden adresini arat bak gelmişmi die

https://warden-explorer.paranorm.pro/warden/block
```
curl --data '{"address": "cüzdan-adresi-yaz"}' https://faucet.alfama.wardenprotocol.org
```
### 🚧 sync status False olması gerekli
```
wardend status 2>&1 | jq .sync_info
```

### 🚧 Validator Olusturma
Not: altaki kodla pubkey öğren
```
wardend comet show-validator
```
Not: öğrendiğin pubkeyi aşağıda nano ile içine akataracağın yere yazıcan
```
nano $HOME/validator.json
```
```
{    
    "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"lR1d7YBVK5jYijOfWVKRFoWCsS4dg3kagT7LB9GnG8I="},
    "amount": "1000000uward",
    "moniker": "your-node-moniker",
    "identity": "eqlab testnet validator",
    "website": "optional website for your validator",
    "security": "optional security contact for your validator",
    "details": "optional details for your validator",
    "commission-rate": "0.1",
    "commission-max-rate": "0.2",
    "commission-max-change-rate": "0.01",
    "min-self-delegation": "1"
}
```
Not: ctrl xy enter kaydet çık.
### 🚧  Validator olusturucaz ama eşleşmesini beklemeniz gerek....
```
wardend tx staking create-validator $HOME/validator.json \
--from=wallet \
--chain-id=alfama \
--fees=500uward
```
### 🚧 Delegete etme
```
wardend tx staking delegate $(wardend keys show wallet --bech val -a)  1000000uward \
    --from=wallet \
    --chain-id=alfama \
    --fees=500uward

```# Warden-Protocol
