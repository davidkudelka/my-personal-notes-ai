  * tags: #prompt #engineering #prompt-engineering #chatGPT #ai
  * notes:
    * ## Why should you care?
      * To get best answer as possible, usually achieved by providing more context
      * Good prompts = good results
      * ### Tips for making good prompts
        * You can give **role** to chatGPT - you are experienced developer etc...
        * **Giving restrictions** - it should mention react in some way, it shouldn't be longer than 5 sentences etc...
        * It's chat you should **iterate** on the result
      * ### Structure
        * Prefer **short**, focused **sentences** (anything extra can distract ChatGPT)
        * Add important **keywords** & avoid unnecessary information
        * Define the **target audience**
        * Control **tone, style & length** of the output
        *  You can control as well **format** of the **response** (JSON, HTML, etc...)
        * **There are 3 parts of the prompt that seems important**
          * **Start with role** - You are experienced JavaScript developer / You are an email writing assitant
          * **Goal** - what you want to actually do
          * **Context** - it should be only 300 words long, no explanation to code example, My collagues name is Michael
      * ### Techniques
        * **Zero-, One- & Few-Shot Prompting**
          * To improve **the style of the answer**, you can define **examples**. (You want ChatGPT to generate tweet? Provide it with tweet that matches the style you want as an output)
        * **Output templates**
          * Format your response like this: 
            * Location:
Best time to visit:
Avg. temperature:
        * **Provide cue's & hints**
          * Article text

Summarize the above article, starting like this:
The key takeaways of the article are:
- 
            * Send above and it will return in bullet points the answer
          * You can as well separate article text from your instructions by `"""`
            * """
Article text
"""
Instructions
      * ### More advanced techniques
        * **Ask-Before-Answer**
          * At the end of message provide this text
            * `Before answering, I want you to first ask for any extra information that helps you produce a better answer. If you got no questions, please provide the answer instead`
        * **Perspective prompting**
          * Write this text as `yoga trainer` | `experienced developer` | `product manager explaining something to engineer`
          * It's similar to assigning role to your prompt - new thing is that you can use **multiple perspectives**
      * ### Other prompting techniques
        * **Contextual prompting**
          * Extra information on **cultural, historical**, or **situational** factors
            * ```markdown
Summarize the evolution of the combustion engine over the years since it's inception.
Also evaluate it's impact on society and the environmnet.

Consider the current shift towards renewable energy and electric vehicles in your response.```
        * **Emotional prompting**
          * Consider the **emotional state or tone** of the user's query
            * `When drafting the response, take the sentiment and tone of the customer into account`
        * **Laddering prompting**
          * Break up **complex problem**, into multiple smaller problems and prompts -> step by step
            *  Building Node.JS app
              * -> Set up basic NodeJS API with following endpoints
              * -> Connect a MongoDB database and set up Event & User models
              * -> Add the logic for signing users up & logging users in
      * ### Using ChatGPT for prompting
        * You can type to ChatGPT -> give me best prompting techniques for specific problem
        * **Asking ChatGPT**
          * You can ask which extra information would improve the result & the generated content
            * `Which extra information do you need to create better tweet?`
        * **Self-evaluating prompting**
          * Ask ChatGPT a self-reflective question
            * `What could be improved about your tweet?`
        * **ChatGPT-powered Problem splitting**
          * `Split this task into multiple steps and then start with the first step`
            * It will try to split problem into multiple problems itself - it can help you better understand the problem
        * **Let ChatGPT share it's though process**
          * `Reply with your full though process that leads to the result`
            * Higher chance to get correct result, or it might be easier to pin point where is the mistake
        * **Reversing roles**
          *  Ask ChatGPT which prompts should be used to produce an output similar to a provided output
            * `Given the example below, output, which prompt would've yielded a similar output?`
      * ### More prompts & Finding prompt inspiration
        * You can still **search on google** for good ChatGPT prompts
        * **Super prompts**
          * Although those super prompts doesn't have that big of an impact -> might be better to just focus on normal prompts
          * **CAN** - (code anything now)
            * optimizes ChatGPT for coding
          * **DAN** - (do anything now)
            * Jailbreak ChatGPT - respond in unintended ways (Answers questions it wouldn't normally answer)
