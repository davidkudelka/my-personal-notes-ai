  * tags: #engineering #articles #[[Unit Tests]] 
  * Author: [[Eric Elliot]]
  * Rating: 
  * Finished: [[2020-10-19]]
  * Notes:
    * 5 questions that every unit tests must answer
      * What is the unit under test (module, function, class, whatever)?
      * What should it do? (Prose description)
      * What was the actual output?
      * What was the expected output?
      * How do you reproduce the failure?
    * The problem with most test frameworks is that they are so busy making it easy for you to take shortcuts with their "convenient" assertions that they forget that the biggest value of a test is realised when test fails.
    * **RITE** testing principles
      * R - readable
      * I - Isolated - (for unit tests) or Integrated (for functional and integration tests, test should be isolated and components/modules should be integrated)
      * T - Thorough
      * E - Explicit
    * **Example of good RITE test**
      * ```javascript
describe('sum()', async assert => {
  assert({
    given: 'no arguments',
    should: 'return 0',
    actual: sum(),
    expected: 0
  });
});```
      * We can answer all 5 questions listed above
    * **riteway** - library for testing
  * Action Points:
    * [ ] Look into riteway testing library