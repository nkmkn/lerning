# Golang基礎
## 変数
1. 明示的な定義
  - **var 変数名 型 = 値**
  - 関数の外でも使用可能。
  - 基本的にはこっちの方が型がわかりやすいのでこっちを使う。
  ```go
  // 基本
  var i int     = 2
  var s string  = "Hello"
  var t, f bool = true, false
  ```

  ```go
  // まとめて定義する 
  var (
    i int = 2
    s = string = "Hello"
  )
  ```

  ```go
  // 宣言のみ
  var i int
  var s string
  ```
  
2. 暗黙的な定義
  - **変数名 := 値**
  - 関数の外では使用不可
  ```go
  i := 2
  s := "Hello"
  t, f := true, false
  ```
<br>
<br>

## 基本型
### 配列
後から要素数を変更することができない。

#### 定義
```go
// 要素数3の配列arrayを定義。初期値は [0,0,0]。
var array [3]int
```

```go
// 要素数3の配列arrayを定義。初期値は [1,2,3]。
var array [3]int = [3]int{1,2,3}
```

```go
// 要素数3の配列arrayを定義。初期値は [A,B,(空文字)]。
var array [3]string = [3]string{"A", "B"}
```

```go
// 配列arrayを暗黙定義。初期値は [1,2,3]。
array := [3]int{1, 2, 3}
```
```go
// 配列arrayを定義。初期値は [A,B]。
array := [...]string{"A", "B"}
```
<br>

### interface型
- 全ての型と互換性がある。
- 初期値としてnilを持つ。
- 演算ができない。
```go
// 定義
var x interface{}

// あらゆる型を代入できる。
x = 1
x = "A"
x = [3]int{1,2,3}
```
<br>

### 型変換
#### 文字列型?数値型
```go 
var s string = "100"

//変換
i, err := strconv.Atoi(s)

//エラーハンドリング(正常なら err = nil で帰ってくる )
if err != nil{

}
```
#### 数値型?文字列型
```go
var i int = 1

// 変換
s := strconv.Itoa(i)

```
#### 文字列?バイト配列
```go
var s1 string = "Hello"

// バイト配列へ変換
b := []byte(s1)

// 文字列に変換
s2 := string(b)
```
<br>
<br>

## 定数
```go
// 定数の定義。関数の外で定義する。
const Pi = 3.14

// 複数の定数を定義
const (
  URL = "http://xxxx.co.jp"
  SiteName = "test"
)

// 複数の定数を定義するとき、値を省略して代入することが可能
const (
  A = 1
  B /* 1が入っている */
  C /* 1が入っている */
  D = "A"
  E /* Aが入っている */
)

// 連続する整数の連番を生成する
const (
  c0 = iota
  c1
  c2
)
func main(){
}
```
<br>
<br>

## 関数
### 基本
```go
// 返り値が一つ
func Plus(x int, y int) int {
  return x + y
}

// 返り値が複数。引数が同じ型なら以下のように省略して書ける。
func Div(x,y int) (int, int) {
  q := x / y
  r := x % y
  return q, r
}

// 返り値の変数を指定
func Double(price int) (result int) {
  result = price * 2
  return // returnの後を省略できる
}

// 返り値がない変数
func Noreturn() {
  fmt.Println("Hello")
  return
}
```
### 無名関数
```go
func main () {
  // fという変数に無名関数を定義
  f := func (x,y int) int {
    return x + y
  }

  // fという変数に入った無名関数で演算 
  i := f(1,2)
}
```

```go
func main () {
  // fという変数を使わずにそのまま処理することも可能。
  i := func (x,y int) int {
    return x + y
  }(1,2)
}
```
### 関数を返す関数
```go
// 返り値がfunc()
func ReturnFunc() func() {
  // 無名関数を返す
  return func() {
    fmt.Println("Hello")
  }
}

func main () {
  // 変数fに関数を登録
  f := ReturnFunc()

  // 実行
  f()
}
```
### 関数を引数にとる関数
```go 
func CallFunction( f func() ) {
  f()
}

func main () {
  // 無名関数を引数にとる
  CallFunction( func() {
      fmt.Println("Hello")
  })
}
```
### クロージャー
Goの無名関数はクロージャーで
クロージャー（関数閉包）とは、関数と関数の処理に関する関数外の環境をセットして閉じ込めたもの。

https://artgear.hatenablog.com/entry/20120115/1326635158

```go
func Later() func(string) string {
  

}

```