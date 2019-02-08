# vuls-try-it-out

## ssh 鍵の生成（初回のみ）

```bash
ssh-keygen -t ecdsa -N '' -f keys/id_ecdsa
cat keys/id_ecdsa.pub >>keys/authorized_keys
ln keys/authorized_keys data/
```

## コンテナの起動

```bash
# sudo docker pull centos:7
# sudo docker pull debian:9
sudo docker-compose up -d --build
```

## ssh ログイン

```bash
ssh vuls@localhost -p 2222 -i keys/id_ecdsa cat /etc/centos-release
ssh vuls@localhost -p 2223 -i keys/id_ecdsa cat /etc/debian_version
```

## ログディレクトリ作成（初回のみ）

```bash
sudo mkdir -p /var/log/vuls
sudo chown "$(id -u):$(id -g)" /var/log/vuls
```

## Vuls の設定をテスト

```bash
vuls configtest
```

## CVE の取得

```bash
go-cve-dictionary fetchnvd -last2y
go-cve-dictionary fetchjvn -last2y
```

## OVAL の取得

```bash
goval-dictionary fetch-redhat 7
goval-dictionary fetch-debian 9
```

## 脆弱性スキャン

```bash
vuls scan
```

## 脆弱性レポートの作成

```bash
vuls report -format-json
```
