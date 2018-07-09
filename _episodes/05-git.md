---
title: "Version Control (git)"
teaching: 105
exercises: 15
questions:
- "How to keep track of changes in text files"
objectives:
- "Learn the basic commands of git to version control text files"
keypoints:
- "Version control systems were created to keep track of changes in a set of files."
- "They work better with text files"
---

# Version Control with Git

A version control system is a tool that keeps track of changes in a folder and all the files there in. That works by effectively creating different versions of our files. It allows us to decide which changes will be made to the next version (each record of these changes is called a commit), and keeps useful metadata about them. The complete history of commits for a particular project and their metadata make up a repository. Repositories can be kept in sync across different computers, facilitating collaboration among different people.

In scientific computing there are 3 typical scenarios where using a Version Control system is crucial in your effectiveness as researcher.

1. You write code, scripts and sometimes even data and you need to keep track on the changes on that code in case you need to go back and review for example, why a previous version was producing better results!.

2. You are writing a paper: Your paper will go into a spiral of reviews, by you, your collaborators, you PhD advisor,  the referees. If you are using LateX for you paper, as you probably should do, it is easy to keep track of changes and keep your paper in sync across several computers.

3. You are writing your Thesis, same principle, your manuscript will have several cycles of review and corrections. You do not want to keep all your precious PhD Thesis on a single place and you do not want to get lost figuring out which version is the last version!.

Version control systems can help you with this, they are designed to keep track of changes on files, specially text files. Even if they work also for binary files like figures and plots, they are not able to detect the internal changes on those binary files, each version of the file, even if the change is small is an entirely different file.

We will go quickly to cover the basics of Version control using git, there is a complete lesson on Git on Software Carpentry [Version Control with Git](http://swcarpentry.github.io/git-novice/), consider to follow the lesson for a more detailed coverage about what git can do for you.

For the purpose of this hands-on, we will create and work entirely o an local repository. You can otherwise create an account on Github and get the ability to create public repositories for free or private repositories for a fee. WVU Research Computing offers to researchers private repositories for free via an special agreement with Github.

This are the first commands to prepare your environment for using with Github:

~~~
git config --global user.name "<Your Full Name>"
git config --global user.email "<username>@mix.wvu.edu"
~~~
{.source}

The default editor for commits is `vim` and for the purpose of this introduction we will keep it like that.

Now, lets create a folder `project_01` that we will convert into a git repository so Git can store versions of our files.
Move inside the folder (`cd project_01`) and execute:

~~~
$ git init
~~~
{: .bash}

If we use `ls` to show the directory's contents you will see no new file apparently.

~~~
$ ls
~~~
{: .bash}

But if we add the `-a` flag to show hidden files and folders,
we can see that Git has created a hidden folder within `projexct_01` called `.git`:

~~~
$ ls -a
~~~
{: .bash}

~~~
.	..	.git
~~~
{: .output}

Git uses this special sub-directory to store all the information about the project,
including all files and sub-directories located within the project's directory.
If we ever delete the `.git` sub-directory, we will lose the project's history.
That folder is hidden for a good reason, in almost all circumstances, you are not suppose to manipulate the contents of the `.git` folder directly.

We can check that everything is set up correctly by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .bash}
~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

If you are using a different version of `git`, the exact
wording of the output might be slightly different.





{% include links.md %}
