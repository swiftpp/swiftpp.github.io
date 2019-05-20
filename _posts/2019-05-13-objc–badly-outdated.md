---
layout: post
title: Objective-C–Badly Outdated?
---

A comment was made on Twitter that the programming language Objective-C was badly outdated, and Swift's syntax was easier to learn for programmers brought up on C-style programming languages. Let me suggest the contrary in a laboriously long-ass post.

### tl;dr

Swift is inferior to Objective-C, and especially to its forebear, Smalltalk:

* Swift's syntax is an offshoot of FORTRAN. There's nothing modern about it.
* Fortran's comma-delimited parameter passing, which Swift adopted, was selected without regard for cognitive impact.
* The ambiguous nature of Swift's parameter syntax makes it harder to recall their context when writing and reading, resulting in increased cognitive load and lost productivity.
* Swift's syntax makes it hard enough to read code with commas, but adding named parameters makes it worse.
* Swift's use of comma-delimited parameters obscures the purpose of each parameter: its purpose and its type.
* Swift's syntax for expressions has multiple modes: prefix and postfix operators, modifiers, attributes, etc.
* Swift's syntax for control-flow statements is inconsistent with that of invoking functions and methods.
* Swift's syntax for defining data structures and elements is inconsistent with the rest of the language.

### Don't Drink the Kool-aid

Swift's comma-delimited parameters are a holdover from Cold War era FORTRAN. Now, I don't know how much consideration [Chris Lattner](https://twitter.com/clattner_llvm) put into picking comma delimiters over ObjC's infix notation, but [John Backus](https://www.computerhistory.org/fellowawards/hall/john-backus/), who led the development of Fortran later remarked, "…our entire attitude about language design had alwavs been a very casual one…"[<sup>1</sup>](#1). In contrast, the Smalltalk syntax which ObjC is based on incubated ~10 years at Xerox PARC in Alan Kay's Learning Research Group, which was focused on making the computer accessible as a problem-solving tool for children and non-programmer adults. Not to take anything away from Lattner's brain, but LRG was a decent-sized interdisciplinary team of professionals working on ways for non-technical folks to learn a system sufficiently well to develop their own tools to solve problems, and to do it in less than a day. Let's see how well the Smalltalk language they contrived stacks up against the Fortran Way.

Fortran-style syntax might seem practical when writing code, but it's troublesome when reading; dropping vital context for which one will need to pause to review mentally. Or worse, take the time to manually add into the code as a comment for a mnemonic. No code completion when adding comments, so you lose productivity, and the comment delimiters add more semiotic noise on top of the commas.

<img src="/images/semiotic-noise.png">

If you think it's inconvenient to use infix notation when you write a function call, which you only do once, you should find it very inconvenient to have to stop to recall the data type of each position in the call and its purpose. The inconvenience of manually typing argument names vs the inconvenience of mentally switching contexts. Higher cognitive load. Less effective mind.

"A-ha!", you'll say. "Swift's modern syntax with named arguments eliminates the need to write the argument's context in comments!" Sure, but in Swift it's optional. Not only have you given up the consistency of named parameters across the codebase, but because it's optional you're still obligated to use commas when named arguments are used. Crufting context into a clunky interface adds more cognitive load.

Comma-delimited arguments anonymizes each argument. Context is lost for its data type. Context is lost for its purpose. Microsoft tried to mitigate this with Hungarian Notation, but it's still deficient. And the order in which arguments are to be written are also lost with this format. Infix notation gives you named, ordered parameters. Cleanly.

Moreover, the Fortran-style of syntax Swift uses is inconsistent in its structure and symbols. Expressions have prefix and postfix operators, modifiers, and attributes.

Smalltalk's syntax, which ObjC never truly followed, gave you a simple grammar which was consistent for the whole expression of code. Messages are:

```
unary-expression: receiver (unary-selector)*.
binary-expression: unary-expression (binary-selector unary-expression)*.
keyword-expression: binary-expression (keyword: binary-expression)*.
```

Similarly, the syntax for Swift's control structures use convoluted designs; again, inheriting Fortran's mess. Smalltalk's control structures are implemented as keywords sent as messages, conforming naturally to the existing syntax.

```
boolean-expression ifTrue: [block].           "Or ifFalse:"
[block] whileTrue: [block].                   "Or whileFalse:"
numeric-expression timesRepeat: [block].
collection do: [block].                       "Smalltalk's map function"
collection select: [block].                   "Smalltalk's filter function"
```

The same is true for defining structures and classes. Swift uses yet another format, while Smalltalk retains its message-sending paradigm.

```
Object subclass: #Stack
   instanceVariableNames: 'anArray top'
   classVariableNames: ''
   poolDictionaries: ''.
```

Swift's syntax was built on picking obvious structures which are inconsistent in their usage.
The language was designed with the easiest choice for the designers to make. It wasn't designed to be the easiest in which to write code. It also wasn't designed to be easy to implement. Swift's lexical analyzer and parser are horrible messes. As is its semantic analyzer, which uses a constraint solver to resolve the programmer's intent. Just trying to get it to figure out which are valid function calls and which aren't is difficult to debug.

<img src="/images/debugging-constraint-solver.png">

And because it has no clean, consistent mechanism for definitions of any kind, every feature added to the language looks like syntactic arsenic. Bells and whistles duct taped to Swift.

<img src="/images/swift-millenniumfalcon-1200x900.jpg">
*It's the compiler that did RC4 encryption in less than 12 parsecs, kid.*

Smalltalk's syntax conforms to a model which was refined to the simplest, most consistent metaphor: sending messages, in which the transmission mechanism is implied by the syntax. Consequently, there is no separate API to send a message, no other function call. A single abstraction for programmers to describe behavior and structure.

Swift doesn't have, as far as I've seen, a mechanism to add control-flow statements. But Smalltalk's singular reliance on messaging ensures a programmer can define the control mechanisms which are natural for its problem domain.

Swift's clunky, 1950's era comma-delimited parms have higher cognitive load than Smalltalk's infix names. Commas are semiotic noise v less unnecessary tokens.

To say Swift is easier to learn for those used to Fortran-style languages is to resort to training wheels. I use a programing language in a professional capacity. Pro tools are higher level than consumer. Granted, there's some getting used to better tools. I'll allow that a professional C/C++ programmer might need a week to get used to reading infix method names, I myself have had to do it. But that's a minor inconvenience compared to the lifetime of a codebase in which they'll be more productive.

Swift's programming model is too dependent on past mental models. State vars v state objects. 

Swift's reversion to Fortran's programming style abandons 3 important facets of the programming profession: 30 years of advances in the psychology of programming, using computers to offload mental and manual labor, and  facilities for the definition of programming expressions and tools that amplify our mental abilities.

If Objective-C, which is a half-hearted copy of Smalltalk, is now badly outdated, Swift started out as a relic of a long dead era.

## References

<a class="anchor" id="1" href="http://www.softwarepreservation.org/projects/FORTRAN/paper/p165-backus.pdf">The history of FORTRAN I, II, III, 1978, page 169</a>
