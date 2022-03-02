# Types & Values

## Top Types: any & unknown
- `unknown` must define a type guard before you can use it
- `any` does not require a type guard at any point

## Bottom Types: never
- useful for `Exhaustive conditionals`

## Type Guards & Narrowing
- built in typeguards, e.g `typeof`, `instanceof`, `in` etc.
- user-defined typeguards:
  ```
  interface CarLike {
    make: string
    model: string
  }

  let maybeCar: unknown

  function isCarLike(valueToTest: any): valueToTest is CarLike {
    return (
    valueToTest && 
    typeofValueToTest === 'object' && 
    "make" in valueTestTest
    // && ...etc
    )
  }

  if (isCarLike(maybeCar)) {
    maybeCar // CarLike
  }

- assertions:
  ```
    // the guard
    function assertsIsCarLike(valueToTest: any): asserts valueToTest is CarLike {
      if (!(
      valueToTest && 
      typeofValueToTest === 'object' && 
      "make" in valueTestTest
      // && ...etc
      )) throw new Error('Value is not car like')
    }

    // using the guard
    maybeCar // unknown

    assertsIsCarLike(maybeCar)
    maybeCar // CarLike

## Nullish Values
- `null`
  - there is a value, and that value is nothing
  - a presence, rather than an absence, of information
- `undefined`
  - the value isn't available (yet?)
- `void`
  - should be exclusively used to describe that a function's return value should be ignored
- Non-null assertion operator:
  - `!` is used to cast away the possibility that a value might be `null` or `undefined`
  - best to limit use of this in app or library code; useful in testing