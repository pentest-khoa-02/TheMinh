# What is Git?
* The most widely used modern version control system in the world today is Git. Git is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel.

* In addition to being distributed, Git has been designed with performance, security and flexibility in mind.

# Why use Git for your organization?
## Feature branch workflow
* One of the biggest advantages of Git is its branching capabilities. Unlike centralized version control systems, Git branches are cheap and easy to merge. This facilitates the feature branch workflow popular with many Git users.

* Feature branches provide an isolated environment for every change to your codebase. When a developer wants to start working on something—no matter how big or small—they create a new branch. This ensures that the main branch always contains production-quality code.

* Using feature branches is not only more reliable than directly editing production code, but it also provides organizational benefits. They let you represent development work at the same granularity as your agile backlog. For example, you might implement a policy where each Jira ticket is addressed in its own feature branch.

## Distributed development
* Git is a distributed version control system. Instead of a working copy, each developer gets their own local repository, complete with a full history of commits.

* Having a full local history makes Git fast, since it means you don’t need a network connection to create commits, inspect previous versions of a file, or perform diffs between commits.

* Distributed development also makes it easier to scale your engineering team. Everybody can continue going about their business in their own local repositories.

* And, similar to feature branches, distributed development creates a more reliable environment. Even if a developer obliterates their own repository, they can simply clone someone else’s and start anew.

## Pull requests
* A pull request is a way to ask another developer to merge one of your branches into their repository. This not only makes it easier for project leads to keep track of changes, but also lets developers initiate discussions around their work before integrating it with the rest of the codebase.

* Since they’re essentially a comment thread attached to a feature branch, pull requests are extremely versatile. When a developer gets stuck with a hard problem, they can open a pull request to ask for help from the rest of the team. Alternatively, junior developers can be confident that they aren’t destroying the entire project by treating pull requests as a formal code review.

## Community
* In many circles, Git has come to be the expected version control system for new projects. If your team is using Git, odds are you won’t have to train new hires on your workflow, because they’ll already be familiar with distributed development.

* In addition, Git is very popular among open source projects. This means it’s easy to leverage 3rd-party libraries and encourage others to fork your own open source code.

## Faster release cycle
* The ultimate result of feature branches, distributed development, pull requests, and a stable community is a faster release cycle. These capabilities facilitate an agile workflow where developers are encouraged to share smaller changes more frequently. In turn, changes can get pushed down the deployment pipeline faster than the monolithic releases common with centralized version control systems.

* As you might expect, Git works very well with continuous integration and continuous delivery environments. Git hooks allow you to run scripts when certain events occur inside of a repository, which lets you automate deployment to your heart’s content. You can even build or deploy code from specific branches to different servers.

* For example, you might want to configure Git to deploy the most recent commit from the develop branch to a test server whenever anyone merges a pull request into it. Combining this kind of build automation with peer review means you have the highest possible confidence in your code as it moves from development to staging to production.

# The three states of Git
## The three main states of a Git project: the working tree, the staging area, and the Git directory.

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%203/images/1.jpg" width="666px" align="center">

* The working tree is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.
* The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the “index”, but the phrase “staging area” works just as well.
* The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer.
* The basic Git workflow goes something like this:
    - You modify files in your working tree.
    - You selectively stage just those changes you want to be part of your next commit, which adds only those changes to the staging area.
    - You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

# Install Git
## For Windows
* Download and install the lastest at: https://gitforwindows.org/
## For Linux

* Debian / Ubuntu (apt-get)
```sh
$ sudo apt-get update
$ sudo apt-get install git
```

* Fedora (dnf/yum)
```sh
$ sudo dnf install git
// or
$ sudo yum install git
```

* Verify the installation was successful by typing git --version:
```sh
$ git --version
git version 2.9.2
```

# Git cheat sheet
## Git init
* The git init command creates a new Git repository. It can be used to convert an existing, unversioned project to a Git repository or initialize a new, empty repository. Most other Git commands are not available outside of an initialized repository, so this is usually the first command you'll run in a new project.

