> # ⬛Undoing changes
## <p >1.Git revert</p>
The  ``git revert`` command can be considered an 'undo' type command, however, it is not a traditional undo operation. Instead of removing the commit from the project history, it figures out how to invert the changes introduced by the commit and appends a new commit with the resulting inverse content. This prevents Git from losing history, which is important for the integrity of your revision history and for reliable collaboration.

Reverting should be used when you want to apply the inverse of a commit from your project history. This can be useful, for example, if you’re tracking down a bug and find that it was introduced by a single commit. Instead of manually going in, fixing it, and committing a new snapshot, you can use ``git revert`` to automatically do all of this for you.
***************
##How it works :
The ``git revert`` command is used for undoing changes to a repository's commit history. Other 'undo' commands like, git checkout and git reset, move the ``HEAD`` and branch ref pointers to a specified commit. 
``Git revert`` also takes a specified commit, however, ``git revert`` does not move ref pointers to this commit. A revert operation will take the specified commit, inverse the changes from that commit, and create a new "revert commit". The ref pointers are then updated to point at the new revert commit making it the tip of the branch.

To demonstrate let’s create an example repo using the command line examples below:
<textarea widt>$ mkdir git_revert_test
$ cd git_revert_test/
$ git init .
Initialized empty Git repository in /git_revert_test/.git/
$ touch demo_file
$ git add demo_file
$ git commit -am"initial commit"
[main (root-commit) 299b15f] initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 demo_file
$ echo "initial content" >> demo_file
$ git commit -am"add new content to demo file"
[main 3602d88] add new content to demo file
n 1 file changed, 1 insertion(+)
$ echo "prepended line content" >> demo_file
$ git commit -am"prepend content to demo file"
[main 86bb32e] prepend content to demo file
 1 file changed, 1 insertion(+)
$ git log --oneline
86bb32e prepend content to demo file
3602d88 add new content to demo file
299b15f initial commit</textarea>

Here we have initialized a repo in a newly created directory named ``git_revert_test``. We have made 3 commits to the repo in which we have added a file ``demo_file`` and modified its content twice. At the end of the repo setup procedure, we invoke ``git log`` to display the commit history, showing a total of 3 commits. With the repo in this state, we are ready to initiate a ``git revert``.
``$ git revert HEAD``
``[main b9cd081] Revert "prepend content ``
``to demo file" 1 file changed, 1 deletion(-)``
Note that the 3rd commit is still in the project history after the revert. Instead of deleting it, ``git revert`` added a new commit to undo its changes. As a result, the 2nd and 4th commits represent the exact same code base and the 3rd commit is still in our history just in case we want to go back to it down the road.
 *********

> #<p color="red"> Common options <p>


<div class="component component--codeblock" > <pre><code class="hljs language-css"><span class="hljs-attr">--no-edit</span></code></pre> </div>
<p>This is a default option and doesn't need to be specified. This option will open the configured system editor and prompts you to edit the commit message prior to committing the revert <p>
 
 <div class="component component--codeblock"> <pre><code class="hljs language-css">-n
<span class="hljs-attr">--no-commit</span></code></pre> </div>


Passing this option will prevent ``git revert`` from creating a new commit that inverses the target commit. Instead of creating the new commit this option will add the inverse changes to the Staging Index and Working Directory. These are the other trees Git uses to manage the state of the repository.


**********
## <p >2.Git reset</p>

<p>The git reset command is a complex and versatile tool for undoing changes. It has three primary forms of invocation. These forms correspond to command line arguments --soft, --mixed, --hard. The three arguments each correspond to Git's three internal state management mechanism's, The Commit Tree (HEAD), The Staging Index, and The Working Directory.</p>

### <p>A.--hard</p>
This is the most direct, DANGEROUS, and frequently used option. When passed --hard The Commit History ref pointers are updated to the specified commit. Then, the Staging Index and Working Directory are reset to match that of the specified commit. Any previously pending changes to the Staging Index and the Working Directory gets reset to match the state of the Commit Tree. This means any pending work that was hanging out in the Staging Index and Working Directory will be lost.

To demonstrate this, let's continue with the three tree example repo we established earlier. First let's make some modifications to the repo. Execute the following commands in the example repo:  

<div class="component component--codeblock"> <pre><code class="hljs language-css">$ echo 'new file content' > new_file
<span class="hljs-attr">$ git add new_file</span></code></pre> </div> 

Let us now execute a ``git reset --hard``and examine the new state of the repository.


![5](/Images/Capture%20d’écran%202023-11-30%20221906.png)



Here we have executed a "hard reset" using the  ``--hard  ``option. Git displays output indicating that  ``HEAD `` is pointing to the latest commit  ``dc67808 ``. Next, we check the state of the repo with  ``git status ``. Git indicates there are no pending changes. We also examine the state of the Staging Index and see that it has been reset to a point before new_file was added. Our modifications to  ``reset_lifecycle_file `` and the addition of  ``new_file `` have been destroyed. This data loss cannot be undone, this is critical to take note of.


### <p>B.--mixed</p>
 This is the default operating mode. The ref pointers are updated. The Staging Index is reset to the state of the specified commit. Any changes that have been undone from the Staging Index are moved to the Working Directory. Let us continue.


 ![2](/Images/Capture%20d’écran%20.png)

 In the example above we have made some modifications to the repository. Again, we have added a ``new_file`` and modified the contents of ``reset_lifecycle_file``. These changes are then applied to the Staging Index with ``git add``. With the repo in this state, we will now execute the reset.

 ![2](/Images/Capture%20d’écran%2022.png)


Here we have executed a "mixed reset". To reiterate, ``--mixed`` is the default mode and the same effect as executing ``git reset``. Examining the output from ``git status`` and ``git ls-files``, shows that the Staging Index has been reset to a state where ``reset_lifecycle_file`` is the only file in the index. The object SHA for ``reset_lifecycle_file`` has been reset to the previous version.
### <p>c.--soft</p>
![2](/Images/git-reset.png)

When the ``--soft argument`` is passed, the ref pointers are updated and the reset stops there. The Staging Index and the Working Directory are left untouched. This behavior can be hard to clearly demonstrate. Let's continue with our demo repo and prepare it for a soft reset.

![2](/Images/soft.png)

The code above executes a "soft reset" and also invokes the ``git status``and ``git ls-files ``combo command, which outputs the state of the repository. We can examine the repo state output and note some interesting observations. First, git status indicates there are modifications to ``reset_lifecycle_file`` and highlights them indicating they are changes staged for the next commit. Second, the ``git ls-files`` output indicates that the Staging Index has not changed and retains the SHA 67cc52710639e5da6b515416fd779d0741e3762e we had earlier.


>see the other page :
 #### <p align="center">   [Collaborating](Tache_6.md) </p>
<p align="center" > Ismail Dakir with : ❤️</p>



