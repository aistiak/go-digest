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

### practical use of differ function 
this example is a sample rpogramm that requests a file from netwok and reads the contents of the file 

```
import (
    'fmt',
    'io/util'
    'log'
    'net/http'
)

func main() {
    res , err = http.Get('https://google/robots.txt')
    if err != nil {
        log.Fatal(err)
    }
    
    robots , err = ioutil.ReadAll(res.Body) 
    
    res.Body.Close()
    
    if err != nil {
        log.Fatal(err)
    }
    
    fmt.Println("%s",robots),
}
```


in the above application defer can help with the body close .  As we can seee we closed the file lines later to the request but htere is a prossibility that we might forget to close it later . Hear defer can help us after the request we can close e witha deffered keyword 

so code could be like below 

```
import (
    'fmt',
    'io/util'
    'log'
    'net/http'
)

func main() {
    res , err = http.Get('https://google/robots.txt')
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()
    robots , err = ioutil.ReadAll(res.Body) 
    
    
    
    if err != nil {
        log.Fatal(err)
    }
    
    fmt.Println("%s",robots),
}

```
> NB. the most common use case for using defer allows us to associate opening and closing of reses next to each other 

### A common pattern 
- Open resource 
- check for error 
- close the resource with differ 
- we have to check for error beacuse if the resource never opens trying to close it will cause error 

> NB. when we are opening a lot of resources say with a loop then using defer might not be the best choice as defer will execute before main returns so milions of resources will stay oen and close all togather at the end . we might explicitly close then after are done delegate resource handelling to another function and let it handel the closing of it 


```
    func main () {
        
         a := "start"
         defer fmt.Println(a)
         a = "end"
    }
    // output 
    // "start"
```
> defer takes the value of a variable at the time defer was called 


# Panic 

In go there are no `Exception` . like most languages what is said to be exceptional like most it go it is quite normal . 

lets sat we are trying to open a file that does not exist many languages will consider it as an exception but go will simply return an error value 

however there are cases where a Go application can not continue which in go is called `panic` 

__Ex__

```
    func main () {
        a,b := 1,0
        and := a/b
        fmt.Println(ans)
    }
    // output 
    // panic : runtime error : integer devided by zero 
    // {stack trace}
```


__ex__ 

```
    fmt.Println("start")
    panic(" something bad happned")
    fmt.Println("end")
    
    // out
    // panic : something bad happned 
    // {stack trace }
```



>NB.it is very rare that go is going to panic . it would in most cases return a error value its up to use how we handel it 

>NB.Panics happen after the deffered function are executed 

__ex__ 

```
fmt.Println("start")
defer fmt.Println(" this was deffered ")
panic("something bad")
fmt.Println(" end ")
// output 
// start 
// this was deffered 
// panic : something bad 
// {stack trace}

```

`recover function returns nil if application is not panicing else will return error that causes the application to panic `

```
fmt.Println("start")
defer func () {

    if err :=recover() ; err != nil {
        log.Println(err)
    }
}
panic("something bad") 
fmt.Println("end") 


// output 
// start 
// log-time : something baf 
```

hear we see recover catches the error but our programm still exists . But recover still has impact if we have depper call stack which we will see in the next example 

__ex__ 

```
func () { 
  fmt.Println( " start " ) 
  panicker()
  fmt.Println("end") // <- will execute 
} 


func panicker () {
   fmt.Println(" about to panic " ) 
   defer func () {
     if err := recover() ; err != nil {
       log.Println(err)
     }
   }
   
   panic(" something bad")
   fmt.Println(" donr panicing " ) // will not execute 
}


// output 
// start 
// about to panic 
// error 
// end
```

when the panic occurs in the panicker function . the usual execution will stop and execute the derrered function the deffered function recovers the application and the normal excution flow starts again


calling recover means that we are going to deal with what ever is wrong with but in case we cant we can re panic the application 

so if we change the code a bit 

``` 
if err := recover() ; err != nil {
   log.Println(err)
   panic(err) 
}

// start 
// about to panic 
// error : something  bad 
// panic : something bad 
// { stack trace } 
```

# Pointer 

agenda 
- creating pointer 
- dereferencing pointer 
- the new function 
- working with nil 
- types with internal pointer 

__ex__ 

``` 
 var a int = 42 
 var b *int  = &a 
 fmt.Println(a,b)
 // 42 , 0x0040 
 fmt.Println(a,*b)
 // 42 , 42 
 a = 27 
 fmt.Println( a, b ) 
 // 27 , 27 
 *b = 10
 fmt.println(a,b)
 // 10 10

```

