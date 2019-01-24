# Start versioning everything with git

In the software industry, every software goes through several versions during it's lifecycle. But how to efficiently keep track of changes and provide older versions for compatibility purpose? Sure, we can keep a large collection of .zip files, but there is a better way of doing it, it could apply to a lot more domains than the software industry:

## Version Control

Also known as 'revision control' or 'versioning', it's a process to delegate the modifications tracking to a piece of software that will monitor every changes made to a project. Contributors can then read an history of those changes, get information about who did it and when, and eventually revert back to a former state of the project.

As these softwares has to be consciously manipulated by contributors, version control induce a workflow that has to be agreed upon amongst the team and that each collaborator will eventually have to learn. And I insure you that you will have great benefits to start learning the basics right now, whatever your level in programming actually is.

## Git

Git is the **version control system** initiated by Linus Torvald, it differentiates from older vcs like SVN or CVS byt it's **distributed** approach. That means that, unlike the centralized approach taken by CVS and SVN, each contributor has a complete repository of the project on her machine. There's no differences between these repositories, except for the current changes on which a contributor is working on, which then have to be propagated to every other repositories. For that reason, it is typical for team to use a distant repository as a 'main' repository to centralized all changes made by the team, but it is in no way enforced by Git. Just remember that every repository is of equal importance and you can create just has many of them as you want.

As it started as Linus Torvald's project, Git naturally integrates within Linux systems, and may already be installed depending on the Linux distributions you use. If you use windows, you will have to install Git like any software, it will come packed with an command line interface to mimic Linux commands, called 'Git Bash', that you will use to interact with git. If you're not familiar with Linux command line interface, don't panic! The only commands you need are pretty basics:

- `ls` : List all the files and directories that are within the same directory in which you currently are (in command line interface, you are always inside a directory of your system)
- `cd directory_name` : Change the current directory to the directory called "directory_name" (in this example), this directory must be inside the directory where you currently are
- `cd path/to/your/directory` : Does the same thing, but allow you to navigate through several directories in one commande, in the example, we will end up in the "directory" directory, which is inside the "your" directory, which is in turn inside the "to" directory, etc.
- `cd ..` : Allows you to move in the parent directory from the directory where you currently, you can combine it in a path, for example: `cd ../my/directory` which will move one directory up from your current position then inside the "my" directory then inside the "directory" directory

All this will quickly become natural after some wandering inside your directories. There are tools that plugs on Git to give it a graphical interface, such as the basic *Git GUI* that comes with your Windows installation or the fancier *GitKraken* that cost some bucks but is renown to be worth it, but you have to know the name of the commands to execute anyway, so it's best to start with the command line (plus it'll make you feel like a badass hacker).

I've never used Git on a Mac (in fact, I've never used anything on a Mac ...) so I won't tell you how to do that, but if you've found that obscure post from an unknown geek in a shadowy corner of the web, I trust you to be able to find a helpful installation tutorial in shinier places of the world wide web.

## Initialize a project

Let's start by some basics. I've said that you can apply version control to much more than programming projects, I'll use my blog posts as an example.

The reason why we're able to use Git with either source code or plain text posts is because what Git care about could be summarized as, in Git words :

- *trees* (folders/directory) : the structural parts of the project, trees contains either other trees (sub-trees) or:
- *blobs* (files) : the parts of the project that gives it a point, files can be either binaries or text files, but Git works a lot better with the later.

Here a representation of my folders' structure:

    blog-posts
		|- en
		||- some-post.md
		||- another-post.md
		|-fr
		||- some-post-translated.md

I want Git to track the totality of my blog posts, as I consider my project to be the blog and not each individual post. To do that, I start a terminal/git bash prompt in the folder "blog-posts" (you can do that by right clicking usually). To be sure that I'm in the correct folder, I type the command `ls` and I shall see my two sub-folders "en" and "fr". Then I start a Git project with the command :

    git init

The terminal then informs me that I have successfully initialized a git project, but I don't see no changes if I look at it in my file explorer... That's because all the Git relatives files have been stored in a hidden folder labeled ".git". To see it I can use the command `ls` but with the option "a" (for "all", I suppose), so I type `ls -a`.

This folder contains Git's data related to this project, such as a very important part of Git that is the *index*. In time, this will be a complete copy of my project which will store every changes I want to keep permanently, but as I just initialized my *repository*, it is totally empty. I can view the differences between the version I'm working on, which is called in Git terms the *working tree* (sometimes called the *working directory* as well) and the *index* by typing the command:

    git status

