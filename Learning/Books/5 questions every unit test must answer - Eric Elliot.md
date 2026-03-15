  * tags: #engineering #[[Unit Tests]] #testing
  * Author: [[Eric Elliot]]
  * Rating:
  * Finished: [[2020-10-20]]
  * Notes:
    * **Why Bother with Test Discipline?**
      * **Design Aid** - Writing tests first gives you a clearer perspective on the ideal API design
      * **Feature Documentation (for developers)** - Test descriptions enshrine in code every implemented feature requirement
      * **Test your developer understanding** - Does the developer understand the problem enough to articulate in code all critical component requirements?
      * **Quality Assurance** - Manual QA is error prone. In my experience, it's impossible for a developer to remember all features that need testing  after making a change to refactor, add new features, or remove features.
      * **Continuous Delivery Aid** - Automated QA affords the opportunity to automatically prevent broken builds from being deployed to production
    * [[TDD]]
      * TDD can reduce bug density
      * TDD can encourage more modular designs (enhancing software agility/team velocity)
      * TDD can reduce code complexity
    * Write tests first
    * **What's in a Good Unit Test?**
      * Unit test as a bug report
        * A failing test should read like a high-quality bug report
      * What's in a good test failure report ?
        * What were you testing ?
          * What component aspect are you testing ?
            * Example -> 'Compose function output type'  and you are testing what output type compose function can give you
        * What should it do ?
          * What should the feature do ?
            * Example -> 'compose() should return a function'
        * What was the output (actual behaviour)?
          * The best way how to test is to use just **equal()**, because it answers those 2 important questions (What is the actual output and what is the expected output)
        * What was the expected output  (expected behaviour)?
      * **Equal is your new default assertion. It is the staple of every good test suite.**
    * Next time you write a test, remember to answer all the questions
      * What are you testing ?
      * What should it do ?
      * What is the actual output ?
      * What is the expected output ?
      * Wow can the test be reproduced ?
  * Summary:
  * Action Points: