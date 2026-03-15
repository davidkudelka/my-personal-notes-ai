  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **The Forgotten History of OOP**
      * The essential ingredients of **OOP** are ( by [[Alan Kay]])
        * Message passing
        * Encapsulation
        * Dynamic binding
      * ## **The Essence of OOP**
        * The combination of message passing and encapsulation serve some important purposes
          * **Encapsulating state** - by isolating other objects from local state changes. The only way to affect another object's state is to ask (not command) that object to change it by sending a message. State changes are controlled at a local, cellular level rather than exposed to shared access
          * **Decoupling objects from each other** - the message sender is only loosely coupled to the message receiver, through the messaging API
          * **Runtime adaptability** - via late binding. Runtime adaptability provides many great benefits that [[Alan Kay]] considered essential to OOP
      * ## **What OOP Doesn't Mean**
        * ### **What is non-essential?**
          * Classes
          * Class inheritance
          * Special treatment for objects/functions/data
          * The new keyword
          * Polymorphism
          * Static Types
          * Recognizing a class as a "type"
        * Today what we call object is actually composite data type, with none of the implications from either class-based programming or Alan Kay's message-passing