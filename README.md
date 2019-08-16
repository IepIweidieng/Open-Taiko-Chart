# 「Open Taiko Chart」とは？
太鼓譜を記述するためのフォーマットです。太鼓譜を記述するためのフォーマットとして、「.tjf」や「.tja」等がありますが、複数の難易度、ダブルプレイを記述する場合複雑なテキストファイルとなり、さらにソフトウェア側でのパースも難解な処理になってしまうという欠点がありました。また、これらのファイルフォーマットで使用されているエンコーディングはShift-JISであり、ソフトウェアの国際化が顕著な今日では、とても扱いが難しいエンコーディングでもあります。「Open Taiko Chart」では、推奨するエンコーディングをUTF-8とし、どの言語、どの環境でも扱えるオープンなフォーマットとして公開します。

# 「Open Taiko Chart」のファイル構成
「Open Taiko Chart」では複数のファイルを使用し、「ひとつの作品」として成り立ちます。
## 「Open Taiko Chart Infomation」 (.tci)
このファイルには、その太鼓譜の名前やアーティスト、使用する音源のファイル名などの作品の情報と、各種難易度である「Open Taiko Chart Course」の情報が格納されます。
## 「Open Taiko Chart Course」 (.tcc)
このファイルは、「Open Taiko Chart Infomation」から呼び出されます。このファイルには、実際の譜面内容が記述されます。
## その他のファイル
譜面で使用する音源ファイルや、動画ファイルなどがこれに当てはまります。「Open Taiko Chart Infomation」と同じフォルダに入れておく必要があります。対応するコーデックやコンテナは、各ソフトウェアの実装で変わります。

## これらのファイルの制約
「Open Taiko Chart Infomation」は、「ひとつの作品」に対して2つ以上作成してはいけません。
「Open Taiko Chart Course」は、難易度の数より多く作成することができますが、難易度の数分しか有効ではありません。

# 「Open Taiko Chart Infomation」の記法

* エンコーディングは「BOM無し UTF-8」です。改行コードの指定はありません(理由は後述)。
* 「Open Taiko Chart Infomation」では、フォーマットにJSONを採用しています。エンコーディングが「BOM無し UTF-8」である理由は、このJSONフォーマットで決まっているからです(HAVE TO ではなく MUST)。改行してもしなくても問題ありません。
* JSONフォーマット採用しているため、多くのプログラミング言語ではデシリアライズが可能です。

## 「Open Taiko Chart Infomation」の書き方

```json
{
  "title": "The Sample M@ster",
  "subtitle": "Sample Song",
  "artist": [ "Tanaka Ichiro", "Tanaka Jiro", "Tanaka Saburo"],
  "creator": [ "Suzuki Ichiro" ],
  "audio": "Audio-Source.wav",
  "background": "Background-Image.png",
  "bpm": 160,
  "courses":
  [
    {
      "difficluty": "oni",
      "level": 9,
      "single": "Oni.tcc"
    },
    {
      "difficluty": "edit",
      "level": 10,
      "single": "Edit.tcc",
      "double": [ "Edit_1P.tcc", "Edit_2P.tcc" ]
    }
  ]
}
```
