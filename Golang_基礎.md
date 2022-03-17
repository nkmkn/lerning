# Golang��b
## �ϐ�
1. �����I�Ȓ�`
  - **var �ϐ��� �^ = �l**
  - �֐��̊O�ł��g�p�\�B
  - ��{�I�ɂ͂������̕����^���킩��₷���̂ł��������g���B
  ```go
  // ��{
  var i int     = 2
  var s string  = "Hello"
  var t, f bool = true, false
  ```

  ```go
  // �܂Ƃ߂Ē�`���� 
  var (
    i int = 2
    s = string = "Hello"
  )
  ```

  ```go
  // �錾�̂�
  var i int
  var s string
  ```
  
2. �ÖٓI�Ȓ�`
  - **�ϐ��� := �l**
  - �֐��̊O�ł͎g�p�s��
  ```go
  i := 2
  s := "Hello"
  t, f := true, false
  ```
<br>
<br>

## ��{�^
### �z��
�ォ��v�f����ύX���邱�Ƃ��ł��Ȃ��B

#### ��`
```go
// �v�f��3�̔z��array���`�B�����l�� [0,0,0]�B
var array [3]int
```

```go
// �v�f��3�̔z��array���`�B�����l�� [1,2,3]�B
var array [3]int = [3]int{1,2,3}
```

```go
// �v�f��3�̔z��array���`�B�����l�� [A,B,(�󕶎�)]�B
var array [3]string = [3]string{"A", "B"}
```

```go
// �z��array���Öْ�`�B�����l�� [1,2,3]�B
array := [3]int{1, 2, 3}
```
```go
// �z��array���`�B�����l�� [A,B]�B
array := [...]string{"A", "B"}
```
<br>

### interface�^
- �S�Ă̌^�ƌ݊���������B
- �����l�Ƃ���nil�����B
- ���Z���ł��Ȃ��B
```go
// ��`
var x interface{}

// ������^�����ł���B
x = 1
x = "A"
x = [3]int{1,2,3}
```
<br>

### �^�ϊ�
#### ������^?���l�^
```go 
var s string = "100"

//�ϊ�
i, err := strconv.Atoi(s)

//�G���[�n���h�����O(����Ȃ� err = nil �ŋA���Ă��� )
if err != nil{

}
```
#### ���l�^?������^
```go
var i int = 1

// �ϊ�
s := strconv.Itoa(i)

```
#### ������?�o�C�g�z��
```go
var s1 string = "Hello"

// �o�C�g�z��֕ϊ�
b := []byte(s1)

// ������ɕϊ�
s2 := string(b)
```
<br>
<br>

## �萔
```go
// �萔�̒�`�B�֐��̊O�Œ�`����B
const Pi = 3.14

// �����̒萔���`
const (
  URL = "http://xxxx.co.jp"
  SiteName = "test"
)

// �����̒萔���`����Ƃ��A�l���ȗ����đ�����邱�Ƃ��\
const (
  A = 1
  B /* 1�������Ă��� */
  C /* 1�������Ă��� */
  D = "A"
  E /* A�������Ă��� */
)

// �A�����鐮���̘A�Ԃ𐶐�����
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

## �֐�
### ��{
```go
// �Ԃ�l�����
func Plus(x int, y int) int {
  return x + y
}

// �Ԃ�l�������B�����������^�Ȃ�ȉ��̂悤�ɏȗ����ď�����B
func Div(x,y int) (int, int) {
  q := x / y
  r := x % y
  return q, r
}

// �Ԃ�l�̕ϐ����w��
func Double(price int) (result int) {
  result = price * 2
  return // return�̌���ȗ��ł���
}

// �Ԃ�l���Ȃ��ϐ�
func Noreturn() {
  fmt.Println("Hello")
  return
}
```
### �����֐�
```go
func main () {
  // f�Ƃ����ϐ��ɖ����֐����`
  f := func (x,y int) int {
    return x + y
  }

  // f�Ƃ����ϐ��ɓ����������֐��ŉ��Z 
  i := f(1,2)
}
```

```go
func main () {
  // f�Ƃ����ϐ����g�킸�ɂ��̂܂܏������邱�Ƃ��\�B
  i := func (x,y int) int {
    return x + y
  }(1,2)
}
```
### �֐���Ԃ��֐�
```go
// �Ԃ�l��func()
func ReturnFunc() func() {
  // �����֐���Ԃ�
  return func() {
    fmt.Println("Hello")
  }
}

func main () {
  // �ϐ�f�Ɋ֐���o�^
  f := ReturnFunc()

  // ���s
  f()
}
```
### �֐��������ɂƂ�֐�
```go 
func CallFunction( f func() ) {
  f()
}

func main () {
  // �����֐��������ɂƂ�
  CallFunction( func() {
      fmt.Println("Hello")
  })
}
```
### �N���[�W���[
Go�̖����֐��̓N���[�W���[��
�N���[�W���[�i�֐���j�Ƃ́A�֐��Ɗ֐��̏����Ɋւ���֐��O�̊����Z�b�g���ĕ����߂����́B

https://artgear.hatenablog.com/entry/20120115/1326635158

```go
func Later() func(string) string {
  

}

```