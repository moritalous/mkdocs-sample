# Dockerのインストール

WSL2で以下のコマンドを実行

```bash title="WSL2"
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

!!! info
    途中で以下のコメントが出ますが、気にせず待ちます。

```
WSL DETECTED: We recommend using Docker Desktop for Windows.
Please get Docker Desktop from https://www.docker.com/products/docker-desktop

You may press Ctrl+C now to abort this script.
+ sleep 20
```

## sudoなしでdockerコマンドが実行できるように設定

```bash title="WSL2"
sudo usermod -aG docker $USER
```

## sudoなしでDockerデーモンの起動ができるように設定

```bash title="WSL2"
sudo visudo
```

nanoエディタが起動するので、末尾に以下を追加

```
%docker ALL=(ALL)  NOPASSWD: /etc/init.d/docker
```

編集後、`Ctrl+X`、`Y`、`Enter`で保存します。

## WSL2起動時にDockerが自動起動するように設定

`~/.bashrc`の末尾に以下を追記

```
sudo /etc/init.d/docker start
```

## Docker Composeのインストール


```bash title="WSL2"
mkdir -p ~/.docker/cli-plugins
curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
```

インストール確認

```bash title="WSL2"
docker compose version
```

```
Docker Compose version v2.4.1
```