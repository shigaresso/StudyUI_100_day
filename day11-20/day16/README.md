## ショートカット

Option + Command + P プレビューの再開
Option + Comman + Return プレビューの非表示

## SwiftUI

ビューは状態の変数であると言われている。  

```
Form {

}

Group {

}

Section {

}
```

## @State

View内で構造体のプロパティを変更出来ないので、変更したいプロパティに ＠State を付ける。  
なぜこれにクラスを使わないのかはパフォーマンスの為である。  
また、＠State は 1 つの View に保存される単純なプロパティ用に設計されている為、 @State private とすることが推奨される。  

## 双方向バインディング

TextField は読み込みだけでなく、書き込みの双方向バインディングをしたいので、 $name としなければいけない。  
Text は読み込みしかしないので、$name ではなく、 \(name) としている。  

```swift
struct ContentView: View {
    @State private var name = ""
    var body: some View {
        Form {
            TextField("Enter your name", text: $name)
            Text("Your name is \(name)")
        }
    }
}
```

## Viewをループで作成する

メニューの項目を配列にし、ForEach ループでメニューを制作したりする事に使う。

```swift
Form {
    ForEach(0 ..< 100) { number in
        Text("Row \(number)")
    }
}

// 上の省略構文
Form {
    ForEach(0 ..< 100) {
        Text("Row \($0)")
    }
}
```

```swift
struct ContentView: View {
    let students = ["Harry", "Hermione", "Ron"]
    @State private var selectedStudent = 0
    
    var body: some View {
        VStack {
            Picker("Select your student", selection: $selectedStudent) {
                ForEach(0 ..< students.count) {
                    Text(self.students[$0])
                }
            }
            
            Text("You choose: Student # \(students[selectedStudent])")
        }
    }
}
```

上のコードでは以下のことが言える。  

1. students 配列は変わることはないので ＠State を付ける必要がない。  
2. selectedStudent には ＠State が付く理由は Picker ビューで変更されるから。  
3. Picker の引数の文字列は読み上げ機能を利用した時に使われる。  
4. Picker は双方向性バインディングを用いている。  
ユーザーが Picker を変更するとプロパティが更新される。  
5. ForEach はstudents の要素数分カウントされる。