__ex__*(pointer arithmetic)*

```
a := [3]int{1,2,3}
b := &a[0] // ❌
c := &a[1] // ❌
```
go does not support pointer arithmetic built in. if we must use it we have to use the `unsafe` package 

P.A was left out of go for simplicity as P.A can get very complicated 

__ex__ *(how can we create pointer types )* 

```
type mySteuct struct {
  foo int 
}
func main () {

  var ms *myStruct // ms := &myStruct{foo:42}
  fmt.Println(ms) 
  
}

// output 
// &{42} 

```

another way to initialize variable to be pointed to an object is 

```
var ms *myStruct 
ms = new (myStruct)
fmt.Println(ms)
// output 
// &{0} 
```
> NB.with new we can only create empty objects

```
var ms *myStruct 
fmt.Println(ms)
// outout 
// <nil>
```

dereferencing with pointer 

```
var ms *myStruct
ms = new(myStruct)
(*ms).foo = 42 
fmt.Println((*ms).foo)
// output 
// 42
```
>the perenthesis are hear because dereferencing operation ( * ) has lower precidence then the dot (.) operator 

>without the perenthesis we would be dereferencing 
>(ms.foo ) the whole thing 

the above code can also be written as 

```
var ms *myStruct
ms = new (myStruct)
ms.foo = 42 
fmt.Println(ms.foo)
// output 
// 42 
```

as go had limits of pointer it can help us out by making syntax easy , this is just syntactic sugar the compiler is helping us out  (*ms).foo and ms.foo are same to the compiler hear

__ex__*(why are slice / map copied by reference when assigned to another variable)*

>beacuse they are a pointer reference to an underlying array 

```
    a := []int{1,2,3}
    b := a // <- passing pointer reference 
    fmt.Printn(a,b)
    a[1] = 42 
```
>same thing with maps 

__ex__*(how to declare pointer of a type)*

>prefix the type with an asterics of the variable 

```
var a *int 
```

# Functions 

agenda 
- basic syntax 
- parameter 
-  return values 
- anoynymus function 
- function as type (first class citizen) 
- method (special king of function)

__ex__
> function starts with func if function name is upper case it will be exported 

```
func main () {
    // stuff 
}
```

### parameters 

```
func sayMessage(msg string) {
    fmt.Println(msg)
}

func main() {
    sayMessage("hello there")
}
```

if multiple parameters are of the same type we can specity the parameter at once 

```
func test (geet,name string) {

}
```

we can pass parameters as pointer in a function for small values it might not matter much but for large data structures passing by pointer is efficient as the value need to be copied every single time 

But passing maps and slices to a function is always as a pointer 


### variable parameters 

```
func main () {
    sum(1,2,3,4,5,6)
    // output 
    // [1 2 3 4 5]
    // the sum is 15 
}

func sum(values ...int) { // tells the compiler to wrap all the parameters in a slice name values 
    fmt.Println(values)
    resut := 0 
    for _ , v  := range values {
        result += v
    }
    fmt.Println("the sum is ",result)
}

```

>when passing variable parameter we can only pass one and it has to be the last one 

### return of function 

```
func foo (values ...int) int { // hear int at end is the return type 
    // stuff 
    sum := 0 
    
    return sum 
}

```

>NB. a rare feature that go has that other languages do not is go can return a loal variable as a pointer 

```

func foo(values ...int) *int {
    sum := 0
    return &sum 
}
```

>it is rare beacuse when we declare the `sum` variable we decalre it in the execution stack of this function which is a special section of the memory which is set aside for all the operation this function is going to be working with . when this function exits that execution stack is destroyed and memory is freed up 


> but he pointer would be pointing to a blank location with garbage value but in go lang when it realizes we are returning a value that is in the local stack it is autometically going to promote the variable in the shared memory on the compiler which is also called `heap memory`


#### named return value 

```
    func sum (values ...int) (sum int) {
        for _ ,v := range values {
            sum += v
        } 
        return // will have to write return without specifying value 
    }
```

>NB. this is helpful when the function is very big/long , to know the return type we have to scroll down at the end of the function , by using named return we can avoid that 


#### multiple return values 

```
    func main () {
        d , err = division(5.0,0)
        if(err != nil) {
            fmt.Println(err)
            return 
        }
        fmt.Println(d)
    }
    
    function division(a,b float64) (float64 , err) {
        if( b == 0) {
            return 0.0 , fmt.Error('cant divide by Zero')
        }
        return a/b , nil 
    }
```

