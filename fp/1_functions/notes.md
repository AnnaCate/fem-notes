# Function Purity

## What is a function?

The  `function` keyword does not make something a function; sometimes it just defines a "procedure".

A true function:
- takes input(s) (absence of an input still counts as input)
- does something with the input
- can only call other functions; if it calls a procedure, it becomes a procedure
- returns output(s) (`undefined` is a valid output, as long as the relationship with the input exists)
- the input and the output are related to each other
- name of the function describes the semantic relationship b/t input and output

Example of a function from grade school math: `f(x) = 2x^2 + 3` draws a parabola

## Side Effects

Definition:
- I/O (console, files, etc)
- database storage
- network calls
- DOM
- timestamps
- random numbers
- accessing anything out of the function
- mutating anything outside of the function
- CPU heat!
- CPU time delay!

We want to avoid side effects -- they invalidate the idea of functions
- prevents provability
- use function calls to avoid side effects

It is not practically or theoretically possible to avoid all side effects. So in actuality, we want to _minimize_ side effects, and make them obvious when we do them.

Bugs are more likely to be in side effects, rather than function.

## Pure Functions

- Meets criteria for function
- No side effects

No such thing as a pure function, only a pure function call.

Best practice: make it obvious to the reader when something will behave as a constant.

Pure function calls:
```
function addAnother(z) {
  return function addTwo(x, y) {
    return x + y + z;
  };
}

addAnother(1)(20,21); // 42
```

## Same Input, Same Output

How sure would you be that this function would always return the same output?:
```
function getId(obj) {
  return obj.id;
}
```
What if you then found out the following:
```
getId({
  get id() {
    return Math.random();
  }
});
```

Pure function calls act in isolation: given the same input, they always return the same output.

## Levels of Confidence

Function Purity is a level of confidence.

## Extracting Impurity

Impure function:
```
function addComment(userID, comment) {
  var record = {
    id: uniqueID(),
    userID,
    text: comment
  };
  var elem = buildCommentElement(record);
  commentsList.appendChild(elem)
}
```

Turn it into this better function:
```
function newComment(userID, commentID, comment) {
  var record = {
    id: commentID,
    userID,
    text: comment
  };
  return buildCommentElement(record);
}

var commentID = uniqueID();
var elem = newComment(42, commentID, "This is my comment")'
commentsList.appendChild(elem)
```

## Containing Impurity

Contain side effects to a local scope by wrapping a function, and making a local copy of a global item within the wrapper function. Then you can mutate the local copy.

# Argument Adapters

## Arguments

Argument is the value that gets passed in when you call the function.

Versus the parameter is the placeholder for the argument.

"shape of functions":
- unary function takes 1 argument, returns 1 output (preferred)
- binary function takes 2 arguments, returns 1 output
- "n"ary functions takes n arguments

## Arguments Shape Adapters

Higher Order Functions:
- a function that either receives 1+ functions, and/or returns 1+ functions
- used to force functions passed in to be the shape you need

## Flip & Reverse Adapter

Flip:
- Transpose the first 2 arguments.

Reverse:
- Transposes all the arguments
- not a common adapter

## Spread Adapter

```
function spreadArgs(fn) {
  return function spread(args) {
    return fn(...args);
  };
}

function f(x, y, z, w) {
  return x + y + z + w;
}

var g = spreadArgs(f);

g([1,2,3,4]); // 10
```

Same as `.apply()`

# Point Free

## Equational Reasoning

## Point-Free Refactor

Functions with compatible shapes can be called using "equational reasoning".

```
function not(fn) {
  return function negated(...args) {
    return !fn(...args);
  }
}

function isShortEnough(str) {
  return str.lenght <=5;
}

const isLongEnough = not(isShortEnough)

```

### Advanced Point-Free