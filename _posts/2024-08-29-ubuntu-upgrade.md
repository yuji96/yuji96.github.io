---
categories:
  - memo
date: 2024-08-29 00:00:00 +0900
tags:
  - ubuntu
title: 研究室の ubuntu サーバーをアップグレードしたときのメモ
parse_block_html: true
published: true
---

1. unofficial package へのリンクを消す

   - パターン 1 : `/etc/apt/sources.list.d` 内の全ファイルをコメントアウト
   - パターン 2 : `/etc/apt/sources.list.d` を移動する

2. unofficial package を消す

   以下のコマンドで検出されたパッケージを消す

   ```
   grep Foreign /var/log/dist-upgrade/main.log
   ```

   参考: https://askubuntu.com/questions/1238620

3. apt package の整合性をチェック

   ```
   sudo apt update
   sudo apt upgrade -y
   # sudo apt dist-upgrade -y  # いらない気もする
   # sudo apt autoremove  #必須ではなさそう
   ```

   `apt upgrade` の結果が、

   ```
   0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
   ```

   のように全てがゼロにならないと、`Please install all available updates for your release before upgrading.` と言われてしまう

   また、以下のコマンドで何かが表示された場合は、アップデート実行前に必ず修復する。
   これをしないと OS レベルで故障するかもしれない。

   ```
   sudo dpkg -C
   ```

4. アップグレード実行

   ```
   sudo vi /etc/update-manager/release-upgrades
   do-release-upgrade -c  # 何のバージョンになるかチェックだけ
   sudo do-release-upgrade -f DistUpgradeViewNonInteractive
   ```

5. 後処理【重要】

   とりあえず `lsb_release -a` でバージョン確認

   reboot 前にもパッケージの依存関係の確認をする

   ```
   sudo dpkg -C
   ```

6. nvidia-driver のインストール

   ちなみに、OS upgrade 後は GPU を認識していないので GUI が使えなくなる。その場合は Alt+Ctrl+F2 を押して CLI から作業を継続する。

   古いドライバに対応したパッケージを削除する

   ```
   sudo apt remove --purge "*nvidia*" -y
   sudo apt remove --purge "*cuda*" -y
   ```

   `ubuntu-drivers devices` で推奨されているものなど、好きなバージョンをインストール

   ```
   apt install nvidia-driver-???  # 今回はすべて ???=535 とした
   ```

   特に事前設定せずにこれだけでインストールできた

   reboot しなくても以下のコマンドで nvidia-smi が使える（成功していれば）

   ```
   sudo rmmod nvidia_drm nvidia_modeset nvidia_uvm nvidia
   ```
