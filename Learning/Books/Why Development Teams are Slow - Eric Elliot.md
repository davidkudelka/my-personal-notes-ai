  * tags: #engineering #articles
  * Author: [[Eric Elliot]]
  * Rating:
  * Finished: [[2020-09-30]]
  * Notes:
    * List of causes why development teams are slow
      * **Unrealistic Expectations**
        * In general it is very hard to measure how fast certain things can be completed
        * Different developers have different productivity on certain things
      * **Predictive burndown charts**
        * Those are very bad if we are trying to predict deadline or launch based on past performance of completing tickets
        * Instead of predicting future we can use this graph for seeing if something is going wrong with project (more tasks than week before and etc... , by the end of the project tickets are growing instead of shrinking)
        * "When a measure becomes a target, it ceases to be a good measure"
        * If a prediction tells you you can do something by some date, don't believe it.
        * If a prediction tells you that you can't do something by some date, believe it.
      * **Closed Tickets by Developer**
        * Closed tickets that each developer completed is very misleading metric, because the value of the tickets doesn't match
        * If you complete a lot of small tickets, doesn't mean you created bigger value than one developer which delivered big feature
      * **Too Many Open Issues**
        * Try to reduce the number of open issues, it reduces noise in the list. Don't put there something you are not planning to start with soon
      * **Unmanageable Task Size**
        * Good approach is to assign developers to tasks and let them break up big features into tasks that can be delivered in a day
        * This way they can learn how to break up difficult tasks into smaller separate and testable chunks
        * You can use feature toggle system to not break production
      * **Code Review Pile Up**
        * By keeping PR's small and staying on top of them, we can significantly reduce rework caused by code churn and integration conflicts
      * **Poor Training**
        * Code Review - developers learn a great deal from looking at each others code
        * Pair senior engineers with junior developers
        * Dedicated time to mentorship sessions
      * **Developer burnout**
        * Almost every time, the reason of developer burnout is poor management
        * How to avoid burnout
          * Prioritise better and cut scope
          * Use a more productive process (e.g., implement better bug control measures)
          * Identify and refactor sources of churn in the code
      * **Poor Employee Retention**
        * It's expensive to hire new developers, because you have to spend a lot time and resources and then it even takes time for that developer to start being productive
        * It's big problem in tech, 60% of developers changed job in less than 2 years
        * How to avoid loosing employees
          * Pay fairly
          * Offer regular salary raises
          * Offer generous vacation time
          * Offer remote work
          * Keep your expectations realistic
          * Provide work that aligns well with the engineers interests
          * Don't let your tech stack fall to far behind
          * Provide excellent training and professional development opportunities
          * Provide excellent health benefits
          * Don't ask developers to work more than 40 hours/week
          * Provide current equipment
      * **Bugs**
        * If you think you don't have time to implement a high-quality software development process, you really don't have time to skip it
        * Bug prevention is much more efficient than fixing bugs in the production
        * How you can prevent bugs:
          * Practice deign review
          * Good code reviews
          * Use TDD - [[Test Driven Development]]
          * Use [[Roam/david_kudelka_notes/CI/CD|CI/CD]]
          * Improve test coverage
  * Summary:
    * **Unrealistic expectations**
      * In general it is hard to measure complexity of the tasks
      * We can do that with these 2 charts
        * **Predictive burndown charts**
          * Chart that tries to predict how fast we can finish up project based on past experience
          * This chart is in general wrong approach, because it is not reliable source at all
          * It can serve you well as indication something can go wrong
          * If a prediction tells you you can do something by some date, don't believe it
          * If a prediction tells you that you can't do something by some date, believe it
        * **Closed Tickets by Developer**
          * Again wrong metric, because sometimes one task can mean bigger value and time complexity that multiple small ones
      * **Too Many Open Issues**
        * Try to keep your issue list clean, so you reduce noice in the list
      * **Unmanageable Task Size**
        * Separate tickets into small tickets which can be delivered on daily basis, separate testable chunks of big feature
      * **Code Review Pile Up**
        * Chunking features into small tasks leads to small pr and that means things get merged faster without any extra work with rebasing and etc.
      * **Poor Training**
        * Be focused on training your employees, mentorship, pair programming, code reviews, dedicated mentorship
      * **Developer Burnout**
        * Try to reduce developer burnout by being fair with your employees and treat them with good planning
      * **Poor Employee Retention**
        * Companies a lot of times loosing a lot of employees, because they do not offer some pay raise plan and all other perks, more info in notes
      * **Bugs**
        * Prevention of bugs is much more efficient than fixing bugs in production
        * Have good CI/CD
        * Good Code Reviews
        * Improve Test Coverage
        * You can use TDD - [[Test Driven Development]]
  * Action Points:
    * [ ] Check out
      * Practice design review. The combination of design and code inspection can catch 70% of software defects. [“Measuring Defect Potentials and Defect Removal Efficiency”](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.170.4926&rep=rep1&type=pdf), (Caspers Jones, 2008)