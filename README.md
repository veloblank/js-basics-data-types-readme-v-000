# JavaScript Data Types

## Problem Statement

Did you ever hear this song from educational TV?

```text
One of these things is not like the others.
One of these things doesn't belong.
Can you tell which thing is not like the other by the time
I finish this song?
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/rsRjQDrDnY8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

What this song is asking the young viewer to engage in is a pretty powerful
behavior: _abstraction_. It's looking at several _concrete_ examples and
finding some sort of "ideal" that the _concrete_ examples all have in common
and using that as a rule to find something that doesn't _quite_ fit.

Doing this is one of the most profound problems in philosophy and human development.
No less an authority than Aristotle wrote a [whole book][] on it and how humans do
it is one of the essential reasons why he [differs][] from his teacher, Plato.

Who knew JavaScript would lead us to ancient Greece as well as "Sesame Street?"

In JavaScript _concrete_ instances of data can be categorized into _abstract_ names
called "data type" or, more simply, "type."

## Objectives

1. Define a data type
2. Demonstrate basic type checking with the `typeof` operator
3. Identify JavaScript's seven basic data types
4. Describe interactions between data of various types in JavaScript

## Define a Data Type

***Everything is JavaScript is data*** except:

1. **Operators**: `+`, `!`, `<=`, etc.
2. **Reserved Words** (`function`, `for`,`debugger`, etc.)

Every piece of data falls into one of JavaScript's seven data types: numbers, strings,
booleans, symbols, objects, `null`, and `undefined`.

## Demonstrate Basic Type Checking with the `typeof` Operator

Throughout this lesson, we'll use the `typeof` operator to give us an idea of
what data types we're dealing with. `typeof` accepts one argument, the piece of
data that we'd like to know the _type of_.

> **CAREFUL** `typeof` is an operator, just like `+` or `!`. We get used to operators
being only one character, but JavaScript (and many other languages) have operators
with more than character. As such, **we don't need parentheses with `typeof`**. That
said, JavaScript also supports `()` after `typeof`, but it's commonly not done.

## Identify JavaScript's Seven Basic Data Types

### Numbers

Some programming languages divide numbers up into integers,
decimals, doubles, floats, and so on. They do this so that they can have higher
_precision_ in their calculations. In a banking application or airplane wing 
engineering application we want our interest rate or the curve of the wing to be
***as accurate as possible***. For good reason: we want to make sure we get paid
or have a safe plane! When JavaScript was created, this level of precision was not
thought to be a thing that would be needed, so JavaScript only has a single, all-
encompassing `number` type:

```js
typeof 42
//=> "number"

typeof 3.141592653589793
//=> "number"

typeof 5e-324
//=> "number"

typeof -Infinity
//=> "number"
```

> **Think About This** As JavaScript has become a language for the back-end as well
as the front-end, it's imprecision around numbers keep it from entering many 
banking or engineering applications where precision is vital.

### Strings

Strings are how we represent text in JavaScript. A string consists of a matching
pair of `'single quotes'`, `"double quotes"`, or `` `backticks` `` with zero or
more characters in between:

```js
typeof "I am a string."
//=> "string"

typeof 'Me too!'
//=> "string"

typeof `Me three!`
//=> "string"
```

Even empty strings are strings:

```js
typeof ""
//=> "string"
```

### Booleans

A boolean can only be one of two possible values: `true` or `false`. Booleans
play a big role in if statements and looping in JavaScript.

```js
typeof true
//=> "boolean"

typeof false
//=> "boolean"
```

### Objects

JavaScript `Object`s are a collection of properties bounded by curly braces (`{
}`), similar to a hash in Ruby or a dictionary in Python.

The properties can point to values of any data type — even other objects:

```js
{
  "name": "JavaScript",
  "createdBy": {
    "firstName": "Brendan",
    "lastName": "Eich"
  },
  "firstReleased": 1995,
  "isAwesome": true
}

