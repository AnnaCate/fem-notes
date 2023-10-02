## Closure

- when a fn remembers the vars around it even when that fn is executed elsewhere
- is not necessarily pure

### Closure Exercise

### Closure Solution

## Lazy vs Eager Execution

Lazy:
```
function repeater(count) {
  return function allTheAs(){
    return "".padStart(count, "A")'
  };
}

var A = repeater(10);

A(); // "AAAAAAAAAA"
A(); // "AAAAAAAAAA"
```
Downside: do work every time you call.
Do it when you don't know if A will be called or not.

Eager:
```
function repeater(count) {
  var str = "".padStart(count, "A")'
  return function allTheAs(){
    return str:
  };
}

var A = repeater(10);

A(); // "AAAAAAAAAA"
A(); // "AAAAAAAAAA"
```
Benefit: only do the work once.
Do it if you know it will be called a bunch of times.

## Memoization
Happy medium between lazy and eager. Do the work once, but only when asked for.

```
function repeater(count) {
  var str;
  return function allTheAs(){
    if (str === undefined) {
      str = "".padStart(count, "A")'
    }
    return str;
  };
}

var A = repeater(10);

A(); // "AAAAAAAAAA" <-- work is only done here
A(); // "AAAAAAAAAA"
```

Built-in utility to memoize your functions:
```
function repeater(count) {
  return memoize(function allTheAs(){
    return "".padStart(count, "A")'
  });
}

var A = repeater(10);

A(); // "AAAAAAAAAA" <-- work is only done here
A(); // "AAAAAAAAAA"
```

## Referential Transparency

## Generalized to Specialized

## Partial Application Currying

## Partial Application & Currying Comparison

## Changing Function Shape with Curry