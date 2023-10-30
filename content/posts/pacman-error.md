+++
title = "Arch Linuxが更新できない"
date = 2023-10-31T02:23:23+09:00
tags = ["ArchLinux", "Proxmox"]
draft = false
+++

### Arch Linuxの更新でのエラー
Proxmoxで久しぶりにArchのコンテナを立てて`pacman -Syu`をしたら
```bash
:: File /var/cache/pacman/pkg/xxx.tar.zst is corrupted (invalid or corrupted package (PGP signature)).
```
とか出て更新できなくなっていました。  
多分PGP鍵の期限切れです。  

昔からArchの更新をしばらくほっぽっておくとこうなっていましたね。  
今回も調べたらProxmoxのLXCテンプレートが古いものでした。  
多分そのせいでしょう。  
このエラーに毎回毎回Qiitaとかで調べて対処していましたが、今後毎回調べるのも手間だし、Arch Linuxはこれからも使い続けるだろうから、この際しっかり備忘録として残すことにします。  

### とりあえずArchWikiを見る
まあPGP鍵が悪いなら更新してしまいましょう。  
ただまあ普段勝手にやってくれているものを手動でやる方法を僕が覚えてるはずもありません。  
ここは大正義ArchWiki様に教えを請うことにしましょう。  
[ArchWiki](https://wiki.archlinux.jp/index.php/Pacman/%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E7%BD%B2%E5%90%8D)によると、以下のコマンドで鍵の手動更新ができるみたいです。
```bash
# pacman -S archlinux-keyring

```
実際に実行してみましょう。  

```bash
:: File /var/cache/pacman/pkg/archlinux-keyring-20231026-1-any.pkg.tar.zst is corrupted (invalid or corrupted package (PGP signature)).
```

ダメですね（白目）  
まずarchlinux-keyringのことを信用できないらしい。
よく考えなくてもpacmanがそもそも動いてないのにpacmanで愚直に解決できるはずがありませんでしたね。  
しかしArchWikiには別の方法で手動更新する方法も書いています。

```bash
# pacman-key --refresh-keys
```

コレもだめでした（白目）  
こっちは実行できるけれど、やっぱりなんかエラーを吐いています。  
どうせこっちも鍵周りでしょう。  
一応ArchWikiには最終手段として「鍵をすべて信用する」という手法が紹介されています。  
できれば避けたいですね。  
最終手段一歩手前に「[すべての鍵をリセット](https://wiki.archlinux.jp/index.php/Pacman/%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E7%BD%B2%E5%90%8D#.E5.85.A8.E3.81.A6.E3.81.AE.E9.8D.B5.E3.81.AE.E3.83.AA.E3.82.BB.E3.83.83.E3.83.88)」という面白そうな項目があるので、そっちをやってみましょう。  
これによると、「rootで`/etc/pacman.d/gnupg`フォルダを削除し`pacman-key --init`を実行して`pacman-key --populate archlinux`としてデフォルトの鍵を再度追加してください。」だそうです。  
指示に従ってみると、なんかうまく通ってる気がしますね。  
そして`pacman -Syu`もうまく通りました。  
やりましたね。  

### おわり
いやぁ…さすがArchWikiですね！  
無知な自分でもここまでできるのだから、コレほど初心者向けのディストリビューションもありませんね。  
ありがたい話です。  

それじゃあ更新も終わったのでこれから設定に入っていこうと思います（白目）

### 追伸
そういえばいつからかbase-develがインストールするときに必須じゃなくなっていましたね。  
元々そうだったのかもしれませんが、昔はインストールガイドに絶対書いていたんですけれどね。  
ProxmoxのLXCテンプレートはそっちに準拠しているみたいです。  
sudo使えなくてびっくりしました。  
一応覚えておきましょう。
