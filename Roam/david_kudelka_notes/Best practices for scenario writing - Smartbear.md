  * tags: #article #testing #scenarios #bdd #best-practices
  * author: [[Smartbear.com]]
  * link to article: https://support.smartbear.com/cucumberstudio/docs/tests/best-practices.html
  * notes:
    * ## Testing process
      * ### Write test scenarios at early stages
        * If you will start writing test scenarios before you start coding, it helps you figure out the main structure and main bottle-necks, as well understand the feature better
      * ### Don't write in isolation, work as a team
        * If product-owner or business analyst write the tests, they can be rarely automated without adjustments
        * At the same time if engineers or QA are the only ones writing the scenarios they can be full of unnecessary details and shift away from the main functionality
        * Find a way how to get feedback on those
      * ### Don't test several rules at a time
        * Good scenario should be clear as much as possible
        * Usually good rule of thumb is that good scenario has only one pair of **When-Then**, if you have more of them it signalises you are testing too many things
        * Another good way how to test this is to show someone else (who don't know the functionality) the scenario, if it make sense to them - good, if it doesn't you should probably improve it
      * ### Use a reasonable number of scenarios in a feature file
        * If there are too many of them, think of splitting them into sub-features, or lower level tests
      * ### Remove unneeded scenarios
        * You usually start some feature with simple scenario
          * ```javascript
Given the user is logged in
And their bank account is empty
When the user checks the balance
Then the balance should be zero```
        * But as time progresses maybe this one would be covered by other scenarios as well, don't be afraid to remove this one
    * ## Scenario content
      * ### Describe the core and avoid insufficient details
        * we will show you 2 examples
          * ```javascript
Given I sign up as "JohnSmith"
And my password is "password"
And my password confirmation is "password"
And I have deposited "$60" in my account
And I have deposited "$40" in my account
When I check my bank balance
Then my bank balance is "$100"```
          * But purpose of this test is to check the balance, not sign up with a password
        * improved version
          * ```javascript
Given a user signed up as "JohnSmith"
And has deposited "$60" in their account
And has deposited "$40" in their account
When that user checks their bank balance
Then the balance should be "$100"```
      * ### Avoid creating too high-level scenarios
        * Example
          * ```javascript
Given I have an account
When I withdraw some money
Then the balance should be the original balance minus the amount withdrawn```
        * This scenario doesn't talk abot how much user withdraw or what should be the balance, it's therefore too abstract and hard to understand
      * ### Don't write procedure-driven scenarios
        * Do not write scenarios the same way you test UI components
        * If UI changes, you will most likely have to update scenario tests as well
      * ### Use a reasonable number of steps in a scenario
        * good rule of thumb is 2-3 **And's** for each **Given, When or Then**
      * ### Avoid "I" in steps definition
        * There are 2 ways how to write scenarios, first-person and third-person
          * First of all - don't combine both in one scenario
          * Second of all - third-person is better as it better describes who the user is
      * ### Use meaningful scenario titles and descriptions
        * Try to think about as living documentation, it should rather describe business behaviour than user steps
          * **Examples of bad ones**
            * Sign Up, open the Balance Screen, check balance, log off
          * **Examples of good ones**
            * Check balance when it is positive
            * Check balance when an overdraft is on
      * ### Reuse step definitions, when possible
        * Something like **Given the user is logged in** is good example, it makes your tests
          * Easy to maintain when changes happens
          * Simplify automation
      * ### Use Given, When and Then clearly
        * They exist so people can write scenarios that are logically structured
        * Think of them as
          * **Given** - something that happened in the **past**
          * **When** - something happening in **present**
          * **Then** - something that will happen in **future**