>NB. this pattern is very common in go this left justifies  our code as much as possible as we dont have to write the arternative code isdise else block 

#### Annoynimus function 

```
func main () {
    func() { // this function can read outer scope variables 
        fmt.Println("hello there !")
    }() 
}
// output 
// hello there !

```

>NB.if we want to read outer scope stuff we have to pass that as argument / parameter or it might cause error in async code 

```
    for  i := 0 ; i < 5 ; i+=1 {
        func(arg){
            fmt.Println(arg)
        }(i)
    }
```


### function as type 

```
    var f  func() = func () {
        fmt.Println("hello GO")
    }
    f()
```
>NB.  as they are types they can be stored in variable 


### methods 

```
func main () {
    g := greeter {
        greeting : 'hello',
        name : 'go'
    }
    g.greet() // method invocation 
    
 
}

type greeter struct {
    greeting string 
    name string 
}

func (g greeter) greet() {
    fmt.Println(g.greeting,g.name)
}
// (g greeter ) is known as method reciver 
```
>NB. method reciver is what makes a function method in go , what this does is gives function a context were to execute , so we can do `g.greet()` 

>methods are functions with syntactic suger that provides a contet the function should execute 

```
    func man struct {
        name string 
    }
    
    func (m man) getName()(name string) {
        return m.name 
    }
    
    func (m *man) setName(name string) {
        m.name = name 
        return m 
    }

```
>`getName` uses a copy of `man` , but `setName` uses a reference to man which is more efficient 

if we return pointer from a set method we can make a builder 

```
func (m *man) setName(name string) *man {
    m.name = name 
    return m 
}
m := man {
    name : ''
}
m.setName("arif").setName("kasif")

```

# Interfaces 

> ## " the way interfaces are implemented in GO makes it so scaleable compared to java and other languages "

agenda 
- basic 
- composing interfaces 
- type conversion 
    - empty interface
    - type switching 
- implementing with values vs pointer
- best practices 


```
type Writer interface {
    write([]byte))(int , err)
}

type ConsoleWriter struct {} 

func (cw ConsoleWriter) Write (data []byte) (int , err ) {
    n , err = fmt.Println(string(data))
    
    return n , err 
}

func main () {
    var w Writer = ConsoleWriter{} 
    w.Write([]byte("hello go"))
}
```

>inside structs we define data but inside interfaces we describe behaviours (method defination)

> in got we do no explicitly implement interface we do it implicitly 

> console writer hear can be replaced with any kind of struct that has method writer what is polymorphis behaviour 


> so what we can do is for a concreate type we can create an interface 


### naming convension of interface 

if we have a single method interface we name the interface like method name + er

write+ er = writer 

>structs are the most common way to implement interfaces , but we dont have to use structs we can use any type 

__ex__ 
we dont have controll over int type as it is a primitive type we have controll over types that we define 

```
    type Incrementer interface {
        Increment() int 
    }
    
    type IntCounter int 
    
    func (inc *IntCounter) Increment() int {
        *inc += 1 
        return int(*inc)
    }
    
    func main() {
        myInt := IntCounter(0) 
        var inc Incrementer = &myInt 
        for i :=0 ; i< 10 ; i +=1 {
            fmt.Println(inc.Increment())
        }
    }
    // output 
    // 1 
    // 2
    // 3 
    // .. 
    // .. 
    // 9 
```

### interface implementing interface 

```

type WriterCloser interface {
    Writer 
    Closer 
}

type Writer interface {
    Write([]byte) (int,err)
}
type Closer interface {
    Close() err
}
type BufferWriterCloser struct {
    buffer *bytes.Buffer 
}

func (bwc *BufferWriterCloser) Write (data []byte) (int , err){
    n , err := bwc.Buffer.Writer(data)
    if err != nil {
         return 0 , err    
    }
    
    v := make([]byte,8)
    
    for bwc.buffer.len() > 8 {
        _,err  := bwc.buffer.Read(v)
        if (err != nil) {
            return 0 , err 
        }
        _ , err2 = fmt.Println(string(v))
        
        if err2 != nil {
            return 0 , err2
        }
    }
}

fucn main () {
    
    var wc WriterCloser = new BufferWriterCloser() 
    wc.Write([]byte("hello youtube listeners, this is test"))
    we.Close()
}

func NewBUfferWriterCloser() *BufferWriterCloser {
    return &BufferWriterCloser {
        buffer : bytes.NewBuffer([]byte{})
    }
}

func (bwc *BufferWriterCloser) Close() error { // flushing the buffer 
    for bwc.buffer.len() > 0 {
        data := bwc.buffer.Next(8)
        _,err = fmt.Println(string(data))
        if err != nil {
            return err 
        }
    }
    return nil 
}

// output 
// hello yo
// utube li
// sterners ,
// this is 
// a test 
// -> charecters are getting printed with 8 charecters chunk 

```

