# 第2回 解答

## 演習

- 使ったモデル・設定（`result.json` の `config` から）：
- 自分で学習を実行したか（`executed_training_myself`）：はい（実行できた範囲：　）
- 学習前：`format_rate` =　0.095238 / `content_rate` =　0.000000	
- 学習後：`format_rate` =　1.000000	 / `content_rate` =　0.761905
- 退行した質問：　なし
- 学習後に残った失敗と、その型（根拠なしの質問に断定した / 根拠ありの質問に確認要求で逃げた / 形式の崩れ）：（6）PDF以外でも出せますか、（10）オフィスアワーの曜日と時間を教えてください　（17）課題の文字数に制限はありますか　（18）提出した課題へのフィードバックはもらえますか　（19）参考文献の書き方に指定はありますか
- 知識を問う質問（セクション 6）の結果（学習前の分類 → 学習後の分類）と気づいたこと：
(0)format_error → asserted
(1)format_error → needs_review
(2)format_error → needs_review
(3)format_error → asserted
学習前はすべてformat_errorだったが、学習後はassertedとneeds_reviewが表示されている。
- 学習で変わったこと・変わらなかったこと：学習することでformat_rateとcontent_rate、both_rateがそれぞれ向上している。一方で実行時間は学習後のほうが5.1秒長かった。

## 宿題

- 取り組んだレベル：基礎
- 変えた設定やデータ：num_train_epochsを 20 → 5 に変更した。
- 結果（比較表や数字）：
before
    "format_rate": 0.09523809523809523,
    "content_rate": 0.0,
    "both_rate": 0.0,
    "seconds": 43.1
after
    "format_rate": 1.0,
    "content_rate": 0.7619047619047619,
    "both_rate": 0.7619047619047619,
    "seconds": 44.9
学習前と学習後を比べた結果、format_rate、content_rate、both_rateが学習前よりも学習後のほうが向上していることが分かる。また、実行時間は学習前よりも学習後のほうが1.8秒長かった。これらのことから、num_train_epochsを 20 → 5 に変更することで実行時間を短くできることが分かった。また、今回の検証ではformat_rate、content_rate、both_rateには学習回数による変化がないことが分かった。
- ファインチューニングが向く場面・向かない場面についての考察：ファインチューニングが向く場面は言葉の形式を整えるときである。
向かない場面は解答が誤っていた場合や解答の精度が悪い場合などは適していない。
