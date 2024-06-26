### Why do I need to squash my commits?
https://softwareengineering.stackexchange.com/a/263172


### How
Before you start, make sure you are in the feature branch you want to squash and **not** the `main` branch.

1. `git rebase -i main`
2. Replace `pick` at the start of each line **except the top line** with `s`( which stands for squash) then save.

    Example:
    ```bash
    pick 47a32d7e WIP: first Commit
    s bc0037a1 WIP: second Commit
    s c5b81945 WIP: third Commit
    ```

3. You should now be able to reword the first commit with the normal `because` and `This commit` template we use - [example here](https://github.com/TheOdinProject/theodinproject/pull/2808/commits/fd2feaef36ffa27c2862480ce58a34e3c49ed812)

4. Pushing to remote

    **If you have already pushed to the remote previously**

    *Warning: only force push if you are the only one working on the branch. Never force push to branches anyone else is working on, and especially never force push to the main branch*

    * You will have to force push your branch because your commits have been rebased: `git push -f` 
  
    **Otherwise, if this is the first time pushing the branch to the remote**

    * Then push as normal `git push`