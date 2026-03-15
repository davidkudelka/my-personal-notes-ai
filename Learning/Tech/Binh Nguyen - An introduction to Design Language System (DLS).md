  * tags: #react #conference #talk
  * author: [[Binh Nguyen]]
  * notes:
    * # An introduction to Design Language System - DLS
      * ### Storybook article on how to structure your DLS
        * https://storybook.js.org/blog/structuring-your-storybook/
      * ### What is DLS
        * Basically all documentation about your components
        * All documentation on how to use and work with your components and how to get consistency and everything connected to your system
        * Points
          * **Serves as Single source of thruth**
          * **Uses atomic design** - better for searchability
          * **Is UI framework agnostic** - least external dependencies as possible
          * **Provides functional / behavioural reference of UI components** - developers know how to work with them, how to use them
      * ### Atomic Design
        * Organize components to structure that is logical and structured
        * **Structure**
          * Pages
            * Templates
              * Organism
                * Molecules 
                  * Atoms - buttons, selects ...
                    * Foundation - Colour (used in the app), Typography 
          * Shared folder
            * foundations.scss - all the variables 
            * Fonts/Robotico - Put fonts, typography styling file - declaring font-faces 
            * sb-docs.csss - 