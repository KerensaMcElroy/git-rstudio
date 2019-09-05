---
layout: episode
title: Sharing repositories online
teaching: 30
exercises: 35
questions:
  - How can I clone a public repository to my computer?
  - How can I set up a public repository online?
objectives:
  - To get a feeling for remote repositories.
  - Learn how to publish a repository on the web.
  - Learn how to fetch and track a repository from the web.
keypoints:
  - "A repository can have one or multiple remotes."
  - "A remote serves as a full backup of your work."
  - "`git clone` initialises a repository using content from somewhere else."
  - "`git push` sends local changes to the remote."
  - "`git pull` gets remote changes onto your local machine."
  - "A remote allows other people to collaborate with you."
---

In this episode, we will learn about putting git repositories on the web and will publish our 
guacamole recipe. Don't worry, you will be able to remove it afterwards.

## From our laptops to the web

We have seen that **creating Git repositories and moving them around is
simple** and that is great.

So far everything was local and all snapshots are saved under `.git`.

If we remove `.git`, we remove all Git history of a project.

But...
- What if the hard disk fails?
- What if somebody steals my laptop?
- How can we collaborate with others across the web?

---

## Remotes

To store your git data on another computer, you use **remotes**.  A
remote is like making another copy of your repository, but you can choose to only
**push** the changes you want to the remote and **pull** the changes you need
from the remote.

You might use remotes to:
- Back up your own work.
- To collaborate with other people.

