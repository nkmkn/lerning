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

�Q�l : �ȈՕ��t��if�� 
https://code-database.com/knowledges/97

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
### �G���[�n���h�����O

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
```

### �X���C�X�@append make len cap
#### append
```go
sl := int{100,200} 
// �v�f���g�� [100,200,300�ƂȂ�]
sl = append(sl, 300)
// �v�f�𕡐��n�����Ƃ��ł���[100, 200, 300, 400, 500, 600, 700]�ƂȂ�
sl = append(sl, 400, 500, 600, 700)
```
#### make
```go
// �v�f��5�̃X���C�X�𐶐�
sl := make([]int, 5)
```

```go
// �v�f��5, �e��10�̃X���C�X�𐶐�
sl := make([]int, 5, 10)

// �v���O�����̃��������C�ɂ���ꍇ�́A �e�ʂ����߂Ă����B
// �X���C�X�̗e�ʂ𒴂��ėv�f�����Ă��܂��ƁA�����I�ɗe�ʂ��Q�{�ɂȂ�
// �ߏ�Ƀ��������m�ۂ��Ă��܂��Ǝ��s���x���������肷��B
```

#### len, cap 
```go
// �X���C�X�̗e�ʂ��擾
cap(sl)

// �X���C�X�̒������擾
len(sl)
```

### �X���C�X copy
```go
sl := []int{1,2}
// �������Ă��܂���...,sl[0]�������������Ă��܂�
sl2 := sl
sl2[0] = 10000
```

```go
sl1 := []int{1,2}
sl2 := make([]int, 5, 10)

// �Ԃ�l�̓R�s�[�ɐ��������v�f��
n := copy(sl2, sl1)
```

### �X���C�X for
```go
sl := []string{"A", "B", "C"}
//�z��Ɠ��l��range�Ŏ��o����
for i, v := range sl {
  fmt.Println(i, v) 
}

//�������ÓT�Ifor�ł��\
for i := 0 ; i < 10 ; i++ {
  fmt.Println(sl[i]) 
}
```

### �ϒ�����
```go
// �������X���C�X�̂悤�Ɉ�����->�ϒ����������֐����ȒP�ɍ�邱�Ƃ��ł���B
func Sum(s ...int) int {
  n := 0
  for _, v := range s {
    n += v
  }
  return n
}

func main () {
  fmt, Println(Sum(1,2,3))

  /* �������D���Ȃ����L�΂��� */
  fmt, Println(Sum(1,2,3,4,5,6,7,8,9))

  /* �������X���C�X�ŗ^���Ă�OK */
  sl := []int{1,2,3}
  fmtPrint(Sum(sl...))
}
```
### �}�b�v
Ruby�ł���**�n�b�V��**
Python�ł���**����**
Javascript�ł���**�I�u�W�F�N�g**
```go
// map[�L�[�^��]�o�����[�^��{ �L�[ : �o�����[ ,�L�[ : �o�����[ ,�L�[ : �o�����[ ...}
var m = map[string]int{"A" : 100, "B" : 200, "C":300}

//�}�b�v�̎��o�� �}�b�v�ϐ���[�L�[]
fmt.Prinln(m["A"])
```

```go

//��}�b�v�̐���
m = make(map[int]string)

//�}�b�v�̓o�^
m[1]="JAPAN"
m[2]="CHINA"

//�}�b�v�̎��o��
fmt.Prinln(m[1])

//�}�b�v�����o���Ȃ��������̃G���[�n���h�����O
//ok�ɂ�false�������Ă���
s, ok := m[3]

if !ok {
  fmt.Println("error!")
}

//�}�b�v�̍폜
delete(m, 3)

//�}�b�vfor
for k, v := range m {
  fmt.Println(k,v)
}
```

�z��A�X���C�X�A�}�b�v�͈̔�for��

```go
arr = [3]int{1,2,3}
sl := []int{1,2,3}
var m := map[int]string{
  1 : "JAPAN",
  2 : "CHINA",
  3 : "USA"
}

for i, v := range arr {
  fmt.Println(i,v)
}

for i, v := range sl {
  fmt.Println(i,v)
}

for k,v := range m {  
  fmt.Pringln(k,v)
}
```
### �`���l��
![](2022-03-20-13-59-02.png)

