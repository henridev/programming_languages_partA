# general

- compiler for quick debugging https://sosml.org/

TABLE OF CONTENTS: Introduction to functional programming

- S1: Functions / recursion / scope / variables / tuples / lists
- S2: Datatypes / pattern-matching / tail recursion
- S3: First-class functions / closures
- S4: Type inference / modules / equivalence

## S1 Functions / recursion / scope / variables / tuples / lists

- ML program = sequence of bindings
- binding = type check + evaluation
- static environment = types of preceding binding in a file
- dynamic environment = types of preceding binding evaluation in a
- syntax = how to write
- semantics = how to type check and evaluate
- **value** = expression with no computation left todo
- immutable bindings = a variable binding will always map to the same value but it can be shadowed later within a different environment

binding types:

- variable bindings
- function bindings
- datatype bindings

### **variable binding**

- syntax `val x = e;`
- semantics:
  1: type check in current static env + create new static env with type T of e
  2: evaluation using current dynamic env + create new dynamic env with **value** V as result of evaluating e

### **function binding**

- syntax `fun x0 (x1: t1, ..., xn: tn) = e;`
- semantics:
  1: type checking - type check body e in current static env - this is where x1 to xn will already be mapped - create new static env with type (arg types -> Type of e) - type of e is found thanks to type inference. - x0 gets added to new static env not the arguments
  2: function is a **value** x0 can be called later and is thus value part of current dynamic env
- function calls
  1. syntax
     - `e0 (e1, ... en)` where e0 of type `t1*...*tn -> t`
  2. evaluation
     - use dynamic env of point of call to evaluate e0 to v0, e1 to v1 ...
     - we have lexical scope so be careful we extend env that was current on definition not on call

### **tuples and lists**

tuple

- syntax: `(e1, ..., en)`
- semantics:
  1: type check in current static env + create new static env with type (t1*t2) of (e1, e2)
  2: evaluation using current dynamic env + create new dynamic env with **value** (v1*v2) as result of evaluating (e1, e2)

list

- syntax: `[e1, ..., en]`
- semantics:
  - type check in current static env + create new static env with type list of t of [e1, e2]
  - evaluation using current dynamic env + create new dynamic env with **value** [v1, v2] as result of evaluating [e1, e2]

### **scope**

syntax: `let 'bindings...' in 'expressions...' end`
let expression = allows for local binding

## S2 Datatypes / pattern-matching / tail recursion

### **datatype binding**


after we saw val and function binding now we see datatype binding

we introduce into our environment

- constructors -> info which tells us which variant of type is used

  - way to create value of new type
  - or actual value of new type

- type for which values can be int or string or nothing

let's say we create a pizza "peperoni" --> we now have a value of type food

now we have created a value of x how do we get values of it for each variant --> if we know the variant we know the data available

**answer is case expressions**

<pre>
<code>datatype Food = Pasta of string
                | Pizza of string
                | Fasting;


fun x Fasting = "no food"
  | x  (Pasta s) = "we are eating pasta "  ^ s
  | x  (Pizza s) = "we are eating pizza "  ^ s;


val meal = Pizza "pepperoni";

x meal; (*output: we are eating pizza pepperoni*)
</code>
</pre>

### **type inference**

it is not necesarry to write arguments on our functions SML has algorithm that can infer argument types


