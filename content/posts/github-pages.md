+++
title = "GitHub Pagesでの管理"
date = 2023-10-30T16:07:02Z
draft = false
+++

### ブログの構成
このブログはHugoを用いて作成しています。  
これは昔から使ってたから慣れているというのがありますね。  
ただ記事を書いているだけのブログのために、わざわざ動的にしてリソース無駄遣いしたり、攻撃される隙を与えなくてもいいですからね。  
~~動的サイトとか面倒だし…~~  
何より自分のサーバを使わなくてもGitHub経由でいい感じに公開できるのがいいですね。  
僕のような貧乏な学生にとってはサーバの電気代もVPSの料金もバカになりません。  
### ブログの公開方式
さて、ブログの作成方法自体はそれで問題ないのですが、公開方法はどうするかというところですね。
まあドメインくらいは新しく取らないといけないかなぁ…と思っていましたが、GitHub PagesならユーザのIDか何かに対応したURLでうまいことやってくれるのを思い出しました。  
別のブログでは[netlify](https://www.netlify.com/)を使っていてGitHub Pagesは使ったことなかったので、ここに至るのに少し時間がかかりました。  
新しいことを覚える機会でもありますし、ちょうどいいですね！  
ということでGitHub Pagesを使います。  

### 参考文献
基本的には[Hugoの公式](https://gohugo.io/hosting-and-deployment/hosting-on-github/)と[こちらのサイト](https://developer.mamezou-tech.com/blogs/2022/09/08/github-pages-new-deploy-method/)を参考にしました。  
ありがとうございます。  

### ブログの作成・公開
ブログを作るに当たり、とりあえずGitHubにレポジトリ作って適当にHugoで作ったディレクトリをポイッとしておきます。  
そしてHugoで適当にページを作って`hugo server`を使ってページを確認できるところまで持っていきます。
ここまででとりあえずブログ自体は完成ということにします。
GitHubに`push`しておきましょう。
これをどう公開するかと言うのが話のミソですね。

まずGitHubのブログのコードを管理しているレポジトリに行きます。  
自分の場合だと[ここ](https://github.com/okazaki418/tech_blog)ですね
ページの上の方にCodeとかIssuesとか並んでるタブがありますが、その中のSettingsを選びます。  
そっからPagesを選んで、SourceをGitHub ActionsにするとHugoが出てくるのでそっからConfigureで適当にコミットすればもう完成です。  

### おわり
~~画像を撮り忘れて曖昧な記憶から書いたせいで~~なんか説明が雑になりましたが、この程度でパッとできちゃいます。
本当に簡単でしたね。  
しかも何もせずともhttpsですからね、お気楽です。

コレを完全に自前のサーバとかVPSでやろうとすると、やれドメイン管理だやれ証明書だやれ支払いだと面倒だらけです。  
ただこれならドメインも要らないしネットワーク系のアレもうまいことやってくれるし、楽でいいですね。  
楽でいいですが、一度オンプレでやったりCloudflareを活用したりしておくと勉強になるのでそれもいいですね。  
そう…あれは無駄な時間ではなかったんだ…  

そういえばCloudflare Pagesとかもありましたね。  
脳死でGitHub Pages使わずに比較してからやっておけばよかったです。  
まあドメインが必要そうですが…  

そんな感じでGitHub Pagesはなかなかいい感じです！
ソースコード管理とページの公開みたいに、色々なことを1つのサービスに依存しておくと、それが倒れたときが怖いというのがあります。  
そのため、今まで便利すぎるサービスは使わずできるだけ単機能のサービスを組み合わせて運用してきましたが、これは便利でしょうがないですね。
まあGitHubならしばらく倒れることもないでしょう。  

皆さんもGitHub Pagesでブログ公開チャレンジ！