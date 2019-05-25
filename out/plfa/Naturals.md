---
src       : src/plfa/Naturals.lagda
title     : "Naturals: Natural numbers"
layout    : page
prev      : /Preface/
permalink : /Naturals/
next      : /Induction/
---

<pre class="Agda">{% raw %}<a id="149" class="Keyword">module</a> <a id="156" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}" class="Module">plfa.Naturals</a> <a id="170" class="Keyword">where</a>{% endraw %}</pre>

The night sky holds more stars than I can count, though fewer than five
thousand are visible to the naked eye.  The observable universe
contains about seventy sextillion stars.

But the number of stars is finite, while natural numbers are infinite.
Count all the stars, and you will still have as many natural numbers
left over as you started with.


## The naturals are an inductive datatype

Everyone is familiar with the natural numbers

    0
    1
    2
    3
    ...

and so on. We write `ℕ` for the *type* of natural numbers, and say that
`0`, `1`, `2`, `3`, and so on are *values* of type `ℕ`, indicated by
writing `0 : ℕ`, `1 : ℕ`, `2 : ℕ`, `3 : ℕ`, and so on.

The set of natural numbers is infinite, yet we can write down
its definition in just a few lines.  Here is the definition
as a pair of inference rules:

    --------
    zero : ℕ

    m : ℕ
    ---------
    suc m : ℕ

And here is the definition in Agda:
<pre class="Agda">{% raw %}<a id="1127" class="Keyword">data</a> <a id="ℕ"></a><a id="1132" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="1134" class="Symbol">:</a> <a id="1136" class="PrimitiveType">Set</a> <a id="1140" class="Keyword">where</a>
  <a id="ℕ.zero"></a><a id="1148" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a> <a id="1153" class="Symbol">:</a> <a id="1155" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a>
  <a id="ℕ.suc"></a><a id="1159" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a>  <a id="1164" class="Symbol">:</a> <a id="1166" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="1168" class="Symbol">→</a> <a id="1170" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a>{% endraw %}</pre>

Here `ℕ` is the name of the *datatype* we are defining,
and `zero` and `suc` (short for *successor*) are the
*constructors* of the datatype.

Both definitions above tell us the same two things:

* _Base case_: `zero` is a natural number.
* _Inductive case_: if `m` is a natural number, then `suc m` is also a
  natural number.

Further, these two rules give the *only* ways of creating natural numbers.
Hence, the possible natural numbers are:

    zero
    suc zero
    suc (suc zero)
    suc (suc (suc zero))
    ...

We write `0` as shorthand for `zero`; and `1` is shorthand
for `suc zero`, the successor of zero, that is, the natural that comes
after zero; and `2` is shorthand for `suc (suc zero)`, which is the
same as `suc 1`, the successor of one; and `3` is shorthand for the
successor of two; and so on.

#### Exercise `seven` {#seven}

Write out `7` in longhand.

<pre class="Agda">{% raw %}<a id="2073" class="Comment">-- Your code goes here</a>{% endraw %}</pre>


## Unpacking the inference rules

Let's unpack the inference rules.  Each inference rule consists of
zero or more _judgments_ written above a horizontal line, called the
_hypotheses_, and a single judgment written below, called the
_conclusion_.  The first rule is the base case. It has no hypotheses,
and the conclusion asserts that `zero` is a natural.  The second rule
is the inductive case. It has one hypothesis, which assumes that `m`
is a natural, and the conclusion asserts that `suc m`
is a also a natural.


## Unpacking the Agda definition

Let's unpack the Agda definition. The keyword `data` tells us this is an
inductive definition, that is, that we are defining a new datatype
with constructors.  The phrase

    ℕ : Set

tells us that `ℕ` is the name of the new datatype, and that it is a
`Set`, which is the way in Agda of saying that it is a type.  The
keyword `where` separates the declaration of the datatype from the
declaration of its constructors. Each constructor is declared on a
separate line, which is indented to indicate that it belongs to the
corresponding `data` declaration.  The lines

    zero : ℕ
    suc  : ℕ → ℕ

give _signatures_ specifying the types of the constructors `zero` and `suc`.
They tell us that `zero` is a natural number and that `suc` takes a natural
number as argument and returns a natural number.

You may have noticed that `ℕ` and `→` don't appear on your keyboard.
They are symbols in _unicode_.  At the end of each chapter is a list
of all unicode symbols introduced in the chapter, including
instructions on how to type them in the Emacs text editor.  Here
_type_ refers to typing with fingers as opposed to data types!


## The story of creation

Let's look again at the rules that define the natural numbers:

* _Base case_: `zero` is a natural number.
* _Inductive case_: if `m` is a natural number, then `suc m` is also a
  natural number.

Hold on! The second line defines natural numbers in terms of natural
numbers. How can that possibly be allowed?  Isn't this as useless a
definition as "Brexit means Brexit"?

In fact, it is possible to assign our definition a meaning without
resorting to unpermitted circularities.  Furthermore, we can do so
while only working with _finite_ sets and never referring to the
_infinite_ set of natural numbers.

We will think of it as a creation story.  To start with, we know about
no natural numbers at all:

    -- In the beginning, there are no natural numbers.

Now, we apply the rules to all the natural numbers we know about.  The
base case tells us that `zero` is a natural number, so we add it to the set
of known natural numbers.  The inductive case tells us that if `m` is a
natural number (on the day before today) then `suc m` is also a
natural number (today).  We didn't know about any natural numbers
before today, so the inductive case doesn't apply:

    -- On the first day, there is one natural number.
    zero : ℕ

Then we repeat the process. On the next day we know about all the
numbers from the day before, plus any numbers added by the rules.  The
base case tells us that `zero` is a natural number, but we already knew
that. But now the inductive case tells us that since `zero` was a natural
number yesterday, then `suc zero` is a natural number today:

    -- On the second day, there are two natural numbers.
    zero : ℕ
    suc zero : ℕ

