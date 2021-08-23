# 35日目

## ForEachについて

何故次のコードは上の書き方ではないといけないのか？  
SwiftUI の ForEach のコードの定義が Range<Int> だから  

```swift
// Range<Int> true
ForEach(0..<5) {}

// ClosedRange<Int> false
ForEach(0...5) {}
```

## string.countについて

string.count は文字列を先頭から数えるので正しいことが保障されるが、文字列の数に依存するため、高速ではない。  
