  * tags: #git #how-to
  * author: [[CBEAMS]]
  * notes:
    * ### The seven rules of a great Git commit message
      * Separate subject from body with a blank line
      * Limit the subject line to 50 characters
      * Capitalize the subject line
      * Do not end the subject line with a period
      * Use imperative mood in the subject line
      * Wrap the body at 72 characters
      * Use the body to explain what and why vs how
    * **Separate subject from body with a blank line**
      * There should be separation between body and subject, this is automatically done in github
    * **Limit the subject line to 50 characters**
      * It ensures subject is readable, and forces the author to think for a moment about the most concise way to explain what's going on
    * **Capitalize the subject line**
      * For example
        * Accelerate to 88 miles per hour
      * Instead of
        * ~~accelerate to 88 miles per hour~~
    * **Do not end the subject line with a period**
      * Example
        * Open the pod bay doors
      * Instead of
        * ~~Open the pod bay doors:~~
    * **Use the imperative mood in the subject line**
      * **Imperative mood** just means "spoken or written as if giving a command or instruction". A few examples
        * Clean your room
        * Close the door
        * Take out the trash
      * This is for example git build-in convention, it is very useful for reporting facts
    * **Wrap the body at 72 characters** 
      * make it concise
    * **Use the body to explain what and why vs how**
      * Good example from bitcoin core
        * ```shell
   Simplify serialize.h's exception handling

   Remove the 'state' and 'exceptmask' from serialize.h's stream
   implementations, as well as related methods.

   As exceptmask always included 'failbit', and setstate was always
   called with bits = failbit, all it did was immediately raise an
   exception. Get rid of those variables, and replace the setstate
   with direct exception throwing (which also removes some dead
   code).

   As a result, good() is never reached after a failure (there are
   only 2 calls, one of which is in tests), and can just be replaced
   by !eof().

   fail(), clear(n) and exceptions() are just never called. Delete
   them.```