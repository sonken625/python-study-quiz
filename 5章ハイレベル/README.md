
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



## レベル10：アルゴリズム入門（並べ替えと探索）

プログラミングの面接や試験でもよく出る、「仕組みを自分で作る」問題です。

### 問題10-1（バブルソートの再現）
以下の配列 `numbers` を、**小さい順（昇順）**に並べ替えてください。
Pythonには `sort()` という便利な機能がありますが、**勉強のために使わずに**、`for`文と `if`文を使って自力で並べ替えるロジックを書いてください。

```python
numbers = [5, 3, 8, 1, 2]
```

<details><summary>ヒント（アルゴリズムの考え方）</summary>
「隣り合う2つの数字」を比較し、左の方が大きければ場所を入れ替える（交換する）、という操作を何度も繰り返します。
1. `numbers[j]` と `numbers[j+1]` を比べる。
2. もし `numbers[j] > numbers[j+1]` なら、中身を入れ替える。
3. これを配列の先頭から末尾まで何度も繰り返す（2重ループが必要）。
</details>

<details><summary>解答例</summary>

```python
numbers = [5, 3, 8, 1, 2]

# 外側のループ：何回スキャンするか（要素数分繰り返せば確実）
for i in range(len(numbers)):
    # 内側のループ：隣同士を比較して進む
    # (len(numbers) - 1 - i) にしているのは、すでに後ろが決まっているため短縮できるが、
    # 難しければ range(len(numbers) - 1) でもOK
    for j in range(len(numbers) - 1):
        
        # 隣り合う要素を比較（左が大きい場合）
        if numbers[j] > numbers[j+1]:
            # 入れ替え（スワップ）処理
            temp = numbers[j]
            numbers[j] = numbers[j+1]
            numbers[j+1] = temp

print(numbers)
```
**実行結果**
```
[1, 2, 3, 5, 8]
```
**解説**
これは「バブルソート」と呼ばれる有名なアルゴリズムです。変数 `temp` を使った「値の交換テクニック」は必須スキルです。
</details>

### 問題10-2（重複の削除）
以下の配列 `data` には重複した数字が含まれています。
**「元の並び順を維持したまま」**、重複を取り除いた新しい配列 `unique_data` を作成してください。
（`set()` を使うと順序が変わってしまうことがあるため、`for`文で実装してください）

```python
data = [1, 3, 5, 1, 2, 3, 8, 1]
```

<details><summary>解答例</summary>

```python
data = [1, 3, 5, 1, 2, 3, 8, 1]
unique_data = []

for num in data:
    # 新しいリストに「まだ入っていない」なら追加する
    if num not in unique_data:
        unique_data.append(num)

print(unique_data)
```
**解説**
`if 値 in 配列:` は「配列の中に値が含まれているか」をチェックします。これの逆（`not in`）を使うことで、「まだ登録されていないものだけ追加する」というロジックが組めます。
</details>

---

## レベル11：データの分析ロジック（移動と範囲）

実務でデータを扱う際、「特定の範囲だけ計算したい」という場面で使う頭の使い方です。

### 問題11-1（移動平均の計算）
株価の分析などで使われる「移動平均」を計算します。
以下の `sales` 配列について、**「連続する3日間の平均」**を順番に計算して表示してください。
（1〜3日目の平均、2〜4日目の平均、3〜5日目の平均…という順です）

```python
sales = [10, 20, 30, 40, 50, 60]
```
**期待する出力例**
```
期間1の平均: 20.0  (10+20+30の平均)
期間2の平均: 30.0  (20+30+40の平均)
...
```

<details><summary>ヒント</summary>
`sales[i]` から `sales[i+2]` までの3つを足して3で割ります。
`i` が増えすぎると `i+2` が配列の外に出てエラーになるので、ループの回数（rangeの範囲）に注意してください。
</details>

<details><summary>解答例</summary>

```python
sales = [10, 20, 30, 40, 50, 60]

# 最後の要素の2つ手前までループする（3つセットで作るため）
for i in range(len(sales) - 2):
    # 3つの要素の合計を計算
    part_sum = sales[i] + sales[i+1] + sales[i+2]
    
    # 平均を出す
    avg = part_sum / 3
    print("期間" + str(i+1) + "の平均: " + str(avg))
```
</details>

