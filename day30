# 30日目

## 配列への追加方法の違い

配列への追加方法の違いによって View に表示される時に違いが生じる

```swift
配列名.append(追加する要素)
// こちらの場合は作成される View が一番下に追加されるので、数が多くなると画面外に配置される可能性がある
```

```swift
配列名.insert(追加する要素, at: 0)
// こちらの場合は作成される View が一番上に追加されるので、自動的に上部にスライドされる
```

## List に 2番目の View を追加する

自動的に HStack になる

```swift
List(usedWords, id: \.self) {
    Image(systemName: "\($0.count).circle")
    Text($0)
}
```
