# Notes on git
## change language interface of git
in the `~/.bash_profile` type  
`alias="LANG=en_US git"`  
and in the current terminal type `. ~/.bash_profile`  
here is a link to the [language setting](https://stackoverflow.com/questions/10633564/how-does-one-change-the-language-of-the-command-line-interface-of-git)  
here is a link to [reload terminal](https://stackoverflow.com/questions/4608187/how-to-reload-bash-profile-from-the-command-line)
## chapter 5 using git gui
here is a good link to [gitk usage](https://lostechies.com/joshuaflanagan/2010/09/03/use-gitk-to-understand-git/)
### gitk command
after creating file.txt and git add
modified file.txt

after type
``` 
git
```
I get the following error:
```
Error in startup script: 58:103: execution error: System Events got an error: Application isn’t running. (-600)
    while executing
"exec osascript -e [format {
        tell application "System Events"
            set frontmost of processes whose unix id is %d to true
        end te..."
    invoked from within
"if {[tk windowingsystem] eq "aqua"} {
    exec osascript -e [format {
        tell application "System Events"
            set frontmost of processes ..."
    (file "/usr/local/bin/gitk" line 12212)
```
but if using 
``` 
gitk --all
```
it's fine and the gui started
### exploring the citool
using
```
git citool
```
to get a snapshot of the current file status
![file](./git_add_diffFile.png)
Note the file.txt are both in the *Unstaged Changes* and *Staged Changes*
Now in the gui window, select *Repository -> Visualize master's History*
I get the gitk window:
![gitkImage](./gitk_diff_File.png)
if type in the command line
```
git rm file.txt
```
I get the error message
```
error: the following file has staged content different from both the
file and the HEAD:
    file.txt
(use -f to force removal)
```
so by using 
```
git checkout file.txt
```
then using 
```
git rm file.txt
```
still get the error
```
error: the following file has changes staged in the index:
    file.txt
(use --cached to keep the file, or -f to force removal)
```
it says that the file has changes in the staging index, while the head
has not pointed to that change 
![gitkChek](./gitk_chec.png)

so using the hint
```
git rm --cached file.txt
```
we finally deleted the file.txt from the staging index

type
```
git ls-files
```
output:
```
LICENSE.pages
readme.txt
sample.rtf
```
Note that if using bash command 
``` 
ls
```
we get
```
LICENSE.pages		file.txt		gitk_chec.png		readme.txt
MyNotes.md		git_add_diffFile.png	gitk_diff_File.png	sample.rtf
```

## Notes on markdown
here are links on 
* [how to load image](https://medium.com/markdown-monster-blog/getting-images-into-markdown-documents-and-weblog-posts-with-markdown-monster-9ec6f353d8ec)
* [relationship to html](https://wilsonmar.github.io/markdown-text-for-github-from-html/)

## Notes on GUI
here is a link on graphical commands with [Tcl/Tk](http://tldp.org/HOWTO/Scripting-GUI-TclTk/index.html)

## chapter 7 
### remove file
using `git rm filename` if filename already tracked and committed
and dont have to use `rm` plus `git rm`
### adding parts of changes
initially the file *math.sh*
```
# Comments
a=1
```
now modify that to
```
# Adding two numbers 
a=1
b=2
# output a and 
echo $a
echo $b
let c=$a+$b
echo $c
```
open gui and add lines wanted for commits (cf book p89)
after commit
using `git diff`
the result
```
diff --git a/math.sh b/math.sh
index d0bd5ab..cb73eb4 100644
--- a/math.sh
+++ b/math.sh
@@ -1,5 +1,8 @@
 # Adding two numbers
 a=1
 b=2
+# output a and
+echo $a
+echo $b
 let c=$a+$b
 echo $c
 ```
 To do
 - [ ] how to see file in the commited version(not the one in the working area, using cat)
 - [ ] multiple stages of `git add` how to use `git reset` to come back to a certain changed version ,eg, 3 times of `git add` reset to the second modification


 ## chapter 8
 ### git log
 * example output of `git log --patch`
 ```
 commit b474553295189a451c724f6ee034d2177790a018 (HEAD -> master, origin/master, origin/HEAD)
Author: BillMark98 <hupanweibill@gmail.com>
Date:   Tue Aug 27 14:51:15 2019 +0200

    adding task list with squares

diff --git a/MyNotes.md b/MyNotes.md
index 8683b14..01b51be 100644
--- a/MyNotes.md
+++ b/MyNotes.md
@@ -144,5 +144,5 @@ index d0bd5ab..cb73eb4 100644
  echo $c
```
*To do*
- [ ] how to see file in the commited version(not the one in the working area, using cat)
- [ ] multiple stages of `git add` how to use `git reset` to come back to a certain changed version ,eg, 3 times of `git add` reset to the second modification

* example out put of `git log --stat`
```
commit b474553295189a451c724f6ee034d2177790a018 (HEAD -> master, origin/master, origin/HEAD)
Author: BillMark98 <hupanweibill@gmail.com>
commit b474553295189a451c724f6ee034d2177790a018 (HEAD -> master, origin/master, origin/HEAD)
Author: BillMark98 <hupanweibill@gmail.com>
Date:   Tue Aug 27 14:51:15 2019 +0200

    adding task list with squares

 MyNotes.md | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
 ```
 * combined version using `git log --patch-with-stat`
 ```
 commit b474553295189a451c724f6ee034d2177790a018 (HEAD -> master, origin/master, origin/HEAD)
Author: BillMark98 <hupanweibill@gmail.com>
Date:   Tue Aug 27 14:51:15 2019 +0200

    adding task list with squares
---
 MyNotes.md | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)

diff --git a/MyNotes.md b/MyNotes.md
index 8683b14..01b51be 100644
--- a/MyNotes.md
+++ b/MyNotes.md
@@ -144,5 +144,5 @@ index d0bd5ab..cb73eb4 100644
  echo $c
  ```
*To do*
- [ ] how to see file in the commited version(not the one in the working area, using cat)
- [ ] multiple stages of `git add` how to use `git reset` to come back to a certain changed version ,eg, 3 times of `git add` reset to the second modification


## git rev-parse
here is a link to discuss the usage of [`git rev-parse`](https://stackoverflow.com/questions/15798862/what-does-git-rev-parse-do)
## git checkout
git checkout to a previous version
do some change e.g `chmod 755 math.sh` (the previous mode is 644)
then `git checkout master`
```
error: Your local changes to the following files would be overwritten by checkout:
	math.sh
Please commit your changes or stash them before you switch branches.
Aborting
```
to do
- [ ] how to delete the changes that has not been staged

# chapter 9
TO DO:
- [ ] how to use alias to input like `git lol 4` which means will display 
the latest 4 commits info? 

after creating a new branch and doing some changes, swichting back to master successfully :
```
BillHus-MBP:learngit bill$ git checkout master
M	math.sh
M	newfile.txt
```

but switch back to the new branch and commit the changes. Now do some changes, switching back
aborted
```
error: Your local changes to the following files would be overwritten by checkout:
	math.sh
Please commit your changes or stash them before you switch branches.
Aborting
```
using ` git stash`

some info:
* [print commit message](https://stackoverflow.com/questions/3357280/print-commit-message-of-a-given-commit-in-git)
* [amend commit message](https://linuxize.com/post/change-git-commit-message/),
use the code `git commit --amend -m "revised message"` to modify the latest commit
* [dashes in `git checkout`](https://superuser.com/questions/1154393/git-checkout-filename-vs-git-checkout-filename)

* [count commit](https://stackoverflow.com/questions/11657295/count-the-number-of-commits-on-a-git-branch)
also [here](https://stackoverflow.com/questions/677436/how-do-i-get-the-git-commit-count)

* [comit id of tag](https://stackoverflow.com/questions/1862423/how-to-tell-which-commit-a-tag-points-to-in-git#comment1759935_1862542)
## chapter 10
git add -p only for the file with no merge conflict.
For example, if use `git add -p` to  `baz` that merged with conflict.
Then I got the message:
```
ignoring unmerged: baz
No changes.
```

The `git diff` gives the output:  
```
diff --cc baz
index f836512,1c52108..0000000
--- a/baz
+++ b/baz
@@@ -1,4 -1,4 +1,8 @@@
  a=1
- b=0
+ b=1
  let c=$a/$b
++<<<<<<< HEAD
 +printf "The answer is %d" $c
++=======
+ echo $c
++>>>>>>> bugfix
```  
if dont commit changes. Doing instead `git reset baz`  
After that, type `git merge bugfix`  
I got  
```
fatal: You have not concluded your merge (MERGE_HEAD exists).
Please, commit your changes before you merge.
```  
it seems there is a head created after merge

`git mergetool` usage scenario :  
already performed the `git merge branchname` but the merge conflicted  
then use the `mergetool`. If typing `git mergetool` before the merge operation,  
get the message :  
```
This message is displayed because 'merge.tool' is not configured.
See 'git mergetool --tool-help' or 'git help config' for more details.
'git mergetool' will now attempt to use one of the following tools:
opendiff kdiff3 tkdiff xxdiff meld tortoisemerge gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare emerge vimdiff
No files need merging
```  

## chapter 11
#### Questions
1.where is `clonee existing repository` in th git gui?  
2. in the `ff.clone1` checkout to `remotes/origin/new_feature`  
and commit some changes,  
the `git lol` output:   
```
* bc74f22 (HEAD) add remote.txt
* cb86553 (origin/new_feature, origin/HEAD, new_feature) Committing bar.
* b62e9b6 Committing foo.
* d8e2082 (origin/master, master) Committing baz.
* a4a8eec Committing the README.
```   

the `git branch -v` output:  
```
* (HEAD detached from origin/new_feature) bc74f22 add remote.txt
  master                                  d8e2082 Committing baz.
  new_feature                             cb86553 Committing bar.
```  
then checkout to master   
```
Warning: you are leaving 1 commit behind, not connected to
any of your branches:

  bc74f22 add remote.txt

If you want to keep it by creating a new branch, this may be a good time
to do so with:

 git branch <new-branch-name> bc74f22

Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```  

then go back to `ff` branch `new_feature`  I did not find the `new.txt`  
and in the `ff.clone1`  I could not find the branch where I commited the change.   
### notes
**bare repositories** can't perform opreations like `git add`  
e.g create the `ff` directory by running the `make_merge_ff.sh`  
and use `git clone --bare ff ff.git`  
cd into `ff.git`  and add new file like `new.txt`  
then `git add new.txt`  
I got  
```
fatal: this operation must be run in a work tree
```  
but `git log`  can be performed, just as in a normal working directory  