And we repeat the process again. Now the inductive case
tells us that since `zero` and `suc zero` are both natural numbers, then
`suc zero` and `suc (suc zero)` are natural numbers. We already knew about
the first of these, but the second is new:

    -- On the third day, there are three natural numbers.
    zero : ℕ
    suc zero : ℕ
    suc (suc zero) : ℕ

You've got the hang of it by now:

    -- On the fourth day, there are four natural numbers.
    zero : ℕ
    suc zero : ℕ
    suc (suc zero) : ℕ
    suc (suc (suc zero)) : ℕ

The process continues.  On the _n_'th day there will be _n_ distinct
natural numbers. Every natural number will appear on some given day.
In particular, the number _n_ first appears on day _n+1_. And we
never actually define the set of numbers in terms of itself. Instead,
we define the set of numbers on day _n+1_ in terms of the set of
numbers on day _n_.

A process like this one is called _inductive_. We start with nothing, and
build up a potentially infinite set by applying rules that convert one
finite set into another finite set.

The rule defining zero is called a _base case_, because it introduces
a natural number even when we know no other natural numbers.  The rule
defining successor is called an _inductive case_, because it
introduces more natural numbers once we already know some.  Note the
crucial role of the base case.  If we only had inductive rules, then
we would have no numbers in the beginning, and still no numbers on the
second day, and on the third, and so on.  An inductive definition lacking
a base case is useless, as in the phrase "Brexit means Brexit".


## Philosophy and history

A philosopher might observe that our reference to the first day,
second day, and so on, implicitly involves an understanding of natural
numbers.  In this sense, our definition might indeed be regarded as in
some sense circular, but we need not let this disturb us.
Everyone possesses a good informal understanding of the natural
numbers, which we may take as a foundation for their formal
description.

While the natural numbers have been understood for as long as people
can count, the inductive definition of the natural numbers is relatively
recent.  It can be traced back to Richard Dedekind's paper "_Was sind
und was sollen die Zahlen?_" (What are and what should be the
numbers?), published in 1888, and Giuseppe Peano's book "_Arithmetices
principia, nova methodo exposita_" (The principles of arithmetic
presented by a new method), published the following year.


## A pragma

In Agda, any text following `--` or enclosed between `{-`
and `-}` is considered a _comment_.  Comments have no effect on the
code, with the exception of one special kind of comment, called a
_pragma_, which is enclosed between `{-#` and `#-}`.

