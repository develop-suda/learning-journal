# Learning Journal - November 2024

## 目次
- [11月28日](#11月28日)
- [11月29日](#11月29日)
- [11月30日](#11月30日)

## 11月28日
[実用Go言語](https://www.oreilly.co.jp/books/9784873119694/)

#### 1.4章 Goのエラーを扱う

基本的に既に持っている知識、超基本的なことが書かれていた

やっぱりGo内部の処理をみると理解が深まるね

```go
type error interface {
    Error() string
}
```

## 11月29日
[実用Go言語](https://www.oreilly.co.jp/books/9784873119694/)

### 5章　エラーハンドリング
#### 5.1 エラーの書き方

##### 5.1.1 errors.New

```go
//  シンプルなエラーの生成、宣言
errors.New("エラーメッセージ")
```

##### 5.1.2 fmt.Errorf
``` go
func createError() error{
    return fmt.Errorf("エラーメッセージ: %v", "test")
}
```

#### 5.1.3 独自のエラー型
```go
//Errorインターフェースを満たした構造体を定義してあげて、独自のエラー型を作ろう

type validationError struct{
    msg string
}

func (vE *validationError) Error() string{
    return fmt.Sprintf("validation error message: %v",msg)
}
```

#### 5.1.4 エラーのラップ、アンラップ
errors.Unwrap()関数があってエラーをアンラップできる
ということで詳細を取り出せるよ

#### 5.1.5 エラーの色々な比較

```go
// エラーの値や形を調べる関数
errors.Is()
errors.As()
```

###### エラーを値として比較する
```go
//↓はエラーを値として比較することができる
//
errors.Is()

//定義
func Is(err, target error) bool

// こんな感じで使ってた
if err != nil {
    if !errors.Is(err,findRows) {
        return fmt.Errorf("hogehoge")
    }
}
```

## 11月30日
[実用Go言語](https://www.oreilly.co.jp/books/9784873119694/)
#### 5.2 エラーハンドリングの基本テクニック
##### 5.2.1 呼び出し元に関数の引数などの情報を付与してエラーを返す
```go
if err != nil {
    // このメッセージをそのまま返すのは後から確認する時分かりずらい
    return err
}
```

```go
if err != nil {
    // こんな感じでわかりやすいエラーを返そう
    // 本見て実際の感じを確認してくれ￥
    return fmt.Errorf("msg:%w email:%s",err,email)
}
```
##### 5.2.2 ログを出力して処理を継続する
DBからレコードがあった場合はそれを使うけど、なかった場合はデフォルトの値を使って処理を継続する、みたいな時
##### 5.2.3 リトライを実施する
ネットワーク呼び出しの場合一瞬接続できなくなる時とかあるから、何回かリトライする時とかに使うよ
##### 5.2.4 リソースをクローズする
いつものdeferについて
##### 5.2.5 複数のエラーをまとめる方法
同じエラー処理をまとめる方法が記載されているよ
マジで賢い・・・
コードは本読んで


複数の処理を実行し正常終了したものは有効、エラーはエラーとして報告する
かつエラーの詳細を保持するパッケージがあるよ
激アツ

##### 5.3  エラーのチェック忘れを予防する
##### 5.3.1　kisielk/errcheckの利用
##### 5.3.2　%w利用箇所の制限

