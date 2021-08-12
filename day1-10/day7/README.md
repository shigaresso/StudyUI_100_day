## 構造体

型の定義

```swift
struct Sport {
    var name: String
}

// 構造体はインスタンスを作成して使用する。
var tennis = Sport(name: "Tennis")
print(tennis.name)

// 構造体のプロパティは変数と同じように値の変更が出来る。
tennis.name = "Lawn tennis"
```

### タプルと構造体の違い

タプルは名前のない構造体のようなもの。

```swift
// タプル
(
    name: String,
    age: Int, 
    city: String
)

// 構造体
struct User {
    var name: String
    var age: Int
    var city: String
}
```

ただし、タプルは 1 回の使用ならいいが、以下のようになると新しい変数をタプルに追加する場合変更が大変だ。  
構造体なら少なくとも引数を変更する必要はない。  

```swift
func authenticate(_ user: (name: String, age: Int, city: String)) { ... }
func showProfile(for user: (name: String, age: Int, city: String)) { ... }
func signOut(_ user: (name: String, age: Int, city: String)) { ... }
```

タプルは 2 つ以上のデータを返したい場合、関数の戻り値に使うが引数に使う場合や、関数間での複数回のやり取りの場合は、構造体の方が良い。  

## storedプロパティと、computedプロパティ

storedプロパティは
computedプロパティはコードを実行して値を計算する。 

```swift
struct Sport {
    // ストアドプロパティ
    var name: String
    var isOlympicSport: Bool

    // コンピューテッドプロパティ
    var olympicStatus: String {
        if isOlympicSport {
            return "\(name) is an Olympic sport"
        } else {
            return "\(name) is not an Olympic sport"
        }
    }
}
```

値が変更されていなくても読み込む場合は、ストアドプロパティが良い。  
プロパティが読み取られない場合はメモリに保存する必要がないので、コンピューテッドプロパティが良い。  

## プロパティオブザーバー

didSet を用いると値が変化した時に自動でコードを実行する。  

```swift
struct Progress {
    var task: String
    var amount: Int {
        // amount が変更されるとこのコードが実行される
        didSet {
            print("\(task) is now \(amount)% complete")
        }
    }
}
```

時間が掛かるコードの場合はアプリに様々な問題を起こす。  

## メソッド

構造体、列挙型、クラスなどの型に属している関数はメソッドと呼ばれる。  
また、メソッドは名前空間の汚染を回避する。  
これによって関数の名前衝突がなくなる。  
必要に応じて構造体内のプロパティをメソッドのスコープ内で使える。  

```swift
struct City {
    var population: Int
    
    func collectTaxes() -> Int {
        return population * 1000
    }
}

let london = City(population: 9_000_000)
london.collectTaxes()
print(london.population)
```

## Mutating Method
 
メソッド内でその構造体のプロパティを変更したい場合、 mutating とメソッドの宣言の前に付ける。  

```swift
struct Person {
    var name: String

    mutating func makeAnonymous() {
        name = "Anonymous"
    }
}
var person = Person(name: "Ed")
person.makeAnonymous()
print(person.name)
```

## 文字列は構造体

構造体だから以下のような事が元から備わっている。  

```swift
let string = "Do or do not, there is no try."
print(string.uppercased())
```

## イニシャライザ

プロパティと同じ初期化子を作成する場合、 self が必要になる。

```swift
struct Person {
    var name: String
    
    init(name: String) {
        print("\(name) was born!")
        self.name = name
    }
}

let person = Person(name: "Swift")
print(person.name)
```

## Lazy Property

最初に使用された時にプロパティを作成するようにする。  

## 静的プロパティ

構造体において静的プロパティは全てのインスタンス間で共有される。  

```swift
struct Student {
    static var classSize = 0
    var name: String

    init(name: String) {
        self.name = name
        Student.classSize += 1
    }
}

let ed = Student(name: "Ed")
let taylor = Student(name: "Taylor")
print(Student.classSize)
// => 2
```

## アクセス制御

プロパティやメソッドに private を付ける事で構造体外からそれを使うことが出来ない。  

```swift
struct Person {
    private var id: String

    init(id: String) {
        self.id = id
    }
    
    func identify() -> String {
            return "My social security number is \(id)"
        }
}
let ed = Person(id: "12345")
print(ed.identify())
```
