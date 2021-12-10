# go-digest

### creators of golang 
a small team of google 
- robert griesemer
- rob pike 
- ken thompson (unix,unicode) 

### why create golang
google used three languages 
- __python__ interpreted , has issues with large scale problems 
- __java__ increasingly complex type system 
- __CPP__ complex type system + compile time is very slow 

### why is cpp compile time slow ?
it is a legacy issue when c and cpp was designed computers did not have much memory so they had to be compiled at low memory so compile time was compromised 

### others vs golang concurrency 
when python , java and cpp was designed computers had to do one task at a time 
so there was only one thread but now we need many concurrent things to happen  so concurrency was added in later or patched at best . But at the the time of designing __*GO*__ concurrency was there from the beginning  . 

## Now comes go 
- strong and statically typed language (inharits from java and cpp )
*__strongly typed__ means the type of a variable can not change over time ,
__statically typed__ means all variables have to be defined at compile time (there is a way to get around this which is called __shadowing__ )*

### key features 
- Excellent community 
- simplicity 
- fast compile time 
- garbage collected language (*trading systems have hard time with garbage collection*)
- built in concurrency 
- compiles to stand alone binary 

### Go Resources 
...

### a sample programm 

```
package main 

import (

    "fmt"
)

func main() {

    fmt.println("hello there !")
}
// output -> hello there !
```

#### disection of the code 

`package main` every programm has to be in a package  and main is a special package as its the entry point 

`import ("fmt")` generric import statement , `fmt` is a package for formatting string (usually pronunced as ফমট / fomt )

`func main` main function in the main package , ( entry point ) 


### installation and project setup convension 
... 

## variable

### variable declaration 

1) `var i int` hear `var` is keyword for declaration  , `i` is variable name and `int` is variable type 
2) `var i int = 43` 
3) short hand `i:=43`  , hear compiler determines what type it is and assigns value 
4) ``` 
    package main 
    var  i int = 27
    func main(){
        // code 
    }
hear `i` is a package level variable 

5) we can also do this 
```
var (
    i int = 0 
    j int = 1
)

var (
    k = 40 
)

```
a more organized way to decalre multiple variables 

6) __SHOADOWNING__ 
```
package main 

import "fmt"

vat i int = 10 

func main () {

    var i int = 20 
    
    fmr.println(i)
}
// output -> 20 
```
ther same variable in the inner scope gets preference this is called __SHADOWING__ , this allows bothe the variable value and type to be changed 

7) decalred valirables in GO have to be used or will cause compiler error 
8) __NOMIANL CONVENSION__
there are 3 levels of visibility in *GO*
    - __package level__ if first letter of variable name is of lower case then it is scoped to the package and file in the same package can access the variable 
    - if it is upper case at the package level then it is exported from the package and it is globally visible 
    - block scoped ( inside `{}` ) , the variable is never visible outside the block
    - there are no private scope 
    
## type conversion 
```
var i float  = 42.5 

var j int 

j = int(i)

```

## Primitive types 

1) Boolean 
2) Number (int , float , complex)
3) text (string , rune)

- __Boolean__
```
var r bool = true 
n := 1 == 1 // true 
m := 1 == 2 // false 
```
unassinged bool variable has default value as false 

__*type conversion is not posssible for bool , so no bool -> int or int -> bool possible*__

- __Numeric__ 
*for go in every system int is treated differently , but it is farunteed that it would at least be 32 bit but based  on the system it could also be 64 bits or 128 bits* 

1) default integer keyword is `int`

__signed__ 

|     |  |
| ----------- | ----------- |
| int8      | -128 to 127       |
| int16   | -32786 to 32767    |
| int32   | - 2 billion to 2 billion        |
| int64   | -9 quintillion to 9 quintillion        |

*if bigger number is needed theres a way in math package to get arbitary big numbers*

__unsigned__

`var n uint8  = 43`

|     |  |
| ----------- | ----------- |
| uint8      | 0 to 255     |
| uint16   | 0 to 66535    |
| uint32   | 0 to 4 billion        |

*there are no 64 bit unsigned integer . byte type which is alias of unit8 as it is very __"famouse"__*

#### basic arethmatic 

|   sign  | operation |
| ----------- | ----------- |
| +      | add     |
| -   | subtract    |
| *   | multipply        |
| /   | division        |
| %   | reminder        |

*cat operate on different type on __*GO*__ , there are no type coertion like __*JS*__ , explicit type conversion has to be done in __*GO*__*

#### bit operations

|   sign  | operation |
| ----------- | ----------- |
| &      | and     |
| \|   | or    |
| ^   | xor        |

### bit shifting 
```
a := 8 
a << 3  // 64 
a >> 3  // 1 

