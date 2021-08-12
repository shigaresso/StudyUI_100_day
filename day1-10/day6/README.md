## クロージャー

クロージャーは単なる無名関数？  
クロージャーは関数を 1 つの変数にまとめて格納できる。  
クロージャーの in はパラメーターの終わりとクロージャー本体の始まりを表す。  
クロージャーの例  

```swift
let driving = {
    print("I'm driving in my car")
}
driving()
```

下と何が違うのか不明  

```swift
func driving() {
    print("I'm driving in my car")
}
driving()
```

### クロージャーでパラメータを受け取る

クロージャーは関数と異なり呼び出す時に引数ラベルを使用しない。  

```swift
let driving = { (place: String) in
    print("I'm going to \(place) in my car")
}
driving("London")
```

### クロージャーから値を返す

パラメーターがある場合  

```swift
let driving = { (place: String) -> String in
    return "I'm going to \(place) in my car"
}

let message = driving("London")
print(message)
```

パラメーターがない場合

```swift
let payment = { () -> Bool in
    print("Paying an anonymous person...")
    return true
}
```

## パラメーターとしてクロージャーを使う

クロージャーは文字列や整数と同じように使用できるので、関数に渡す事ができる。  
利点は Siri をアプリと統合する時である。  

```swift
let driving = {
    print("I'm driving in my car")
}

func travel(action: () -> Void) {
    print("I'm getting ready to go.")
    action()
    print("I arrived!")
}

travel(action: driving)
```

## 末尾のクロージャー

```swift
func travel(action: () -> Void) {
    print("I'm getting ready to go.")
    action()
    print("I arrived!")
}

// 引数が 1 つしかなく、その末尾がクロージャーなので()を省略できる
travel {
    print("I'm driving in my car")
}
```