Yes, right now, both *trees* are totally different. That's normal as I just initialized a *git repository*, because Git only does its magic while I ask it to do so, good puppy.

You may wonder if a complete copy of the project is a bright idea, don't you? We should loose an awful lot of space by duplicating every project like this... Well don't worry for that, everything in the ".git" folder is compressed to optimize space and the files are really small in fact. And in fact there will be many more copies of the project as I start to *version* it! Let's see how it goes:

## Basic Git workflow

Okay, to summarize what we've talked about so far, here is a little scheme :

![Three trees monitored by Git](start-git-fig01.png)

As you can see, both trees are almost exactly the same, except that, as I'm actually writing this post, it appears in the *working directory*. I've had put quite some content in this post to this point, I feel I should store the modifications to the project right now (in fact, I should have had as soon as I started writing).

If I use the `git status` command at this point, Git will inform me that it have noticed a new file in my working directory (or should I say, a new *blob* in my "working directory" *tree*). To propagate the change to the other trees, I have to first inform the *index* of those changes. So I will type:

    git add en/start-git.md

Now, if I type `git status` again, Git will inform me that the file "start-git.md" has been added to the index, and is ready to be *committed*. That last word should have raised your curiosity, otherwise you are not paying attention, shame on you! So refocus, because you gonna hear this word in almost every line you gonna read about Git from that point.

![The index tree is updated](start-git-fig02.png)

The *commits* are the copies of your project that Git keeps for you. You can think of these as "snapshots", once you've *committed* your work, a new copy of your project is created and it is \*almost\* set in stone. To *commit* (I've said you gonna hear this word a lot!) my work, I type:

  git commit

Okay, I should explain this command a little more in details: you may guess now what the word "commit" stand for, even if you don't realize everything it implies, just remember it creates a copy **of the index tree**. So because I added my file to the *index* with the former command (remember, `git add`), Git understood what *blobs* I wanted to *commit* when I typed this command.

![The changes have been committed](start-git-fig03.png)

As you're smart and attentive, you have realized that I wrote a little more text between the moment I added changes to the *index*, and the moment I made my *commit*. You probably think that this text couldn't have been added in the *commit*, since the *index* hasn't been updated to include it... and you're totally right! To inspect the content of the last *commit* I type:

    git show

Then I can read the changes that have been *committed*, those written in green and preceded by a "+" are lines that were added, where those written in red and preceded by a "-" sign are lines that were deleted (if any). If lines are modified, git will simply consider that they were deleted and added again. I won't show you the output of my terminal here since it is basically this post from the beginning to `git add en/start-git.md`. But that's what we were searching for, changes between `git add en/start-git.md` and `git commit` are not present in the *commit*.

***Note:*** _When using `git show`, your terminal will be in reading mode, that lets you goes up and down the document with your keyboard's arrows, you can quit this mode by hitting 'q'._

## The Git goes on

I bet that not everything is cristal clear for you at the moment and you may still have unanswered questions that have rose from what I wrote previously. But as I wrote a little more since my last committed work, let's *commit* these changes:

    git add en/start-git.md
		git commit -m "New chapter 'Going on'"

What's that `-m` followed by a message? You may ask. That is a ... **message**. Yup, that's all it is, me writing for myself in order to remember what I committed. Because I have now two *commits* and will have several more as the project goes on, so I better start writing what I did in each *commit*. I can visualize my *commit* history in my terminal by typing:

    git log

And this is what Git shows me:

		commit b6a083df24f44af9d2fa6423108ae58669245297
		Author: raaaahman <contact@devindetails.com>
		Date:   Mon Oct 15 12:35:44 2018 +0200

		    New chapter 'Going on'

		commit 7aaca9131ea03d129380edc68f946e19d2c017d8
		Author: raaaahman <contact@devindetails.com>
		Date:   Sun Oct 14 14:42:28 2018 +0200

Let's review what we have here. This is a list of *commits*, it is sorted by descending date order. For each *commit* you have several informations:
- It's **SHA-1**: this is an unique identifier for this *commit*, it is automatically generated.
- The **author**'s name and e-mail, so we know who committed the changes.
- The **date** when the changes were committed
- Eventually, the **message** that the author have written so anyone can know whats were the changes about

At the moment this is a simple blog post written by a single author and only two commits have been added. I can postpone that each *commit* will be about me adding more text to the post and things will be simple and linear. But in a larger project, with numerous features and several *authors*, you can imagine how important it is that each *author* should write **explicit messages** each time she commits some changes, so her collaborators won't have to inspect the files to know what were the changes about.

