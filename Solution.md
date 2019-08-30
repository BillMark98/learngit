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

## chapter 7
## some solutions
### 8.5.1
2.  list just the most recent N commits? using `git log -n N`
3.  display the date as time relative to the current time (for example 2 hours ago)?  `git log --date=relative`
4.  `--oneline` passed to `git log` shorthand for ?
> --pretty=oneline --abbrev-commit

### 8.5.3

output for `git rev-parse master^3`
> the corresponding SHA1 ID for the last but three commit
output for ` git show master@{3}`
```
commit bb6bf3694cface50d7f508917ebb5e0878e542ef
Author: BillMark98 <hupanweibill@gmail.com>
Date:   Wed Aug 28 15:59:48 2019 +0200

    for math.sh:
    Adding printf
    This is to make the output more human readble

    printf is part of BASH, works just like in C

    for MyNotes.md
    adding notes on git log

diff --git a/.DS_Store b/.DS_Store
new file mode 100644
index 0000000..135b522
Binary files /dev/null and b/.DS_Store differ
diff --git a/MyNotes.md b/MyNotes.md
index 01b51be..4e2dfc0 100644
--- a/MyNotes.md
+++ b/MyNotes.md
@@ -145,4 +145,70 @@ index d0bd5ab..cb73eb4 100644
  
  To do
  ```
output for `git show master^^^ `  (output the same as above)
```
commit bb6bf3694cface50d7f508917ebb5e0878e542ef
Author: BillMark98 <hupanweibill@gmail.com>
Date:   Wed Aug 28 15:59:48 2019 +0200

    for math.sh:
    Adding printf
    This is to make the output more human readble

    printf is part of BASH, works just like in C

    for MyNotes.md
    adding notes on git log

diff --git a/.DS_Store b/.DS_Store
new file mode 100644
index 0000000..135b522
Binary files /dev/null and b/.DS_Store differ
diff --git a/MyNotes.md b/MyNotes.md
index 01b51be..4e2dfc0 100644
--- a/MyNotes.md
+++ b/MyNotes.md
@@ -145,4 +145,70 @@ index d0bd5ab..cb73eb4 100644
  ```
  To do
  ```

works also if additional tag is added (will display it)
e.g
```
commit bb6bf3694cface50d7f508917ebb5e0878e542ef (tag: printF)
Author: BillMark98 <hupanweibill@gmail.com>
Date:   Wed Aug 28 15:59:48 2019 +0200

    for math.sh:
    Adding printf
    This is to make the output more human readble

    printf is part of BASH, works just like in C

    for MyNotes.md
    adding notes on git log

diff --git a/.DS_Store b/.DS_Store
new file mode 100644
index 0000000..135b522
Binary files /dev/null and b/.DS_Store differ
diff --git a/MyNotes.md b/MyNotes.md
index 01b51be..4e2dfc0 100644
--- a/MyNotes.md
+++ b/MyNotes.md
@@ -145,4 +145,70 @@ index d0bd5ab..cb73eb4 100644
  ```
  To do
  ```

 ` git rev-parse :/" MESSAGE "` will display the SHA1 ID according to the commit with commit message which contains a substring of MESSAGE
 like `git rev-parse :/" chap8"`
 will display the SHA1 ID with corresponding commit message "some solution to chap8"