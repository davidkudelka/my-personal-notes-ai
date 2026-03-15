  * tags: #css #css-in-js
  * link to article: https://cord.com/blog/migrating-from-css-in-js-to-vanilla-extract
  * author: [[Alberto Morabito]] & [[Ludo Fardel]]
  * notes:
    * Cord is company providing some chat UI components, maybe as well chat functionality of those compoennt
    * ### Goal of the article
      * **Make every piece of Cord UI customasible via plain old CSS**
      * **Create the best developer experience possible**
      * **Re-write out CSS without causing self-inflicted problems in the future**
      * **Move away from JSS to boost performance**
    * ## Issue of CSS-in-JS
      * They are generating custom unique styles for every single piece of a component
      * DOM is very polluted with those 
        * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/allhB51TrJ.png]]
    * ## Decision to use vanilla-extract lib
      * They decided to use - vanilla-extract library
        * So they can still use variables and typescript to write css and have some type-safety there
        * So they can have 0-runtime css
      * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/MHPyD44dFy.png]]
        * Here with usage of globalSyle instead of normal style, they are able to achieve fully custom names of the classes
    * ## Performance boost of moving away from JSS
      * On a page with 173 Cord threads, it took almost 7 seconds to load hundreds of thousands of JSS dynamic styles 
        * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/9Fsx7CFXFs.png]]
      * Switching to vanilla-extract, it reduced this time to basically 0
        * Vanilla Extract’s cost is not tied to how many components are on the page. Whether you have one or one thousand threads on the page doesn’t make a difference at all. Instead, the cost is tied to how many styles we have (i.e. how big Cord’s stylesheet gets)
        * Parsing of newly created css sheet with vanilla-extract, costs about 45ms
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/lSwMXsJCXa.png]]