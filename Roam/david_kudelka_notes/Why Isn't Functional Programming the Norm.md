  * tags: #functional-programming
  * video link: https://www.youtube.com/watch?v=QyJZzq0v7Z4&ab_channel=Metosin
  * notes:
    * To answer why isn't functional programming the norm, we need to answer question **why are the things they are ?**
    * ## Why are the things they are?
      * 3 reasons 
        * Language
        * Paradigm
        * Style
      * ### **Language**
        * There are 0 programming languages that are functional in top 10
        * reasons for that ?
          * **Killer app**
            * there is rails for ruby
            * there is drupal and wordpress for PHP
            * systems programming for C
            * **Potential for FP killer apps**
              * for elm elm-ui
              * for clojure Datomic
              * for ReasonML revery
          * **Platform Exclusivity**
            * **Object C and Swift** - it is build for iOS and for this reason it doesn't matter how good they are
            * **JavaScript** - the same thing, just the platform makes it popular and not really the programming language itself
            * **C#** - Windows exclusivity
          * **Quick upgrade**
            * Benefits
            * Familiarity
            * Learning Curve - (I don't know what category theory is, what is monad ? this is the difficulties we face)
            * Code migrations effort - Typescript - it is basically javascript plus something, it is easy to start
              * You can just take javascript file rename it to .ts and that's it, you can slowly start and making it better slowly
          * If you have a lot of money pumping from companies using the old programming languages it makes a lot of difference, there are tools and so on which makes it easier, big marketing
          * That's how JavaScript became what it is, they make it easy for other developers to transition
          * And that is the reason to think about it, it slowly happens that FP is getting better and slowly people transitioning and that is reason why you should slowly getting familiar and slowly trying to make stuff with it
          * **Other popularity factors**
            * Syntax
            * Job market - we have this big project in object oriented language and you have to work with it
            * Community
      * ## **Paradigm**
        * Programming paradigms are a way to classify programming languages based on their features
        * Language can be classified into multiple paradigms
          * Imperative, object oriented, declarative, FP
        * Are OO languages the norm because of **uniquely OO features**?
          * What are uniquely OO features?
            * Inheritance
              * interface inheritance
              * implementation inheritance
                * it is not considered to be best practice (composition over inheritance), it disfavourite
              * GO language - we support object oriented but there is no inheritance
            * **Modular programming**
              * Modularity lets you define a public interface to hide private implementation details
              * **Encapsulation** is just subset of modularity, it just encapsulates object
          * So the answer to the are OO languages the norm because of **uniquely OO features** and the answer is **NO**
      * ## **Style**
        * Style of functional programming = "Avoid mutation and side effects"
        * No language features are **required**
        * Languages differ in their **support** for this style
        * Why isn't FP **style** the norm?
          * Kotlin has both OO and FP, you can use both
          * Swift included functional programming patterns
          * JavaScript has some support of functional patterns as well
          * And those supports are growing
          * Maybe JavaScript, Swift, Kotlin being hybrid and this is just transition between those 2 styles, but who knows how soon this can happen 
          * Answer why isn't a norm
            * No sufficient large "killer apps"
            * No exclusivity on large platforms
            * Can't be a quick upgrade if substantially different
            * No epic marketing budgets
            * Slow & steady growth takes decades
    * ## **Issues with performance**
      * The main thing to understand is that those things doesn't usually have connection to the programming style
        * C is good because of the low level memory management
      * Then we go to the world of garbage collectors languages, where it really matters about the implementation