```

 ## Decimal (32 & 64 bit)
 
 |  | | 
 |---|---|
 |float32 | +- 1.18E-38 to +- 3.4E38|
 |float64 | +- 2.23E-308 to += 1.8E308|
 
 ```
 n := 3.14 // this will be by default float 64 
 n := 13.72
 n := 1E14 
 ```
 
 *bit operator dont work with float*
 


## complex type 

*NB. no other language treats complex type as a basic type that why __GO__ is suitable for data science*

there are two complex type based on capacity 
```
// 1. complex64
// 2. complex128
var n complex64 = 1 + 2i 
real(n) // output -> float 
imag(n) // output -> float 
// complex64  = raal(float64)  + imag(float64)
// complex128 = raal(float128) + imag(float128)
complex(5,12) // output 5 + 2i
```

# Text Type (string and rune)
## string 
> __String__ is array of utf-8 ( 8 bit )charecters , so it can encode every charecter avaiable thatsw why we need other type (rune) ,

> string can be treated as array 

> byte is an alias of string 

```
s := "this is a string"
fmt.printf("%v , %T",s[1],s[1]) 
// output -> h , uint-8 
```

> ther is psudo arethmetic support for string s1 + s2 

```
 b := []byte(s) 
 // type casted to byte array , this is also a collection of 
 // utf-8/uint-8
 // this is also know as byte slicing 
```
> byte slicing is needed when sending response to ohter services over the web



## Rune 

> in utf-32 any charecter can be 32 bits long but does not have to be 32 bit long . so a valid utf-8 is a valid utf-32 charecter (this is a bit tricky)

```
r := 'a' 
```
or 
```
var r rune = 'a' 
```

```
fmt.println("%s , %T",r,r)
// output -> r , int32
```

> rune is type alisa of int32 , ther is a built in function named __ReadRune__


# constants 

```
const myConst  int = 42 
```

```
import "math"

const myConst float64 = math.Sin(1.57) // ❌
```
the above code will cause error beacuse const has to be assigned at compile time and the function will execute at runtime 

> __*NB. arrays/collections are mutable types by default and they can not be typed constant*__

> const can be shadowed 
```
// package level 
const a  int64 = 24 

// block level 
const a int = 43 
```
> const is untyped , the compiler simply replaces all a with 10 , so the below code will cause error 
```
const a int32 = 10 
var b int8 = 20

a + b // ❌
```

### enumarated constants 
> iota is used for counter in a scope 
> 
__ex-1__
```
// package scode 

const a  = iota 

fmt.println(a) // output 0 
```

__ex-2__

```
const (
    a = iota 
    b = iota 
    c = iota
)

// print(a,b,c) -> 0 , 1 , 2
```

__ex-3__

```
const (
    a = iota 
    b 
    c
)
// output -> 0 , 1, 2 
const (
    a2 =iota 
)
// output -> 0 
```

__ex-4__

```
// package level 

const (

    catSpecialist = iota 
    dogSpecialist 
    snkaeSpecialist
)

func main() {

    var specialist int = catSpecialist 
    
    // print(specialist == catSpecialist) -> true 
}

```

__ex-5__

```
// package level 

const (

    catSpecialist = iota 
    dogSpecialist 
    snkaeSpecialist
)

func main() {

    var specialist int  
    
    // print(specialist == catSpecialist) -> true 
}

```

default int value is 0 amd iota starting value is also 0 , this might cause unexpected error 

to solve this issue we can initiate iota with error value 

```
const (
    errorSpecialist = iota 
    catSpecialist 
    dogSpecialist 
)

```

__ex-6__

```
const (
     _ = iota // tells the compiler i dont care about the value 
     cat 
     dog 
)
// print(cat,dog) ->  1 , 2
```

> we can also offset iota like this 

```
 const (
     cat = iota + 5 
     dog 
     snake 
 )
 // print(cat,dog,snake) -> 5 , 6 , 7
 
```

__ex-7__
(*example of file size const with iota*)

```
const (
    _ = iota 
    KB = 1  << (10 * iota)
    MB
    GB
    TB
    OB
    EB
    ZB
    YB
)

func main () {

    filesize := 40000000
    fmt.println("%.2f GB", filesize / GB)
    // output 3.73 GB

}

```

__ex-8__
(*role and permissions implementation with iota*)

```
const  (
    isAdmin = 1 << iota 
    isHeadquater
    canSeeFinantial
    canSeeAfrica
    canSeeAsia
    canSeeEurope
    canSeeNorthAmerica
    canSeeSouthAfrica
)