* Executing git init creates a .git subdirectory in the current working directory, which contains all of the necessary Git metadata for the new repository. This metadata includes subdirectories for objects, refs, and template files. A HEAD file is also created which points to the currently checked out commit.

### Usage
```sh
git init
```

* Transform the current directory into a Git repository. This adds a .git subdirectory to the current directory and makes it possible to start recording revisions of the project.

```sh
git init <directory>
```

* Create an empty Git repository in the specified directory. Running this command will create a new subdirectory called ＜directory＞ containing nothing but the .git subdirectory.

## Git clone
### Git clone is a Git command line utility which is used to target an existing repository and create a clone, or copy of the target repository:
* Cloning a local or remote repository

* Cloning a bare repository

* Using shallow options to partially clone repositories

* Git URL syntax and supported protocols

### Usage

```sh
git clone ssh://john@example.com/path/to/my-project.git 
cd my-project 
```

* Cloning to a specific folder

```sh
git clone <repo> <directory>
```

Clone the repository located at ＜repo＞ into the folder called ~＜directory＞! on the local machine.

* Cloning a specific tag
```sh
git clone --branch <tag> <repo>
```
Clone the repository located at ＜repo＞ and only clone the ref for ＜tag＞.

## Git remote
* The git remote command lets you create, view, and delete connections to other repositories. Remote connections are more like bookmarks rather than direct links into other repositories. Instead of providing real-time access to another repository, they serve as convenient names that can be used to reference a not-so-convenient URL.

### Viewing git remote configurations

```sh
git remote
```

List the remote connections you have to other repositories.

```sh
git remote -v
```

Same as the above command, but include the URL of each connection.

* Creating and modifying git remote configurations
The git remote command is also a convenience or 'helper' method for modifying a repo's ./.git/config file. The commands presented below let you manage connections with other repositories. The following commands will modify the repo's /.git/config file. The result of the following commands can also be achieved by directly editing the ./.git/config file with a text editor.

```sh
git remote add <name> <url>
```

Create a new connection to a remote repository. After adding a remote, you’ll be able to use ＜name＞ as a convenient shortcut for ＜url＞ in other Git commands.

```sh
git remote rm <name>
```

Remove the connection to the remote repository called ＜name＞.

```sh
git remote rename <old-name> <new-name>
```

Rename a remote connection from ＜old-name＞ to ＜new-name＞.

## Git config
* The git config command is a convenience function that is used to set Git configuration values on a global or local project level. These configuration levels correspond to .gitconfig text files. Executing git config will modify a configuration text file.

### Usage
* The most basic use case for git config is to invoke it with a configuration name, which will display the set value at that name. Configuration names are dot delimited strings composed of a 'section' and a 'key' based on their hierarchy. For example: user.email

```sh
git config user.email
```

In this example, email is a child property of the user configuration block. This will return the configured email address, if any, that Git will associate with locally created commits.

```sh
git config --global user.email "your_email@example.com"
```
This example writes the value your_email@example.com to the configuration name user.email. It uses the --global flag so this value is set for the current operating system user.

## Git alias
* Alias creation is a common pattern found in other popular utilities like `bash` shell. Aliases are used to create shorter commands that map to longer commands. Aliases enable more efficient workflows by requiring fewer keystrokes to execute a command.

### Git alias overview
* Let us create some examples.

```sh
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```

* The previous code example creates globally stored shortcuts for common git commands. Creating the aliases will not modify the source commands. So git checkout will still be available even though we now have the git co alias. These aliases were created with the --global flag which means they will be stored in Git's global operating system level configuration file. On linux systems, the global config file is located in the User home directory at /.gitconfig.

```sh
    [alias]
        co = checkout
        br = branch
        ci = commit
        st = status
```

* This demonstrates that the aliases are now equivalent to the source commands.

## Git branch

* In Git, branches are a part of your everyday development process.

* Git branches are effectively a pointer to a snapshot of your changes. When you want to add a new feature or fix a bug—no matter how big or how small—you spawn a new branch to encapsulate your changes. This makes it harder for unstable code to get merged into the main code base, and it gives you the chance to clean up your future's history before merging it into the main branch.

