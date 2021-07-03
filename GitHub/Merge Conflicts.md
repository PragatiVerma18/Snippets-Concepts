# Merge Conflicts

**To get the merge conflict on terminal:**

You need to update your local master branch. Do the following steps:

 - `git checkout master`
 - `git pull origin master` 
 - `git checkout << your branch >>`
 - `git merge master`

After you execute the 4th command, you will get merge conflicts. Resolve them and then do:

 - `git commit`

** To remove the merge header (in case of incomplete merge):**

> If you get this message on doing `git pull`:
> ```
>You have not concluded your merge (MERGE_HEAD exists).
Please, commit your changes before you can merge.
```
    rm -rf .git/MERGE*
```
And the error will disappear.

**To abort merge:**
```
git merge --abort

git fetch --all
```

Then, you have two options:
```
git reset --hard origin/master
```    

OR If you are on some other branch:
```
git reset --hard origin/<branch_name>
```
---


