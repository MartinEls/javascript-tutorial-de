
# The JavaScript Tutorial

This repository hosts the German translation of the Modern JavaScript Tutorial. The original content is published at [https://javascript.info](https://javascript.info).

## Translation

If you want to contribute to the translation fork this repository and go ahead. Submit your work via pull request.

The table of content below indicates already translated chapters via an active link to the translated file. Chapters without a link are stil in the original, english shape.

Please note that the tutorial can run locally using <https://github.com/iliakan/javascript-tutorial-server/>.

## Structure

Every chapter, article or a task has its folder.

The folder is named like `N-url`, where `N` is a number for the sorting purposes and `url` is the URL part with title of the material.

The type of the material is defined by the file inside the folder:

  - `index.md` stands for a chapter
  - `article.md` stands for an article
  - `task.md` stands for a task (solution must be provided in `solution.md` file as well)

Each of these files starts from the `# Main header`.

Assets required for the material reside in the same folder.

----

## Übersetzungskonventionen

Bei Übersetzungen von IT-Themen ins Deutsche begegnet man immer wieder Eigennamen, die keine gute Übersetzung finden und deshalb im Original stehen bleiben sollten. Für einige Wendungen gibt es aber durchaus treffende Deutsche Entsprechungen. Die folgende Tabelle sammelt einige Zweifelsfälle um eine einheitliche Verwendung über alle Kapitel im Tutorial zu gewährleisten.

Wortgruppen die im Englischen getrennt geschrieben werden, wie "HTML file", sollten im Deutschen mit einem Bindestrich verbunden werden (HTML-Datei) um eine gute Lesbarkeit zu gewährleisten. 

| English | Deutsch |
|---------|---------|
| browser | Browser |
| code | Code |
| command | Befehl |
| cookie | Cookie |
| engine | Engine |
| header | Header |
| low-level | systemnah |
| page | Seite |
| script | Script |
| statement | Anweisung |
| string | String |
| tag | Tag |
| tool | Werkzeug |

----

# The JavaScript language - TOC

## An introduction

[Eine Einführung in JavaScript](1-js/01-getting-started/1-intro/article.md)

[Code-Editoren](1-js/01-getting-started/2-code-editors/article.md)

[Entwicklerkonsole](1-js/01-getting-started/3-devtools/article.md)

## JavaScript Fundamentals

[Hello, world!](1-js/02-first-steps/01-hello-world/article.md)

[Code-Struktur](1-js/02-first-steps/02-structure/article.md)

[Moderne Spracheigenschaften: "use strict"](1-js/02-first-steps/03-strict-mode/article.md)

[Variablen](1-js/02-first-steps/04-variables/article.md)

[Datentypen](1-js/02-first-steps/05-types/article.md)

Type Conversions

Operators

Comparisons

Interaction: alert, prompt, confirm

Conditional operators: if, '?'

[Logische Operatoren](1-js/02-first-steps/11-logical-operators/article.md)

Loops: while and for

The "switch" statement

Functions

Function expressions and arrows

JavaScript specials

## Code quality

[Debuggen in Chrome](1-js/03-code-quality/01-debugging-chrome/article.md)

Coding style

Comments

Ninja code

Automated testing with mocha

Polyfills

## Objects: the basics

Objects

Garbage collection

Symbol type

Object methods, "this"

Object to primitive conversion

Constructor, operator "new"

## Data types

Methods of primitives

Numbers

Strings

Arrays

Array methods

Iterables

Map, Set, WeakMap and WeakSet

Object.keys, values, entries

Destructuring assignment

Date and time

JSON methods, toJSON

## Advanced working with functions

Recursion and stack

Rest parameters and spread operator

Closure

The old "var"

Global object

Function object, NFE

The "new Function" syntax

Scheduling: setTimeout and setInterval

Decorators and forwarding, call/apply

Function binding

Currying and partials

Arrow functions revisited

## Objects, classes, inheritance

Property flags and descriptors

Property getters and setters

Prototypal inheritance

F.prototype

Native prototypes

Methods for prototypes

Class patterns

Classes

Class inheritance, super

Class checking: "instanceof"

Mixins

## Error handling

Error handling, "try..catch"

Custom errors, extending Error

Browser: Document, Events, Interfaces

## Document

Browser environment, specs

DOM tree

Walking the DOM

Searching: getElement* and querySelector*

Node properties: type, tag and contents

Attributes and properties

Modifying the document

Styles and classes

Element size and scrolling

Window sizes and scrolling

Coordinates

## Introduction into Events

Introduction to browser events

Bubbling and capturing

Event delegation

Browser default actions

Dispatching custom events

## Events in details

Mouse events basics

Moving: mouseover/out, mouseenter/leave

Drag'n'Drop with mouse events

Keyboard: keydown and keyup

Scrolling

Page lifecycle: DOMContentLoaded, load, beforeunload, unload

Resource loading: onload and onerror

## Forms, controls

Form properties and methods

Focusing: focus/blur

Events: change, input, cut, copy, paste

Form submission: event and method submit

Additional articles

## Animation

[Bezierkurven](3-animation/1-bezier-curve/article.md)

CSS-animations

JavaScript animations

## Frames and windows

Popups and window methods

Cross-window communication

The clickjacking attack

## Regular expressions

Patterns and flags

Methods of RegExp and String

Character classes

Escaping, special characters

Sets and ranges [...]

The unicode flag

Quantifiers +, *, ? and {n}

Greedy and lazy quantifiers

Capturing groups

Backreferences: \n and $n

Alternation (OR) |

String start ^ and finish $

Multiline mode, flag "m"

Lookahead (in progress)

Infinite backtracking problem

## Promises, async/await

Introduction: callbacks

Promise

Promises chaining

Promise API