Including the line
<pre class="Agda">{% raw %}<a id="8299" class="Symbol">{-#</a> <a id="8303" class="Keyword">BUILTIN</a> NATURAL <a id="8319" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="8321" class="Symbol">#-}</a>{% endraw %}</pre>
tells Agda that `ℕ` corresponds to the natural numbers, and hence one
is permitted to type `0` as shorthand for `zero`, `1` as shorthand for
`suc zero`, `2` as shorthand for `suc (suc zero)`, and so on.  The
declaration is not permitted unless the type given has exactly two
constructors, one with no arguments (corresponding to zero) and
one with a single argument of the same type given in the pragma
(corresponding to successor).

As well as enabling the above shorthand, the pragma also enables a
more efficient internal representation of naturals using the Haskell
type for arbitrary-precision integers.  Representing the natural _n_
with `zero` and `suc` requires space proportional to _n_, whereas
representing it as an arbitrary-precision integer in Haskell only
requires space proportional to the logarithm of _n_.


## Imports

Shortly we will want to write some equations that hold between
terms involving natural numbers.  To support doing so, we import
the definition of equality and notations for reasoning
about it from the Agda standard library:

<pre class="Agda">{% raw %}<a id="9412" class="Keyword">import</a> <a id="9419" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html" class="Module">Relation.Binary.PropositionalEquality</a> <a id="9457" class="Symbol">as</a> <a id="9460" class="Module">Eq</a>
<a id="9463" class="Keyword">open</a> <a id="9468" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html" class="Module">Eq</a> <a id="9471" class="Keyword">using</a> <a id="9477" class="Symbol">(</a><a id="9478" href="https://agda.github.io/agda-stdlib/v0.17/Agda.Builtin.Equality.html#83" class="Datatype Operator">_≡_</a><a id="9481" class="Symbol">;</a> <a id="9483" href="https://agda.github.io/agda-stdlib/v0.17/Agda.Builtin.Equality.html#140" class="InductiveConstructor">refl</a><a id="9487" class="Symbol">)</a>
<a id="9489" class="Keyword">open</a> <a id="9494" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#3975" class="Module">Eq.≡-Reasoning</a> <a id="9509" class="Keyword">using</a> <a id="9515" class="Symbol">(</a><a id="9516" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4076" class="Function Operator">begin_</a><a id="9522" class="Symbol">;</a> <a id="9524" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">_≡⟨⟩_</a><a id="9529" class="Symbol">;</a> <a id="9531" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4374" class="Function Operator">_∎</a><a id="9533" class="Symbol">)</a>{% endraw %}</pre>

The first line brings the standard library module that defines
equality into scope and gives it the name `Eq`. The second line
opens that module, that is, adds all the names specified in the
`using` clause into the current scope. In this case the names added
are `_≡_`, the equality operator, and `refl`, the name for evidence
that two terms are equal.  The third line takes a module that
specifies operators to support reasoning about equivalence, and adds
all the names specified in the `using` clause into the current scope.
In this case, the names added are `begin_`, `_≡⟨⟩_`, and `_∎`.  We
will see how these are used below.  We take these as givens for now,
but will see how they are defined in
Chapter [Equality]({{ site.baseurl }}{% link out/plfa/Equality.md%}).

Agda uses underbars to indicate where terms appear in infix or mixfix
operators. Thus, `_≡_` and `_≡⟨⟩_` are infix (each operator is written
between two terms), while `begin_` is prefix (it is written before a
term), and `_∎` is postfix (it is written after a term).

Parentheses and semicolons are among the few characters that cannot
appear in names, so we do not need extra spaces in the `using` list.


## Operations on naturals are recursive functions {#plus}

Now that we have the natural numbers, what can we do with them?
For instance, can we define arithmetic operations such as
addition and multiplication?

As a child I spent much time memorising tables of addition and
multiplication.  At first the rules seemed tricky and I would often
make mistakes.  It came as a shock to me to discover _recursion_,
a simple technique by which every one of the infinite possible
instances of addition and multiplication can be specified in
just a couple of lines.

Here is the definition of addition in Agda:
<pre class="Agda">{% raw %}<a id="_+_"></a><a id="11305" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">_+_</a> <a id="11309" class="Symbol">:</a> <a id="11311" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="11313" class="Symbol">→</a> <a id="11315" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="11317" class="Symbol">→</a> <a id="11319" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a>
<a id="11321" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a> <a id="11326" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="11328" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11328" class="Bound">n</a> <a id="11330" class="Symbol">=</a> <a id="11332" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11328" class="Bound">n</a>
<a id="11334" class="Symbol">(</a><a id="11335" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="11339" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11339" class="Bound">m</a><a id="11340" class="Symbol">)</a> <a id="11342" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="11344" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11344" class="Bound">n</a> <a id="11346" class="Symbol">=</a> <a id="11348" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="11352" class="Symbol">(</a><a id="11353" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11339" class="Bound">m</a> <a id="11355" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="11357" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11344" class="Bound">n</a><a id="11358" class="Symbol">)</a>{% endraw %}</pre>

Let's unpack this definition.  Addition is an infix operator.  It is
written with underbars where the argument go, hence its name is
`_+_`.  The first line is a signature specifying the type of the operator.
The type `ℕ → ℕ → ℕ`, indicates that addition accepts two naturals
and returns a natural.  Infix notation is just a shorthand for application;
the terms `m + n` and `_+_ m n` are equivalent.

The definition has a base case and an inductive case, corresponding to
those for the natural numbers.  The base case says that adding zero to
a number, `zero + n`, returns that number, `n`.  The inductive case
says that adding the successor of a number to another number,
`(suc m) + n`, returns the successor of adding the two numbers, `suc (m + n)`.
We say we use _pattern matching_ when constructors appear on the
left-hand side of an equation.

If we write `zero` as `0` and `suc m` as `1 + m`, the definition turns
into two familiar equations:

     0       + n  ≡  n
     (1 + m) + n  ≡  1 + (m + n)

The first follows because zero is an identity for addition, and the
second because addition is associative.  In its most general form,
associativity is written

     (m + n) + p  ≡  m + (n + p)

meaning that the location of parentheses is irrelevant.  We get the
second equation from the third by taking `m` to be `1`, `n` to be `m`,
and `p` to be `n`.  We write `=` for definitions, while we
write `≡` for assertions that two already defined things are the same.

The definition is _recursive_, in that the last line defines addition
in terms of addition.  As with the inductive definition of the
naturals, the apparent circularity is not a problem.  It works because
addition of larger numbers is defined in terms of addition of smaller
numbers.  Such a definition is called _well founded_.

For example, let's add two and three:
<pre class="Agda">{% raw %}<a id="13223" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#13223" class="Function">_</a> <a id="13225" class="Symbol">:</a> <a id="13227" class="Number">2</a> <a id="13229" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13231" class="Number">3</a> <a id="13233" href="https://agda.github.io/agda-stdlib/v0.17/Agda.Builtin.Equality.html#83" class="Datatype Operator">≡</a> <a id="13235" class="Number">5</a>
<a id="13237" class="Symbol">_</a> <a id="13239" class="Symbol">=</a>
  <a id="13243" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4076" class="Function Operator">begin</a>
    <a id="13253" class="Number">2</a> <a id="13255" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13257" class="Number">3</a>
  <a id="13261" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="13268" class="Comment">-- is shorthand for</a>
    <a id="13292" class="Symbol">(</a><a id="13293" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13297" class="Symbol">(</a><a id="13298" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13302" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a><a id="13306" class="Symbol">))</a> <a id="13309" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13311" class="Symbol">(</a><a id="13312" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13316" class="Symbol">(</a><a id="13317" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13321" class="Symbol">(</a><a id="13322" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13326" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a><a id="13330" class="Symbol">)))</a>
  <a id="13336" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="13343" class="Comment">-- inductive case</a>
    <a id="13365" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13369" class="Symbol">((</a><a id="13371" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13375" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a><a id="13379" class="Symbol">)</a> <a id="13381" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13383" class="Symbol">(</a><a id="13384" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13388" class="Symbol">(</a><a id="13389" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13393" class="Symbol">(</a><a id="13394" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13398" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a><a id="13402" class="Symbol">))))</a>
  <a id="13409" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="13416" class="Comment">-- inductive case</a>
    <a id="13438" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13442" class="Symbol">(</a><a id="13443" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13447" class="Symbol">(</a><a id="13448" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a> <a id="13453" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13455" class="Symbol">(</a><a id="13456" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13460" class="Symbol">(</a><a id="13461" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13465" class="Symbol">(</a><a id="13466" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13470" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a><a id="13474" class="Symbol">)))))</a>
  <a id="13482" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="13489" class="Comment">-- base case</a>
    <a id="13506" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13510" class="Symbol">(</a><a id="13511" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13515" class="Symbol">(</a><a id="13516" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13520" class="Symbol">(</a><a id="13521" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13525" class="Symbol">(</a><a id="13526" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13530" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a><a id="13534" class="Symbol">))))</a>
  <a id="13541" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="13548" class="Comment">-- is longhand for</a>
    <a id="13571" class="Number">5</a>
  <a id="13575" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4374" class="Function Operator">∎</a>{% endraw %}</pre>
We can write the same derivation more compactly by only
expanding shorthand as needed:
<pre class="Agda">{% raw %}<a id="13688" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#13688" class="Function">_</a> <a id="13690" class="Symbol">:</a> <a id="13692" class="Number">2</a> <a id="13694" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13696" class="Number">3</a> <a id="13698" href="https://agda.github.io/agda-stdlib/v0.17/Agda.Builtin.Equality.html#83" class="Datatype Operator">≡</a> <a id="13700" class="Number">5</a>
<a id="13702" class="Symbol">_</a> <a id="13704" class="Symbol">=</a>
  <a id="13708" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4076" class="Function Operator">begin</a>
    <a id="13718" class="Number">2</a> <a id="13720" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13722" class="Number">3</a>
  <a id="13726" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
    <a id="13734" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13738" class="Symbol">(</a><a id="13739" class="Number">1</a> <a id="13741" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13743" class="Number">3</a><a id="13744" class="Symbol">)</a>
  <a id="13748" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
    <a id="13756" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13760" class="Symbol">(</a><a id="13761" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13765" class="Symbol">(</a><a id="13766" class="Number">0</a> <a id="13768" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="13770" class="Number">3</a><a id="13771" class="Symbol">))</a>
  <a id="13776" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
    <a id="13784" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13788" class="Symbol">(</a><a id="13789" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="13793" class="Number">3</a><a id="13794" class="Symbol">)</a>
  <a id="13798" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
    <a id="13806" class="Number">5</a>
  <a id="13810" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4374" class="Function Operator">∎</a>{% endraw %}</pre>
