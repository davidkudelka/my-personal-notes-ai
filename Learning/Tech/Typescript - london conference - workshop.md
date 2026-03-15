  * tags: #typescript #workshop #react-advanced 
  * date: [[2023-10-19]]
  * notes:
    * ### Function overloading
      * could be useful for hiding internal types
    * Exercise number 1
      * ```javascript
/**
 * concatMessages currently accepts 0..n arguments.
 * Change the signature, so that it requires at least one argument!
 */
function concatMessages(...messages: [string, ...string[]]) {
  return messages.join(", ");
}

// Correct invocations
concatMessages("Hello");
concatMessages("Hello", "World");

// These lines should all trigger compile errors:
concatMessages(); // Make sure this errors! at least one string is required
concatMessages("Hello", 42);
concatMessages(1, 2, 3);
```
      * Using tuple it is possible 
    * Type assertion -> https://ts191023.surge.sh/#89
