
---

## Python基礎力トレーニング問題(第5章：配列)

この問題は、動画で解説された `配列（リスト）` の操作（作成、参照、追加、更新）と、前章の `for`文 を組み合わせて解くことを想定しています。

---

## レベル1：配列の中身を順に処理する（基本）

### 問題1-1
以下の配列 `members` に格納された名前を、`for`文を使って先頭から順に「◯◯さん」と敬称をつけて表示してください。

```python
members = ["佐藤", "鈴木", "高橋", "田中"]
```

**表示形式**
```
佐藤さん
鈴木さん
高橋さん
田中さん
```

<details><summary>解答例</summary>

```python
members = ["佐藤", "鈴木", "高橋", "田中"]

# 配列から1つずつ要素を取り出すパターン
for name in members:
    print(name + "さん")
```
</details>

### 問題1-2
以下の配列 `scores` にはテストの点数が格納されています。
`for`文と `range()`、`len()` を使って、「◯番目の点数は◯点です」と順に表示してください。
（※ユーザーに見せる番号なので、0番目ではなく1番目から表示されるようにしてください）

```python
scores = [80, 60, 90, 70, 100]
```

<details><summary>ヒント</summary>
`len(scores)` で配列の長さ（要素数）が取得できます。`range(len(scores))` で添字（インデックス）を回しましょう。
</details>

<details><summary>解答例</summary>

```python
scores = [80, 60, 90, 70, 100]

for i in range(len(scores)):
    # iは0から始まるので、表示用に+1する
    num = i + 1
    print(str(num) + "番目の点数は" + str(scores[i]) + "点です")
```

**解説**
配列のインデックスそのもの（何番目か）を使いたい場合は、`for item in 配列:` ではなく `for i in range(len(配列)):` の形を使うのが定石です。

</details>

---

## レベル2：配列データの集計（Sum, Maxの再現）

### 問題2-1（合計の算出）
以下の配列 `prices` の数値をすべて足し合わせた「合計金額」を計算し、**最後に1回だけ**表示してください。（組み込み関数の `sum()` は使わずに `for`文で書いてみましょう）

```python
prices = [100, 250, 180, 500, 320]
```

<details><summary>解答例</summary>

```python
prices = [100, 250, 180, 500, 320]
total = 0

for price in prices:
    total = total + price

print("合計金額は " + str(total) + "円です")
```
</details>

### 問題2-2（最大値の算出）
以下の配列 `numbers` の中から、**最も大きい数字（最大値）**を見つけて表示してください。（組み込み関数の `max()` は使わずに書いてみましょう）

```python
numbers = [12, 45, 2, 78, 34, 56]
```

<details><summary>ヒント</summary>
「暫定トップ」を入れておく変数（例：`max_val`）を用意します。最初は配列の0番目の値を暫定トップにしておき、ループの中で「もし今の値が暫定トップより大きければ、暫定トップを更新する」という処理を行います。
</details>

<details><summary>解答例</summary>

```python
numbers = [12, 45, 2, 78, 34, 56]

# 最初の要素を暫定の最大値とする
max_val = numbers[0]

for num in numbers:
    # 今見ている数が、暫定最大値より大きければ
    if num > max_val:
        # 最大値を更新する
        max_val = num

print("最大値は " + str(max_val) + " です")
```

**解説**
これは「アルゴリズム」の基礎中の基礎です。人間がリストを見て一番大きい数字を探すとき、「今のところこれが一番大きいな…お、もっと大きいのがあった」と更新していく思考プロセスをコードにします。

</details>

---

## レベル3：条件抽出と新しい配列の作成（Append）

### 問題3-1
以下の配列 `scores` から、**「80点以上」の点数だけ**を取り出し、新しい配列 `passed_scores` に格納（append）してください。
最後に `passed_scores` を表示してください。

```python
scores = [55, 80, 45, 90, 75, 100, 30]
```

<details><summary>解答例</summary>

```python
scores = [55, 80, 45, 90, 75, 100, 30]
passed_scores = [] # 空の配列を作っておく

for s in scores:
    if s >= 80:
        # 条件を満たす場合のみ追加する
        passed_scores.append(s)

print(passed_scores)
```

**実行結果**
```
[80, 90, 100]
```
</details>

### 問題3-2
以下の配列 `files` の中から、拡張子が **".jpg" で終わるファイル名だけ**をカウントし、その個数を表示してください。

```python
files = ["photo1.jpg", "note.txt", "image.png", "photo2.jpg", "vacation.jpg"]
```

<details><summary>ヒント</summary>
文字列が特定の文字で終わるかどうかは、動画では扱っていないかもしれませんが `文字列.endswith(".jpg")` という便利な命令があります。今回はそれを使ってみましょう（または `if ".jpg" in f:` でも簡易的にはOKです）。
</details>

<details><summary>解答例</summary>

```python
files = ["photo1.jpg", "note.txt", "image.png", "photo2.jpg", "vacation.jpg"]
count = 0

for f in files:
    # ".jpg" で終わるかどうか判定
    if f.endswith(".jpg"):
        count = count + 1

print("jpg画像は " + str(count) + "枚あります")
```
</details>

