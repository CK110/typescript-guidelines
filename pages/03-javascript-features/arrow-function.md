# Arrow Function

Arrow function (or fat-arrow function) is one of the favorite features introduced in ES2015.
It provides a compact syntax for writing function.
Most of the time it makes code easier to read.

The most significant difference between arrow function and function declaration and expression is that the `this` value is lexically binded at the declaration site, instead of at call site.

## Anonymous Callback

- use arrow function for callbacks

  > Why? It binds to your lexical context, which is usually what you want. It is also easier to read.
  >
  > Why not? If the callback has its own concept of `this` (usually this indicates a bad design, e.g. `$.each()`) AND you need to access it, then you don't have other choices.
  >
  > If your callback is complicated, move it out to its own function declaration. Large callback makes the code harder to understand since it obstructs the main flow of the code.

  ```ts
  // bad
  [1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
  });

  // good
  [1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
  });
  ```

## Function Expression

- If you want to define a function, use function declaration instead of function expression or arrow function

  > Why? Arrow function has the same hoisting issue as with function expression.
  > When declaring file scoped function, use function declaration to avoid hoisting suprise.
  >
  > Function declaration can be recognized by the langauge service as callable function,
  > so you will get the right hint from your IDE.

  ```ts
  // bad
  const foo = function() { return 'foo' }

  // bad
  const foo = () => 'foo'

  // good
  function foo() { return 'foo' }
  ```

## Higher-order Functions

- If you are defining a higher-order function, you can use arrow-function due its compact form.

  > Why? Although this contradicts with the function expression guideline,
  > higher-order function are typically used as argument or export to be used elsewhere.
  >
  > Therefore, you can justify to use array function syntax for this purpose.

  ```ts
  // ok
  export const high = store => next => action => next(action)
  ```

## Single Expression

- If the function body consists of a single expression, omit the brackets.

  > Why? It reads well especially when multiple functions are chained together.

  ```ts
  // bad
  [1, 2, 3].map(number => {
    return `A string containing the ${number}.`;
  });

  // good
  [1, 2, 3].map(number => `A string containing the ${number}.`);
  ```

## Other Mentions

- <https://stackoverflow.com/questions/22939130/when-should-i-use-arrow-functions-in-ecmascript-6>
