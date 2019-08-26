# some solutions to the book *Learn git in a month of lunches*
## chapter 6
1. another way to call ` git diff -- staged`?
```
 git diff --cached
 ```
2. short form of ` git add --dry-run`?
```
 git add -n
 ```
3. display line number via the `cat` command?
```
cat -n filename
```
4. `--oneline` passed to `git log` shorthand for ?
> --pretty=oneline --abbrev-commit
5. `-a` switch to `git commit` is shorthand for?
```
git add --all
```
> by using the -a switch with the commit command to automatically "add" changes from all known files (i.e. all files that are already
           listed in the index) and to automatically "rm" files in the index that have been removed from the working tree, and then perform the
           actual commit