The first line matches the inductive case by taking `m = 1` and `n = 3`,
the second line matches the inductive case by taking `m = 0` and `n = 3`,
and the third line matches the base case by taking `n = 3`.

Both derivations consist of a signature (written with a colon, `:`),
giving a type, and a binding (written with an equal sign, `=`),
giving a term of the given type.  Here we use the dummy name `_`.  The
dummy name can be reused, and is convenient for examples.  Names other
than `_` must be used only once in a module.

Here the type is `2 + 3 ≡ 5` and the term provides _evidence_ for the
corresponding equation, here written in tabular form as a chain of
equations.  The chain starts with `begin` and finishes with `∎`
(pronounced "qed" or "tombstone", the latter from its appearance), and
consists of a series of terms separated by `≡⟨⟩`.

In fact, both proofs are longer than need be, and Agda is satisfied
with the following:
<pre class="Agda">{% raw %}<a id="14776" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#14776" class="Function">_</a> <a id="14778" class="Symbol">:</a> <a id="14780" class="Number">2</a> <a id="14782" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="14784" class="Number">3</a> <a id="14786" href="https://agda.github.io/agda-stdlib/v0.17/Agda.Builtin.Equality.html#83" class="Datatype Operator">≡</a> <a id="14788" class="Number">5</a>
<a id="14790" class="Symbol">_</a> <a id="14792" class="Symbol">=</a> <a id="14794" href="https://agda.github.io/agda-stdlib/v0.17/Agda.Builtin.Equality.html#140" class="InductiveConstructor">refl</a>{% endraw %}</pre>
Agda knows how to
compute the value of `2 + 3`, and so can immediately
check it is the same as `5`.  A binary relation is said to be _reflexive_
if every value relates to itself.  Evidence that a value is equal to
itself is written `refl`.

In the chains of equations, all Agda checks is that each term
simplifies to the same value. If we jumble the equations, omit lines, or
add extraneous lines it will still be accepted.  It's up to us to write
the equations in an order that makes sense to the reader.

Here `2 + 3 ≡ 5` is a type, and the chains of equations (and also
`refl`) are terms of the given type; alternatively, one can think of
each term as _evidence_ for the assertion `2 + 3 ≡ 5`.  This duality
of interpretation---of a type as a proposition, and of a term as
evidence---is central to how we formalise concepts in Agda, and will
be a running theme throughout this book.

Note that when we use the word _evidence_ it is nothing equivocal.  It
is not like testimony in a court which must be weighed to determine
whether the witness is trustworthy.  Rather, it is ironclad.  The
other word for evidence, which we will use interchangeably, is _proof_.

#### Exercise `+-example` {#plus-example}

Compute `3 + 4`, writing out your reasoning as a chain of equations.

<pre class="Agda">{% raw %}<a id="16101" class="Comment">-- Your code goes here</a>{% endraw %}</pre>


## Multiplication

