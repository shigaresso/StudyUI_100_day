## 三項間演算子

名前の由来は一度に 3 つの値を処理するから。  

```swift
let firstCard = 11
let secondCard = 10
print(firstCard == secondCard ? "Cards are the same" : "Cards are different")
```

あまり使用は推奨されていない。  

## なぜ　else を利用するのか

以下のコードでも正常に動作する。  
しかし score の値を 2 回チェックする事になる。  
このくらい単純だと差はないが、コードがより複雑な場合は、遅くなる。  

```swift
let score = 9001

if score > 9000 {
    print("It's over 9000!")
}

if score <= 9000 {
    print("It's not over 9000!")
}

```

従って else を用いるとチェックする回数が 1 度になり早くなる。

```swift
let score = 9001

if score > 9000 {
    print("It's over 9000!")
} else {
    print("It's not over 9000!")
}
```

## switch ステートメント

同じ値について条件分岐をさせる場合は、if よりも switch がわかりやすい場合が良くある。  
他の言語と違い、 break は不要。  
ただし、続けたい場合に fallthrough と記述する。  

```swift
let weather = "sunny"

switch weather {
case "rain":
    print("Bring an umbrella")
case "snow":
    print("Wrap up warm")
case "sunny":
    print("Wear sunscreen")
    fallthrough
default:
    print("Enjoy your day!")
}
```

## ハーフオープンレンジがある理由

配列などのインデックスが 0 から始まり、要素数 − 1 で終わるので使いやすい。  


## forループではなくwhileループを使う場合

繰り返し回数が不確定な時や、ユーザーが任意のタイミングで止めたい場合。  


## リピートループの使い所

元の配列をコピーし、要素の順番をランダム化する。  
ただし、コピーした配列の順番はコピー元の順番とは別にしたい。

```swift
let numbers = [1, 2, 3, 4, 5]
let random = numbers.shuffled()

while random == numbers {
    random = numbers.shuffled()
}
```

上のコードだと、

```swift
random = numbers.shuffled()
```

を 2 度書いている。  
単純なコードなら良いが、繰り返しているコード部分が多くなればなるほど困る。  
よって、以下のように書くと解決される。  

```swift
let numbers = [1, 2, 3, 4, 5]
var random: [Int]

repeat {
    random = numbers.shuffled()
} while random == numbers
```

## ラベル付きループの使い所

以下のコードは目当てのものが見つかってもループが終了しない。  

```swift
let options = ["up", "down", "left", "right"]
let secretCombination = ["up", "up", "right"]

for option1 in options {
    for option2 in options {
        for option3 in options {
            print("In loop")
            let attempt = [option1, option2, option3]

            if attempt == secretCombination {
                print("The combination is \(attempt)!")
            }
        }
    }
}
```

なので見つかったらループを終了させたい場合、以下のようにする。  

```swift
outerLoop: for option1 in options {
    for option2 in options {
        for option3 in options {
            print("In loop")
            let attempt = [option1, option2, option3]

            if attempt == secretCombination {
                print("The combination is \(attempt)!")
                break outerLoop
            }
        }
    }
}
```
