> # ⬛Undoing changes
## <p >Git revert</p>
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