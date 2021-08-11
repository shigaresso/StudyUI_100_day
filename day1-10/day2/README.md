## 配列について

配列とは、単一の値として格納される値のコレクションのこと。  
配列は格納した順番の順序を持つ。  
配列名[数値] で値を取り出せる。  
ただし、存在しない配列番号の場合、Swift がクラッシュする。  

```swift
let john = "John Lennon"
let paul = "Paul McCartney"
let george = "George Harrison"
let ringo = "Ringo Starr"

let beatles = [john, paul, george, ringo]
beatles[1]
// => "Paul McCartney"

beatles[9]
// => エラー
```

型アノテーションを使用する場合は次の例のように書く。  

```swift
let beatles: [String] = [john, paul, george, ringo]
```

## セットについて

セットは 2 つの違いを除いて、配列と同じように値のコレクションである。  
1. 要素は順序を持たない。  
2. 同じ名前の要素を持てない。  
重複している場合は、2 つ目以降の重複したものを無視する。  

```swift
// Playground 上では毎回順序が異なる
let colors = Set(["red", "green", "blue"])

// 2 個目の red, blue は無視される
let colors2 = Set(["red", "green", "blue", "red", "blue"])
```

配列とセットの違いは検索する時に配列だと全てを検索する。  
セットだと重複がなく、一瞬である。  
要素があるかないかを検索したい場合はセットが有用である。  

## タプルについて

複数の値を 1 つの値にまとめて格納する事が出来る。  
配列のように感じるが異なる。    

1. タプルにアイテムを追加したり、削除したり出来ない。  
2. タプル内の型を変更出来ない。  
3. タプル内の要素には数値の位置や名前を書くことでアクセス出来る。  

タプルの作成方法は、次のように複数のアイテムを括弧で囲む事によって作成出来る。  
また、0 から始まる数値位置、または名前を利用して要素にアクセスする。  

```swift
var name = (first: "Tylor", last: "Swift")
name.0
name.first
```

配列とタプルの違い  
配列は可変長である。  
タプルはコレクション内に複数の型を持てる。  

## 配列　VS　セット　VS　タプル

||可変か|順序|重複|
|----|----|----|----|
|配列|可変|出来る|ある|許す|
|セット|可変|ない|許さない(唯一のものである必要性がある)|
|タプル|不可変|||


### タプルを使う利点

要素を追加したり削除出来ないため  
1. 各要素に正確な位置や名前がある(正確性が求められる時)  
2. 関連する値の固定のコレクションが必要な場合  

### セットを使う利点

1. 要素が重複してはいけない  
2. 検索速度が重要な場合  

### 配列を使う利点

1. 要素が重複する可能性がある  
2. 要素の順序が重要な場合

## 辞書について

辞書は配列と同じように、値のコレクションだが、整数の値で物を格納するのではなく、一般的にはキーと呼ばれる文字列で値にアクセスする。  

```swift
let heights = ["Teylor Swift": 1.78, "Ed Sheeran": 1.73]
heights["Teylor Swift"]
```

配列と辞書は似ているが、辞書だとキーを書けばアクセス出来る。  
配列だと番号を覚えておかないといけない。  
辞書はセットと同様に特定の順序でアイテムを保存しないのでキーのアイテムが即座に検索出来る。  
タプルとは異なり、辞書にキーが存在する事は保証することが出来ないので存在しないキーを要求した場合 nil が返ってくる。  
タプルの場合存在しなければ、エラーとなる。  

```swift
let week = Set(["Monday", "Tuesday", "Wednesday", "Thurday", "Friday", "Saturday", "Sunday"])

for day in week {
    print(day)
}
```

##　辞書のデフォルト値について

存在しないキーを指定した場合、nil が返される。  
その場合でも値が欲しい場合は、以下のように書く。  

```swift
let favoriteIceCream = [
    "Paul": "Chocolate",
    "Sophie": "Vanilla"
]
favoriteIceCream["Paul"]
// => "Chocolate"

favoriteIceCream["Charlotte"]
// => nil

favoriteIceCream["Charlotte", default: "Unknown"]
// => "Unknown"

```

## 空のコレクションを作成する

空の辞書を作る。  
エントリーの追加  

```swift
var teams = [String: String]()
teams["Paul"] = "Red"

teams
// => ["Paul": "Red"]
```

整数値を入れる空の配列  

```swift
var result = [Int]()
```

空のセットを作る場合

```swift
var words = Set<String>()
var numbers = Set<Int>()
```

セットの場合のみ空のコレクションの作り方が異なるように思えるが、これは辞書と配列には別の作り方があったからだ

```swift
var score = Dictionary<String, Int>()
var result = Array<Int>()

```

### なぜ空の配列を作りたいのか

全てのデータを事前に把握していない場合、空のコレクションを作成し、データを計算する時に追加するのが一般的。  

## 列挙について

関連する値のグループを使いやすくする方法である。  
実行中の作業を成功か失敗で表すコードを記述したい場合は、

```swift
let result = "failure"
```

とすればいいが、次のように他の異なった名前を使われるかもしれない。  

```swift
let result2 = "failed"
let result3 = "fail"
```

これらは全て異なる文字列なので意味が異なる。  
列挙型を使えば、今回で言えばResult型の success か failure のどちらか一つを使う事になる。  

```swift
enum Result {
    case success
    case failure
}

let result4 = Result.failure
```

これにより、誤って異なる文字列を使うことがなくなる。  
スペルミスもなくなる。  

### 列挙型の存在意義

列挙型を作ることで間違った物を宣言すると、Swift がエラーを出し、コードのビルドを拒否する。  
これによって間違ったものを参照しないので、安全になる。  

## 関連する値を列挙

列挙型に追加情報を付加する事により、より詳細なデータを表すことが出来る。  

```swift
enum Activity {
    case bored
    case running(destination: String)
    case talking(topic: String)
    case singing(volume: Int)
}

let talking = Activity.talking(topic: "football")
```

## 生の値を列挙する

列挙型に値を割り当てて意味を持たせる場合がある。  
これによって動的に作成したり、様々な方法で使用出来る。  
Swift は以下のコードに 0 から始まる番号を自動的に割り当てる。  

```swift
enum Planet: Int {
    case mercury
    case venus
    case earth
    case mars
}

let earth = Planet(rawValue: 2)
```

ただ、特定の値を割り当てたい場合は指定できる。  

```swift
enum Planet: Int {
    case mercury = 1
    case venus
    case earth
    case mars
}
```
