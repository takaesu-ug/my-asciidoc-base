my-asciidoc-base
=======================

## チートシート
http://powerman.name/doc/asciidoc


## 環境構築

### pluntumlやgraphvizを使うとき

brewで pluntuml(依存関係のある graphviz) をインストールする

[asciidoctor/asciidoctor-diagram](https://github.com/asciidoctor/asciidoctor-diagram) のgemを入れる

plunt umlのインストール等

* http://yohshiy.blog.fc2.com/blog-entry-152.html
  * java
  * graphviz
  * plantuml.jar (http://plantuml.sourceforge.net/download.html)

[asciidoctorで日本語の本文とPlantUMLのクラス図が入った文書をPDFに変換してみた - Qiita](http://qiita.com/hnakamur/items/33a5e342ea79cffbbd9b)


```
asciidoctor-diagramを読み込み（plantumlなどを出力するため）実行する
% bundle exec asciidoctor --backend html5 -r asciidoctor-diagram -o sample.html sample.adoc
```

