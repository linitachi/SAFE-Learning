---

theme : "night"
transition: "slide"
highlightTheme: "monokai"
slideNumber: true
title: "SAFE Stack"

---

### ch 1

### F# Introduction

<style>
pre {
  background: #303030;
  padding: 10px 16px;
  border-radius: 0.3em;
  counter-reset: line;
}
pre code[class*="="] .line {
  display: block;
  line-height: 1.8rem;
  font-size: 1em;
}
pre code[class*="="] .line:before {
  counter-increment: line;
  content: counter(line);
  display: inline-block;
  border-right: 3px solid #6ce26c !important;
  padding: 0 .5em;
  margin-right: .5em;
  color: #afafaf !important;
  width: 24px;
  text-align: right;
}

.reveal .slides > section > section {
  text-align: center;
}

h1,h2,h3,h4 {
  text-align: center;
}

p {
  text-align: center;
}
</style>

---

## [F# syntax](https://github.com/swlaschin/dotnetconf2021/blob/main/syntax.fsx)
note: 接下來為大家介紹F#的語法

--

```fsharp=

// ===================================
// Introducing "let something = something else"
// ===================================

let x = 42
// x is an immutable *value*
// everywhere you see "x" you can replace it with 42

// val x : int = 42
//       ^colon is for type annotations









// let is used to define functions as well

// a 2-parameter function
let add x y = x + y
//      ^ spaces between params
//            ^ no return keyword


// test it
add 2 3
// ^ ^ spaces between params
//     (except when calling OO code like .NET library)













// ===================================
// code blocks are represented by indentation
// ===================================

let square x =
    x * 2

let double x =
    let two = 2
    x * two

let squareAndDouble x =
    let y = square x
    double y  // no return keyword






(*
How to convert from a C-style language to F#
    * change to "let ... =" for definitions
    * indent how you normally would
    * delete the { }
    * delete "return"
    * delete semicolons
    * you often can delete type annotations as well!
*)

(*
// C-style language
int squareAndDouble(int x)
{
    var y = square(x);
    return double(y);
}
// python
def squareAndDouble(x):
    y = square(x)
    return double(y)
*)








// ===================================
// Computation expressions: Special code blocks
// with customizable behavior
// ===================================

let downloadFile filename : Async<string> = failwith "not implemented"
let uploadFile filename url : Async<unit> = failwith "not implemented"


let downloadManyFiles() =
    async {
       let! contentsA = downloadFile "source/a.txt"
       do! uploadFile contentsA "target/a.txt"
       return "OK"
    }
    // in an "async" computation expression:
    //  ^let! is like "await"
    //  ^do! is like "await void"

(*
computation expressions are used for:
* async/task
* queries (like query expression in C#)
* generating collections/enumerables
* validation
* error handing
* testing
* code generation
* etc etc
*)








// generate an sequence/enumerable
seq {
    yield! [1..11]
    if System.DateTime.Now.Hour > 12 then
        yield! [12..24]
    for i in [1..5] do
        yield square i
}










// dummy database
let db =
    {| Student = [
        {| StudentId=1; Name="Alice" |}
        {| StudentId=42; Name="Bob" |}
    ] |}

// query a database
query {
    for student in db.Student do
    where (student.StudentId > 4)
    sortBy student.Name
    select student
}










// ===================================
// Introducing the pipeline operator
// ===================================

let add42 x = x + 42

let squareDoubleAdd42 x =
    add42(double(square(x)))











let squareDoubleAdd42 x =
    x |> square |> double |> add42












// ===================================
// Pipelines are a bit like LINQ
// ===================================

open System // same as "using"
open System.Linq

[1..10]
  .Select(fun x -> x * 2)   // lambda syntax in F#
  .Where(fun x -> x <= 6)
  .Select(fun x -> $"x={x}")
  .ToArray()

[1..10]
|> List.map (fun x -> x * 2)  // 2 4 6...20
|> List.filter (fun x -> x <= 6)  //2 4 6
|> List.map (sprintf "x=%i") // 2 * 4 * 6 = 48















// pipelines are more flexible because
// you don't need extension methods

let product aList =
    List.fold (*) 1 aList

let logToConsole input =
    printfn "input=%i" input
    input

[1..10]
|> List.map (fun x -> x * 2) //2 4 6...20
|> List.filter (fun x -> x <= 6) //2 4 6
|> product // 2 * 4 * 6 = 48
|> logToConsole






















(* ======================================
SOLID works well with functional programming
Open-closed principle:
You can add new code, but don't change existing code
Pipeline-oriented programming is a good technique for this!
====================================== *)

// some dummy functions
let log label input =  failwith "not implemented"
let checkAuthorization query =  failwith "not implemented"
let loadFromDb (query:string) :string =  failwith "not implemented"
let saveToDb input :unit =  failwith "not implemented"

open System.Text.Json  // same as "using" or "import"

let myImportantWorkflow query =
    // Onion architecture: I/O at edges
    query
    |> loadFromDb
    |> JsonSerializer.Deserialize

    // pure domain logic
    |> List.map (fun x -> x * 2)
    |> List.filter (fun x -> x <= 6)

    // I/O
    |> JsonSerializer.Serialize
    |> saveToDb









// ===================================
// How type inference works
// ===================================

// with type annotations
let add2 (x:int) :int = x + 2
//         ^ type annotation (type comes AFTER parameter name)
//               ^ type annotation

// without type annotations
let add3 x = x + 3









let doSomething f x =
   let y = f (x + 1)
   "hello" + y











// use it
let intToStr i = sprintf "%i" i
doSomething intToStr 42













(*
Benefits of type inference
* less typing
* less noise, more logic
// C# code
public IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(
    IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector
    )
{
   ...
}
// F# code
let GroupBy source keySelector =
   ...
*)

// here's proof!
let groupBy source keySelector =
   List.groupBy keySelector source
```

---

### References

- [https://www.youtube.com/watch?v=kSfi6kcZrzM&ab_channel=dotNET](https://www.youtube.com/watch?v=kSfi6kcZrzM&ab_channel=dotNET) 

---

## [return to Outline](../../export/index.html#/2)