func main () {
    
    var roles byte = isAdmin | canSeeFinancial | canSeeEurope

    fmt.println("%b",rules)
    
    // output -> 1 0 0 1 0 1
    
    fmt.println("is admin %v ", (isAdmin & rules) == true)
    
    // output -> true 
    
    fmt.println("is headwauater %v ", (isHeadwauater & rules) == true)
    
    // output -> false 
}

```
|||||||||||
|--|--|--|--|--|--|--|--|--|--|
|isAdmin| 1 << iota | 0 | 0 |0 |0 |0 |0 |0 |1 |
|isHeadquater|  | 0 | 0 |0 |0 |0 |0 |1 |0 |
|canSeeFinantial| | 0 | 0 |0 |0 |0 |1 |0 |0 |
|canSeeAfrica|  | 0 | 0 |0 |0 |1 |0 |0 |0 |
|canSeeAsia|  | 0 | 0 |0 |1 |0 |0 |0 |0 |
|canSeeEurope|  | 0 | 0 |1 |0 |0 |0 |0 |0 |
|canSeeNorthAmerica|  | 0 | 1 |0 |0 |0 |0 |0 |0 |
|canSeeSouthAfrica|  | 1 | 0 |0 |0 |0 |0 |0 |0 |


# Array and Slices 

## Array 

__method-1__
```
 grades := [3]int {97,85,93}
```
__method-2__
```
 grades := [...]int {97,85,93} // unspecified array size 
```
> *__NB. empty array value is []*

> len() function is used to determine array length 

### 2d array 

```
var matrix = [3][3] int {

    [3]int{1,1,1} ,
    [3]int{2,2,2} ,
    [3]int{3,3,3}
}

// print(matrix[0]) -> [3]int {1,1,1}
```

> array in go are different than other languages , array in go are considered value 

```
 a := [...]int{1,2,3}
 
 b := a // changing b wont effect a 
```

in other languages when copying an array we will be using the same data ( passing by reference) but in go when copying another exact copy of the array is made . 

__so why is this even important to note ?__
> when passing an array to a function , if the array is really big with millions of data the programm is going to be slowed down as copy by value is going to be occure 

__to avoid this__ use 
```
 b := &a // pointer 
```
> & is called address of operator 

b := &a tells compiler b is going to point to the same data as a  ( a and b will be pointing to the same data )


## Slice 

> the length of an array has to be known at compile time which limits its usefullness , hear slice comes to rescue 

```
a := []int{1,2,3} // this is a slice 
```

> len() function is avaiable , cap() shows the capacity of slice 

now for slice 
```
b :=a 
```
a and b are pointing to the same data 
```
    a := []int{1,2,3,4,5,6,7,8,9,10}
    b := a[:]
    c := a[3:]
    d := a[:6]
    e := a[3:6]
```
hear a , b , c ,d , e are pointing at the same data in different ranges , 

> [3:6] hear is  [inclusive:exclusive] , will output [4,5,6]


## other ways to create slice 
```
a := make([]int,3) 
// output [0,0,0], len-> 3 , cap -> 3

b := make([]int,3,100)
// output [0,0,0] , len -> 3 , cap -> 100

```
appending a slice 
```
a = append(a,1)
```

__ex-1__

```
    a := []int{}
    // len(a) -> 0 
    // cap(a) -> 0
    // a -> []
```

__ex-2__

```
    a := []int{}
    a = append(a,1)
    // a -> [1]
    // len(a) -> 1
    // cap(a) -> 2 ❓ but why
```
explanation , we first created  slice with 0 elements so go created an empty array , but when we appended 1 it could not fit so go had to create an new array (double is size )and copy all the values there ,


this is ok for a samll slice but as things get big copy operation gets costly ,

__to avoid this__ we can use a suitable value is make functions third parameter , then append function would not need to copy to a new array 

## append 
append can take two or more arguments 

```
    a = append(a,1) // -> [1]
    a = append(a,2,3,4,5) // -> [1,2,3,4,5]
