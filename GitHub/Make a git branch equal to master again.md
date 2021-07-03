# Make a git branch equal to master again
- try this one in your branch :

```
git reset --hard master
```
This will make your branch identical to master, remove all commits you may have done, and discard all the files in the staging area.

- If you really want to blow away the previous branch with that name, and create a new one you could just use:

```
git checkout -B <branch> master
```
Using the capital version rather than -b will cause git to switch to the named branch, and reset it to the new starting point named as the last argument. If you're currently at the desired starting point you could leave off the last argument (master here), it will default to using HEAD.

---
