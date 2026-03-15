  * tags: #testing #bdd #article
  * author: [[Andy Knight]]
  * link to article: https://techbeacon.com/app-dev-testing/better-behavior-driven-development-4-rules-writing-good-gherkin
  * notes:
    * In the very center of BDD is Gherkin, the language that we use to describe the scenarios
    * People of then make mistakes in writing those tests scenarios, either too much detail or too ambiquios scenarios
    * ### 1. Gherkin Golden Rule
      *  Make sure all your scenarios is as declarative and descriptive as possible, but at the same time you want to be describing behaviour, not specific steps
        * **Example with too little detail**
          * ```javascript
Scenario: Shoes
  Given I want shoes
  When I buy shoes
  Then I get them```
        * **Example with too much detail, describing steps rather than actions**
          * ```javascript
Scenario: Purchase shoes through the app
  Given my username is "jessica8494"
  And my password is "PleaseDontPutSecretsInGherkin"
  When I navigate the browser to "www.shoestore.com"
  And I enter my username into the "Username" field
  And I enter my password into the "Password" field
  And I click the login button
  And I wait "10" seconds
  Then the Shoe Store home page is displayed
  And the title banner contains the text "Shoe Store"
  And the shopping cart is empty
  When I click the search bar
  And I type "red pumps" into the search bar
  And I click the search button
  And I wait "30" seconds
  Then the search results page is displayed
  And the search results page shows "10" results per page
  And ...```
        * **The good scenario**
          * ```javascript
Scenario: Add shoes to the shopping cart
  Given the shoe store home page is displayed
  When the shopper searches for "red pumps"
  And the shopper adds the first result to the cart
  Then the cart has one pair of "red pumps"```
      * **Rule** -> always ask yourself, what kind of scenario would you like to read?
    * ### The cardinal rule of BDD
      * one-to-one rule: One scenario should cover exactly one single independent behaviour
      * Focusing on one behaviour has several benefits
        * **Collaboration** - more focus and less confusion
        * **Automation** - each test failure points to a unique problem
        * **Efficiency** - less complex work makes for faster cycle times
        * **Traceability** - 1 behaviour -> 1 example -> 1 scenario -> 1 test -> 1 result
        * **Accountability** - teams cannot hide or avoid behaviours
      * Example
        * ```javascript
Scenario: Simple product search
  Given the shoe store home page is displayed
  When the search phrase "red pumps" is entered
  Then results for "red pumps" are shown
  When the user searches for images from the results page
  Then image results for "red pumps" are shown```
        * It's easy to spot that it covers 2 scenarios. **How?** -> usually when there is more than 1x When->Then combination it covers more than one behavior, in this case searching for shoes and searching for images
        * Luckily it's easy to split
          * ```javascript
Scenario: Simple Web search
  Given the shoe store home page is displayed
  When the search phrase "red pumps" is entered
  Then results for "red pumps" are shown

Scenario: Simple Web image search
  Given shoe store search results for "red pumps" are displayed
  When the user searches for images from the results page
  Then image results for "red pumps" are shown```
    * ### The Unique example rule
      * Sometimes testing less is better than testing more
      * It's ok to test only unique use cases
      * Example
        * ```javascript
Scenario Outline: Simple product search
  Given the shoe store home page is displayed
  When the search phrase "<phrase>" is entered
  Then results for "<phrase>" are shown
 
  Examples: Shoes
    | phrase        |
    | red pumps     |
    | sneakers      |
    | sandals       |
    | flip flops    |
    | flats         |
    | slippers      |
    | running shoes |```
        * In this example the test will run for all of those types of shoes and it seems to be using the same logic, so maybe testing only one type would be enough
    * ### The Good grammar rule
      * Its important to proof-read after yourself
        * Use good words, make sure you choose from which perspective you are talking about the user -> either "I am the shoes store" or "user at the shoe store". It seems to be much better to use 3rd person perspective
      * Use subject-predicate phrases
        * ```javascript
  And image links for "sneakers"
  And video links for "sneakers"```
          * It's hard to understand what exactly is happening here
        * ```javascript
  And the results page shows image links for "sneakers"
  And the results page shows video links for "sneakers"```
          * Here it's obvious what are you trying to test
      * Using past, present, future tense correctly
        * **Given steps** - should use past or present-perfect tense, because they represent an initial state that must already be established
        * **When steps** - should use present tense, because they represent what should happen after the behaviour actions
        * **Then steps** - should use present or future tense, because they represent what should happen after the behaviour actions