```

>NB. if slice append exceeds the base size of the slice go is going to pow 2 the size of the underlying array   2 -> 4 -> 16


__ex-2__ *(concatinate two slices in go)*

```
a := []int{1,2,3}
a = append(a,[3]int{4,5,6}) // ❌
```
above code will not work as we are trying to append two differenct types array and slice 

to make this work we have to spread the array 
```
a = append(a,[3]int{4,5,6}...)
```
this becomes 
```
a = append(a,4,5,6)
```


__ex-3__ *(implement stack in go)*

stack has push and pop functions . push will be done by append and pop can be done by shift operation 

```
// pop first 
a := []int{1,2,3,4,5}
b := a[1:]
// pop last 
b := a[:len(a)-1] 
```

__ex-4__ *(remove element from the middel of a slice)*

lets assume we want to remove the third element from a slice 
```
 a := []int{1,2,3,4,5,6,7}
 
 b := append(a[:2],a[:3]...)

```

we have to be careful as we are working with references as we will ses in the code below 

```
 a := []int{1,2,3,4,5}
 fmt.Println(a) //  1 2 3 4 5 
 b := append(a[:2],a[:3]...) 
 fmt.Println(b) // 1 2 4 5 
 fmt.Println(a) // 1 2 4 5 5 , 🤷‍♀️ unexpected behavior 
```

we have to be careful of not using the same reference in other places 


# Other collection types

## Maps 

example 

```
    statePopulation ;= map[string]int{
        "dhaka" : 2323423 ,
        "pabna" : 2131237
    }
    fmt.Println(statePopulation)
    // map[dhaka:2323423 pabna:2131237]
```

value for a map can be of any type but to be a key for a map the type has to be testable with euqality 

for example string , array , numbers can be tested if they are equal 1 == 1 
"arif" == "sarif" , but not slice and map 

another way of creating map is make function 

```
 mp := make(map[string]int)
 mp = map[string]int{
     "arif" : 27
 }
```
> NB . the return order of map keys is not gaurenteed 

remove entry from a map
```
    delete(mp,"arif")
```

> default map key value is 0 . not existing key returns 0 
> 
> so if a map has value as 0 how can we know if the key exists and is 0 or the does not exist thuse the value 0 

```
    pop , ok = mp["jabed"] 
    // ok -> false 
    // pop -> 0 

```
if key existed ok would be true 

> how do we know how many elements are there in map 
```
len(mp) // 1 
```
> NB. mpas are passed by reference 


## Struct 

another collection type 

```
    type Doctor struct {
        number int 
        actorName string 
        companions []string 
    }
    
    func main () {
    
        doc := Doctor {
            number : 3
            actorName : "istiak"
            companions : []string {
                "sarif",
                "samad",
                "jabed"
            }
        }
    }
```

we could also write this as 
```
doc := {
    3,
    "istiak",
    []string {
       "sarif",
       "samad",
       "jabed"
    }
}
```
for this approch order has to be maintained 

```
doc.number // 3
doc.actorName // "istiak"
doc.companions[2] // "jabed"
```

### thing about struct naming convension 
> struct name starting with capital letter will be exported but if the property names are not capitized they wont be visible outside the package 

#### annonymu struct 

```
 aDoctor := struct {name string} {
     name : "arif"
 }
 aDoctor.name // "arif"
```
used mostly in short lived use cases 

> NB. structs are passed by value not reference 

> to pass reference we can use address of operator (&)

```
    bDoctor = &aDoctor 
```
#### extra bits 
go does not have traditional OOP for example it does not have inharitance but to implement inharitance we can use embaded struct

```
type Animal struct {
    Name  string 
    Origin string 
}

type Bird struct {
    Speed float32
    CanFly bool 
}

```
Go does not support isA relation but supports hasA relation or embaded 

```
type Bird {
    Animal // embaded 
    Speed float32
    CanFly bool
}
```
we can say a bird  has animal like characteristics

```
    b := Bird()
    b.name = "penguin"
    b.Origin = "alaska"
    b.Speed = 23.2
    b.CanFly = false 
```
but if we use literal syntax 

```
    b := {
        Animal { Name : "penguin" , Origin : "alaska" }
        Speed : 23.2
        CanFly : false 
    }
```

#### Tags 
> tags just pass a string with property as metadata nothing else 

```
    type Animal {
        Name string `required max:100`
        Origin string 
    }
```
tags are written in the right side of the property with backticks 

to retrive tags 

```
    import "reflect"
    
    t := reflect.TypeOf(Animal{})
    filed , _ = t.FieldByName("Name")
    field.Tag // -> 'required max:100'
```


## So now if we list all the collection types in go they are 
1. Array 
2. Slice 
3. map
4. Struct




# Control Flow 

basic example 

```
    if true {
        fmt.Println("this is true ")
    }
```
in got we will alwasy have to use brances 

```
    if initializer ; condition {
        // stuff 
    }
```

```
    population := map[string]int{
        "mirpur" : 10000 ,
        "baridhara" : 232000,
    }
    
    if data , ok = population["mirpur"] ; ok {
        fmt.Println(date) // initializer statement variables are scoped to this block 
    }
