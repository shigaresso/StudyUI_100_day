## SwiftUIはなぜ構造体なのか？

UIKit や AppKit はビューにクラスを用いている。  
SwiftUI が構造体な理由は、いくつかある。  
1. パフォーマンス  
構造体は、クラスより単純で高速である。  

2. クリーンな分離  
クラスは値を自由に変更出来てしまう。  
なのでコードが煩雑になる可能性がある。  
SwiftUI は時間が経過しても変化しないビューを作成する。  

## 修飾子に条件をつける

一番簡単な方法は三項間演算子を使用することである。  

```swift
struct ContentView: View {
    @State private var useRedText = false
    
    var body: some View {
        Button("Hello, World!") {
            self.useRedText.toggle()
        }
        .foregroundColor(useRedText ? .red : .blue)
    }
}
```

## プロパティとしてビューを作成する

プロパティとしてビューを作成すると、body のコードの見通しがいい。

```swift
struct ContentView: View {
    let motto1 = Text("Draco dormiens")
    let motto2 = Text("nunquam titillandus")
    
    var body: some View {
        VStack {
            motto1
                .foregroundColor(.red)
            motto2
                .foregroundColor(.blue)
        }
    }
}
```

Swift ではストアドプロパティを参照とするストアドプロパティを作成できない。  
この問題は TextField をローカルプロパティへのバインドを作成しようとすると問題が発生する。  

## 複雑なビューを小さなビューに分割

SwiftUI を利用すれば、パフォーマンスに影響を与えることなく、複雑なビューを小さなビューに分割出来る。  

このコードを  

```swift
struct ContentView: View {
    var body: some View {
        VStack(spacing: 10) {
            Text("First")
                .font(.largeTitle)
                .padding()
                .foregroundColor(.white)
                .background(Color.blue)
                .clipShape(Capsule())

            Text("Second")
                .font(.largeTitle)
                .padding()
                .foregroundColor(.white)
                .background(Color.blue)
                .clipShape(Capsule())
        }
    }
}
```

このコードに変える  

```swift
struct ContentView: View {

    var body: some View {
        VStack(spacing: 10) {
            CapsuleText(text: "First")
            CapsuleText(text: "Second")
        }
    }
}

// カスタムビュー
// 別ファイルにこちらの構造体を書いても良い
struct CapsuleText: View {
    var text: String
    
    var body: some View {
        Text(text)
            .font(.largeTitle)
            .padding()
            .foregroundColor(.white)
            .background(Color.blue)
            .clipShape(Capsule())
    }
}
```

## ViewModifier

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .modifier(Title())
    }
}

struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .foregroundColor(.white)
            .padding()
            .background(Color.blue)
            .clipShape(RoundedRectangle(cornerRadius: 10))
    }
}
```

カスタム修飾子を使用する場合、ラップすると良い。  

```swift
extension View {
    func titleStyle() -> some View {
        self.modifier(Title())
    }
}
```

## 構造体とクラスの違い

1. クラスにはメンバーごとの初期化子がない。  
構造体にはデフォルトでこれらを取得する。  
2. クラスは継承できるが、構造体は出来ない。
3. クラスをコピーした場合、両方が同じになる。  
構造体はそれぞれが別。  
4. クラスはでイニシャライザを持つ。  
構造体は持たない。  
5. 定数クラス内の変数プロパティを変更出来る。  
定数構造体の場合、プロパティは変数、定数であるかに関わらず固定される。  

## didSetと@State


## ボタンを利用して配列を動的に追加する


ForEach() の部分で ForEach(0..<arrays.count) とすると動的に生成出来ない。  
なので、 ForEach(arrays, id: \.self) としなければいけない。  

```swift
struct ContentView: View {
    @State private var arrays = ["りんご", "りんご", "りんご"]
    
    var body: some View {
        VStack {
            List {
                ForEach(arrays, id: \.self) { array in
                    Text(array)
                }
            }
            // こちらでも可
            List {
                ForEach(arrays, id: \.self) { 
                    Text($0)
                }
            }
            Spacer()
            
            Button(action: {addArray()}) {
                Text("追加")
                    .padding()
                    .background(Color.green)
            }
        }
    }
    
    func addArray() {
        arrays.append("りんご")
    }
}
```

## static変数

構造体内のプロパティが構造体内の別のプロパティからアクセスされようとすると、 Swift はプロパティが作成される順序を認識していないので、エラーが出る。  
static をつけることで、構造体の特定のインスタンスではなく、構造体自身に属する(インスタンス化した全ての構造体で共有される)ので通常のプロパティは静的プロパティを参照できる。  

## リストの動的生成

```swift
List {
    Text("Static row 1")

    ForEach(0..<5) {
        Text("Dynamic row \($0)")
    }

    Text("Static row 2")
}
```

ただし、リスト内が静的生成を含まず、全て動的生成の場合は ForEach を用いずに書ける。  

```swift
List(0..<5) {
    Text("Dynamic row \($0)")
}
```
