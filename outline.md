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

![](./img/photo.jpg =400x400)

---

### Outline

1. [F# Introduction](../FsharpIntroduction/export/index.html#)
2. [Domain Modeling Made Functional](../DomainModeling/export/index.html#)
3. [SAFE Introduction](../SAFE-intro/export/index.html#)
4. [Saturn](../Saturn/export/index.html#)
5. [Fable+Elmish](../Fable&Elmish/export/index.html#)
6. [SAFE Template Overview](../SAFETemplateOverview/export/index.html#)
7. [Functional Programming With F#](../fp/export/index.html#)

note:
F# Introduction:let everyone know what is F# and introcution of syntax
Domain modeling made functional:Introduction power of F# type system
SAFE Introduction

---

### References

- <https://github.com/swlaschin/dotnetconf2021>