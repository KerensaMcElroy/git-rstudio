---
layout: episode
title: Fixing mistakes
teaching: 30
exercises: 35
questions:
  - How can I fix mistakes with Git?
  - What sort of mistakes can be fixed using Git within RStudio?
objectives:
  - Learn to undo changes safely
  - See when changes are permanently deleted and when they can be retrieved
keypoints:
  - "Git history can be reverted without modifying it"
  - "Changes that are not committed can be deleted permanently"
  - "Once changes are committed they are safe"
  - "Sometimes, you just need to burn it all down and start again"
---

## Undoing things

The whole point of version control is that you can see and retrieve previous snapshots of your work.

With Git, if you have committed (made a snapshot) of a file, you can get it back, even if it gets 
deleted or modified in the future.

If changes are **uncommitted**, they are not safe, and when they are deleted, they are gone.

The ability to reverse mistakes in Git is very sophisticated, however more advanced usage 
will require calling Git from the command line. For our purposes, there are three sort of mistakes 
we can look at resolving from within RStudio:

1. Mistakes that **have** been committed
2. Mistakes that have broken your Git repository
3. Mistakes that **have not** yet been committed

----

### Reverting commits

Imagine that we have made a few commits, but realized that the latest commit was a mistake and we 
wish to undo it. Because Git stores the state of each file at every commit, it is easy to return to 
any point in time.  

In the History window, there is a link to show the contents of a file at any specific commit 
![]({{ site.baseurl }}/fig/09-revert-commit.png){:height="30px"}{:style="display: inline; margin:0px"}. Open that link
and you are able to overwrite the current contents of the file with the historical version. You can 
also access just the history of changes for that file from this window if you are having trouble finding
the exact version you want.

Save, stage and commit this change and you have reverted the file to its older state.

> ## Challenge: revert a commit
>
> Make a new commit in your guacamole repo (it can be whatever you like)
> 
> Inspect the history, and revert the commit. 
{: .challenge}

This same process will allow you to return any deleted files to your working directory.

> ## Challenge: recover a deleted file
> 
> How much do you trust Git...?
> 
> Delete one (or more) of your committed files using any method you like.
> 
> Can you get it/them back?
{: .challenge}

-----

### Starting over

Learning Git can be hard. As a beginner you are unlikely to actually mess up your files, but you may 
end up in a situation where you have made an error with Git and now can't work out how to fix your
repository. There are two options here:

1. **Searching online for a solution.** In your search terms, make sure to include 'RStudio' or you will 
end up with complicated instructions on how to solve the problem using Git from the command line (e.g. green writing on a black background). This is a good opportunity for a learning experience, however can be time consuming. 
2. **Save, delete, and start again.** Sometimes we just need a problem solved quickly so we can get on with our work. An effective approach in this situation is demonstrated in this [xkcd comic](https://xkcd.com/1597/: 
![](https://imgs.xkcd.com/comics/git.png)

Under approach (2), your remote repository acts as a fallback that you will return to in the case
of major issues. Save any changes you want to keep locally elsewhere, then start again by cloning 
the remote repository. Now you are free to delete the old, broken version and start fresh.

Testing out this approach now should help reduce the stress if you find yourself needing it in the 
future.

> ## Challenge: save, clone, delete
> - Make sure your local and remote repositories are all synced up with a pull/push
> - Make a change to your local files
> - Let's assume that you have now broken your local repository
> - Save your change somewhere else
> - Create a new RStudio project and clone your work from your remote repository
> - Reintroduce your change from the saved file
{:.challenge}

### Undo unstaged/uncommitted changes

This situation should rarely occur with the RStudio/Git workflow, but in case it does, here is how you can resolve it.

> ## DANGER!! 
> Changes that have not been committed will be deleted permanently and cannot be recovered by Git.
{:.callout}

#### Unstaged changes

The simplest situation is where you have modified a file, but not yet staged the changes. In this 
case, it is easy to roll the file back to the last committed state by selecting it in the Git pane
and using the "Revert" button ![]({{ site.baseurl }}/fig/09-revert-button.png){:height="30px"}{:style="display: inline; margin:0px"}
from the "More" menu.

> ## Challenge: delete unstaged change
> - Make a silly change to repo, do not stage it or commit it.
> - Inspect the change in the Status and Diff windows.
> - Now undo the change using the "Revert" button
> - Verify that the change is gone.
{: .challenge}

#### Some staged changes

If you have staged the changes but still want to reverse everything you have done, the process is 
exactly the same.

It becomes more complicated if we want to retain some staged changes, but *can* be done using the 
Diff window. Let's consider the situation where we have staged some sensible changes to our project,
but then made an unstaged mistake. Following the process above would lead to us losing the staged 
changes that we want to keep.

> ## Challenge: delete parts of a change
> - Make a reasonable change to the project, stage it.
> - Then make a silly change but do not stage it.
> - Inspect the situation in the Diff window. In particular, swap between staged and unstaged changes 
> with the radio buttons ![]({{ site.baseurl }}/fig/09-staged-unstaged.png){:height="30px"}{:style="display: inline; margin:0px"}.
> - Swap to the Unstaged changes and remove them with the "Unstage chunk" button
> - Inspect the new situation to confirm that your silly change has been removed, but the sensible one is retained.
{: .challenge}

---
