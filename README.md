# mywebsite
static website on github. Demo site is [here](https://yukoga.github.io/mywebsite/index.html)


## 使い方  
1. このリポジトリを適当なところに clone  
2. 作業用に、適当な [Google Tag Manager のコンテナを作る](https://support.google.com/tagmanager/answer/6103696?hl=ja)（ここに、json の設定ファイルを import して設定内容を見れるようにする）。  
3. 2. で作ったコンテナに、[GTM-XXXXX_workspace3.json を import](https://support.google.com/tagmanager/answer/6106997?hl=ja)  
4. import が無事にできると、download_tracking というフォルダが出来るので、その中の設定内容を参照しながら上のデモサイトを見る
5. 実際に自分で動かしてみたい場合は、  
- フォルダ download_tracking の中の、Var Google Analytics basic config という変数の、Tracking ID を、自分の GA の ID に変更して  
- [preview なり Publish](https://support.google.com/tagmanager/answer/6103696?hl=ja&ref_topic=3441530) すると、実際に GA で計測出来る様子が試せる  
- リアルタイム レポートの「イベント」というメニューを参照して、「カテゴリ」という値をクリックすると、「ラベル」のところにダウンロードしたファイルの名称が計測されるようになっているのがわかる  


## 設定のポイント  
フォルダ download_tracking の中の、Trg DL link for with class と Trg DL link with url regex という設定がすべて。  
この設定では、
- すべてのページで、クリックの listen を行い  
- クリックされたアンカータグのクラス名や URL の正規表現が正しい場合に、タグが発火されるようなトリガー設定になっている  
- また、クリックされた時、ちゃんと計測されてから遷移するように、2 秒待つ設定がされている  

という実装がされている。  
また、ダウンロードされたファイル名の計測方法は、  
- タグマネージャ の機能により、クリックされたときに、href の値が、変数 Click URL に格納されるようになっている(変数 Click URL は、タグマネージャの Built in の変数だが、デフォルトでは無効になっているので有効にしておく必要がある)。  
- その Click URL の値が、GA のタグの設定の中で、Event Label に設定されている。

