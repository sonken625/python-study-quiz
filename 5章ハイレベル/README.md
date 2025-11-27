
## レベル6：2重ループ（ネスト）の世界

ここからは `for`文の中に `for`文を入れる「入れ子（ネスト）」構造の練習です。
最初は頭がこんがらがるかもしれませんが、「外側のループが1回まわる間に、内側のループが全部まわる」という動きを意識しましょう。

### 問題6-1（九九の計算）
1から9までの数字が入った配列 `numbers` を使って、九九の計算結果をすべて表示してください。
（1の段から9の段まで、`1 x 1 = 1` ... `9 x 9 = 81` のように表示）

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

<details><summary>ヒント</summary>
外側のループで「◯の段（left）」を決め、内側のループで「掛ける数（right）」を回します。
```python
for left in numbers:
    for right in numbers:
        # ここで計算と表示
```
</details>

<details><summary>解答例</summary>

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]

for i in numbers:
    for j in numbers:
        ans = i * j
        print(str(i) + " x " + str(j) + " = " + str(ans))
```

**解説**
外側の `i` が `1` の状態で、内側の `j` が `1〜9` まで動きます。それが終わると `i` が `2` になり、また `j` が `1〜9` まで動きます。これが2重ループの基本動作です。
</details>

### 問題6-2（総当たりの組み合わせ）
トランプの「マーク（絵柄）」と「数字」の配列があります。
この2つの配列を使って、存在するすべてのカードの組み合わせ（「ハートのA」「ハートの2」…）を表示してください。

```python
suits = ["ハート", "ダイヤ", "スペード", "クラブ"]
ranks = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]
```

<details><summary>解答例</summary>

```python
suits = ["ハート", "ダイヤ", "スペード", "クラブ"]
ranks = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]

count = 0
for s in suits:
    for r in ranks:
        print(s + "の" + r)
        count = count + 1

print("合計 " + str(count) + " 枚です")
```
</details>

### 問題6-3（重複なしの組み合わせ）
以下の配列 `teams` から、**自分自身以外のチーム**との対戦組み合わせをすべて表示してください。
（例：「Aチーム vs Aチーム」は表示してはいけません）

```python
teams = ["Aチーム", "Bチーム", "Cチーム", "Dチーム"]
```

<details><summary>ヒント</summary>
2重ループの中で `if`文を使い、「外側のチーム名」と「内側のチーム名」が**等しくない場合のみ**表示するようにします。
</details>

<details><summary>解答例</summary>

```python
teams = ["Aチーム", "Bチーム", "Cチーム", "Dチーム"]

for t1 in teams:
    for t2 in teams:
        if t1 != t2:
            print(t1 + " vs " + t2)
```
</details>

---

## レベル7：2次元配列（リストの中にリスト）

実務データ（Excelの表など）は「行と列」で管理されることが多いため、配列の中に配列を入れる構造がよく使われます。

### 問題7-1（2次元配列の参照）
以下の `matrix` は、3行3列の数字の並びを表しています。
2重ループを使って、すべての数字を順番に表示してください。

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

<details><summary>ヒント</summary>
`matrix` の要素1つひとつが「配列」であることに注意してください。
`for row in matrix:` で取り出した `row` は `[1, 2, 3]` という配列になります。
</details>

<details><summary>解答例</summary>

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    # row は [1, 2, 3] のような配列
    for num in row:
        print(num)
```
</details>

### 問題7-2（各行の合計）
Aさん、Bさん、Cさんの3人が、それぞれ「国語・数学・英語」のテストを受けました。
以下の `grades` 配列を使って、**一人ひとりの合計点**を表示してください。

```python
# [国語, 数学, 英語]
grades = [
    [80, 50, 60], # Aさんの点数リスト
    [90, 95, 100],# Bさんの点数リスト
    [40, 30, 50]  # Cさんの点数リスト
]
students = ["Aさん", "Bさん", "Cさん"]
```

<details><summary>解答例</summary>

