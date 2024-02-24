# Jenkins のセットアップ

Ubuntu22.04LTS（wsl2）への Jenkins 初期セットアップメモ

## 手順

### Java のインストール

Jenkins は Java で動作するため、まず Java をインストールする必要があり。
前提 OS（Ubuntu22.04）で対応している Java11 をインストール。

```
sudo apt update
sudo apt install openjdk-11-jdk

java -version // Javaのバージョン確認

    openjdk 11.0.21 2023-10-17
    OpenJDK Runtime Environment (build 11.0.21+9-post-Ubuntu-0ubuntu122.04)
    OpenJDK 64-Bit Server VM (build 11.0.21+9-post-Ubuntu-0ubuntu122.04, mixed mode, sharing)

```

### Jenkins の公式リポジトリの追加

Jenkins を使用するための公開鍵を取得。

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \ /usr/share/keyrings/jenkins-keyring.asc > /dev/null

```

Jenkins の APT リポジトリをシステムの APT ソースリストに追加。
※ debian 形式のリポジトリのため、必要

```
 echo 'deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null'
```

Jenkins のインストール

```
sudo apt update
sudo apt install Jenkins
```

### 初期動作確認

```
// アクティブ確認
sudo systemctl status jenkins

    jenkins.service - Jenkins Continuous Integration Server
        Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
        Active: active (running) since Sun 2024-02-25 00:50:01 JST; 2min 43s ago
    Main PID: 28776 (java)
        Tasks: 73 (limit: 19090)
        Memory: 3.5G
        CGroup: /system.slice/jenkins.service
                └─28776 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
```

```
// 8080 port の許容
sudo ufw allow 8080
// SSH接続の許容
sudo ufw allow ssh
// UFW（Linux用ファイアウォール）の有効化
sudo ufw enable
// Status確認
sudo ufw status
// 初期アクセス用の生成パスワードを取得
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Jenkins の Web インタフェースでログイン
http://localhost:8080/

推奨設定でプラグインのインストール
