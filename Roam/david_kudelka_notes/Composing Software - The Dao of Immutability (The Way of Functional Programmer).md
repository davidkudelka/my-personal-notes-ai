  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * Notes:
    * # **The Dao of Immutability (The Way of the Functional Programmer)**
      * Immutability is foundation of functional programming and functional programming is foundation of JavaScript, so you can't fully understand JavaScript without knowing what is immutability about
      * 5 rules of functional programming
        * **Immutability** - The true constant is change. Mutation hides change. Hidden change manifests chaos. Therefore, the wise embrace history. (Mutation tends to hide past, if you have 1 dollar and I give you one more, it doesn't change the fact the you just had one dollar)
        * **Separation** - Logic is thought. Effects are action. Therefore the wise think before acting, and act only when the thinking is done. (good separation leads to easily manageable code)
        * **[[Composition]]** - All things in the nature work in harmony. A tree cannot grow without water. A bird cannot fly without air. Therefore the wise mix ingredients together to make their soup taste better. (Writing type specific functions is not effective, they should be flexible, you can always lift functions if you need different data-type, do not create new tool for every use case, but try to reuse as much code as possible)
        * **Flow** - Still waters are unsafe to drink. Food left alone will rot. The wise prosper because they let things flow (do not share state of something inside the functions)
        * **Wisdom** - The wise programmer understands the way before walking the path. Therefore the wise programmer is functional, while the unwise get lost in the jungle