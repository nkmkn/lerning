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
  var store string
  return func(next string) string {
    s := store
    store = next
    return s
  }
}

func main () {
  f := Later()
  fmt.Println(f("Hello"))
}
```
### �W�F�l���[�^�[
���炩�̃��[���ɏ]���ĘA�������l��Ԃ�������d�g�݂̂���

```go
// �N���[�W���[���g���ăW�F�l���[�^�[����邱�Ƃ��ł���
func intergers() func() int {
  i := 0
  return func() int {
    i++
    return i
  }
}
```
<br>
<br>

## ����\��
### if��
```go
func main () {
  
  /* ��{ */
  a := 0
  if a == 2 {

  } else if a == 1 {

  } else {

  }

  /* �ȈՕ��t��if�� */
  /* if �ȈՕ�; ������ */
  if b := 100; b == 100 {
      println(b)
      /* 100���o�͂���� */
  }
  println(b)
  /* ����`(0)���o�͂���� */
}
```
�Q�l : �ȈՕ��t��if�� 
https://code-database.com/knowledges/97


###�@�G���[�n���h�����O
```go
var s string = "100"

i, err := strcomv.Atoi(s)
if err {
  fmt.Prinfln(err)
}
```
### for
```go
/* ����loop */ 
for {

}
```

```go
i := 0
for i < 10{
  i++
}
```

```go
for i := 0 ; i < 10 ; i++ {

}
```

```go
// �z��̒��g�����o��
arr := [3]int{1,2,3}
for i := 0 ; i < len(arr) ; i++ {
  fmt.Println(arr[i])
}
```
```go
// �͈�for���Ŕz��̔ԍ��Ɨv�f�����o��
arr := [3]int{1,2,3}
for i, v := range arr {
  fmt.Println(i, v)
}
```
```go
// �͈�for���Ŕz��̔ԍ������o��
arr := [3]int{1,2,3}
for i := range arr {
  fmt.Println(i)
}
```
```go
// �͈�for���Ŕz��̗v�f�����o��
arr := [3]int{1,2,3}
for _, v := range arr {
  fmt.Println(v)
}
```

```go
// �X���C�X���z��Ɠ��l��range�Ŏ��o����
sl := []string{"Python", "PHP", "GO"}
for i, v := range sl {
  fmt.Println(i,v)
}
```

```go
// �}�b�v���z��Ɠ��l��range�Ŏ��o����
m := map[string]int{"apple":100, "banana":200}
for k,v := range m {
  fmt.Println(k,v)
}
```

### switch ���X�C�b�`
```go
/* ���ꂪ��{�Bcase 1,2�ŕ����l���w��ł���̂��֗��ȂƂ���B */
n := 2

switch n {
  case 1,2:
    fmt.Println("1 or 2")
  case 3,4:
    fmt.Println("3 or 4")
  default:
    fmt.Println("other")
}
```
```go
/* n��switch���̒��Œ�`�ł���B���̕����Ǐ��������߂邱�Ƃ��ł���B */
switch n:=2; n {
  case 1,2:
    fmt.Println("1 or 2")
  case 3,4:
    fmt.Println("3 or 4")
  default:
    fmt.Println("other")
}
```

```go
/* case�̔���͏��������������Ƃ��ł���B */
/* �������������ƒl��case����switch���̒��ɍ��݂����邱�Ƃ͂ł��Ȃ��B */
switch n:=2; n {
  case n > 0 && n < 4:
    fmt.Println("0 < n < 4")
  case n > 3 && n < 9:
    fmt.Println("3 < n < 9")
  default:
    fmt.Println("other")
}
```
### switch �^�X�C�b�`
```go
func anything (a interface{}) {
  fmt.Println(a)
}   

func main () {
  anything("aa")
  anything(1)

  var x interface{} = 3
  // �^�A�T�[�V���� �ϐ�.(�����������^)
  i := x.(int)
  fmt.Println(i+2)

  // ����̓G���[�B�v�Z���邱�Ƃ��ł��Ȃ��B
  // fmt.Println(x+2)


  /* x��3�Œ�`���Ă���̂ŁA�^�A�T�[�V�����ł����ɋ����I������B */
  f := x.(float64)
  
  /* ��������ƁA�����I�������ɂ��ށBf�ɂ�0�AisFloat64�ɂ�False���Ԃ��Ă��� */
  f, isFloat64 := x.(float64)

  /* ����𗘗p�����if���ł���Ȃ��Ƃ��ł��� */
  if x == nil {
    fmt.Println("None")
  } else if i, isInt := x.(int) ; isInt {

  } else if s, isString := x.(string) ; isString {

  } else {

  }

  switch x.(type) {
    
  case int:

  case string:

  default:
  
  }
  
  switch v := x.(type) {
    
  case bool:

  case string:

  default:
  
  }

}
```
## �Q�ƌ^
### �X���C�X
```go
//�錾�B�z��Ɣ�ׂ�Ɨv�f���������Ȃ�
var sl []int
```
```go
// �����I�Ȑ錾
var sl []int = []int{100,200}
```
```go
// �ÖٓI�Ȑ錾
sl := []string{"A", "B"}
```

```go
//�������ɗv�f��������
sl := make([]int, 5)

// [0 0 0 0 0]�����������
```

```go
// �l�̍X�V
sl[0] = 1000
```

```go
// �l�̎��o��
sl :=[]int{1,2,3,4,5}

// 0�Ԗڂ����o��
sl[0]

// �Q�Ԗڂ���S�Ԗڂ܂őS�Ď��o��[3 4]
sl[2:4]

// �Q�Ԗڂ܂őS�Ď��o��[1 2]
sl[:2]

// �Q�Ԗڈȍ~�S�Ď��o�� [3 4 5]
sl[2:]

//�z��̑S�Ă����o����. [1 2 3 4 5]
sl[:]

// �Ō�����o�� 5
sl[len(sl) - 1]

// �ŏ��ƍŌ�ȊO�����o��w[2 3 4]
sl[1 : len(sl) - 1]
