  * tags: #git #versioning-system #article
  * author: [[Jakub Janecek]]
  * link to article: https://blog.jakubjanecek.com/blog/20230820_git-automatic-rebase/
  * notes:
    * ### Introduction
      * I often find myself in the situation where I have just pushed a branch with my changes and created a pull request, only to later realize that I forgot to add a file or made a typo in my code. In such cases, my goal is to make a small change while maintaining a clean Git history, so I opt to rebase the last commit to essentially hide it. Of course this wouldn’t work if there was a chance that someone already used my branch or I cooperated with someone on it. But usually the branch is just mine and I make the changes almost immediately after pushing it so I think it’s worth it to keep the history clean.
    * ### Automated process
      * ```javascript
function git_rebase_last_and_push
    set -lx GIT_EDITOR "vim +2 -c 'normal cwf' -c 'wq'"
    git commit -a -m "wip"
    git rebase -i HEAD~2
    git push -f origin HEAD
end```
    * ### Summary
      * Although this function is interesting, there is native way how to do this
        * `git commit --amend --no-edit` and then `git force push` is necessary