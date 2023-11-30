> # ✅Collaborating 

##  1.Git pull:
The ``git pull`` command is used to fetch and download content from a remote repository and immediately update the local repository to match that content. Merging remote upstream changes into your local repository is a common task in Git-based collaboration work flows. The ``git pull ``command is actually a combination of two other commands, git fetch followed by ``git merge``. In the first stage of operation git pull will execute a git fetch scoped to the local branch that HEAD is pointed at. Once the content is downloaded, git pull will enter a merge workflow. A new merge commit will be-created and ``HEAD`` updated to point at the new commit.

### 🏁 Git pull usage: 
#####How it works
The ``git pull`` command first runs ``git fetch ``which downloads content from the specified remote repository. Then a ``git merge`` is executed to merge the remote content refs and heads into a new local merge commit. To better demonstrate the pull and merging process let us consider the following example. Assume we have a repository with a main branch and a remote origin.

![1](Images/pul1.png)

In this scenario, ``git pull ``will download all the changes from the point where the local and main diverged. In this example, that point is E. ``git pull`` will fetch the diverged remote commits which are A-B-C. The pull process will then create a new local merge commit containing the content of the new diverged remote commits.

![2](Images/pul2.png)

In the above diagram, we can see the new commit H. This commit is a new merge commit that contains the contents of remote A-B-C commits and has a combined log message. This example is one of a few git pull merging strategies. A ``--rebase`` option can be passed to ``git pull`` to use a rebase merging strategy instead of a merge commit. The next example will demonstrate how a rebase pull works. Assume that we are at a starting point of our first diagram, and we have executed ``git pull --rebase``.

![3](Images/pul3.png)

In this diagram, we can now see that a rebase pull does not create the new H commit. Instead, the rebase has copied the remote commits A--B--C and rewritten the local commits E--F--G to appear after them them in the local origin/main commit history.

***************