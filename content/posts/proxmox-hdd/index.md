+++
title = "ProxmoxのVMのHDD容量"
date = 2023-11-03T01:13:25+09:00
tags = ["Proxmox"]
draft = false
+++

ProxmoxはVMをポコポコ立てられて便利です。  
ただ適当に立てたけれど、ちょっと使うことが多くなってきたVM、ありませんか？  
僕は真剣に立てて使いまくってたけれど、見積もりが甘くてHDD容量が足りなくなったVMがあります（白目）  

VMのHDDを増やすのはめんどくさい…  
というかパーティションを広げるのがめんどくさい…  

確かマウントしているパーティションはイジれなかった記憶があります。  
そしてVMを起動している以上間違いなく広げたいパーティションはマウントしています。  
そのため外から（USBとか）LiveイメージでGpartedでも使って広げなければなりません。  
面倒だ…
~~（実際のところProxmoxだとLiveイメージ突っ込めば起動できるからそうでもない）~~  

ということで横着してキャッシュ消したりして対処してきたのですが、いよいよそうも言ってられなくなってきました。  
しょうがないから広げます。  
Proxmoxで仮想HDDの容量を広げること自体は大変簡単であるため、問題ありません。  
とりあえずなにか不思議なことが起きないかなと思って、HDDを広げたあとVMを起動してGpartedを開いてみました。  

なんか広げられた…  

なんででしょうね？  
GPTだからとか関係しているのかな？  
高校生の頃からLinuxは触っていますが、よく考えたら安いノートPCで遊んでいたため、すべてBIOS+MBRでした。  
GPTだと大丈夫なのだろうか…（なんかMBRでも論理パーティションなら行けた気もする）
まあわかりません。  
ただの記憶違いかもしれません。  

結論として、簡単にHDD容量は増やせるから気軽にVMを立てていこうと思いました。