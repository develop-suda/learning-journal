# Learning Journal - November 2024

## 目次
- [11月28日](#11月28日)

## 11月28日
[実用Go言語](https://www.oreilly.co.jp/books/9784873119694/)

#### 1.4章 Goのエラーを扱う

基本的に既に持っている知識、超基本的なことが書かれていた

やっぱりGo内部の処理をみると理解が深まるね

``` go
type error interface {
    Error() string
}
````