* By developing them in branches, it’s not only possible to work on both of them in parallel, but it also keeps the main branch free from questionable code.

* The implementation behind Git branches is much more lightweight than other version control system models. Instead of copying files from directory to directory, Git stores a branch as a reference to a commit. In this sense, a branch represents the tip of a series of commits—it's not a container for commits. The history for a branch is extrapolated through the commit relationships.

### How it work
* A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process. You can think of them as a way to request a brand new working directory, staging area, and project history. New commits are recorded in the history for the current branch, which results in a fork in the history of the project.

* The git branch command lets you create, list, rename, and delete branches. It doesn’t let you switch between branches or put a forked history back together again. For this reason, git branch is tightly integrated with the git checkout and git merge commands.

### Common options

```sh
git branch
```

List all of the branches in your repository. This is synonymous with git branch --list.

```sh
git branch <branch>
```

Create a new branch called ＜branch＞. This does not check out the new branch.

```sh
git branch -d <branch>
```

Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.

```sh
git branch -D <branch>
```

Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently throw away all of the commits associated with a particular line of development.

```sh
git branch -m <branch>
```

Rename the current branch to ＜branch＞.

```sh
git branch -a
```

List all remote branches. 

### Git checkout.

* The git checkout command lets you navigate between the branches created by git branch. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development you’re working on.

### Usage
* Assuming the repo you're working in contains pre-existing branches, you can switch between these branches using git checkout. To find out what branches are available and what the current branch name is, execute git branch.

```sh
$＞ git branch 
 * main 
another_branch 
feature_inprogress_branch 
$＞ git checkout feature_inprogress_branch
```

* The above example demonstrates how to view a list of available branches by executing the git branch command, and switch to a specified branch, in this case, the feature_inprogress_branch.

* New branches

```sh
git branch ＜new-branch＞
// or
git checkout -b ＜new-branch＞
```

* Switching branches

```sh
git checkout ＜branchname＞
```

* Restore deleted branches

```sh
$＞ git log --oneline
e5d6e85
$＞ git checkout -b <branchname> e5d6e85  
```

## Git status
* The git status command displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git. Status output does not show you any information regarding the committed project history. For this, you need to use git log.

### Related git commands

```sh
git tag
```

Tags are ref's that point to specific points in Git history. git tag is generally used to capture a point in history that is used for a marked version release (i.e. v1.0.1). 

```sh
git blame
```

The high-level function of git blame is the display of author metadata attached to specific committed lines in a file. This is used to explore the history of specific code and answer questions about what, how, and why the code was added to a repository.

```sh
git log
```

The git log command displays committed snapshots. It lets you list the project history, filter it, and search for specific changes. 

### Usage

```sh
git status
```

## Git add
* The git add command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit. However, git add doesn't really affect the repository in any significant way—changes are not actually recorded until you run git commit.

* In conjunction with these commands, you'll also need git status to view the state of the working directory and the staging area.

### How it works
* The git add and git commit commands compose the fundamental Git workflow. These are the two commands that every Git user needs to understand, regardless of their team’s collaboration model. They are the means to record versions of a project into the repository’s history.

### Common options

```sh
git add <file>
```

Stage all changes in <file> for the next commit.

```sh
git add <directory>
```

Stage all changes in <directory> for the next commit.

```sh
git add .
```

Stage all changes in for the next commit.

### Examples
* When you’re starting a new project, git add serves the same function as svn import. To create an initial commit of the current directory, use the following two commands:

```sh
git add .
git commit
```

* Once you’ve got your project up-and-running, new files can be added by passing the path to git add:

```sh
git add hello.py
git commit
```

The above commands can also be used to record changes to existing files. Again, Git doesn’t differentiate between staging changes in new files vs. changes in files that have already been added to the repository.

## Git commit
* The git commit command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to.

* Prior to the execution of git commit, the git add command is used to promote or 'stage' changes to the project that will be stored in a commit. These two commands git commit and git add are two of the most frequently used.

### Common options

```sh
git commit
```

Commit the staged snapshot. This will launch a text editor prompting you for a commit message. 

```sh
git commit -a
```

