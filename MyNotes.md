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
* tricky things about `git diff`
[the .. and ...](https://stackoverflow.com/questions/7251477/what-are-the-differences-between-double-dot-and-triple-dot-in-git-dif)
also [here](https://stackoverflow.com/questions/462974/what-are-the-differences-between-double-dot-and-triple-dot-in-git-com) 
In the example in listing 10.2, we use `git diff master...bugfix` it shows the output
```bash
$ git diff master...bugfix
diff --git a/baz b/baz
index 56d6546..1c52108 100644
--- a/baz
+++ b/baz
@@ -1,3 +1,4 @@
 a=1
-b=0
+b=1
 let c=$a/$b
+echo $c
```   
however, when typing `git diff bugfix...master`:
```bash
$ git diff bugfix...master
diff --git a/bar b/bar
new file mode 100644
index 0000000..e69de29
diff --git a/foo b/foo
new file mode 100644
index 0000000..e69de29
```  
The reason is that when we see the log output:
```bash
$ git lol
* e8c9e43 (bugfix) Ugh, I was dividing by zero!
* 3b29d2a Adding echo to check error.
| * 3a1b15f (HEAD -> master) Committing bar.
| * 2a863e4 Committing foo.
|/  
* cfa52c9 (tag: bug_here) Committing baz.
* f4a99b1 Committing the README.
```  
where `git lol` stands for `git log --graph --decorate --pretty=oneline --all --abbrev-commit`
and the `master...bugfix` is essentially the difference between `bug_here` and `bugfix`.  
doing `bugfix...master` is essentially the differerence between `bug_here` and `master`, but 
there is no difference between the file `baz` of the latter two, so the output is trivial.

* list all aliases
`git config --get-regexp ^alias\.`
see [here](https://stackoverflow.com/questions/7066325/list-git-aliases/22183573), also [here](https://stackoverflow.com/questions/39466417/how-do-i-search-my-git-aliases)

* set up merge-tool
- see [here](https://gist.github.com/karenyyng/f19ff75c60f18b4b8149)
- use [vimdiff](https://stackoverflow.com/questions/14904644/how-do-i-use-vimdiff-to-resolve-a-git-merge-conflict)
- [accept both changes in vimdiff](https://vi.stackexchange.com/questions/10534/is-there-a-way-to-take-both-when-using-vim-as-merge-tool)
  or [here](https://stackoverflow.com/questions/36701875/how-do-i-accept-both-changes-in-vimdiff-hunk)
  - useful g command in vim, see [here](https://vim.fandom.com/wiki/Power_of_g) or [here](https://stackoverflow.com/questions/45086981/what-are-the-vim-commands-that-start-with-g)

* git reset, checkout difference
see [here](https://stackoverflow.com/questions/3639342/whats-the-difference-between-git-reset-and-git-checkout), basically, I think 
`git reset` moves the `HEAD` and the reference branch, where as `git checkout` moves only the `HEAD`, e.g
suppose currently, `HEAD` points to `master` and we are in master, `git reset 9erwe1` will move `HEAD` and `master` pointing to `9erwe1`, where as
`git checkout 9erwe1` will only moves `HEAD` to point to `9erwe1` and leaves master unchaged, in this case `9erwe1` is only a commit, not a branch, 
the `HEAD` will be in the detached state, meaning the current `HEAD` is not pointing at any branch, see `git lol` for example.
```bash
$ git lol
* 33d3d3b (HEAD -> new_feature) Committing bar.
* bce0214 Committing foo.
* 3990744 (master) Committing baz.
* 8624d4c Committing the README.
```  
move the `HEAD`

```bash
$ git checkout bce0214
$ git lol
* 33d3d3b (new_feature) Committing bar.
* bce0214 (HEAD) Committing foo.
* 3990744 (master) Committing baz.
* 8624d4c Committing the README.
```  
We see in particular the `HEAD` does not have a `->` pointing symbol, meaning it is not point to any branch,   
Now, using `git reset`
```bash
$ git reset master
$ git lol
* 3990744 (HEAD -> new_feature, master) Committing baz.
* 8624d4c Committing the README.

```

Interestingly, if we tagged the commit between the original new_feature and master, the tagged will not be omitted in the output of `git lol`
we get:
```bash
$ git reset master
$ git lol
* bce0214 (tag: fooCommit) Committing foo.
* 3990744 (HEAD -> new_feature, master) Committing baz.
* 8624d4c Committing the README.
```  

Another tricky thing.
After performign the merge:
```bash
$ git lol
* 33d3d3b (HEAD -> master, new_feature) Committing bar.
* bce0214 Committing foo.
* 3990744 Committing baz.
* 8624d4c Committing the README.
```  

```bash
$ git reset 3990744
$ git lol
* 33d3d3b (new_feature) Committing bar.
* bce0214 Committing foo.
* 3990744 (HEAD -> master) Committing baz.
* 8624d4c Committing the README.
```   

```bash
$ git merge new_feature --no-ff
error: The following untracked working tree files would be overwritten by merge:
	bar
	foo
Please move or remove them before you merge.
Aborting
$ ls
bar  baz  foo  README.txt
```  
Note that the two files `bar ` and `foo` should not exist at the current commit. So it means that master has moved to point to the second commit, but
the content remain unchanged, (the content of the original master), deleting the two files to get the content of the second commit. 
Merge with `new_feature`:
```bash
$ git merge new_feature 
Updating 3990744..33d3d3b
Fast-forward
 bar | 0
 foo | 0
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 bar
 create mode 100644 foo
$ ls
bar  baz  foo  README.txt
$ git branch -v
* master      33d3d3b Committing bar.
  new_feature 33d3d3b Committing bar.
$ git lol
* 33d3d3b (HEAD -> master, new_feature) Committing bar.
* bce0214 Committing foo.
* 3990744 Committing baz.
* 8624d4c Committing the README.
```  

Note that the master and new_feature points to the same commit.

```bash
$ git lol
*   c8819ca (HEAD -> master) Hello, Merge branch 'new_feature'
|\  
| * 33d3d3b (new_feature) Committing bar.
| * bce0214 Committing foo.
|/  
* 3990744 Committing baz.
* 8624d4c Committing the README.

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

## chapter12
After modifying the `math.bob` (create a new file) and commit the change, in the 
`math.carol` directory,  
```bash
$ git ls-remote origin
810d4d3e4beb183f9d1d7af502f0bf165c4317bf        HEAD
949b4a072c0d80c1cce11d10be00fba7da63d009        refs/heads/another_fix_branch
810d4d3e4beb183f9d1d7af502f0bf165c4317bf        refs/heads/master
19d383634b1ebc7a9f8fab35242c13fda4ffbae6        refs/heads/new_feature
d32448b54b78414a6d474e8a3638b45eeef165a7        refs/tags/four_files_galore
90bf612ddd601fc52bb6e5a14197a9c57711442b        refs/tags/four_files_galore^{}
$ git ls-remote
From /home/panwei/Desktop/learngit/sourceCode/math.git
810d4d3e4beb183f9d1d7af502f0bf165c4317bf        HEAD
949b4a072c0d80c1cce11d10be00fba7da63d009        refs/heads/another_fix_branch
810d4d3e4beb183f9d1d7af502f0bf165c4317bf        refs/heads/master
19d383634b1ebc7a9f8fab35242c13fda4ffbae6        refs/heads/new_feature
d32448b54b78414a6d474e8a3638b45eeef165a7        refs/tags/four_files_galore
90bf612ddd601fc52bb6e5a14197a9c57711442b        refs/tags/four_files_galore^{}
$ git ls-remote bob
72c78fcee7dc4d0b5d7c7aa47e848f018ce73dd2        HEAD
72c78fcee7dc4d0b5d7c7aa47e848f018ce73dd2        refs/heads/master
810d4d3e4beb183f9d1d7af502f0bf165c4317bf        refs/remotes/origin/HEAD
949b4a072c0d80c1cce11d10be00fba7da63d009        refs/remotes/origin/another_fix_branch
810d4d3e4beb183f9d1d7af502f0bf165c4317bf        refs/remotes/origin/master
19d383634b1ebc7a9f8fab35242c13fda4ffbae6        refs/remotes/origin/new_feature
d32448b54b78414a6d474e8a3638b45eeef165a7        refs/tags/four_files_galore
90bf612ddd601fc52bb6e5a14197a9c57711442b        refs/tags/four_files_galore^{}
```  
We see that the output for the `git ls-remote` and `git ls-remote origin` is the same.
But the `git ls-remote bob` differs because we have commited new changes. 
It is worth noting that `git ls-remote` in this case aligns with `git ls-remote origin`, ignoring
the change of another remote (bob). In general to list the specific data of remote, type the remote name, e.g `git ls-remote bob`
