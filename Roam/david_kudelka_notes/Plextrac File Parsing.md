  * Todo's
    * [x] Research the json structure
    * [x] Create new structure
    * {[x]}} Implement unzipper
    * {[x]}} Access files after unzipping
    * {[x]}} Parse content of the file
    * {[x]}} Adjust category import based on actions
    * {[x]}} Import into db
    * ==Nice to have==
      * [ ] Research functional programming library
      * [ ] Create functional programming structure for reading the stream
      * [ ] Create functional programming structure for accessing the data
      * [ ] Find a way how to test file upload and file import of the mitre framework
  * File structure
    * ==Structure object==
    * ```javascript
{
  'attack-pattern': 568,
  relationship: 8348,
  'course-of-action': 266,
  identity: 1,
  'intrusion-set': 109,
  malware: 351,
  tool: 61,
  'x-mitre-tactic': 12,
  'x-mitre-matrix': 1,
  'marking-definition': 1
}```
    * Marking Definition, identity
      * useless for us
    * x-mitre-matrix
      * High overview
    * x-mitre-tactic
      * List of tactics
    * Malware, tool, intrusion-set 
      * ?
    * attack-pattern
      * on lower level than tactics
    * relationships
      * describes relationships between different entities
      * plus can have as well description
    * course-of-action
      * mitigations of attack-patterns
  * Activities import
    * Description
    * Supported platforms
    * Inputs
    * (executor -> commands) execution command
  * Category import
    * Adjust the parser to get external_id (Tsomething) and put it into the entity
  * [[Plextrac File Parsing Structure]]