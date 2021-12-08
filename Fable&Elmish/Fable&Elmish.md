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

### [practice-ch5.fable](https://github.com/linitachi/SAFE-LearningCode/tree/master/ch5.fable)

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

### Lab: Wrapping a React component

---

### References

<https://reactjs.org/>

[F# wrappers for React components](<https://www.compositional-it.com/news-blog/f-wrappers-for-react-components/>)

---

## [return to Outline](../../export/#/2)