There are different types of remotes:
- [GitHub](https://github.com) is a popular, closed-source commercial site.
- [GitLab](https://about.gitlab.com) is a popular, open-core
  commercial site.  Many universities have their own private GitLab servers
  set up.
- [Bitbucket](https://bitbucket.org) is yet another popular commercial site.
- CSIRO has an enterprise bitbucket server [bitbucket.csiro.au](bitbucket.csiro.au)

---

## GitHub

One option to host your repository on the web is [GitHub](https://github.com).

GitHub is a for-profit service that hosts remote git repositories for you. It
offers a nice HTML user interface to browse the repositories and handles many
things very nicely.

It is free for public projects and hosting private projects costs a monthly fee
(but educational discounts exist). The free part of the service has made it
very popular with many open source providers.

---

## Set up GitHub account

By now you should already have set up a GitHub account but if you haven't,
please do so [here](https://github.com/join). 

---

## Cloning a repository

Once a repository is on a public service like GitHub, other people can **clone** (make a local copy)
of this repository and contribute changes. To clone a repository in RStudio, create a New Project, 
then select "Version Control" followed by "Git". The Repository URL can be found on GitHub using 
the "Clone or download" button ![]({{ site.baseurl }}/fig/07-clone-button.png){:height="40px"}{:style="display: inline; margin:0px"}
and will end in `.git`.

Think of cloning as downloading the `.git` folder to your computer. After downloading the `.git` 
folder, the files from the latest commit are created in your working directory. This means that you 
will have the most up to date of all the files, as well as the complete Git history contained within
the repository.

We have already seen an example of a repository on GitHub, let's clone it and explore

> ## Challenge 1
> Create a new RStudio project that clones the [example repository](https://github.com/csiro-data-school/example-repo)
> we looked at earlier.
> Using the tools you have learned within RStudio, explore the repository to answer the following 
> questions:
> 
> 1. How many files are now in your working directory?
> 2. How many files were initially added to the repository?
> 3. How many commits ago was the commit by Stephen?
> 4. What did that commit change and why?
>
> > ## Solution to Challenge 1
> > The repository can be cloned using the URL `https://github.com/csiro-data-school/example-repo.git`
> > 
> > 1. Six files are created. `.gitignore`, `data/cows.csv`, `data/cows_weight_sqrt.csv`, `example-repo.Rproj`
> > `README.md`, and `scripts/cows-analysis.R`.
> > (Although if you look at the Git status pane, you will see that the `.gitignore` and `.Rproj` files
> > are untracked by Git and are not actually in the repository. These are created by RStudio when you
> > set up a new project)
> > 
> > 2. Two files, the `README.md` and `data/cows.csv` files, were added in the initial commit.
> >
> > 3. The commit by Stephen (SHA 0afb6d7b) was made three commits ago.
> > 
> > 4. It added lines to the `scripts/cows-analysis.R` files (lines 8-11 at the time) to get the 
> > mean and standard deviation of each weight.
> {: .solution}
{: .challenge}

Now that we have seen how to download a repository already existing on GitHub, how can we get our 
own on there? In order to do that, we need to take three steps:

1. Create a new repository on GitHub
2. Link it to our local repository
3. "Push" and "pull" changes to keep the local and GitHub repositories synced up

## Create a new repository on GitHub

1. Login
2. Click on "Repositories"
3. Click on the green button "New"

On this page choose a project name (screenshot).

For the sake of this exercise **do not select**
"Initialize this repository with a README" (what will happen if you do?).

![create new repo on github]({{ site.baseurl }}/fig/github/1.jpg)

Once you click the green "Create repository", you will see a page similar to:

![github repo setup page]({{ site.baseurl }}/fig/github/2.jpg)

This has created an empty repository on GitHub and provides some hints about how you can fill it.


## Linking our local repository to GitHub

To be able to send our local changes to GitHub, we need to tell the local repository that the one we
just created on GitHub's servers exists. To do this, we create a 'remote'. Git repositories can have
any number of remotes, although it is by far the most common to only use one. Each git remote is 
given a name so that it can be referred to easily. The default remote name is `origin`.

You'll see that GitHub has given us the instructions for how to do this under the option

> **... or push an existing repository from the command line**

You *could* copy those commands and paste them into a shell window ("More">"Shell" from the Git pane),
but we will show you a way to achieve the same result using the RStudio interface to run the 
commands.

1. Open up the guacamole project on your computer.
2. Click the "New Branch"" button in the Git pane ![]({{ site.baseurl }}/fig/07-branch-button.png){:height="35px"}{:style="display: inline; margin:0px"}
and select "Add Remote".
  
    (We will probably not have time to discuss branches, but this is also where you can set up a remote
    repository)

3. For the "Remote name", enter `origin`, and for the "Remote URL" enter the URL shown on GitHub
when you set up the repository (will look something like `https://github.com/<USER>/<REPO_NAME>.git`).
Click "Add" to set the GitHub repository as your remote

4. The default branch name for your repository is `master`. Put that as the branch name in the next
dialog box, ensure that "Sync branch with remote" is checked and click "Create". 

    > It will complain about the local branch already existing. Select "Overwrite" from the options
    > it provides. 
    {: .callout}

You should now see some logging information that ends with the line:

```
Branch master set up to track remote branch master from origin.
```

**Reload your GitHub project website and - taa-daa - your commits should now be
online!**

What just happened? **Think of publishing a repository as uploading the `.git` part online**.

In the first instance, we provided a URL as the address where we want to upload the repository. Then
we uploaded the data and could access our Git history through GitHub.

After this initial setup, the GitHub repository will be remembered as the remote repository for your
project. In Github terminology, when uploading changes from your machine to the remote you `push` the
changes. When downloading changes from the remote to your machine, you `pull` them. 

Not that the remote URL is set, we can use the Pull/Push buttons to perform these steps ![]({{ site.baseurl }}/fig/07-push-pull.png){:height="30px"}{:style="display: inline; margin:0px"}.


> ## Challenge 2
>
> Make a change to your project and commit the changes locally. 
>
> Push the changes to your GitHub remote.
> 
> What information can you access about the commit you just made?
{: .challenge}

## Getting changes from the remote

Of course we don't want information to only go one way - if the remote has changes to the project 
from a collaborator we need to get those onto our local machine. To do this, we're doing the 
opposite of a `push`, so it's helpfully called a `pull`.

> ## Challenge 3
> 
> Make a change to your repository using the GitHub web interface (look for the pencil icon to edit a file).
>
> Once you've made a change, use the "Pull" button to get the changes onto your local machine.
>
> Inspect the history to confirm that you have incorporated the change from online in your local files.
{: .challenge}

> ## Discussion: security
> 
> Slack poll: is your data "confidential", "in between", or "open"? Talk about strategies for each.
> Consider how you might use your `.gitignore` file, and remotes like the CSIRO bitbucket. 
> 
{: .discussion}


