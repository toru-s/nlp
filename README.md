# nlp-algos
NLP algos for Splunk DeepLearningTook Kit NLP

Splunk DLTK3.0 拡張版Apps https://splunkbase.splunk.com/app/4978　として公開した、NLP 固有表現抽出アルゴリズムの日本語版です。

NLPで使用しているSpaCyライブラリを使って実装されている固有表現抽出アルゴリズム、spacy_nerの代わりに　spacy_ner_ja を指定することでTokenizerをGinzaライブラリに切り替え日本語モデルをロードすることにより、日本語対応にしています。

Ginzaに関する詳細は　https://megagonlabs.github.io/ginza/　を参照してください。

2020/05/07 Splunk DLTK3.1 にNLP Ginzaとしてマージされました。https://www.splunk.com/en_us/blog/machine-learning/deep-learning-toolkit-3-1-examples-for-prophet-graphs-gpus-and-dask.html

DLTK3.1 で利用する場合は、以下の手順を踏んでください。

1. Docker Host上で、docker pull anthonygtellez/mltk-container-nlp-ginza を実行します。
2. DeepLearning Took Kitの「Containers」からContainer Image 「NLP Ginza」を選択して　コンテナをSTARTします。
3. NLPコンテナが起動したら「JUPYTER LAB」ボタンを押してJupyter Notebookをブラウザで開きます。パスワードは「Splunk4DeepLearning」
4. Jupyter Notebookの/notebooksディレクトリにspacy_ner_ja.ipynb ファイルを配置してください。※2020/05/09時点で必要
5. DLTKのOverview of all Container  Modelsの画面にモデル　spacy_ginza_entity_extraction_model　が表示されていない場合は、App DLTKのサーチタブを開き、mode=stageを指定してfitを実行するとファイルの実体がコンテナ内に生成されます。
　　SPLは　| makeresults | eval text = "アメリカのトランプ大統領は、新型コロナウイルス対策で制限を受けている経済活動について、20日から、テキサス州などで一部再開すると発表した。トランプ大統領「テキサス州とバーモント州では、20日に一部のビジネスを開始するだろうが、引き続き、感染予防としてソーシャルディスタンスを求める」。またトランプ大統領は、モンタナ州では、24日に経済活動の規制を解除し、5月1日からは、オハイオ、ノースダコタ、それにアイダホの各州で、段階的に経済活動再開の準備を進めていることを明らかにした。トランプ大統領が公表した、経済活動を3段階に分けて再開するとしたガイドラインでは、第1段階で、テレワークを継続しながら通勤も可能などとしているが、「安全を優先させるべき」と慎重な声も多くある。" | makemv text delim="。" | mvexpand text | fit MLTKContainer mode=stage algo=spacy_ner_ja epochs=100 text into app:spacy_ginza_entity_extraction_model


https://github.com/splunk/splunk-mltk-container-docker　をベースに拡張したNLPイメージは　docker pull storu/mltk-container-nlp でも取得できます。こちらのコンテナイメージでは　/notebooksディレクトリにspacy_ner_ja.ipynb ファイルが事前に配置されています。　

最後に、現状のGinza　3.1.2の標準実装のままでは固有表現抽出ラベル精度があまりよろしくないため、将来的に拡張をしたいと思っています。
