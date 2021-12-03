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




