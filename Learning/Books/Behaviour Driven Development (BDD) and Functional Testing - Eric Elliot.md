  * tags: #engineering #articles #bdd #[[functional testing]] 
  * Author: [[Eric Elliot]]
  * Rating: 
  * Finished: [[2020-10-08]]
  * Notes:
    * **What is Behaviour Driven Development?**
      * It is branch of [[Test Driven Development]]
      * You write human readable tests in english, those should describe functionality and not implementation details (because implementation details might likely change in the future)
      * It is called black box tests (you do not care about implementation details), white box tests on the other care about implementation details
      * You can use Cucumber software for BDD
    * BDD is good for communication with stakeholders but it gets very difficult if you wanna create from it test scenarios that covers well the whole functionality of application
    * These **3 types of tests** does it much better
      * **Unit tests** - can test local client state is updated correctly and presented correctly in the client view
      * **Functional tests** - can test UI interactions and ensure that user requirements are met at the UI layer. This also ensures that UI elements are wired up appropriately
      * **Integration tests** - can test the API communications happen appropriately and that the user wallet amounts were actually updated correctly on the blockchain
    * Stakeholder usually do not care about those low level UI components and etc. so it is useless to translate everything to BDD
    * But there are as well **advantages of BDD**
      * The formation of a **shared vocabulary** that engineers and stakeholders can use to communicate effectively about the user needs and software solutions
      * The creation of **user stories** and scenarios that help formulate acceptance criteria and a definition of done  for a particular feature of the software
      * The practice of **collaboration** between users, the quality team, product team, and engineers to reach consensus on what the team is building\
    * **What is Functional Testing?**
      * "Functional tests are written from the user's perspective and focus on system behaviour that users are interested in." - IBM
      * They are not E2E or UI testing because they are not focusing on implementation details, but on the core functionality, e.g. I am able to login
      * Functional test is for testing the units in integration with rest of the app
    * **Unit Tests vs Functional Tests**
      * **Advantages of Unit tests**
        * **Unit tests run very fast** - they are not dependent on I/O and etc, they complete in milliseconds
        * **Units must be modular** - it must be easy to test them in isolation
      * **Functional tests**
        * **Take longer to run** - because they integrate various parts of application, they run minutes or hours
        * **Ensure that the units work together as a whole system** - it's important to ensure that different units communicate together well
      * "Functional tests help us build the right product. (Validation). Unit tests help us build the product right. (Verification)"
    * **How to Write Functional Tests for Web Applications**
      * Three is new good engine for writing functional tests and it is TestCafe
    * **Dos and Don't of Functional Tests**
      * **Don't alter the DOM** - it might cause problems
      * **Don't share mutable state between tests** - they should not manipulate the same user data
      * **Don't mix functional tests in with units tests** - they should run at the different moments and they should be written for different purposes
      * **Do run tests in headless mode** - it helps you speed up your functional tests
      * **Do run tests on multiple devices**
      * **Do grab screenshots on test failures** - it can be useful for development team
      * **Do keep your functional test runs under 10 minutes**
      * **Do halt the continuous delivery pipeline when tests fail**