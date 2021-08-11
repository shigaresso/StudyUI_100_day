## forループについて

for ループの書き方は以下のようになる。  

```swift
let count = 1...10
for number in count {
    print("Number is \(number)")
}
```

配列を使ったループも可能である。  

```swift
let albums = ["Red", "1989", "Reputation"]
for album in albums {
    print("\(album) is on Apple Music")
}
```

for ループが与える定数を使用しない場合、代わりにアンダースコアを使用し、Swift が不要な値を作成しないようにする。  

```swift
for _ in 1...5 {
    print("play")
}
```
