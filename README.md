# nlp-algos
NLP algos for Splunk DeepLearningTook Kit NLP

https://splunkbase.splunk.com/app/4978　を利用される場合、Docker コンテナの/srv/notebook に日本語対応版アルゴリズムを配置してください。

1. Docker Host上で　docker pull storu/mltk-container-nlp:latest を実行します。
2. DeepLearning Took Kitの「Containers」からContainer Image 「NLP」を選択して　コンテナをSTARTします。
3. NLPコンテナが起動したら「JUPYTER LAB」ボタンを押してJupyter Notebookをブラウザで開きます。パスワードは「Splunk4DeepLearning」
4. Jupyter Notebookのnotebookディレクトリにspacy_ner_ja.ipynb ファイルを配置してください。

オリジナルの固有表現抽出アルゴリズム　spacy_nerの代わりに　spacy_ner_ja を指定することで日本語モデルをロードし、SpaCyのTolenizerがGinzaに切り替えて日本語処理を可能にします。

