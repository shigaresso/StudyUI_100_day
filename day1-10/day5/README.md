## 関数

関数を使用すると、コードが再利用出来る。  
プログラミングにおいて一般的には、コードを繰り返すことは悪い考えだ。  
関数はそれを避ける事に役立つ。  

関数の利点  
1. 同じコードが複数必要な場合 1 つの記述で全ての部分が変更される  
2. 大きな 1 つの関数を小さな関数に分割することで、コードを読むのが簡単になる  
3. 既存の関数から、新しい関数を作成できる

### 関数のパラメーターの個数

6 つ以上だとパラメーターが多いと考える。  
その場合、関数を分割出来るか考える。  
それが出来ない場合はパラメーターをグループ化(タプルなど)出来ないか考える。  

ここでは、戻り値に複数のパラメーターを含ませたい場合、タプルが良い理由を述べる。  
そこで、人の名前を返す関数を考える。  

配列の場合  

```swift
func getUser() -> [String] {
    ["Taylor", "Swift"]
}

let user = getUser()
print(user[0])
```

これには　2 つの問題がある。  
1. 一部の場所では　Swift Taylor と名前を記述することがある。  
その場合、配列のインデックス 0, 1 ではどちらがファーストネームかラストネームかわからない。  
2. ミドルネームを挿入した場合、インデックス番号が変化するので問題になる。 
そして、どれがミドルネームなのか判断のしようがない。   

辞書の場合

```swift
func getUser() -> [String: String] {
    ["first": "Taylor", "last": "Swift"]
}

let user = getUser()
print(user["first"])
```

今回は user["first"] でファーストネームを呼び出せるので、ミドルネームを挿入しても問題にはならない。  
ただし、まだ理想的ではない。  

1. user["first"] だとキーが "First" だと nil になる。  
2. ファーストネーム、ラストネームと別れているかわからない(例：Beyonce など)
3. 値が確実にあるかわからないから値を読み取る時に常にオプションのラップが必要になる。  

タプルの場合

```swift
func getUser() -> (first: String, last: String) {
    (first: "Taylor", last: "Swift")
}

let user = getUser()
print(user.first)
```

1. タプルなので、パラメーターのキーに該当する部分をしっかり合わせないといけない。  
これによりミドルネームを挿入してもミドルネームのキーに入れないといけない。  
2. 値の読み取り中に大文字、小文字を区別しなければいけないという間違いを補完に出てくるため犯さない。
3. キー部分がない場合は nil ではなく空文字になる。  
4. オプショナルがない。  

これらの理由により、タプルは関数からの複数のパラメーターの戻り値に相応しい。  

### 関数の呼び出しの速度

関数の呼び出し(実行)には時間がかかり、コードの時間の比率として 5 割が関数の呼び出しにかかる。  

## 関数の戻り値

複数の値が必要な場合、タプルなどを使う

## 可変個引数関数

引数の型に ... をつける事で引数の数を可変に出来る。  

```swift
func square(numbers: Int...) {
    for number in numbers {
        print("\(number) squared is \(number * number)")
    }
}
```

## 関数での三項間演算子

関数内の式が 1 つだと return を記述しなくて済む。  
なので関数内や SwiftUI 内では特に利用される事が多い。  

## 関数ラベルの存在意義

```swift
func setAge(for person: String, to value: Int) {
    print("\(person) is now \(value)")
}
// ポールの年齢を40歳に設定してください と文っぽい
setAge(for: "Paul", to: 40)

// 年齢設定者ポール値40 と良くわからない
setAge(person: "Paul", value: 40)
```

逆に外部ラベルを使わない場合

```swift
func setAge(for: String, to: Int) {
    // for is now to だと意味がわからない
    print("\(for) is now \(to)")
}
```

## スロー関数

エラーがあった場合 catch して欲しい式全てに対して try をつける
