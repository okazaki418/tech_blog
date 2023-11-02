+++
title = "Proxmox上のLXC上でのDocker"
date = 2023-11-02T06:29:23+09:00
tags = ["Docker", "LXC", "Proxmox"]
draft = false
+++

### Proxmox上のLXC
現在自宅では仮想化基盤としてProxmoxを運用しています。  
これがなかなか便利でなんでもかんでもできます。  
VMじゃなくてLXCがポンポン立てやすいのもGOODですね。  
しかしやはりLXC使うとよくわからない問題がそこそこ起きるんですよね。  
VM使えば解決するので別にいいんですけれども…  
その中でもDockerはちょっと解決しできなかった問題だったため、記録しておきたいと思います。  

### LXC上のDocker
まず大前提としてLXCの上でDockerを動かすのは非効率です。  
普通はやるべきではないと思います。  
ただテスト環境として使いたいだけなので、リソースの無駄遣いだと言うことには目をつぶってください。  

### syscallの失敗？
Docker on LXC (Arch Linux) on ProxomoxでNext.jsのテスト環境を作ろうとしたときのことです。  
なんかnpm周りで失敗しているんですよね。  
しかもエラーもrenameの失敗とかいうあまり聞いたことのないもの。  
なんならsyscallで失敗しているみたいな記述すらあります。  
実際のエラーの一部を以下に示します。  
```bash
npm ERR! code EINVAL
npm ERR! syscall rename
```
何を言っているんだ…  
とりあえずコンテナの中に入って、試しに中のtsconfig.jsonに対してmvをしてみたら
```bash
mv: cannot move 'tsconfig.json' to a subdirectory of itself, 'test'
```
このザマです。  
別にdocker-compose.ymlのvolumesでマウントしたりとかしてないんだけどな…  
調べてもそれっぽい解決方法が出てこなかったのでとりあえず無視してVMでDocker使います。  
何か知っている人がいたら教えてください。  
