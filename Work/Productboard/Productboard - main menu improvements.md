  * tags: #improvements #productboard #graphql
  * todo:
    * [x] Posting message about the current state of main menu improvements
  * notes:
    * Hello I am writing here update about our cooperation with Nucleus on main menu navigation tree component for Fusion
    * 1. We had discussion with @Igor last week where we agreed on some cooperation between us and Nucleus, as part of this cooperation Nucleus should work on proof of concept headless list component that supports Relay architecture (link to post why that is an issue)
    * 2. I should be the point of contact between us and Nucleus, anything you need you can just shoot me message or post in this channel
  * un-resolved issue's:
    * How to work with Relay's connection key in headless list? We need this to reference particular Relay query
      * There is issue with current implementation, each query needs to suport connection to array of edges (to be able to create connection key in Relay)
      * Open question remains how to create different connection key for each section in headless list, maybe we can find it by connection key and input id?
  * issues addressed:
    * Igor contacted me last week with some issue's, here I have answers for most of them
  * tickets:
    * Separating list into 3, top (navigation items), middle (teamspaces and personal), bottom (data section) parts
    * List headless issue's (sorted by importance)
      * **Supporting relay architecture** - we are missing solution for working with cache, plus not supporting Relay data management, state is managed in React store which is not optimised for good performance
      * **D&D support** - supporting D&D have secondary importance after supporting relay architecture
        * What still needs to be discussed - how does it work with drag&drop cross teamspaces and between teamspaces and personal, plus restriction of those d&d actions?
      * **Real-time updates** -  we still didn't resolve this, but potentially just Fusion work with subscriptions or support of polling, for both we need some good way how to manage relays cache (should be resolved in first point)