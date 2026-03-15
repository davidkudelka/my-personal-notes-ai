  * ADT example of stack
  * ## **Definitions**
    * a: Any type
    * b: Any type
    * item: Any type
    * stack(): an empty stack
    * stack(a): a stack of a
    * [item, stack]: a pair of item and stack
  * ## **Construction**
    * The stack operation takes any number of items and returns a stack of those items. Typically, the abstract signature for a constructor is defined in terms of itself. Please don't confuse this with a recursive function
      * stack(...items) => stack(...items)
  * ## **Axioms**
    * The stack axioms deal primarily with stack and item identity, the sequence of the stack items, and the behaviour of pop when the stack is empty
    * ### **Identity**
      * Pushing and popping have no side-effects. If you push to a stack and immediately pop from the same stack, the stack should be in the state it was before you pushed
        * pop(push(a, stack())) = [a, stack()]
        * **Given**: push a to the stack and immediately pop from the stack
        * **Should**: return a pair of 'a' and 'stack()'
    * ### **Sequence**
      * Popping from the stack should respect the sequence: Last In, First Out (LIFO)
        * pop(push(b, push(a, stack()))) = [b, stack(a)]
        * **Given**: push 'a' to the stack, then push b to the stack, the pop from the stack
        * **Should**: return a pair of 'b' and 'stack(a)'
    * ### **Empty**
      * Popping from an empty stack results in an undefined item value. In concrete terms, this could be defined with a Maybe(item), Nothing, or Either. In JavaScript, it's customary to use undefined. Popping from an empty stack should not change the stack
        * pop(stack()) = [undefind, stack()]
        * **Given**: pop from an empty stack
        * **Should**: return a pair of undefined and stack()
  * **Concrete Implementations**
    * ```javascript
const stack = (...elements) => [...elements];

const push = (a, stack) => stack.concat([a]);

const pop = stack => {
  const newStack = stack.slice(0);
  const item = newStack.pop();
  
  return [item, newStack];
} ```
    * Test to ensure we are satisfying all conditions
    * ```javascript

const assert = ({given, should, actual, expected}) => {
  const stringify = value => Array.isArray(value) ? 
        `[${ value.map(stringify).join(',') }]` :
  		`${ value }`;
  
  const actualString = stringify(actual);
  const expectedString = stringify(expected);
  
  if (actualString === expectedString) {
    console.log(`OK:
		given: ${ given }
		should: ${ should }
		actual: ${ actualString }
		expected: ${ expectedString }
	`);
  } else {
    throw new Error(`NOT OK:
		given: ${ given }
		should: ${ should }
		actual: ${ actualString }
		expected: ${ expectedString }
	`);
  }
};

// Concrete values to pass to the functions
const a = 'a';
const b = 'b';

// Proofs
assert({
  given: 'push `a` to the stack and immediately pop from the stack',
  should: 'return a pair of `a` and `stack()`',
  actual: pop(push(a, stack())),
  expected: [a. stacl()]
})

assert({
  given: 'push `a` tp tje stack, then push `b` to the stack, 
  	then pop from the stack',
  should: 'return a pair of `b` and `stack(a)`'
  actual: pop(push(b, push(a, stack()))),
  expected: [b, stack(a)]
})

assert({
  given: 'pop from an empty stack',
  should: 'return a pair of undefined, stack()',
  actual: pop(stack()),
  expected: [undefined, stack()]
})```
