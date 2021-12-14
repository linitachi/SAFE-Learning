---

theme : "night"
transition: "slide"
highlightTheme: "monokai"
slideNumber: true
title: "SAFE Stack"

---

### ch 5

### Fable & Elmish

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

### What is Fable ?

- Fable is an F#-to-JavaScript (JS) compiler.
- Fable brings all the power of F# to the JS ecosystem.
- Use JS libraries from F# (and vice versa) as well as make use of standard JS tools.

<https://safe-stack.github.io/docs/component-fable/>

--

### Benefis of Fable

- Static type
- All of F#'s features
- Runs on JavaScript
- Great interoperability with JavaScript libraries

--

### How to use Fable?

#### Use npm package

<https://fable.io/docs/2-steps/your-first-fable-project.html>

--

### [practice: fable](https://github.com/linitachi/SAFE-LearningCode/tree/master/ch5.fable)

--

### Not enough

<https://fable.io/docs/communicate/js-from-fable.html>

---

### React

--

### what is React?

React is a free and open-source front-end JavaScript library for building user interfaces based on UI components. `by wiki`

--

### features

- Declarative
- Component-Based
- Learn Once, Write Anywhere

---

### F# React wrappers

--

### [Femto](https://fable.io/blog/2019/2019-06-29-Introducing-Femto.html)

Femto is CLI tool that manages the npm packages used by Fable bindings. It installs them using the npm package manager that you are using whether that is npm (default)

--

### Fable Packages

```
Fable.Elmish.React (nuget)
  |
  | -- Fable.Elmish (nuget)
  | -- Fable.React (nuget)
        |
        | -- react@16.8.0 (npm)
        | -- react-dom@16.8.0 (npm)
```

note: 假設我們使用了Fable.React這套件，但這套件相依於npm套件中的react@16.8.0、react-dom@16.8.0，那我們需要再npm當中安裝這兩個套件才行，我們不但需要知道Fable.React要用到哪些npm套件，還要正確安裝才行，這非常麻煩，但Femto可以自動幫我們做掉這件事情。

--

### [Feliz](https://zaid-ajaj.github.io/Feliz/)

A fresh retake of the base React DSL to build React applications, optimized for happiness.

--

Here is how it looks like:

```Fsharp
module App

open Feliz

[<ReactComponent>]
let Counter() =
    let (count, setCount) = React.useState(0)
    Html.div [
        Html.button [
            prop.style [ style.marginRight 5 ]
            prop.onClick (fun _ -> setCount(count + 1))
            prop.text "Increment"
        ]

        Html.button [
            prop.style [ style.marginLeft 5 ]
            prop.onClick (fun _ -> setCount(count - 1))
            prop.text "Decrement"
        ]

        Html.h1 count
    ]

open Browser.Dom

ReactDOM.render(Counter(), document.getElementById "root")
```

---

### [practice: Wrapping a React component](https://github.com/linitachi/SAFE-LearningCode/tree/master/ch5.reactWrapper)

---

### [Elmish](https://safe-stack.github.io/docs/component-elmish/)

--

#### Elmish is a library for building single page applications in F# applications, following the model-view-update(MVU) architecture made famous by Elm

note:Elmish 是一個用於在 F# 應用程序中構建單頁應用程序的函式庫，遵循 Elm 著名的模型-視圖-更新架構。

--

### MVU architeture

![](./img/elmish-architeture.JPG =800x600)

--

### [practice: Elmish - counter](https://github.com/linitachi/SAFE-LearningCode/tree/master/ch5.Elmish)

- <https://thesharperdev.com/getting-started-with-elmish/>
- <https://www.compositional-it.com/news-blog/ui-programming-with-elmish-in-f/>

--

### Elmish on SAFE Template

```fsharp
let update (msg: Msg) (model: Model) : Model * Cmd<Msg> =
    match msg with
    | GotTodos todos -> { model with Todos = todos }, Cmd.none
    | SetInput value -> { model with Input = value }, Cmd.none
    | AddTodo ->
        let todo = Todo.create model.Input

        let cmd =
            Cmd.OfAsync.perform todosApi.addTodo todo AddedTodo

        { model with Input = "" }, cmd
    | AddedTodo todo ->
        { model with
              Todos = model.Todos @ [ todo ] },
        Cmd.none
```

note:剛剛的練習是簡化版本的Elmish，SAFE Template中的是具有command的版本

---

### How to write View?

1. Fable.React
2. Feliz
3. Feliz.Bulma

--

### Fable.React

```fsharp
  div []
      [ button [ OnClick (fun _ -> dispatch Increment) ] [ str "+" ]
        div [] [ str (string model) ]
        button [ OnClick (fun _ -> dispatch Decrement) ] [ str "-" ] ]
```

<https://mangelmaxime.github.io/html-to-elmish/>

--

### Feliz

```fsharp
Html.div [
    prop.className "columns"
    prop.children [
        Html.div [
            prop.className "column is-2"
            prop.children [
                Html.button.a [
                    prop.className "button"
                    prop.text "Click me"
                ]
            ]
        ]
    ]
]
```

--

### Feliz.Bulma

```fsharp
open Feliz.Bulma

Bulma.columns [
    Bulma.column [
        column.is2 // <-- note context helper here
        prop.children [
            Bulma.button.button "Click me"
        ]
    ]
]
```

--

### Difference
[My journey with Feliz | A comparison between Fable.React and Feliz #155](https://github.com/Zaid-Ajaj/Feliz/issues/155#conclusion)

---

### References

<https://reactjs.org/>

[F# wrappers for React components](<https://www.compositional-it.com/news-blog/f-wrappers-for-react-components/>)

[Feliz.Bulma](https://dzoukr.github.io/Feliz.Bulma/#/)

---

## [return to Outline](../../export/#/2)
