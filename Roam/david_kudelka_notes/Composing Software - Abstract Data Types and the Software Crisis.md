  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Abstract Data Types and the Software Crisis**
      * ### **Glossary**
        * **Axioms** - are mathematically sounds statements which must hold true
        * **Mathematically sound** - means that each term is well defined mathematically so that it's possible to write unambiguous and provable statements of fact based on them
      * An **Abstract Data Type (ADT)** is an abstract concept defined by axioms tat represent some data and operations on that data. It's more about **What to do** than How to do.
      * Examples of ADT
        * List
        * Stack
        * Queue
        * Set
        * Map
        * Stream
      * ADT can express many useful algebraic structures, including semigroups, monoids, functors, monads and etc.
      * **Why ADTs?**
        * It is common language to refer to an extensive vocabulary of useful software building blocks
      * **History of ADTs**
        * It was in general hard to describe concepts across various programming languages and machines, that's why ATDs were invented
      * **Specifications for ADTs**
        * Criteria
          * **Formal** - formal definition
          * **Applicable** - should be applicable to different concrete use cases, not specifying one exact application
          * **Minimal** - short as possible
          * **Extensible** - small change in requirements should be small change in code
          * **Declarative** - should describe **what, not how**
        * Must include
          * **Human Readable Description**
          * **Definitions** - clearly define any terms used in the specification to avoid any ambiguity
          * **Abstract Signatures** - Describe the expected inputs and outputs without linking them to concrete types or data structures
          * **Axioms** - Algebraic definitions of the axiom invariants used to prove that an implementation has satisfied the requirements of the specification
        * Example - [[Composing Software - ADT - example]]
      * ### **Conclusion**
        * An **Abstract Data Type** is an abstract concept defined by axioms which represent some data and operations on that data
        * **Abstract Data Types** are focused **on what, not how**
        * **Abstract Data Types** are here for describing mathematically sounds, precise and unambiguous modules