Commit a snapshot of all changes in the working directory. This only includes modifications to tracked files (those that have been added with git add at some point in their history).

```sh
git commit -m "commit message"
```

A shortcut command that immediately creates a commit with a passed commit message. By default, git commit will open up the locally configured text editor, and prompt for a commit message to be entered. Passing the -m option will forgo the text editor prompt in-favor of an inline message.

```sh
git commit -am "commit message"
```

A power user shortcut command that combines the -a and -m options. This combination immediately creates a commit of all the staged changes and takes an inline commit message.

```sh
git commit --amend
```

This option adds another level of functionality to the commit command. Passing this option will modify the last commit. Instead of creating a new commit, staged changes will be added to the previous commit. This command will open up the system's configured text editor and prompt to change the previously specified commit message.

## Git push
* The git push command is used to upload local repository content to a remote repository. Pushing is how you transfer commits from your local repository to a remote repo. It's the counterpart to git fetch, but whereas fetching imports commits to local branches, pushing exports commits to remote branches. Remote branches are configured using the git remote command. Pushing has the potential to overwrite changes, caution should be taken when pushing.

### Usage
```sh
git push <remote> <branch>
```

* Push the specified branch to , along with all of the necessary commits and internal objects. This creates a local branch in the destination repository. To prevent you from overwriting commits, Git won’t let you push when it results in a non-fast-forward merge in the destination repository.

```sh
git push <remote> --force
```

Same as the above command, but force the push even if it results in a non-fast-forward merge. Do not use the --force flag unless you’re absolutely sure you know what you’re doing.

Push all of your local branches to the specified remote.

```sh
git push <remote> --tags
```

* Tags are not automatically pushed when you push a branch or use the --all option. The --tags flag sends all of your local tags to the remote repository.

## Git pull
* The git pull command is used to fetch and download content from a remote repository and immediately update the local repository to match that content. Merging remote upstream changes into your local repository is a common task in Git-based collaboration work flows. The git pull command is actually a combination of two other commands, git fetch followed by git merge. In the first stage of operation git pull will execute a git fetch scoped to the local branch that HEAD is pointed at. Once the content is downloaded, git pull will enter a merge workflow. A new merge commit will be-created and HEAD updated to point at the new commit.

### Common Options

```sh
git pull <remote>
```

* Fetch the specified remote’s copy of the current branch and immediately merge it into the local copy. This is the same as git fetch ＜remote＞ followed by git merge origin/＜current-branch＞.

```sh
git pull --no-commit <remote>
```

* Similar to the default invocation, fetches the remote content but does not create a new merge commit.

```sh
git pull --rebase <remote>
```

* Same as the previous pull Instead of using git merge to integrate the remote branch with the local one, use git rebase.

```sh
git pull --verbose
```

* Gives verbose output during a pull which displays the content being downloaded and the merge details.

```sh
git pull <remote> <branch> --allow-unrelated-histories
```

* Allow merging branches with no common history base, which then should finish the merge without errors. 

## Git revert
* The git revert command can be considered an 'undo' type command, however, it is not a traditional undo operation. Instead of removing the commit from the project history, it figures out how to invert the changes introduced by the commit and appends a new commit with the resulting inverse content. This prevents Git from losing history, which is important for the integrity of your revision history and for reliable collaboration.
Reverting should be used when you want to apply the inverse of a commit from your project history. This can be useful, for example, if you’re tracking down a bug and find that it was introduced by a single commit. Instead of manually going in, fixing it, and committing a new snapshot, you can use git revert to automatically do all of this for you.

### Example

```sh
$＞ git log
commit e5d6e85a840d8c49654d1e9e3386f1c3dd719d91 (HEAD -> oke4, origin/oke3, oke3)
$＞ git revert e5d6e85a840d8c49654d1e9e3386f1c3dd719d91
[oke4 d344bcd] Revert "add ok3 part2"
 2 files changed, 2 deletions(-)
 delete mode 100644 ok4.js
```

## Git rebase
### What is git rebase?

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%203/images/3.jpg" width="666px" align="center">