if we comment out `wc.Close()` we would get output 

```
// output 
// hello yo
// utube li
// sterners ,
// this is 
// -> there will be no `a test` printed out as this is not a 8 charecter chunk , the buffer is not flushed 

```


# Type conversion 

```
bwc := wc.(*BufferWriterCloser) 
```

converting writer closer to buffer writercloser but notice we are using pointer 

```
bwc := wc(io.Reader) // -> this will cause error as io.Reader need read method so it panics 
```
to stop this panic hear we can 

```
n , ok = := wc.(io.Reader)

if ok {
    
}else {
    // conversion failed 
}

```


```
r , ok = wc.(*BufferWriterCloser) // * <- is required as we implemented the interface with pointer 
```

// TODO this section needs more work 


## empty interface 

```
var myObj interface {} = NewBufferWriterCloser() 

if wc , ok := myObj.(WriterCloser) ; ok {
    // stuff 
}
```

>NB. nice thing about empty interface are everthing can be cast into an object that has no method written to it even primitivs


>This is a very important note when working with interfac if any of the methods require a pointer or implementing own reciver we are going to have to implement that interface with a pointer if not through if all the methods require value type then we can go ahed and use value types but we could aslo use a pointer 

implementing an interfce with value 

```
var wc WriterCloser = myWriterCloser{}
```

implementing with pointer 

```
var wc WriterCloser = &myWriterCloser
```
when we are implementing an interface with value type all of the methods need to have value recivers (methods that implement the interface) if we implement with pointers we just need the methods regardless of the the recivers 


so the method set for a value type is all the method with value recivers but method set for a pointer type is all of the methods with value recivers as well as pointer recivers (only for interfaces )

#### what is method set ?
when we define types and we assign methods to them each one of those type has what is called a method set 

now when we are working with methods directly the method set is all of the methods regardless of the recivers associated with that type 

But with interfaces things work differently when we implement interface with concrete value the method set of the value , when we are taking in the context of interface is any method that has a value as a reciver and the method set if a pointer is the sum of all of the value reciver methods and all of the pointer reciver methods 

# need examples 

Encouraged and supported by the go community and good to apply if our application its practical 

1) use many , small interfaces , the samller the interface the useful and powerful they can be (applicable for any language)

2) if we dont need to xport and interface athen we wont (export concrete
video ref (5.25.00)


3) design functions and methods to recive interace whenever possible 


# Goroutines 
Agenda 
- creating goroutines 
- syncronization 
    - waitgroup
    - mutex
- parallelism 
- best pranctices 


__ex__ 
how to create goroutine ?

```

func main() {

    go sayHello()

}

func sayHello() {

    print("hello")

}

// output 
// nothing would be output 

```
`go sayHello()`  spins off a green thread and run the sayhello in the green thread . 

the sayHello is in another go routine and our application exits as soon as the main function is done 

most of the programming languages (PL) use os threads what it means they have an individual call stack handed to that thread these tend to be very very large talking 1mb of RAM quite bit of time for app to set up creation and distruction of thread is very expensive 

GO follows a different model which is similar to `Erlang` language which is green thread which creates an abstruction of a thread which we call go routine . GO scheduler maps these go routines on to the os thread and schedular will take then with cpu thread that available and assign every go routine certain amount of time on these threads 

Go routines are very cheap to create and destroy so a go application can have many go routines at once 

__ex__ 

this is bad practice but just for example 

```
go sayHello() 

time.Sleep( 100 * time.Miliseconds )

// out 
// hello 

```

__ex__ *(clouser)*

go has understanding of clouser 


```
    go func() {
    
    }()
    
    time.Sleep()
    
    // out 
    // hello 
```

```

     msg := "hello"
     
     go func () {
     
         print(msg)
     }()
     
     msg = "bye"
     
     time.Sleep()
     
     // output
     // bye 
     
```

