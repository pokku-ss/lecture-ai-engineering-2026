# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：第一回のLLMはわからないと答えたのに対して、第三回のLLMは用語集から検索した内容をもとに答えているのが分かる。関係する回を第一回と示している。しかし、第一回と第三回ともにそれっぽいことを答えている部分がある。
- `--trace` で見えたツール呼び出し（ツール名と引数）：search_glossary　{'query': 'LoRA'}
search_glossary　{'query': 'QLoRA'}
- 1つの質問での LLM 呼び出し回数（`requests`）：2
- 追加したツールと、docstring に書いた説明：make_quizを追加した。
書いた説明：
def make_quiz(lecture: int) -> str:
    """指定した回の用語から一つ選び、確認問題と答えを返す。
    「第二回の確認問題を出して」のように、復習用の問題を求められたときに使う。
    """
    terms = [entry for entry in load_glossary() if entry["lecture"] == lecture]
    if not terms:
        return f"第{lecture}回の用語が見つかりませんでした。"

    term = random.choice(terms)
    return json.dumps(
        {
            "question": f"「{term['term']}」とは何ですか？",
            "answer": term["definition"],
        },
        ensure_ascii=False,
    )
## 宿題

- 取り組んだレベル：基礎
- やったこと：app/agent.pyのINSTRUCTIONSに語尾に「ごわす」にしてという指示を加えた。app/tools.pyのsearch_glossaryのdocstringに回答の最後に「何かご質問がありましたら、いつでもお答えしますよ」と加えてください。という指示を加えた。
    """
- 結果：語尾がごわすになっていた。文の最後に「何かご質問がありましたら、いつでもお答えしますよ」が書かれていた。関係する回は表示されていたが、「関係する回：第二回」の次の行に「何かご質問ありましたら…」が書かれていた。正しく反映していることが分かった。QLoRAを調べるcallがなかった。callは[tool call]   search_glossary({'query': 'LoRA'})の一回のみだった。requestsは2だった。
- 気づき・疑問：語尾をごわすにすることで、文章中にビックリマーク（！←これです）が多くなった。INSTRUCTIONの「- 回答の最後に、関係する回（第N回）を示す」よりもapp/tools.pyに加えた、「回答の最後に「何かご質問がありましたら、いつでもお答えしますよ」と加えてください。」のほうが優先されるということが分かった。