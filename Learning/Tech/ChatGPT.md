  * tags: #ai #chat #chatGPT #GPT #machine-learning 
  * notes:
    * ## Chat GPT
      * **Chat** - is the application
      * **GPT** - is the Language model
      * **= ChatGPT** - chat that is using language model
      * ### LLM
        * Large language model - it's general concept
        * Machine learning model that performs **natural language processing** (NLP) tasks
        * Trained to use **probability distributions** over words & **sequence of words ** to generate output
        * **LLMs** are neural networks, it has vast amount of nodes
      * ### Tokens
        * Tokens are usually used instead of words, words or part of words are translated into tokens, which are basically id of neural network nodes
        * Through the tokens it can understand better the whole context, not just previous word
      * **ChatGPT** - is pre-trained model that is capable of predicting words, but not only that, it was specifically **fine-tuned to for chat use.**
        * There is as well moderation API - filters out harmful input and etc... (dangerous or malicious)
      * ### Limitations
        * **Limited training data** - some data can be out of date (training can take several months) - ChatGPT (September 21')
          * ChatGPT + have web searching as well
        * **It's about patterns not logic** - ChatGPT doesn't really understand you - even though it often seems like it does
        * **It can only Handle & Output text** - it can't execute code
        * **Token limit** - depends on model you are using
    * ## Basics
      * **ChatGPT+ biggest advantage** is that you can choose different models for your answers
        * **Other advantages**
          * **Web Browsing** - + has capability to browse web, it does it through it's worker -> that visits web pages and read it contents.
            * It provides as well websites it visited and step by step process how it got the information
          * **Plugins** - write & execute code directly in the browser, internet access
            * Plugins with internet data
              * Retrieve Latest Data & Enhance User Experience
              * It can be booking flight tickets, finding hotels with prices of bookings etc ...
      * ### Versions
        * 3.5 (default) and 4
          * **Speed** - 3.5 is a lot faster then 4
            * 4 is way more advanced, bigger model
          * **Reasoning** - 4 is much more elaborate, bigger database of data, more logical
          * **Conciseness** - 4 is again way stronger, same reasons
      * ### How to Use Prompts
        * Different prompt types
          * **Simple facts**
            * How many citizens does Barcelona have?
          * **Context-Aware Prompts**
            *  What is a Wiener Schnitzel? -> Can you give me the recipe? -> I need shopping list for this recipe
      * ### Beware of Hallucinations
        * ChatGPT can create **incorrect or non-context related** output (that still sounds plausible)
      * ### Continue when hitting limit of response
        * If you run into limit of ChatGPT output, you can just type `continue`, and it will continue where it left off
    * # Interesting chapters
      * ##  Prompt engineering
        * **Description:**
          * Basics on How to construct your ChatGPT prompts?
        * **Page:**
          * [[ChatGPT - Prompt engineering basics]]
      * ##  Using ChatGPT for Utility tasks
        * **Description:**
          * Researching, summarizing & translating information
          * Proofreading, improving & enhancing text
          * Creating simple utility tools with ChatGPT
        * **Page:**
          * [[ChatGPT - utility tasks]]
      * ##  Using ChatGPT for Programming and Development
        * **Description**
          * Generating Code With & Without Programming Experience
          * Debugging & Optimizing code
          * Explaining & Refactoring code
        * **Page**
          * [[ChatGPT - Programming & Development]]