typeof {}
//=> "object"
```

From JavaScript's perspective, what we call "arrays" are just special-cases of
an `"object"` where the keys are all `number`s. So while JavaScript has 
`Array`s like `let dogs = ["Byron", "Cubby", "Boo Radley"]`, JavaScript
really thinks that `typeof dogs` is `"object"`.

### `null`

The `null` data type represents an intentionally absent object. For example, if
a piece of code returns an object when it successfully executes, we could have
it return `null` in the event of an error. Confusingly, the `typeof` operator
returns `"object"` when called with `null`:

```js
typeof null
//=> "object"
```

### `undefined`

The bane of many JS developers, `undefined` is a bit of a misnomer. Instead of
'not defined,' it actually means something more like 'not yet assigned a value.'


```js
typeof undefined
//=> "undefined"
```

### Symbols

Symbols are a relatively new data type (introduced in ES2015) that's primarily
used as an alternate way to add properties to objects. Don't worry about symbols
for now.

### Primitive Types

Six of the seven JavaScript data types — everything except `object` — are
**primitive**. All this means is that they represent _single_ values, such as
`7` or `"hello"` or `false`, instead of a collection of values.

## Describe Interactions Between Data of Various Types in JavaScript

Every programming language has its own rules governing the ways in which we can
operate on data of a given type. For example, it's rather uncontroversial that
`number`s can be subtracted from other `number`s...

```js
3 - 2
//=> 1
```
...and that strings can be added to other strings:

```js
"Hello" + ', ' + `world!`
//=> "Hello, world!"
```

But what happens if you mix them?

Some programming languages, such as Python, are strict about how data of
different types can interact, and they will refuse to compile a program that
blends types. Well, that's rather strict.

Other languages, such as Ruby, will attempt to handle
the interaction by converting one of the data types so all data is of the same
type. For example, instead of throwing an error when an integer (`3`) is added
to a floating-point number (`0.14159`), Ruby will simply convert the integer
into a floating-point number and correctly calculate the sum:

```ruby
3 + 0.14159
#=> 3.14159
```

Ruby throws errors when some stranger cases come up

```ruby
> "THX-" + 1138
TypeError: no implicit conversion of Fixnum into String
```

That seems pretty reasonable: I don't know how to make the `Integer` `1138` a `String`
without being directly told that you want it to be a `String` (same as Python's
rule).

That seems like a good baseline. However, JavaScript is a little _too_ nice when
handling conflicting data types. ***No matter what weird combination of types you give it, JavaScript won't throw an
error and will return _something_ (though that _something_ might make no sense
at all)***.

Sometimes this makes _some_ sense

```js
"High " + 5 + "!"
//=> "High 5!"
```
...to the [comical][Wat]:

```js
null ** 2 // null to the power of 2
//=> 0

undefined ** null // undefined to the power of null
//=> 1

{} + {} // empty object plus empty object
//=> "[object Object][object Object]" <-- That's a string!
```

Why JavaScript returns a string when we ask it to add two empty objects is
anyone's guess, but its heart is in the right place. The language always tries
to bend over backwards for its human masters, returning actionable data instead
of throwing errors. However, JavaScript's eagerness occasionally results in data
type issues that surprise both novice and expert programmers alike.

Try to follow along with what's happening here:

```js
1 + 2 + 3 + 4 + 5
//=> 15

"1" + 2 + 3 + 4 + 5
//=> "12345"

1 + "2" + 3 + 4 + 5
//=> "12345"

1 + 2 + "3" + 4 + 5
//=> "3345"

1 + 2 + 3 + "4" + 5
//=> "645"

1 + 2 + 3 + 4 + "5"
//=> "105"
```

As long as we are only adding numbers to other numbers, JavaScript performs the
expected addition. However, as soon as we throw a string in the mix, we stop
adding and start concatenating everything together into a string. In the fourth
example, we add the numbers `1`, `2`, and `3` together to get `6` (a number). We
then ask JavaScript to add `6` (a number) to `"4"` (a string). JavaScript can't
perform addition with a string, so it decides to concatenate the two operands
instead, resulting in `"64"` (a string). The remaining operation, `"64" + 5`, is
also between a string and a number, and JavaScript once again concatenates,
giving us the final result of `"645"` (a string).

You'll encounter a lot of these weird data type behaviors throughout your
JavaScript programming, but fear not: they'll trip you up less and
less often as you gain experience.

## Conclusion

Data types are representations of pieces of information and JavaScript defines
seven different types: numbers, strings, booleans, symbols, objects, `null`, and
`undefined`.

## Resources

- [MDN — JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [Destroy All Software — Types](https://www.destroyallsoftware.com/compendium/types?share_key=baf6b67369843fa2) – A cross-language examination of type in various language
- [Destroy All Software — Wat][Wat] – A beloved ***and hilarious*** talk in which JavaScript's friendliness when mixing types is discussed at a fever pace – with awesome slides

[Wat]: https://www.destroyallsoftware.com/talks/wat
[whole book]: https://plato.stanford.edu/entries/aristotle-categories/
[differs]: https://www.diffen.com/difference/Aristotle_vs_Plato