�����̃S���[�`���ԂŃf�[�^���󂯓n�������邽�߂ɐ݌v���ꂽ�f�[�^�\��

#### �錾
```go
// �`���l���̐錾
var ch chan int

// ��M��p�̃`���l���̐錾
var ch_rev<-chan int

// ���M��p�̃`���l���̐錾
var ch_snd chan<- int
```

#### ������
```go
// ���������s���āA�������݁A�ǂݍ��݂��ł���悤�ɂ���
var ch chan int
ch = make(chan int)
```
```go
// ����make�֐����g���āA�錾&�����������邱�Ƃ��ł���
ch := make(chan int)
```

```go
//�`���l���̗e�ʂ��w�肵�ď�����
ch := make(chan int, 5)
```

#### �f�[�^����M
�`���l���̎d�g�݂�FIFO�ɂȂ��Ă���.
```go
// 1�Ƃ����f�[�^���`���l��ch�ɑ��M
ch <- 1
ch <- 2
ch <- 3

// �f�[�^����M
fmt.Println(len(ch)) //3
fmt.Println(<-ch)    //1����M

fmt.Println(len(ch)) //2
fmt.Println(<-ch)    //2����M

fmt.Println(len(ch)) //1
fmt.Println(<-ch)    //3����M

fmt.Println(len(ch)) //0
```
�`���l���̗e�ʂ𒴂��đ��M���Ă��܂����ꍇ�A�f�b�h���b�N�ƂȂ��Ă��܂��B
```go
var ch := make(chan int, 3)

ch <- 1
ch <- 2
ch <- 3
ch <- 4
// �f�b�h���b�N�I�I�I
```
#### �`���l���ƃS���[�`��
```go
func receiver( c chan int){
  for{
    i := <-c
    fmt.Println(i)
  }
}

// �S���[�`������񏈗���
func main() {
  ch1 := make(chan int)
  ch2 := make(chan int)
  
  go receiver (ch1)
  go receiver (ch2)
  
  i := 0
  fot i < 100 {
      ch1 <- i
      ch2 <- i
      time.Sleep(50*time.Millisecond)
      i++
  }
}
```

#### �`���l��close
�`���l�����N���[�Y���đ��M���ł��Ȃ��悤�ɕύX���邱�Ƃ��ł���B
��������M�͂ł���B
```go
ch := make(chan int)

//1�𑗐M
ch<-1

//�`���l�����N���[�Y�B�ȍ~�A���̃`���l���ւ̑��M�s�ƂȂ�B
close (ch)

//�f�[�^��M�����鎞�ɁA�G���[�n���h�����O�Ń`���l���������Ă��邩�ǂ��������邱�Ƃ��ł���B
// i�ɂ�1, ok�ɂ�false������B
i, ok := <-ch
```

```go
func receiver(name string, chan int){
  for{
      i, ok := <-ch

      //close���ꂽ�甲����
      if !ok {
        break;
      }
      fmt.Println(name, i)
  }

  //�S���[�`���̏I��
  fmt.Println(name + END)
}

func main () {

  // �S���[�`����3�N��������B
  go receiver("1.go routin", ch)
  go receiver("2.go routin", ch)
  go receiver("3.go routin", ch)

  i := 0
  for i < 100 {
    ch <- i
    i++
  }
  close(ch)
}
```

#### �`���l��for
```go
ch := make(chan int, 3)
ch <- 1
ch <- 2
ch <- 3

// for�Œl����M���鎞��close���Ȃ��ƃf�b�h���b�N���Ă��܂��B
close (ch)
for i := range ch {
  fmt.Println(i)
}

```

#### �`���l��select
https://qiita.com/najeira/items/71a0bcd079c9066347b4

```go
//�`���l���ɒl�������Ă��Ȃ����̓u���b�N����B
select {
  case v := <-ch:
    fmt.Println(v)
  default:
    fmt.Println("No Value!")
}
```
close����Ă���ƃu���b�N������`case v:= <-ch`�����s�����B  
��M��close����ʂ������ꍇ�͈ȉ��̂悤�ɂ���B
```go
select{
  case v, ok := <-ch:
    if ok {
      fmt.Println(v)
    }else{
      fmt.Println("closed")
    }
  default:
    fmt.Println("no value")
}

```
## �\����
### struct
```go
//�\���̂��`
type User struct {
  Name string
  Age int
}

func main () {
  var user1 User
  user1.Name = "Nakama"
  user1.Age = 33

  user2 := User{}
  user2.Name = "Nakama"
  user2.Age = 33

  //�����l��ݒ�
  user3 := User{Name: "Nakama", Age: 33}

  //�����l��ݒ� �ϐ������ȗ����邱�Ƃ��ł���
  user4 := User{"Nakama", 33}
}
```
```go
// �\���͎̂Q�Ɠn�������邱�Ƃ�����
func UpdateUser( user *User ){
  User.Name = "Nakama"
  User.Age = 33
}

func main () {
  user := &User{}
  UpdateUser(user)
}
```

### struct ���\�b�h
```go
type User struct {
  Name string
  Age int
}

func (u User) SayName(){
  fmt.Println()
}

func (u *User) SetName(name string){
  u.Name = name
}

func main () {
  user1 := User{Name : Nakama}
  user1.SayName()
  user1.SetName("Nakama")
}
```
### struct ���ߍ���
```go
type t struct{
  User User
}

type User struct{
  Name string
  Age int
}
func (u *User) SetName(name string) {
  u.Name = name
}

func main(){
  t := t{User:User{Name:Nakama, Age:33}}
  t.User.SetName("A")
}
```

```go
//�^�����ȗ��ł���
type t struct{
  User
}

type User struct{
  Name string
  Age int
}

func (u *User) SetName(name string) {
  u.Name = name
}

func main(){
  t := t{User:User{Name:Nakama, Age:33}}

  //�ȗ������ꍇ��User�������Ȃ�
  t.SetName("A")
}
```

### struct�^�R���X�g���N�^
https://golangstart.com/constructor/
```go
type User struct {
  Name string
  Age int
}

func NewUser(name string, age int) *User{
  return &User{Name: name, Age: age}
}

func main () {
  user1 := NewUser("Nakama", 33)
}
```
### struct �X���C�X
```go
type User struct {
  Name string
  Age int
}

type Users []*User

func main () {
  user0 := User{Name: "user0", Age: 10}
  user1 := User{Name: "user1", Age: 10}
  user2 := User{Name: "user2", Age: 10}
  user3 := User{Name: "user3", Age: 10}

  users := Users{}

  users = append(users, user0, user1, user2, user3)
}
```

