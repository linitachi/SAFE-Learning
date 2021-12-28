---

theme : "night"
transition: "slide"
highlightTheme: "monokai"
slideNumber: true
title: "SAFE Stack"

---

### ch 2

### Domain Modeling Made Functional

#### F#

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

### What is Domain model ? 🤔

--

In **software engineering**, a domain model is a **conceptual** model of the domain

--

#### How can we get domain model?

note:我們要怎麼取得domain model呢?既然domain model為某個domain的概念模型，首先我們就要取得domain的知識。

--

![](./img/share_mental_model.jpg =700x500)

note:我們可以透過shared mental model來取得Domain knowledge，當users、Domain experts、developer都參與討論，討論出屬於這個團隊共同的語言，就不會出現爭議，就好像我們在麥噹噹點了一號餐，每個員工都知道1號餐是什麼配置，那它們有shared mental model，對它們而言1號餐就代表著某種餐點，不會出現第二種餐點。
那為什麼code會在裡面呢?code在這邊是我們大家的共通語言，大家都使用code來溝通，這樣code自然而然就會變成domain model、文件

--

#### domain model

- User Story
- Event Storming

---

### Type System

note:用於定義如何將程式語言中的數值和運算式歸類為許多不同的型別，如何操作這些型別，這些型別如何互相作用。

--

#### Why Type System?

> A well designed functional program, on the other hand, will have a strong focus on _data types_ rather than behavior.--  Scott Wlaschin

--

- Code Readability
- Prevent errors
- Pattern Matching
- Domain Modeling

---

### Type abbreviations(alias)

- Code Readability

```Fsharp=
type [typename] = [existingType]
type Name = String
type Fruit = Apple
```

--

#### Have a Question

```Fsharp=
type FirstName = string
type LastName = string

let name firstName lastName = firstName + " " + lastName
let firstName: FirstName = "Jia-Wei"
let lastName: LastName = "Lin"
name firstName lastName //ok
name lastName firstName //ok
```

---

### Prevent errors

```Fsharp=
type FirstName = FirstName of string
type LastName = LastName of string

let firstName = FirstName "Jia-Wei"
let lastName = LastName "Lin"
let name (FirstName firstName) (LastName lastName) = firstName + " " + lastName

name firstName lastName // ok
name lastName firstName // error
```

---

### Pattern Matching

```Fsharp=
type Fruit =
    | Apple
    | Banana
    | Papaya

let fruitList = [ Apple; Banana; Papaya ]

for fruit in fruitList do
    match fruit with
    | Apple -> printfn "Yes! I love apple."
    | Banana -> printfn "Yes! I love banana."
    | Papaya -> printfn "Yes! I love papaya."

```

--

```Fsharp=
type Fruit =
    | Apple of string
    | Banana of string
    | Papaya of string

let fruitList =
    [ Apple "red apple"
      Banana "yellow banana"
      Papaya "Papaya!" ]

for fruit in fruitList do
    match fruit with
    | Apple value -> printfn "Yes! I love %A." value
    | Banana value -> printfn "Yes! I love %A." value
    | Papaya value -> printfn "Yes! I love %A." value
```

---

### Algebraic Data Type (ADT)

- Product Type ➡️ AND
- Sum Type ➡️ OR

--

### Product Type

A & B & C

#### Record

```Fsharp=
type Person1 = {Frst:string; Last:string}
```

#### Tuple

```Fsharp=
type Card = Suit * Rank
```

--

### Sum Type

A + B + C

#### Union

```Fsharp=
type Fruit = Apple | Banana | Papaya
```

--

### We can build up every thing with `ADT`

--

```Fsharp=
type UserContact ={
  FirstName: String50
  MiddleInitial: String1 option
  LastName: String50
  contactMethod: EmailAddress | PhoneNumber
}
```

note:這邊可以看到有一個User的連絡資訊，...
強調做好type後，我們其實不用寫test也可以確保我們的quality。

---

### Recap

- Domain model
  - shared mental model
- F# Type System
- ADT
  - Product type ➡️ And
  - Sum type ➡️ Or

---

### References

  <https://www.youtube.com/watch?v=2JB1_e5wZmU>
  <https://fsharpforfunandprofit.com/posts/overview-of-types-in-fsharp/>

---

## [return to Outline](../../export/index.html#/2)
