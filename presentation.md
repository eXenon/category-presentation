---
title: Category Theory 101
revealOptions:
    transition: 'none'
    slideNumber: true
---
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
<h1>Category Theory 101</h1>

---

This whole presentation was shamelessly stolen from B. Milewski and his PDF "Category Theory for Programmers".

---

Programming is mostly composition. Composing functions, objects, data, modules, and, in the end, programs.

A category is made of two things, _objects_ and _morphisms_. And there must be 3 properties :
```

∀f,g ∈ C, f∘g ∈ C                       < -- Composition
Identity ∈ C                            < -- Identity
∀f,g,h ∈ C, f∘(g∘h) = (f∘g)∘h           < -- Associativity


```

---

<small>

- Specifics about objects are irrelevant
- Only the shape of a category is interesting

</small>

---

<img src="assets/category.jpg">

---

## Examples

- No object
- A graph with one point and one arrow
- An order. A relation that is like ≤ on any set.
- Monoid (set with append and empty)

---

In order to make append an arrow, we consider a function that will append "a", starting with the empty string.

```
[] --( +a )--> [a] --( +a )-> [aa] --( +a )--> [aaa] ...
```

Adding in identity, we have a category!

---

<img src="assets/go-deeper.jpg" height="500px">

---

<img src="assets/monoid.jpg">

---

#### Back to programming

Let's define an algebra on types.

---

Product types :
```
type Pair = (a, b)
let neutral = ()
```

---

Sum types :
```
type Either = Left a | Right b
let neutral = Void
```

---

We can now make analogies :
```
Pair ~ *
() ~ 1
Either ~ +
Void ~ 0
```

---

Let's go deeper :
```
1 + 1 ~ Either () () ~ Bool
1 * 0 ~ ((), Void) ~ Void
a * (b + c) ~ (a, Either b c) 
            ~ Either (a, b) (a, c) ~ a * b + a * c
```

---

```
prodToSum : (a, Either b c) -> Either (a, b) (a, c)
prodToSum =
    | (a, Left b)  -> Left a b
    | (a, Right c) -> Right a c

sumToProd : Either (a, b) (a, c)
sumToProd =
    | Left (a, b)  -> (a, Left b)
    | Right (a, c) -> (a, Right c)
```

---

<small>
To go even deeper : Curry-Howard isomorphism
</small>

And with all this, we can define more Monoids!

---

We now have our programmer category :
- Objects are basic types
- Arrows are functions
- Identity is trivial

---

<small>
Now let's transform Categories :
</small>

## Functors

---

Functors are functions that preserve the structure of the Category.

<img src="assets/functor.jpg">

---

And in real life :

A functor is a type with a `map` function.

- List is a functor
- Option is a functor (Maybe in Haskell)

```
map : (a -> b) -> a List -> b List
```

---

In Haskell : typeclasses

In OCaml : module types

```
Maybe = Nothing | Just a

instance Functor Maybe where
    fmap _ Nothing = Nothing
    fmap f (Just x) = Just (f x)
```

---

Functors also form a category...

<img src="assets/rabbit-hole.png">

---

<small>
And that is how you conclude a presentation about Category Theory without talking about Monads!
</small>

---

https://bartoszmilewski.com/2014/10/28/category-theory-for-programmers-the-preface/