as we see using clouser like this can have unexpected results so we can write is like 

```

    msg := "hello"
    
    go func(){
        
        fmt.Println(msg)
        
    }(msg) // passing by value
    
    msg = "bye"
    
    time.Sleep() 
    
    // output 
    // hello 
    
```


### waitgroup 

__ex__ *(work application without sleep function)*

```

import ('sync')

wc := sync.waitGroup{} // creating waitgroup 

func main () {

    msg := "hello"
    
    wg.Add(1) // adding a goroutine to waitgroup 
    
    go func(msg string) {
    
        fmt.Println(msg)
        
        wg.done()
        
    }(msg)
    
    msg = "goodbye"
    
    wg.Wait() 
    
    // output 
    // hello
}

```

### mutex 

mutex is used to lock resources

__ex__ 

```

import(
    'fmt'
    'sync'
)

wg := sync.WaitGreoup{} 

m := sync.RWMutex{}

counter := 0 

func main () {

    for  i := 0 ; i < 10 ; i+=1 {
    
        wg.Add(2)
        m.RLock() // read lock 
        go sayHello()
        m.Lock() // write lock 
        go increment()
    }
    wg.Wait() 
}

func sayHello () {

    fmt.Println("hello")
    m.RUnlock() // read unlock
    wg.Done()
}

func increment() {

    counter++
    m.Unlock()
    wg.Done()
}
// see video agnain to find out output 

```

# CHANNELS 

its a very unique feature and makes go standout among other 

most PL were design with a single porcessing were in mind when concurrency and perellelsim came in mind . when concurrency and perellelism came they were bolted on the side and had special packages when go was designed concurrency and parallelsim were considered 

> channels can help pass data between go routines in a way which is safe and prevents race condition and memory sharing problem 




Agenda 

- channel basic 
- restricting data flow (send / recive only channel )
- buffered channel 
- close channels 
- for range loop with channels 
- select statement ( specially designed )


__ex__ 

```
 wg := sync.WaitGroup{} 
 
 func main() {
 
     ch := make(chan int) 
     // int is the data type thats going to 
     // flow through the channel are strongly typed 
     wg.Add(2)
     
     go func() {
         i := <-ch
         fmt.Prinln(i)
         wg.Done()
     }()
     
     go func() {
         ch <- 42
         wg.Done()
     }()
     
 }


// out 
// 42 

```

__ex__*( async senders and recivers )*

if the member of senders and recivers do not natch it is going to cause deadlock (PANIC)

only one message at the buffer at once to do otherwise we need buffered channels 

__ex__*( bideirectional routines )*

```

    ch := make(chan int) 
    
    wg.Add(2)
    
    go func() {
       i := <- ch 
       fmt.Println(i)
       ch <- 27 
       wg.Done()
    }()
    
    go func() {
        ch <- 42 
        // passing data to the channel 
        fmt.Println(<- ch)
    }()
    
    wg.Wait()
    
    // output 
    // 42 
    // 27 
```


__ex__*( directional channel )*

```

    ch := make(chan int)
    
    wg.Add(2)
    
    go func(ch <- chan int) {     // recive only channel 
        
        i := <- ch
        
        fmt.Println(i)
        
    }(ch)
    
    go func(ch chan <- int) {    // send only 
        
        ch <- 42 
        
        wg.Done()
        
    }(ch)
    
```

recive data from one side and send from another 

Notice we are passing bidirectional channel and aorking with a single directional channel . hear the go routine understands the needs and does the casting itself so this is a kind of polymorphic behaviour 

__ex__ *( buffer channel)*

```
    func main () {
    
        ch := make(chan int)
        
        wg.Add(2)
        
        func ( ch <- chan int) {
            i := <- ch
            fmt.Println(i)
            wg.Done()
        }(ch)
        
        func (ch chan <- int) {
            ch <- 42
            ch <- 27 
            wg.Done()
        }(ch)
        
        wg.Wait()
        
    }

```

**Output**

fatal error all goroutines are asleep  - deadlock ! 

as the channels are asymetric sending by 2 and reciving from 1 at a time 
(Buffer can solve the problem)


adding buffer to a channel 
```
    ch := make(chan int,50) // 50 is buffer 
```

this channel has a internal data store which can store 50 integers 

buffer are also neededwhen the senders or recivers need a littel time to process and dont want to block the other side 

