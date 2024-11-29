# Learning Journal - November 2024

## 目次
- [11月28日](#11月28日)

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

#### 5章　エラーハンドリング

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