```python
grades = [
    [80, 50, 60],
    [90, 95, 100],
    [40, 30, 50]
]
students = ["Aさん", "Bさん", "Cさん"]

for i in range(len(grades)):
    # その人の点数リストを取り出す（例：[80, 50, 60]）
    person_scores = grades[i]
    
    # その人の合計を計算する
    total = 0
    for s in person_scores:
        total = total + s
        
    print(students[i] + "の合計点は " + str(total) + "点です")
```
</details>

---

## レベル8：インデックス操作の応用（前後比較）

「前の日と比べて増えたか？」「隣り合う数字の差は？」など、配列内の**隣同士**を比較するテクニックです。

### 問題8-1（前日比の計算）
あるお店の1週間の売上が `sales` 配列に入っています。
**「前日と比べていくら増えたか（または減ったか）」** を毎日表示してください。
（初日は比較対象がないので、2日目以降から表示してください）

```python
sales = [100, 120, 110, 150, 150, 90, 140]
```

<details><summary>ヒント</summary>
`i`番目の日の売上は `sales[i]` です。では、「前日」の売上はインデックスを使ってどう書けるでしょうか？
また、ループは `range(1, len(sales))` として1番目（2日目）からスタートさせるのがコツです。
</details>

<details><summary>解答例</summary>

```python
sales = [100, 120, 110, 150, 150, 90, 140]

# 1番目（2日目）からスタート
for i in range(1, len(sales)):
    today = sales[i]
    yesterday = sales[i-1] # 1つ前の要素を取得
    
    diff = today - yesterday
    print(str(i+1) + "日目の前日比: " + str(diff))
```

**実行結果**
```
2日目の前日比: 20
3日目の前日比: -10
4日目の前日比: 40
...
```
</details>

### 問題8-2（隣り合う重複の検出）
以下の配列 `colors` の中で、**「同じ色が連続して並んでいる箇所」**を見つけ、「◯◯が連続しています」と表示してください。

```python
colors = ["赤", "青", "青", "緑", "黄", "黄", "黄", "黒"]
```

<details><summary>解答例</summary>

```python
colors = ["赤", "青", "青", "緑", "黄", "黄", "黄", "黒"]

# 最後の1つ手前までループする（i+1と比較するため）
for i in range(len(colors) - 1):
    if colors[i] == colors[i+1]:
        print(colors[i] + " が連続しています")
```

**解説**
`colors[i]` と `colors[i+1]` を比較する場合、`i` が最後の要素まで行ってしまうと `i+1` が範囲外（エラー）になります。そのため、`range(len(colors) - 1)` としてループ回数を1回減らす必要があります。
</details>

---

## レベル9：実務的な文字列処理と配列

### 問題9-1（CSVデータの解析）
以下の文字列 `csv_data` は、カンマ区切りでデータが並んでいます。
これを分解して配列にし、さらに数値に変換して合計を表示してください。

```python
csv_data = "100,200,300,40,5"
```
※Pythonには `文字列.split(",")` という命令があり、これを使うとカンマで区切って配列にしてくれます。

<details><summary>解答例</summary>

```python
csv_data = "100,200,300,40,5"

# カンマで分割して配列にする
str_list = csv_data.split(",")
# この時点で str_list は ["100", "200", ...] という文字の配列

total = 0
for s in str_list:
    # 文字を整数に変換して足す
    total = total + int(s)

print("合計: " + str(total))
```
</details>

### 問題9-2（データのクレンジング）
アンケート結果の配列 `answers` がありますが、無回答（空文字 `""`）が含まれています。
無回答を除外した、新しい配列 `valid_answers` を作成してください。

```python
answers = ["賛成", "", "反対", "賛成", "", "反対", "その他"]
```

<details><summary>解答例</summary>

```python
answers = ["賛成", "", "反対", "賛成", "", "反対", "その他"]
valid_answers = []

for ans in answers:
    # 空文字でない場合のみ追加
    if ans != "":
        valid_answers.append(ans)

print(valid_answers)
```
</details>