```

> logical operator are same as other languages 

> NB. floating point evaluation has to be do


## switch statement 

```
func main() {
    
    var tag int = 1 
    switch tag {
        case 1 :
            // do stff 
        case 2 :
            // do stuff 
        default : 
            // do stuff 
    }
}
```
falling through , 

in other languages we do 

```
    case 1 :
    case 2 :
    case 3 :
        // do stuff 

```

but in go there is no falling through instead we have the ability to test multiple test in a single case 
```
    case 1 , 5 :
        // do stuff 
    case 2 , 4, 6 :
        // do stuff 
```

if some number is repeted in more then one case it is going to cause an error so the numbers have to be unique 

> NB. in to break statemetns are implicit , as break tends to cause errors when we forget to write it so go designers made it implicit 


__fallthrough in go__ if we put fallthrough keyword after any case the next code is going to execute 

```    
    i := 2
    switch i {
        case i < 10 :
            // code 
            fallthrough
        case i == 1 : 
            // code 
    }
```
> hear event if i is 2 the code is i == 1 is going to execute beacuse of fallthrough 

### typed switch 

```
    var i interface {} = 1 
    switch i.(type) {
        case int :    
            // i is an int 
        case float64 :
            // i is float64 
        case string : 
            // i is a string 
        default : 
            // i is another type 
    }

```

> NB. i.(type) returns the type of a variable  , but only inside switch case controll flow not outside switch 

how do we catch [3]ubt{1,2,3} with typed switch in golang 

```
    switch i {
        case [3]int : 
            // code 
    }

```

> we can break statement explicitly to break out of a switch statement if we want 



# Looping 

a simple loop 
```
    func main () {
        for i := 0 ; i < 5 ; i++ {
            fmt.Println(i)
        } 
    }
```

writing like below will cause error 
```
    for i := 0 , j := 0 ; i < 5 ; i+=1 , j +=1 { // ❌
        // code 
    }
```
instead we have to write it like 

```
    for i , j := 0 , 0 ; i < 5 ; i , j = i+1 , j+1 {
        // code 
    }
```
in the above code increment section if we write i++ and j++ , it would cause error as i++  is not an expression in go it is an statement 
> NB. expression is something that resolves to a value (returns a value )

while loop substitution with for in go , with only the condition section 

```
    for i < 5 {
        // code 
    }

```

this is also valid 
```
    for {
        // infinity loop 
    }
```
> NB. break and continue are same as other languages (like c )

## label in loop 
there is a concept in golang called label , this can be used to break out of loops 

```
    loop :
        for {
            for {
                break loop 
            }
        }
```

this might seem like c langs goto statement but its not . loop hear indicates from where do we want to break out of. 

### looping through other types of collections 

```
    s := []int{10,20,30}
    
    for k,v := range s {
        fmt.Println(k,v)
    }
    
    // 0 1
    // 1 2 
    // 2 3
    
```

we can use this format with 

1. slice 
2. array 
3. map
4. string 
5. channel (discussed latter in concurrent programming section) 

```
    for k,v := range x {
        // code 
    }
```

only loop through keys 
```
    for k := range x {
        // code 
    }
```
or 
```    
    for k , _ := range x {
        // code 
    }
```
only values 
```
    for _ , v := range x {
        // code 
    }
```

> _ is a special variable in go which is called the readonly variable and go compiler ignores it 




# Defer , Panic , Recover 

> __DEFER__ function invokes a function but delays it execution to some future point in time 


> __PANIC__ an application can panic , go application can enter a state when it can no longer continue to run and now go runtime trigger that or trigger it on our own 


> __RECOVER__ when application starts to panic we need to somehow save the application and signal that to the rest of the application 

```
    func main () {
        
        fmt.Println("start")
        
        defer fmt.Println("mid")
        
        fmt.Println("end")
        
    }
    // output
    // start 
    // end 
    // mid 
```
the way defer works hear it it delays the execution of the statement it moves it after the main function but before the main function returns


```
    func main () {
        
        defer fmt.Println("start")
        
        defer fmt.Println("mid")
        
        defer fmt.Println("end")
    }
    // output
    // end 
    // mid
    // start 
    
```

defer works LIFO (last in first out) 

so the last function that gets deffered will be the first to get called 

__use cases__ we often use defer keyword to close out resource and it it logical that we close resources out in the opposit order we open them , as resource might be dependent on the other one 

>NB. defere statement executes after the main function is done but before the main function returns 

