  * tags: #best-practices #bdd #article #testing
  * author: [[Codoid.com]]
  * link to article: https://codoid.com/automation-testing/best-practices-for-automation-testing-with-bdd/
  * notes:
    * ## BDD scenario best pracices
      * **Given-when-then** should be in sequence
      * Each scenario ideally should have only 1 **when**, that clearly points to the purpose of the test
      * ### Tenses
        * use past tense for **given**
        * present tense for **when**
        * future tense for **then**
      * ### And
        * to give more **given** or **then** steps = use **and**
      * Put scenarios prerequisite steps in **Background**. Note: If the prerequisite steps are more technical, then use **Before** hook 
      * Scenarios should be more functionality oriented than UI/UX oriented
      * You can also write BDD Style Acceptance Criteria for web services. However you need to ensure it is understood by the product owner
      * ### Using declarative steps rather than imperative
        * **Declarative example**
          * ```javascript
Given I pass the header information for SSN
When the client request the URL with data
Then the response code should be 200```
        * **Imperative example**
          * ```javascript
Given I pass the header information for SSN
When client request POST "<ServiceURL>" with json data "<RequestFile>"
Then the response code should be 200
And the SSNcached result should be same as valid transaction response "<ResponseFile>"```