Once we have defined addition, we can define multiplication
as repeated addition:
<pre class="Agda">{% raw %}<a id="_*_"></a><a id="16251" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">_*_</a> <a id="16255" class="Symbol">:</a> <a id="16257" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="16259" class="Symbol">→</a> <a id="16261" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="16263" class="Symbol">→</a> <a id="16265" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a>
<a id="16267" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a>  <a id="16273" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">*</a> <a id="16275" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16275" class="Bound">n</a>  <a id="16278" class="Symbol">=</a>  <a id="16281" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a>
<a id="16286" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="16290" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16290" class="Bound">m</a> <a id="16292" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">*</a> <a id="16294" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16294" class="Bound">n</a>  <a id="16297" class="Symbol">=</a>  <a id="16300" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16294" class="Bound">n</a> <a id="16302" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="16304" class="Symbol">(</a><a id="16305" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16290" class="Bound">m</a> <a id="16307" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">*</a> <a id="16309" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16294" class="Bound">n</a><a id="16310" class="Symbol">)</a>{% endraw %}</pre>
Computing `m * n` returns the sum of `m` copies of `n`.

Again, rewriting turns the definition into two familiar equations:

    0       * n  ≡  0
    (1 + m) * n  ≡  n + (m * n)

The first follows because zero times anything is zero, and the second
follows because multiplication distributes over addition.
In its most general form, distribution of multiplication over addition
is written

    (m + n) * p  ≡  (m * p) + (n * p)

We get the second equation from the third by taking `m` to be `1`, `n`
to be `m`, and `p` to be `n`, and then using the fact that one is an
identity for multiplication, so `1 * n ≡ n`.

Again, the definition is well-founded in that multiplication of
larger numbers is defined in terms of multiplication of smaller numbers.

For example, let's multiply two and three:
<pre class="Agda">{% raw %}<a id="17133" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#17133" class="Function">_</a> <a id="17135" class="Symbol">=</a>
  <a id="17139" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4076" class="Function Operator">begin</a>
    <a id="17149" class="Number">2</a> <a id="17151" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">*</a> <a id="17153" class="Number">3</a>
  <a id="17157" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="17164" class="Comment">-- inductive case</a>
    <a id="17186" class="Number">3</a> <a id="17188" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="17190" class="Symbol">(</a><a id="17191" class="Number">1</a> <a id="17193" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">*</a> <a id="17195" class="Number">3</a><a id="17196" class="Symbol">)</a>
  <a id="17200" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="17207" class="Comment">-- inductive case</a>
    <a id="17229" class="Number">3</a> <a id="17231" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="17233" class="Symbol">(</a><a id="17234" class="Number">3</a> <a id="17236" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="17238" class="Symbol">(</a><a id="17239" class="Number">0</a> <a id="17241" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Function Operator">*</a> <a id="17243" class="Number">3</a><a id="17244" class="Symbol">))</a>
  <a id="17249" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="17256" class="Comment">-- base case</a>
    <a id="17273" class="Number">3</a> <a id="17275" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="17277" class="Symbol">(</a><a id="17278" class="Number">3</a> <a id="17280" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Function Operator">+</a> <a id="17282" class="Number">0</a><a id="17283" class="Symbol">)</a>
  <a id="17287" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>    <a id="17294" class="Comment">-- simplify</a>
    <a id="17310" class="Number">6</a>
  <a id="17314" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4374" class="Function Operator">∎</a>{% endraw %}</pre>
The first line matches the inductive case by taking `m = 1` and `n = 3`,
The second line matches the inductive case by taking `m = 0` and `n = 3`,
and the third line matches the base case by taking `n = 3`.
Here we have omitted the signature declaring `_ : 2 * 3 ≡ 6`, since
it can easily be inferred from the corresponding term.


#### Exercise `*-example` {#times-example}

Compute `3 * 4`, writing out your reasoning as a chain of equations.

<pre class="Agda">{% raw %}<a id="17786" class="Comment">-- Your code goes here</a>{% endraw %}</pre>


#### Exercise `_^_` (recommended) {#power}

Define exponentiation, which is given by the following equations:

    n ^ 0        =  1
    n ^ (1 + m)  =  n * (n ^ m)

Check that `3 ^ 4` is `81`.

<pre class="Agda">{% raw %}<a id="18030" class="Comment">-- Your code goes here</a>{% endraw %}</pre>



## Monus

We can also define subtraction.  Since there are no negative
natural numbers, if we subtract a larger number from a smaller
number we will take the result to be zero.  This adaption of
subtraction to naturals is called _monus_ (a twist on _minus_).

Monus is our first use of a definition that uses pattern
matching against both arguments:
<pre class="Agda">{% raw %}<a id="_∸_"></a><a id="18430" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">_∸_</a> <a id="18434" class="Symbol">:</a> <a id="18436" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="18438" class="Symbol">→</a> <a id="18440" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a> <a id="18442" class="Symbol">→</a> <a id="18444" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1132" class="Datatype">ℕ</a>
<a id="18446" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18446" class="Bound">m</a>     <a id="18452" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="18454" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a>   <a id="18461" class="Symbol">=</a>  <a id="18464" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18446" class="Bound">m</a>
<a id="18466" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a>  <a id="18472" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="18474" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="18478" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18478" class="Bound">n</a>  <a id="18481" class="Symbol">=</a>  <a id="18484" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1148" class="InductiveConstructor">zero</a>
<a id="18489" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="18493" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18493" class="Bound">m</a> <a id="18495" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="18497" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#1159" class="InductiveConstructor">suc</a> <a id="18501" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18501" class="Bound">n</a>  <a id="18504" class="Symbol">=</a>  <a id="18507" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18493" class="Bound">m</a> <a id="18509" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="18511" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18501" class="Bound">n</a>{% endraw %}</pre>
We can do a simple analysis to show that all the cases are covered.

  * Consider the second argument.
    + If it is `zero`, then the first equation applies.
    + If it is `suc n`, then consider the first argument.
      - If it is `zero`, then the second equation applies.
      - If it is `suc m`, then the third equation applies.

Again, the recursive definition is well-founded because
monus on bigger numbers is defined in terms of monus on
smaller numbers.

For example, let's subtract two from three:
<pre class="Agda">{% raw %}<a id="19047" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#19047" class="Function">_</a> <a id="19049" class="Symbol">=</a>
  <a id="19053" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4076" class="Function Operator">begin</a>
     <a id="19064" class="Number">3</a> <a id="19066" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="19068" class="Number">2</a>
  <a id="19072" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
     <a id="19081" class="Number">2</a> <a id="19083" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="19085" class="Number">1</a>
  <a id="19089" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
     <a id="19098" class="Number">1</a> <a id="19100" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="19102" class="Number">0</a>
  <a id="19106" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
     <a id="19115" class="Number">1</a>
  <a id="19119" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4374" class="Function Operator">∎</a>{% endraw %}</pre>
We did not use the second equation at all, but it will be required
if we try to subtract a larger number from a smaller one:
<pre class="Agda">{% raw %}<a id="19270" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#19270" class="Function">_</a> <a id="19272" class="Symbol">=</a>
  <a id="19276" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4076" class="Function Operator">begin</a>
     <a id="19287" class="Number">2</a> <a id="19289" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="19291" class="Number">3</a>
  <a id="19295" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
     <a id="19304" class="Number">1</a> <a id="19306" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="19308" class="Number">2</a>
  <a id="19312" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
     <a id="19321" class="Number">0</a> <a id="19323" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Function Operator">∸</a> <a id="19325" class="Number">1</a>
  <a id="19329" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4134" class="Function Operator">≡⟨⟩</a>
     <a id="19338" class="Number">0</a>
  <a id="19342" href="https://agda.github.io/agda-stdlib/v0.17/Relation.Binary.PropositionalEquality.html#4374" class="Function Operator">∎</a>{% endraw %}</pre>

#### Exercise `∸-examples` (recommended) {#monus-examples}

Compute `5 ∸ 3` and `3 ∸ 5`, writing out your reasoning as a chain of equations.

<pre class="Agda">{% raw %}<a id="19511" class="Comment">-- Your code goes here</a>{% endraw %}</pre>


## Precedence

We often use _precedence_ to avoid writing too many parentheses.
Application _binds more tightly than_ (or _has precedence over_) any
operator, and so we may write `suc m + n` to mean `(suc m) + n`.
As another example, we say that multiplication binds more tightly than
addition, and so write `n + m * n` to mean `n + (m * n)`.
We also sometimes say that addition _associates to the left_, and
so write `m + n + p` to mean `(m + n) + p`.

In Agda the precedence and associativity of infix operators
needs to be declared:
<pre class="Agda">{% raw %}<a id="20096" class="Keyword">infixl</a> <a id="20103" class="Number">6</a>  <a id="20106" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Primitive Operator">_+_</a>  <a id="20111" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Primitive Operator">_∸_</a>
<a id="20115" class="Keyword">infixl</a> <a id="20122" class="Number">7</a>  <a id="20125" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Primitive Operator">_*_</a>{% endraw %}</pre>
This states operators `_+_` and `_∸_` have precedence level 6,
and operator `_*_` has precedence level 7.
Addition and monus bind less tightly than multiplication
because they have lower precedence.
Writing `infixl` indicates that all three
operators associate to the left.  One can also write `infixr` to
indicate that an operator associates to the right, or just `infix` to
indicate that parentheses are always required to disambiguate.


## Currying

We have chosen to represent a function of two arguments in terms
of a function of the first argument that returns a function of the
second argument.  This trick goes by the name _currying_.

Agda, like other functional languages such as Haskell and ML,
is designed to make currying easy to use.  Function
arrows associate to the right and application associates to the left

`ℕ → ℕ → ℕ` stands for `ℕ → (ℕ → ℕ)`

and

`_+_ 2 3` stands for `(_+_ 2) 3`.

The term `_+_ 2` by itself stands for the function that adds two to
its argument, hence applying it to three yields five.

Currying is named for Haskell Curry, after whom the programming
language Haskell is also named.  Curry's work dates to the 1930's.
When I first learned about currying, I was told it was misattributed,
since the same idea was previously proposed by Moses Schönfinkel in
the 1920's.  I was told a joke: "It should be called schönfinkeling,
but currying is tastier". Only later did I learn that the explanation
of the misattribution was itself a misattribution.  The idea actually
appears in the _Begriffschrift_ of Gottlob Frege, published in 1879.

## The story of creation, revisited

Just as our inductive definition defines the naturals in terms of the
naturals, so does our recursive definition define addition in terms
of addition.

Again, it is possible to assign our definition a meaning without
resorting to unpermitted circularities.  We do so by reducing our
definition to equivalent inference rules for judgments about equality:

    n : ℕ
    --------------
    zero + n  =  n

    m + n  =  p
    ---------------------
    (suc m) + n  =  suc p

Here we assume we have already defined the infinite set of natural
numbers, specifying the meaning of the judgment `n : ℕ`.  The first
inference rule is the base case.  It asserts that if `n` is a natural number
then adding zero to it gives `n`.  The second inference rule is the inductive
case. It asserts that if adding `m` and `n` gives `p`, then adding `suc m` and
`n` gives `suc p`.

Again we resort to a creation story, where this time we are
concerned with judgments about addition:

    -- In the beginning, we know nothing about addition.

Now, we apply the rules to all the judgment we know about.
The base case tells us that `zero + n = n` for every natural `n`,
so we add all those equations.  The inductive case tells us that if
`m + n = p` (on the day before today) then `suc m + n = suc p`
(today).  We didn't know any equations about addition before today,
so that rule doesn't give us any new equations:

    -- On the first day, we know about addition of 0.
    0 + 0 = 0     0 + 1 = 1    0 + 2 = 2     ...

Then we repeat the process, so on the next day we know about all the
equations from the day before, plus any equations added by the rules.
The base case tells us nothing new, but now the inductive case adds
more equations:

    -- On the second day, we know about addition of 0 and 1.
    0 + 0 = 0     0 + 1 = 1     0 + 2 = 2     0 + 3 = 3     ...
    1 + 0 = 1     1 + 1 = 2     1 + 2 = 3     1 + 3 = 4     ...

And we repeat the process again:

    -- On the third day, we know about addition of 0, 1, and 2.
    0 + 0 = 0     0 + 1 = 1     0 + 2 = 2     0 + 3 = 3     ...
    1 + 0 = 1     1 + 1 = 2     1 + 2 = 3     1 + 3 = 4     ...
    2 + 0 = 2     2 + 1 = 3     2 + 2 = 4     2 + 3 = 5     ...

You've got the hang of it by now:

    -- On the fourth day, we know about addition of 0, 1, 2, and 3.
    0 + 0 = 0     0 + 1 = 1     0 + 2 = 2     0 + 3 = 3     ...
    1 + 0 = 1     1 + 1 = 2     1 + 2 = 3     1 + 3 = 4     ...
    2 + 0 = 2     2 + 1 = 3     2 + 2 = 4     2 + 3 = 5     ...
    3 + 0 = 3     3 + 1 = 4     3 + 2 = 5     3 + 3 = 6     ...

The process continues.  On the _m_'th day we will know all the
equations where the first number is less than _m_.

As we can see, the reasoning that justifies inductive and recursive
definitions is quite similar.  They might be considered two sides of
the same coin.


## The story of creation, finitely {#finite-creation}

The above story was told in a stratified way.  First, we create
the infinite set of naturals.  We take that set as given when
creating instances of addition, so even on day one we have an
infinite set of instances.

Instead, we could choose to create both the naturals and the instances
of addition at the same time. Then on any day there would be only
a finite set of instances:

    -- In the beginning, we know nothing.

Now, we apply the rules to all the judgment we know about.  Only the
base case for naturals applies:

    -- On the first day, we know zero.
    0 : ℕ

Again, we apply all the rules we know.  This gives us a new natural,
and our first equation about addition.

    -- On the second day, we know one and all sums that yield zero.
    0 : ℕ
    1 : ℕ    0 + 0 = 0

Then we repeat the process.  We get one more equation about addition
from the base case, and also get an equation from the inductive case,
applied to equation of the previous day:

    -- On the third day, we know two and all sums that yield one.
    0 : ℕ
    1 : ℕ    0 + 0 = 0
    2 : ℕ    0 + 1 = 1   1 + 0 = 1

You've got the hang of it by now:

    -- On the fourth day, we know three and all sums that yield two.
    0 : ℕ
    1 : ℕ    0 + 0 = 0
    2 : ℕ    0 + 1 = 1   1 + 0 = 1
    3 : ℕ    0 + 2 = 2   1 + 1 = 2    2 + 0 = 2

On the _n_'th day there will be _n_ distinct natural numbers, and
_n × (n-1) / 2_ equations about addition.  The number _n_ and all equations
for addition of numbers less than _n_ first appear by day _n+1_.
This gives an entirely finitist view of infinite sets of data and
equations relating the data.


## Writing definitions interactively

Agda is designed to be used with the Emacs text editor, and the two
in combination provide features that help to create definitions
and proofs interactively.

Begin by typing:

    _+_ : ℕ → ℕ → ℕ
    m + n = ?

The question mark indicates that you would like Agda to help with
filling in that part of the code. If you type `C-c C-l` (pressing
the control key while hitting the `c` key followed by the `l` key)
the question mark will be replaced:

    _+_ : ℕ → ℕ → ℕ
    m + n = { }0

The empty braces are called a *hole*, and 0 is a number used for
referring to the hole.  The hole will display highlighted in green.
Emacs will also create a window displaying the text

    ?0 : ℕ

to indicate that hole 0 is to be filled in with a term of type `ℕ`.
Typing `C-c C-f` will move you into the next hole.

We wish to define addition by recursion on the first argument.
Move the cursor into the hole and type `C-c C-c`.   You will be given
the prompt:

    pattern variables to case (empty for split on result):

Typing `m` will cause a split on that variable, resulting
in an update to the code:

    _+_ : ℕ → ℕ → ℕ
    zero + n = { }0
    suc m + n = { }1

There are now two holes, and the window at the bottom tells you the
required type of each:

    ?0 : ℕ
    ?1 : ℕ

Going into hole 0 and type `C-c C-,` will display information on the
required type of the hole, and what free variables are available:

    Goal: ℕ
    ————————————————————————————————————————————————————————————
    n : ℕ

This strongly suggests filling the hole with `n`.  After the hole is
filled, you can type `C-c C-space`, which will remove the hole:

    _+_ : ℕ → ℕ → ℕ
    zero + n = n
    suc m + n = { }1

Again, going into hole 1 and type `C-c C-,` will display information on the
required type of the hole, and what free variables are available:

    Goal: ℕ
    ————————————————————————————————————————————————————————————
    n : ℕ
    m : ℕ

Going into the hole and type `C-c C-r` will fill it in with a constructor
(if there is a unique choice) or tell you what constructors you might use,
if there is a choice.  In this case, it displays the following:

    Don't know which constructor to introduce of zero or suc

Filling the hole with `suc ?` and typing `C-c C-space` results in the following:

    _+_ : ℕ → ℕ → ℕ
    zero + n = n
    suc m + n = suc { }1

Going into the new hole and typing `C-c C-,` gives similar information to before:

    Goal: ℕ
    ————————————————————————————————————————————————————————————
    n : ℕ
    m : ℕ

We can fill the hole with `m + n` and type `C-c C-space` to complete the program:

    _+_ : ℕ → ℕ → ℕ
    zero + n = n
    suc m + n = suc (m + n)

Exploiting interaction to this degree is probably not helpful for a program this
simple, but the same techniques can help with more complex programs.  Even for
a program this simple, using `C-c C-c` to split cases can be helpful.


## More pragmas

Including the lines
<pre class="Agda">{% raw %}<a id="29272" class="Symbol">{-#</a> <a id="29276" class="Keyword">BUILTIN</a> NATPLUS <a id="29292" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#11305" class="Primitive Operator">_+_</a> <a id="29296" class="Symbol">#-}</a>
<a id="29300" class="Symbol">{-#</a> <a id="29304" class="Keyword">BUILTIN</a> NATTIMES <a id="29321" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#16251" class="Primitive Operator">_*_</a> <a id="29325" class="Symbol">#-}</a>
<a id="29329" class="Symbol">{-#</a> <a id="29333" class="Keyword">BUILTIN</a> NATMINUS <a id="29350" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#18430" class="Primitive Operator">_∸_</a> <a id="29354" class="Symbol">#-}</a>{% endraw %}</pre>
tells Agda that these three operators correspond to the usual ones,
and enables it to perform these computations using the corresponding
Haskell operators on the arbitrary-precision integer type.
Representing naturals with `zero` and `suc` requires time proportional
to _m_ to add _m_ and _n_, whereas representing naturals as integers
in Haskell requires time proportional to the larger of the logarithms
of _m_ and _n_.  Similarly, representing naturals with `zero`
and `suc` requires time proportional to the product of _m_ and _n_ to
multiply _m_ and _n_, whereas representing naturals as integers in
Haskell requires time proportional to the sum of the logarithms of
_m_ and _n_.


#### Exercise `Bin` (stretch) {#Bin}

A more efficient representation of natural numbers uses a binary
rather than a unary system.  We represent a number as a bitstring:
<pre class="Agda">{% raw %}<a id="30239" class="Keyword">data</a> <a id="Bin"></a><a id="30244" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30244" class="Datatype">Bin</a> <a id="30248" class="Symbol">:</a> <a id="30250" class="PrimitiveType">Set</a> <a id="30254" class="Keyword">where</a>
  <a id="Bin.nil"></a><a id="30262" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30262" class="InductiveConstructor">nil</a> <a id="30266" class="Symbol">:</a> <a id="30268" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30244" class="Datatype">Bin</a>
  <a id="Bin.x0_"></a><a id="30274" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30274" class="InductiveConstructor Operator">x0_</a> <a id="30278" class="Symbol">:</a> <a id="30280" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30244" class="Datatype">Bin</a> <a id="30284" class="Symbol">→</a> <a id="30286" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30244" class="Datatype">Bin</a>
  <a id="Bin.x1_"></a><a id="30292" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30292" class="InductiveConstructor Operator">x1_</a> <a id="30296" class="Symbol">:</a> <a id="30298" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30244" class="Datatype">Bin</a> <a id="30302" class="Symbol">→</a> <a id="30304" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Naturals.md %}{% raw %}#30244" class="Datatype">Bin</a>{% endraw %}</pre>
For instance, the bitstring

    1011

standing for the number eleven is encoded, right to left, as

    x1 x1 x0 x1 nil

Representations are not unique due to leading zeros.
Hence, eleven is also represented by `001011`, encoded as:

    x1 x1 x0 x1 x0 x0 nil

Define a function

    inc : Bin → Bin

that converts a bitstring to the bitstring for the next higher
number.  For example, since `1100` encodes twelve, we should have:

    inc (x1 x1 x0 x1 nil) ≡ x0 x0 x1 x1 nil

Confirm that this gives the correct answer for the bitstrings
encoding zero through four.

Using the above, define a pair of functions to convert
between the two representations.

    to   : ℕ → Bin
    from : Bin → ℕ

For the former, choose the bitstring to have no leading zeros if it
represents a positive natural, and represent zero by `x0 nil`.
Confirm that these both give the correct answer for zero through four.

<pre class="Agda">{% raw %}<a id="31232" class="Comment">-- Your code goes here</a>{% endraw %}</pre>


## Standard library

At the end of each chapter, we will show where to find relevant
definitions in the standard library.  The naturals, constructors for
them, and basic operators upon them, are defined in the standard
library module `Data.Nat`:

<pre class="Agda">{% raw %}<a id="31528" class="Comment">-- import Data.Nat using (ℕ; zero; suc; _+_; _*_; _^_; _∸_)</a>{% endraw %}</pre>

Normally, we will show an import as running code, so Agda will
complain if we attempt to import a definition that is not available.
This time, however, we have only shown the import as a comment.  Both
this chapter and the standard library invoke the `NATURAL` pragma, the
former on `ℕ`, and the latter on the equivalent type `Data.Nat.ℕ`.
Such a pragma can only be invoked once, as invoking it twice would
raise confusion as to whether `2` is a value of type `ℕ` or type
`Data.Nat.ℕ`.  Similar confusions arise if other pragmas are invoked
twice. For this reason, we will usually avoid pragmas in future chapters.
Information on pragmas can be found in the Agda documentation.


## Unicode

This chapter uses the following unicode:

    ℕ  U+2115  DOUBLE-STRUCK CAPITAL N (\bN)
    →  U+2192  RIGHTWARDS ARROW (\to, \r, \->)
    ∸  U+2238  DOT MINUS (\.-)
    ≡  U+2261  IDENTICAL TO (\==)
    ⟨  U+27E8  MATHEMATICAL LEFT ANGLE BRACKET (\<)
    ⟩  U+27E9  MATHEMATICAL RIGHT ANGLE BRACKET (\>)
    ∎  U+220E  END OF PROOF (\qed)

Each line consists of the Unicode character (`ℕ`), the corresponding
code point (`U+2115`), the name of the character (`DOUBLE-STRUCK CAPITAL N`),
and the sequence to type into Emacs to generate the character (`\bN`).

The command `\r` gives access to a wide variety of rightward arrows.
After typing `\r`, one can access the many available arrows by using
the left, right, up, and down keys to navigate.  The command remembers
where you navigated to the last time, and starts with the same
character next time.  The command `\l` works similarly for left arrows.

In place of left, right, up, and down keys, one may also use control characters:

    C-b  left (backward one character)
    C-f  right (forward one character)
    C-p  up (to the previous line)
    C-n  down (to the next line)

We write `C-b` to stand for control-b, and similarly.  One can also navigate
left and right by typing the digits that appear in the displayed list.

