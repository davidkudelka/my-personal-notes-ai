  * link: https://blog.palantir.com/code-review-best-practices-19e02780015f
  * ## Notes
    * ### Motivation to do code reviews
      * **Committers are motivated** - the fact that other people will see the code forces people to produce better quality software
      * **Sharing knowledge** - makes people more aware about what is happening and strengthen communication, junior can learn from more senior people
      * **Accidental errors and structural errors** - other people can have more context in how certain things are implemented and point out potential mistakes
    * ### Best practices
      *  **Scope and size** - best max length should be 5 files and should take max 20 minutes to review, if some pr takes more than 1-2 days to complete it should be split into multiple pull requests (with added TODO's)
      * **Purpose** - one pr should have one purpose, do not mix multiple tasks / user stories into one pr if possible
      * **Ask questions** - if something is not clear, ask question so you understand scope and functionality of reviewed pr
    * ### What to look for in implementation?
      * Think about how you would have solved the problem
      * Do you see potential for useful abstractions?
      * Intentionally try to find mistakes in the code
      * Does the code follow standard patterns? (types, libraries)
      * Are you able to understand purpose of this code?