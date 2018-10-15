# Start versioning everything with git

In the software industry, every software goes through several versions during it's lifecycle. But how to efficiently keep track of changes and provide older versions for compatibility purpose? Sure, we can keep a large collection of .zip files, but there is a better way of doing it, it could apply to a lot more domains than the software industry:

## Version Control

Also known as 'revision control' or 'versioning', is a process to delegate the modifications tracking to a piece of software that will monitor every changes made to a project. Contributors can then read an history of those changes, get information about who did it and when, and eventually revert back to a former state of the project.

As these softwares has to be consciously manipulated by contributors, version control induce a workflow that has to be agreed upon amongst the team and that each collaborator will eventually have to learn. And I insure you that you will have great benefits to start learning the basics right now, whatever your level in programming actually is.

## Git

Git is the **version control system** initiated by Linus Torvald, it differentiates from older vcs like SVN or CVS byt it's **distributed** approach. That means that, unlike the centralized approach taken by CVS and SVN, each contributor has a complete repository of the project on her machine. There's no differences between these repositories, except for the current changes on which a contributor is working on, which then have to be propagated to every other repositories. For that reason, it is typical for team to use a distant repository as a 'main' repository to centralized all changes made by the team, but it is in no way enforced by Git. Just remember that everything repository is of equal importance and you can create just has many as you want.

As it started as Linus Torvald's project, Git naturally integrates within Linux systems, and may already be installed depending on the Linux distributions you use. If you use windows, you will have to install Git like any software, it will come packed with an command line interface to mimic Linux commands, called 'Git Bash', that you will use to interact with git. If you're not familiar with Linux command line interface, don't panic! The only commands you need are pretty basics:

- `ls` : List all the files and directories that are within the same directory in which you currently are (in command line interface, you are always inside a directory of your system)
- `cd directory_name` : Change the current directory to the directory called "directory_name" (in this example), this directory must be inside the directory where you currently are
- `cd path/to/your/directory` : Does the same thing, but allow you to navigate through several directories in one commande, in the example, we will end up in the "directory" directory, which is inside the "your" directory, which is in turn inside the "to" directory, etc.
- `cd ..` : Allows you to move in the parent directory from the directory where you currently, you can combine it in a path, for example: `cd ../my/directory` which will move one directory up from your current position then inside the "my" directory then inside the "directory" directory

All this will quickly become natural after some wandering inside your directories. There are tools that plugs on Git to give it a graphical interface, such as the basic *Git GUI* that comes with your Windows installation or the fancier *GitKraken* that cost some bucks but is renown to be worth it, but you have to know the name of the commands to execute anyway, so it's best to start with the command line (plus it'll make you feel like a badass hacker).

I've never used Git on a Mac (in fact, I've never used anything on a Mac ...) so I won't tell you how to do that, but if you've found that obscure post from an unknown geek in a shadowy corner of the web, I trust you to be able to find a helpful installation tutorial in shinier places of the world wide web.

## Initialize a project

Let's start by some basics. I've said that you can apply version control to much more than programming projects, I'll use my blog posts as an example.

The reason why you're able to use Git with either source code or plain text posts is because what Git care about could be summarized as, in Git words :

- trees (folders/directory) : the structural parts of the project, trees contains either other trees (sub-trees) or:
- blobs (files) : the parts of the project that gives it a point, files can be either binaries or text files, but Git works a lot better with the later, see the explication below.

Here a representation of my folders structure:

    blog-posts
		|- en
		||- some-post.md
		||- another-post.md
		|-fr
		||- some-post-translated.md

I want Git to track the totality of my blog posts, as I consider my project to be the blog and not each individual post. To do that, I start a terminal/git bash prompt in the folder "blog-posts" (you can do that by right clicking usually). To be sure that I'm in the correct folder, I type the command `ls` and I shall see my two sub-folders "en" and "fr". Then I start a Git project with the command `git init`.

The terminal then informs you that you have successfully initialized a git project, but you don't see no changes if you look at you file explorer, right? That's because all the Git relatives files have been stored in a hidden folder labeled ".git". To see it you can use the command `ls` but with the option "a" (for "all", I suppose), so type `ls -a`.

This folder contains a complete copy of your project in the state it was when you initialized it, which should be the same state as it actually is. To make sure of that, you can use the command `git status` and the terminal should answer you that "nothing changed".

A complete copy of the project in the exact same state doesn't look like a bright idea, does it? You should loose an awful lot of space by duplicating every project like this... Well don't worry for that, everything in the ".git" folder is compressed to optimize space and the files are really small in fact. And to be exact, that's not one copy that you have in this folder, but actually two! There is:

- the project in it's last state (the *HEAD*)
- the changes about to be stored (the *index*)

And if you had the actual directory in which you are working (the ... *working directory*), that's three times the same project in the same place. And more copies will be coming each time you will make a modification to the files! That's how it goes in the version control world, you don't just update your work, but create new copies of it each time you want to make a modification. Still don't worry with space consumption though, Git is smart and optimize it very nicely.

## Basic Git workflow

To summarize the three trees talked just above, I made you a little scheme. These trees are crucial in understanding the internal working of Git.

![Three trees monitored by Git](start-git-fig01.svg)

As you can see, both trees are almost exactly the same, except that, as I'm actually writing this post, it appears in the *working directory*. I've had put quite some content in this post to this point, I feel I should store the modifications to the project right now (in fact, I should have had as soon as I started writing).

If I use the `git status` command at this point, Git will inform me that it have noticed a new file in my working directory (or should I say, a new *blob* in my "working directory" *tree*). To propagate the change to the other trees, I have to first inform the *index* of those changes. So I will type:

    git add en/start-git.md

Now, if I type `git status` again, Git will inform me that the file "start-git.md" has been added to the index, and is ready to be *committed*. That last word should have raised your curiosity, otherwise you are not paying attention, shame on you! So refocus, because you gonna hear this word in almost every line you gonna read about Git from that point.

The *commits* are the copies of your project that Git keeps for you. You can think of these as "snapshots", once you've *committed* your work, a new copy of your project is created and it is \*almost\* set in stone. To *commit* (I've said you gonna hear this word a lot!) my work, I type:

  git commit

Okay, I should explain this command a little more in details: you now understand the word *commit*, even if you don't realize everything it implies, just remember it creates a copy **of the index tree**. So because I added my file to the *index* with the former command (remember, `git add`), Git understood what *blobs* I wanted to *commit* when I typed this command.

As you're smart and attentive, you have realized that I wrote a little more text between the moment I added changes to the *index*, and the moment I made my *commit*. You probably think that this text couldn't have been added in the *commit*, since the *index* hasn't been updated to include it... and you're totally right! To inspect the content of the last *commit* I type:

    git show

Then I can read the changes that have been *committed*, those written in green and preceded by a "+" are lines that were added, where those written in red and preceded by a "-" sign are lines that were deleted (if any). If lines are modified, git will simply consider that they were deleted and added again. I won't show you the output of my terminal here since it is basically this post from the beginning to `git add en/start-git.md`. But that's what we were searching for, changes between `git add en/start-git.md` and `git commit` are not present in the *commit*.

***Note:*** _When using `git show`, your terminal will be in reading mode, that lets you goes up and down the document with your keyboard's arrows, you can quit this mode by hitting 'q'._

## Going on

I bet that not everything is cristal clear for you at the moment and you may still have unanswered questions that have rose from what I wrote previously. But as I wrote a little more since my last committed work, let's *commit* these changes:

    git add en/start-git.md
		git commit -m "New chapter 'Going on'"