```
    ch := make(chan int , 50)
    
    wg.Add(2)
    
    go func(ch <- chan int) {
        for i:= range(ch) {
            fmt.Println(i)
        }
        wg.Done()
    }(ch)
    
    go func(ch chan <- int ) {
        ch <- 42 
        ch <- 27 
        wg.Done()
        close(ch) 
        // if we dont close the channel it will 
        // cause deadlock as it does not know 
        // when to stop reading message 
    }(ch)
    
    wg.Wait()

```

when we are closing the channel we have to remember that we cant send any more data one the channel is closed . so we could defer a funcion to close the channel as if we always keep it open we might have memory leak 


>NB. cant send data in a closed channel and we cant also detect if a channel is closed from sending routine 

to know from reciving routine 


```
    if i,ok := <- ch ; ok { // ok will be true if channel is open 
    
    }
```


__ex__*( logger implementation with channel)*

```
    const (
        logInfo = "INFO"
        logWarning = "WARNING"
        logError = "ERROR"
    )
    
    type logEntry struct {
    
        time time.Time 
        severty string 
        messge string 
    }
    
    logCh := make(chan logEntry,50)

    func main () {
        
        go logger()
        
        logCh <- logEntry{time.Now(),logInfo , "App is starting"}
        
        logCh <- logEntry{time.Now(),logInfo , "App is sutting down"}
        
        time.Sleep( 100 * time.Milisecond)
        
    }
    
    func logger () {
    
        for entry := range logCh {
        
            fmt.Println(" %v - [%v] %v \n")
            
            entry.time.Format(" %v %v ",entry.severty,entry.message)
        }
    }
    
    // output 
    // 2021-12-15 23:00:00 [INFO] App is starting 
```

but the logger needs to shutdown 

now after the main function is done out logger function wripped down forcefully 


to do it more greacefully we could do 

one , with difer 

```
    go logger() 
    
    defer func() { // executes before main exits 
        close(logch)
    }()

```

two , with select statement , zero memory allocation is required in this process 

```

    var doneCh = make(chan struct{})
    
    // this is a singal only channel we cant 
    // send or recive any data with this channel
    // but we can know a message was sent or recive 

    func logger() {
    
        for { // inf loop 
            
            select {
            
                case entry := <- logch : 
                    fmt.Println()
                case <- doneCh : 
                    break  // exits from the loop and exits the channel 
                    
                // if we have a default case it will 
                // become not blocking and exits 
            }
        }
    }
```


now to singal done channel form the main 


```
    func main() {
    
        go logger() 
        
        logCh <- logEntry{sth}
        
        logCh <- logEntry{sth}
        
        time.Sleep()
        
        doneCh <- struct{}{} 
        
        // struct{} is type , statuct{}{} defining a struct 
        // with no fields and then initialize struct with curly braces 
    }

    // output 
    // same as before 
```


## Parsing JSON

golang package for json in `encoding/json`

for encoding `json.Marshal` for decoding `json.Unmarshal`


date type 

|__GO__| __JSON__|
|--|--|
|bool|boolean|
|float64|Numbers|
|string|string|
|nil|null|
|array|array|
|map/struct|Object|


__ex__ 

```
    
    import (
        "fmt"
        "encoding/json"
    )

    type Human struct {
    
        Name  string 
        
        Age Number 
        
        Address string 
    }
```


```

func main() {

    human := Human{"Antik",23,"yemen"}
    
    humanEnc , err := json.Marshal(human) 
    
    if err != nil {
    
        fmr.Println(err)
    
    }
    
    fmr.Println(string(humanEnc))
    
    humans := []Human{
    
        Human{"Antik",23,"yemen"},
        Human{"Istiak",26,"dhaka"},
        
    }
    
    humansEnc , err := json.Marshal(humans)
    
    if err != nil {
    
        fmr.Println(err)
    }
    
    fmr.Pritnln(string(humans))
}

```


__ex__ 

```

var human1 Human 

Data := []byte(`{

    "Name" : "Arif",
    "Age" : "26",
    "Address" : "Mirpur"
}`)

err := json.Unmarshal(Data,&human1)

if err != nil {

}

fmt.Println("this struct is",human1)

var human2 []Human 

Data2 := []byte(`[
    {
        "Name" : "Arif",
        "Age" : "26",
        "Address" : "Mirpur"
    },
    {
        "Name" : "Galib",
        "Age" : "30",
        "Address" : "Faridpur"
    }
]`)

error := json.Unmarshal(Data2,&human2)

fmt.Println("the array is ",&human2)

```