* Rebasing is the process of moving or combining a sequence of commits to a new base commit. Rebasing is most useful and easily visualized in the context of a feature branching workflow. The general process can be visualized as the following:

* From a content perspective, rebasing is changing the base of your branch from one commit to another making it appear as if you'd created your branch from a different commit. Internally, Git accomplishes this by creating new commits and applying them to the specified base. It's very important to understand that even though the branch looks the same, it's composed of entirely new commits.

* Git rebase interactive is when git rebase accepts an -- i argument. This stands for "Interactive." Without any arguments, the command runs in standard mode. In both cases, let's assume we have created a separate feature branch.

* Create a feature branch based off of main 

```sh
git checkout -b feature_branch main
```

* Edit files 

```sh
git commit -a -m "Adds new feature" 
```

* Git rebase in standard mode will automatically take the commits in your current working branch and apply them to the head of the passed branch.

```sh
git rebase <base>
```

This automatically rebases the current branch onto ＜base＞, which can be any kind of commit reference (for example an ID, a branch name, a tag, or a relative reference to HEAD).

## Git merge

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%203/images/2.jpg" width="666px" align="center">

* Merging is Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.

* Note that all of the commands presented below merge into the current branch. The current branch will be updated to reflect the merge, but the target branch will be completely unaffected.

### Example

```sh
# Start a new feature
git checkout -b new-feature main
# Edit some files
git add <file>
git commit -m "Start a feature"
# Edit some files
git add <file>
git commit -m "Finish a feature"
# Merge in the new-feature branch
git checkout main
git merge new-feature
git branch -d new-feature
```

## Git cherry pick
* Git cherry-pick is a powerful command that enables arbitrary Git commits to be picked by reference and appended to the current working HEAD. Cherry picking is the act of picking a commit from a branch and applying it to another. git cherry-pick can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.

### When to use git cherry pick
* Git cherry-pick is a useful tool but not always a best practice. Cherry picking can cause duplicate commits and many scenarios where cherry picking would work, traditional merges are preferred instead. With that said git cherry-pick is a handy tool for a few scenarios...

### Example

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%203/images/4.jpg" width="666px" align="center">

```sh
$ git checkout rel_2.3 # First we checkout to branch rel_2.3
$ git cherry-pick dev~2
# or
$ git cherry-pick F # F here is the commit hash
```

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%203/images/5.jpg" width="666px" align="center">

## Git tag
* Tags are ref's that point to specific points in Git history. Tagging is generally used to capture a point in history that is used for a marked version release (i.e. v1.0.1).
* A tag is like a branch that doesn’t change. Unlike branches, tags, after being created, have no further history of commits. For more info on branches visit the git branch page.

### Example

```sh
git tag <tagname>
// Createing a tag
git tag
// Listing tags
```

* Annotated tags:

```sh
git tag -a v1.4

git tag -a v1.4 -m "my version 1.4"
```

* Lightweight tags:

```sh
git tag v1.4-lw
```

## .gitignore file
* Git sees every file in your working copy as one of three things:
    - tracked - a file which has been previously staged or committed;
    - untracked - a file which has not been staged or committed; or
    - ignored - a file which Git has been explicitly told to ignore.

* Ignored files are usually build artifacts and machine generated files that can be derived from your repository source or should otherwise not be committed.

### Example

```sh
touch .gitignore
```

* If the command succeeds, there will be no output.
* For an example .gitignore file, see "Some common .gitignore configurations" in the Octocat repository.
* If you want to ignore a file that is already checked in, you must untrack the file before you add a rule to ignore it. From your terminal, untrack the file.

```sh
git rm --cached FILENAME
```

## .git folder
* Folder .git is initialized by git init.
* .git contains all information required for version control. If you want to clone your repository, copying .git is enough.
* Four sub-directories:
    - hooks/ : example scripts
    - info/ : exclude file for ignored patterns
    - objects/ : all "objects"
    - refs/ : pointers to commit objects

* Four files:
    - HEAD : the current branch
    - config : configuration options
    - description
    - index : staging area

* Here "object" includes:
    - blobs (files)
    - trees (directories)
    - commits (reference to a tree, parent commit, etc.)
