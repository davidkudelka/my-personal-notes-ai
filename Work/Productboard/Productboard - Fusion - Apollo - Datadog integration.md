  * tags: #apollo #datadog #integration #technical-planning
  * todo:
    * [x] Write to Jany about the Apollo studio -> Datadog integration
    * [x] Write to Dominik about how we are currently tracking GraphQL metrics in microservices
    * [x] Draft message to t-graphql-guild
      * Mention my 2 current worries
        * Who should I get buy-in from, mention the current issue's and how we would solve it with this integration
        * Datadog pricing -> it might bump up price we are paying for datadog, are we ok with it?
        * Duplication of record tracking, check whether it's ok or we would have to do some clean up
  * notes:
    * Steps to integrate are quite simple, it's more about how to get buy-in, clearly communicate issue's and advantages
  * name of queries: #apollo-datadog-integration-pb-todo-list
    * ### [x] mutations
      * [x] **favorites**
        * [x] use-add-board-to-favorites
          * useAddBoardToFavoritesMutation
        * [x] use-remove-board-from-favorites
          * useRemoveBoardFromFavoritesMutation
        * [x] use-move-favorites-board
          * useMoveFavoriteBoardMutation
      * [x] **teamspace**
        * [x] use-archive-teamspace
          * useArchiveTeamspaceMutation
        * [x] use-create-teamspace
          * useCreateTeamspaceMutation
        * [x] use-delete-teamspace
          * useDeleteTeamspaceMutation
        * [x] use-join-teamspace
          * useJoinTeamspaceMutation
        * [x] use-leave-teamspace
          * useLeaveTeamspaceMutation
        * [x] use-unarchive-teamspace
          * useUnarchiveTeamspaceMutation
        * [x] use-update-teamspace
          * useUpdateTeamspaceMutation
      * [x] **board**
        * [x] use-delete-board
          * useDeleteBoardMutation
        * [x] use-duplicate-navigation-board
          * useDuplicateNavigationBoardMutation
        * [x] use-create-navigation-board
          * useCreateNavigationBoardMutation
        * [x] use-rename-features-board
          * useRenameFeaturesBoardMutation
        * [x] user-rename-insights-board
          * useRenameInsightsBoardMutation
        * [x] user-rename-roadmap-board
          * useRenameRoadmapBoardMutation
      * [x] **folder**
        * [x] use-move-folder
          * useMoveFolderMutation
        * [x] use-create-navigation-folder
          * useCreateNavigationFolderMutation
      * [x] use-move-navigation-node
        * useMoveNavigationNodeMutation
    * ### [x] queries
      * [x] use-is-teamspace-member
        * useIsTeamspaceMemberQuery
      * [x] use-polling-for-navigatio-board-query
        * usePollingForNavigationBoardQuery
      * [x] move-to-list-query
        * moveToDropdownListQuery