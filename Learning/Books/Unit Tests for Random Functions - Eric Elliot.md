  * tags: #engineering #articles #[[Unit Tests]] 
  * Author: [[Eric Elliot]]
  * Rating: 
  * Finished: [[2020-10-13]]
  * Notes:
    * **How to test functions that have random output ?**
      * Imagine program that lets you bundle your tweets, set start date and end date and it will randomly post the tweets during this period
      * **How to test such function ?**
        * Even tho you don't know exact outputs, you can still test constraints
        * You can generate a lot of records, lets say 100 and test if all of them much criteria you defined and that are >= startDate and <= endDate
      * **First make the tests fail**
        * This is really important, because you are ensuring that tests you wrote can fail as well
        * "If you haven't seen a test fail, you don't know if the test works" - [[Eric Elliot]] #quote
      * [[TDD]] acts like a double entry accounting ledger. For every change, you have two records of the change, in the code and in your tests