---

## レベル4：配列の中身を書き換える（更新）

### 問題4-1
以下の配列 `prices` は税抜価格です。
すべての要素を **1.1倍（税込価格）** に書き換えて（更新して）、最後に配列を表示してください。
※計算結果が小数になっても構いません（`int()`で整数にしてもOKです）。

```python
prices = [1000, 2500, 500]
```

<details><summary>ヒント</summary>
配列の中身を書き換えるときは、`prices[i] = ...` という形にする必要があります。そのため、`for price in prices:` ではなく、添字（インデックス）を使う `for i in range(len(prices)):` を使いましょう。
</details>

<details><summary>解答例</summary>

```python
prices = [1000, 2500, 500]

for i in range(len(prices)):
    # 元の値を1.1倍して、元の場所に再代入する
    prices[i] = int(prices[i] * 1.1)

print(prices)
```

**実行結果**
```
[1100, 2750, 550]
```

**解説**
`for p in prices:` として `p = p * 1.1` としても、変数 `p` の中身が変わるだけで配列 `prices` の中身は変わりません。配列自体を変更したい場合は、必ず `prices[i]` のように箱を指定して代入する必要があります。
</details>



## レベル5：配列の応用問題

### 問題5-1
以下のリストから「60点以上の人（合格者）」だけの **平均点** を計算して表示するプログラムを作成してください。
`scores = [45, 90, 75, 60, 30, 85, 50, 100]`

<details><summary>解答例</summary>

```python
scores = [45, 90, 75, 60, 30, 85, 50, 100]
passing_total = 0
passing_count = 0

for s in scores:
    if s >= 60:
        passing_total += s
        passing_count += 1

if passing_count > 0:
    print(passing_total / passing_count)
```
</details>

### 問題5-2
以下のリストの中から、 **最大値（一番大きい数字）** を見つけて表示するプログラムを作成してください。
`numbers = [12, 45, 2, 9, 73, 56, 34]`
※Pythonには `max()` という関数がありますが、練習のため使わずに `for`文と `if`文でロジックを組んでみましょう。

<details><summary>ヒント</summary>
「暫定チャンピオン（現在見つかっている最大値）」を保存しておく変数を用意し、リストの数字と次々に戦わせて（比較して）、勝ったら入れ替えます。
</details>

<details><summary>解答例</summary>

```python
numbers = [12, 45, 2, 9, 73, 56, 34]

# 暫定の最大値を、とりあえずリストの最初の数字にしておく
max_val = numbers[0]

for n in numbers:
    # 今見ている数字(n)が、暫定最大値(max_val)より大きければ
    if n > max_val:
        max_val = n # 記録を更新する

print("最大値は " + str(max_val) + " です")
```

**解説**
この「最大値を探す」処理は、アルゴリズムの基本中の基本です。変数をバケツのように使い、ループしながら中身をより条件に合うものに入れ替えていくイメージを持ちましょう。

</details>


### 問題5-3
以下の2つの配列は、あるクラスの「生徒の名前」と「テストの点数」が、**同じ順序**で並んでいます（例：Aさんの点数は80点）。
この2つを使って、「◯◯さんの点数は◯◯点です」と全員分表示してください。

```python
names = ["Aさん", "Bさん", "Cさん", "Dさん"]
scores = [80, 65, 92, 50]
```

<details><summary>解答例</summary>

```python
names = ["Aさん", "Bさん", "Cさん", "Dさん"]
scores = [80, 65, 92, 50]

# 要素数は同じなので、どちらかの長さでループする
for i in range(len(names)):
    # 同じ「i番目」を使うことで、名前と点数を紐付ける
    print(names[i] + "の点数は" + str(scores[i]) + "点です")
```
</details>

### 問題5-4
上記の `names` と `scores` を使い、**「最高得点を取った人の名前」** を表示してください。

<details><summary>ヒント</summary>
レベル2でやった「最大値を見つけるロジック」を使います。ただし、保存しておくのは「最大スコア」だけでなく、「そのスコアを取った人の名前（またはそのインデックス）」も保存しておく必要があります。
</details>

<details><summary>解答例</summary>

```python
names = ["Aさん", "Bさん", "Cさん", "Dさん"]
scores = [80, 65, 92, 50]

# 暫定トップの情報を保存する変数
max_score = 0
top_student = ""

for i in range(len(scores)):
    # 今見ている点数が、暫定トップより高ければ
    if scores[i] > max_score:
        max_score = scores[i]   # 最高得点を更新
        top_student = names[i]  # その時の名前も記録しておく！

print("最高得点は " + top_student + " で、" + str(max_score) + "点でした")
```

**実行結果**
```
最高得点は Cさん で、92点でした
```

**解説**
これは実務でもよく使うロジックです。`i` という共通のインデックスを使うことで、「スコアが高い」と判断した瞬間に、同じ場所にある「名前」も取得することができます。
</details>