On that matter, I couldn't resist to present you the [conventional commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/) initiative, which is an interesting idea to rationalize and normalize commits messages. This may seem a bit too directive when you just start to write your first *commits*, but you may quickly see the benefits of adopting it right of the bat (or your colleagues may appreciate you even more for it). I'll try to give you an overview of what it is about:

Like a well organized article, *conventional commit*'s messages are composed of a *header*, a *body*, and a *footer*. The header contains a label that indicate the **type** of the commit, and a short **description** of what this commit is about. The *type* is a quick way to categorize the kind of work that have been done, like adding a feature, fixing some bug or adding documentation to the existing code, while the *description* tell where this work have been applied and what changes it introduces.

Basically, I can stop my commits messages at this stage, and most commits messages should be that short. Because Git is a smart***, and it already knows every change I've made to my project. But Git is gullible, and if I ask nicely, it will display me the changes. I'm gonna ask it like that:

 		git show

Now Git outputted in my terminal every change I've made in it's habitual fashion (that's said, lines deleted start with a "-" and are colored in red, and lines added start with a "+" and are colored in green, it also show some unmodified lines just to give context around the modified ones). As I've made several grammar corrections here and there, I can't show you the whole log, because it's quite long, but I'll give you an overview:

![The result of the command 'Git show' in my terminal](assets/start-git-en-04_show.png)

Okay, that should do for another chapter, so guess what I'll do now? Right, I will commit it to my project.

		git add en/start-git.md
		git commit -m "Chapter 'Git goes on' finished"

***Note:*** _As an attentive reader, you have noticed that I didn't write my commits messages using the conventional commits ... conventions. Albeit I've adopted it in my programming projects, I feel it makes doesn't really makes sense in the context of a blog. That's a preference and that's usually something that have to be discussed among a team. Feel free to read a bit more about these writing rules, they are light but I haven't told you them all, neither have I listed all their benefits._

## Getting fancy

The last command I've used (`git show`) has been able to show me the change I've made in my last commit. That's a cool feature, but as I've shown you in a former command (`git log`), the project contains more than one commit, and I've added a new since I typed these commands. So, how can I see what I've committed in the previous commits?

One solution would be to `git log` my commits, copy the *SHA-1* (remember, the unique identifier for the commit) for this specific commit and then paste it to the `git show` command, like this:

	git log
	git show 3bba4ec8f814f84ea8782f014b01da81e6cfabde

And I can see every changes that were committed in this commit. That's the usefulness of the *SHA-1* identifier, it is generated by Git and is insured to be absolutely unique, so Git can retrieve the specific commit even if my project would have contained thousand of them (and I hope it will in the future!).

But this suite of hexadecimal numbers are far from being easy to remember by human beings, don't you find? (Yes, in hexadecimal notation, letters from "a" to "f" are numbers too!) Don't worry, there are simpler ways to retrieve the same information, like this command:

	git show HEAD~1

What this do is that it will output the changes committed in the commit preceding the last one. But you may still be confused by the syntax used here, don't you? In fact, you've encountered the fourth fundamental object of Git, which is a **ref** (remember we already have *trees* -folder structures-, *blobs* -binary/text files- and *commits*). *Refs* doesn't really exists by themselves, but instead, they **reference** another Git object so we, users, can access to these objects with an easier notation than *SHA-1*.

The *ref* **HEAD** is a very useful one, as it basically points towards the **last commit you've made**.  But typing `git show HEAD` would be pretty useless, since `git show` already output the last commit if no arguments are passed to it.

What I did instead was mentioning that I wanted to go one commit backward from the HEAD, which is what the `~1` syntax means. You probably have guessed that I can go back as far as my project contains commits by typing `git show HEAD~2`, `git show HEAD~3`, etc. This useful for the `git show` command, but to a plethora of other commands that I won't list here (mainly because I don't know them all or very well, and also because I can't teach you the totality of Git in a single blog post).

Speaking of blog post's length, I feel you may have quantity of information to process at that point (or maybe I just feel lazy to write some more), so I will let you play around with that for now. I hope I've motivated you to take your first step with Git, because I feel it's a crucial tool in an everyday job of developer, and maybe it can save some hassle for other jobs too. I may write some more about it, as I'm far from having covered even it's most common usages in this single post, so stay tuned! But before I go, you've guessed what:

		git add en/start-git.md
		git commit -m "Chapter 'Getting fancy' finished"
