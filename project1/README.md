## グラデーション

グラデーションの要素  
1. 表示する色の配列
2. サイズとグラデーションの方向の情報
3. 使用するグラデーションの種類

## ボタン

ボタンのタイトルとボタンをタップしたときに実行する必要のあるクロージャーを渡す。  

```swift
Button("Tap me!") {
    print("Button was tapped")
}
```

画像や、ビューの組み合わせなど、他に何か必要な場合は、代替フォームを使用する。  

```swift
Button(action: {
    print("Button was tapped")
}) {
    Text("Tap me!")
}
```

画像をボタンに使いたい場合  

```swift
Button(action: {
    print("Edit button was tapped")
}) {
    Image(systemName: "pencil")
}
```

画像とテキストで 1 つのボタンにする。  

```swift
Button(action: {
    print("Edit button was tapped")
}) {
    HStack(spacing: 100) {
        Image(systemName: "pencil")
        Text("Edit")
    }
}
```

ボタンの色が青になる場合は、 .renderingMode(.original) をつける。   

## ビューのプロパティの変更

ビューのプロパティについて SwiftUI の構造体でメソッドから書き込む場合は変数の宣言時に ＠State が必要になる。
