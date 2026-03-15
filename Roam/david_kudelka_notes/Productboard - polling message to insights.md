  * message:
    * Hello tribe :wave:,
    * we just enabled polling for note list results, due to some past performance improvements we lost some frontend real-time sorting capabilities, so we are trying compensate for it with continuously polling for new changes.
    * How is it going to work now?
    * we are polling for changes in the list every 5s
    * We are rolling this functionality only for 20% of production users, it's already enabled for all users on production PB space, and we will be monitoring performance implication of this polling. (so going forward we might tweak some things on it - adding caching, bigger polling interval etc...)
    * Looking into future we would like to replace it with more performance sensitive solution, but currently we don't have anything better :slightly_smiling_face:
    * in case things will be going bad you can revert this functionality with this LD flag -> https://app.launchdarkly.com/apps-main/production/features/main.insights.note-list-result-polling/targeting
    * thanks :slightly_smiling_face: 