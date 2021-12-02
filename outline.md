---

theme : "night"
transition: "slide"
highlightTheme: "monokai"
slideNumber: true
title: "SAFE Stack"
---

## SAFE Stack

### with F #

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

## Lin Jia Wei

![](./img/photo.jpg =500x500)

---

### Outline

1. [F# Introduction](../FsharpIntroduction/export/)
1. [Functional Programming With F#](../fp/export/)
1. [Domain Modeling Made Functional](../DomainModeling/export/)
1. [SAFE Introduction](../ch3/export/)
1. [Saturn](../ch4/export/)
1. [Fable+Elmish](../ch5/export/)
1.

note:
F# Introduction:let everyone know what is F# and introcution of syntax
Domain modeling made functional:Introduction power of F# type system
SAFE Introduction

---

### References

- <https://github.com/swlaschin/dotnetconf2021>