### 問題11-2（順位付け）
以下のテストの点数 `scores` について、それぞれの点数が**「全体の中で何位か」**を表示してください。
（点数が高い順に1位、2位…とします。同じ点数の場合は同じ順位で構いません）

```python
scores = [70, 90, 80, 70, 100]
```
**ヒント**: ある点数について「自分より点数が高い人が何人いるか」を数えれば、順位がわかります（自分より上が0人なら1位、1人なら2位）。

<details><summary>解答例</summary>

```python
scores = [70, 90, 80, 70, 100]

for my_score in scores:
    rank = 1 # 最初は1位だと仮定する
    
    # 全員と比べてみる
    for other_score in scores:
        # もし自分より高い点数の人がいたら
        if other_score > my_score:
            rank = rank + 1 # 順位を下げる
            
    print(str(my_score) + "点は " + str(rank) + "位です")
```
**解説**
これも2重ループの典型的な応用例です。「自分(外側のループ)」と「みんな(内側のループ)」を総当たりで比較してカウンターを動かす手法はよく使われます。
</details>

---

## レベル12：状態管理と文字列操作（パズル系）

ここが解ければ、「配列操作はかなり得意」と言っていいレベルです。

### 問題12-1（ランレングス圧縮のロジック）
文字列圧縮アルゴリズムの基礎です。
`"AAABBCCCCA"` のように同じ文字が続く文字列があります。これを**「文字」＋「続く回数」**の形式で表示してください。
（期待する表示：`A3 B2 C4 A1`）

```python
text = "AAABBCCCCA"
```

<details><summary>ヒント</summary>
ループを回しながら、以下を管理する必要があります。
1. `current_char`：今なんの文字を数えているか
2. `count`：その文字が何回続いているか

「次の文字」を見て、**同じならカウントアップ**、**違うならそこで集計してリセット**、という切り替えを行います。
</details>

<details><summary>解答例</summary>

```python
text = "AAABBCCCCA"

if len(text) > 0:
    current_char = text[0] # 最初の文字
    count = 1

    # 2文字目から最後までループ
    for i in range(1, len(text)):
        next_char = text[i]
        
        if next_char == current_char:
            # 同じ文字が続いている
            count += 1
        else:
            # 文字が変わった！ここまでの結果を表示
            print(current_char + str(count), end=" ")
            
            # 新しい文字に切り替えてカウントリセット
            current_char = next_char
            count = 1
            
    # 最後の文字の結果を表示（ループが終わった後に残っている分）
    print(current_char + str(count))
```
**解説**
この問題の難しいところは、「文字が変わったタイミング」で前の文字の結果を出力することと、**「最後の文字」はループ内で「文字が変わる瞬間」が来ないため、ループの外で出力する必要がある**点です。これを「境界値処理」といい、バグを生みやすいポイントです。
</details>

### 問題12-2（行列の入れ替え：転置）
3行3列のデータ `matrix` があります。この**「行と列」を入れ替えた**新しい配列 `transposed` を作ってください。
（1行目を1列目に、2行目を2列目にする）

```python
# 元のデータ
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# 作りたいデータ
# [
#    [1, 4, 7],
#    [2, 5, 8],
#    [3, 6, 9]
# ]
```

<details><summary>解答例</summary>

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# 結果を入れるための空の2次元配列を作る（3行分）
transposed = [[], [], []]

for i in range(len(matrix)):       # 行のループ (0, 1, 2)
    for j in range(len(matrix[i])):   # 列のループ (0, 1, 2)
        # matrix[i][j] を transposed[j][i] に入れるイメージ
        # appendを使って追加していく
        transposed[j].append(matrix[i][j])

print(transposed)
```

**別解（空の箱を用意しないパターン）**
```python
transposed = []
for j in range(3): # 列数分ループ
    new_row = []
    for i in range(3): # 行数分ループ
        new_row.append(matrix[i][j]) # 列を固定して行を動かす
    transposed.append(new_row)
```

**解説**
「2重ループの `i` と `j` の役割を逆にする」という発想が必要です。画像処理（画像の回転）などでも使われる重要な考え方です。
</details>

 